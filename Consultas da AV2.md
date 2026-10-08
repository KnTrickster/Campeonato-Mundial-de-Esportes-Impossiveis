```sql
-- Atletas mais bem sucedidos do campeonato

SELECT

    a.id_atleta,

    a.nome_completo,

    a.nacionalidade,

    COUNT(r.id)      AS qtd_competicoes,

    SUM(r.pontuacao) AS total_pontos

FROM TB_ATLETA a

INNER JOIN TB_RESULTADO r ON r.id_atleta = a.id_atleta

GROUP BY

    a.id_atleta,

    a.nome_completo,

    a.nacionalidade

ORDER BY total_pontos DESC NULLS LAST;


-- Filtra as modalidades com maiores pontuações médias  

SELECT

    e.id_esporte,

    e.nome          AS esporte,

    e.tipo_esporte,

    COUNT(DISTINCT c.id_competicao) AS total_competicoes,

    ROUND(AVG(r.pontuacao), 2)      AS media_pontuacao

FROM TB_ESPORTE e

INNER JOIN TB_COMPETICAO c ON c.id_esporte    = e.id_esporte

INNER JOIN TB_RESULTADO  r ON r.id_competicao = c.id_competicao

GROUP BY

    e.id_esporte,

    e.nome,

    e.tipo_esporte

HAVING AVG(r.pontuacao) > 100

ORDER BY media_pontuacao DESC;

-- Atletas cadastrados que não possuem nenhum resultado

SELECT

    a.id_atleta,

    a.nome_completo,

    a.nacionalidade,

    a.status,

    e.nome_equipe AS equipe

FROM TB_ATLETA a

LEFT JOIN TB_RESULTADO r ON r.id_atleta = a.id_atleta

LEFT JOIN TB_EQUIPE    e ON e.id_equipe = a.id_equipe

WHERE r.id IS NULL

ORDER BY a.nome_completo;

-- Competições com pontuações máximas acima da média global, competições de alta intensidade  

SELECT

    c.id_competicao,

    c.nome       AS competicao,

    c.fase,

    ev.nome      AS evento,

    es.nome      AS esporte,

    MAX(r.pontuacao) AS pontuacao_maxima,

    ROUND(

        (SELECT AVG(pontuacao) FROM TB_RESULTADO WHERE pontuacao IS NOT NULL),

    2)           AS media_global

FROM TB_COMPETICAO c

INNER JOIN TB_RESULTADO r  ON r.id_competicao = c.id_competicao

INNER JOIN TB_EVENTO    ev ON ev.id_evento     = c.id_evento

INNER JOIN TB_ESPORTE   es ON es.id_esporte    = c.id_esporte

GROUP BY

    c.id_competicao, c.nome, c.fase,

    ev.nome, es.nome

HAVING MAX(r.pontuacao) > (

    SELECT AVG(pontuacao) FROM TB_RESULTADO WHERE pontuacao IS NOT NULL

)

ORDER BY pontuacao_maxima DESC;

  
-- Quadro completo geral de todas as competições, exibindo vários dados gerais

SELECT

    ev.nome                              AS evento,

    ev.cidade || ' / ' || ev.pais        AS local_evento,

    es.nome                              AS esporte,

    es.tipo_esporte,

    c.nome                               AS competicao,

    c.fase,

    TO_CHAR(c.data_hora, 'DD/MM/YYYY HH24:MI') AS data_hora,

    r.colocacao,

    NVL(a.nome_completo, eq.nome_equipe) AS participante,

    NVL(a.nacionalidade, eq.pais_origem) AS origem,

    r.pontuacao,

    r.observacoes

FROM TB_RESULTADO   r

INNER JOIN TB_COMPETICAO c  ON c.id_competicao = r.id_competicao

INNER JOIN TB_EVENTO     ev ON ev.id_evento     = c.id_evento

INNER JOIN TB_ESPORTE    es ON es.id_esporte    = c.id_esporte

LEFT  JOIN TB_ATLETA     a  ON a.id_atleta      = r.id_atleta

LEFT  JOIN TB_EQUIPE     eq ON eq.id_equipe     = r.id_equipe

WHERE r.colocacao IS NOT NULL

ORDER BY ev.nome, c.data_hora, r.colocacao;


-- Eventos que não possuem nenhum contrato de patrocinio

SELECT

    ev.id_evento,

    ev.nome      AS evento,

    ev.cidade,

    ev.pais,

    ev.data_inicio,

    ev.data_fim,

    ev.status_evento

FROM TB_EVENTO ev

LEFT JOIN TB_CONTRATO_PATROCINIO cp

       ON cp.id_evento = ev.id_evento

      AND cp.status    = 'ATIVO'

WHERE cp.id_contrato IS NULL

ORDER BY ev.data_inicio;
  

-- Lista de patrocinadores que investiram mais de 50000 em eventos encerrados  

SELECT

    p.id_patrocinador,

    p.nome           AS patrocinador,

    p.pais_origem,

    COUNT(cp.id_contrato) AS qtd_contratos,

    SUM(cp.valor)         AS total_investido,

    cp.moeda

FROM TB_PATROCINADOR        p

INNER JOIN TB_CONTRATO_PATROCINIO cp ON cp.id_patrocinador = p.id_patrocinador

WHERE cp.id_evento IN (

    SELECT id_evento

    FROM   TB_EVENTO

    WHERE  status_evento = 'ENCERRADO'

)

GROUP BY

    p.id_patrocinador,

    p.nome,

    p.pais_origem,

    cp.moeda

HAVING SUM(cp.valor) > 50000

ORDER BY total_investido DESC;
```