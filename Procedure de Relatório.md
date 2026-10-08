```sql
-- ============================================================

-- PROCEDURE: PRC_RELATORIO_EVENTO

-- Gera o relatório consolidado de desempenho de um evento.

-- Parâmetros:

--   p_id_evento  IN  NUMBER         → ID do evento a analisar

--   p_cursor     OUT SYS_REFCURSOR  → resultado para o cliente

-- ============================================================

CREATE OR REPLACE PROCEDURE PRC_RELATORIO_EVENTO(

    p_id_evento IN  TB_EVENTO.id_evento%TYPE,

    p_cursor    OUT SYS_REFCURSOR

) AS

  

    -- Variáveis locais para validação e alertas

    v_nome_evento    TB_EVENTO.nome%TYPE;

    v_total_patroc   NUMBER := 0;

    v_qtd_sem_arb    NUMBER := 0;

  

    -- Cursor auxiliar: competições sem árbitros alocados

    CURSOR c_sem_arbitros IS

        SELECT c.id_competicao, c.nome, c.fase

        FROM   TB_COMPETICAO c

        WHERE  c.id_evento = p_id_evento

          AND  c.id_competicao NOT IN (

                   SELECT DISTINCT id_competicao

                   FROM   TB_ARBITRAGEM

               );

  

BEGIN

  

    -- ── 1. Validação: evento deve existir ──────────────────

    BEGIN

        SELECT nome

        INTO   v_nome_evento

        FROM   TB_EVENTO

        WHERE  id_evento = p_id_evento;

    EXCEPTION

        WHEN NO_DATA_FOUND THEN

            RAISE_APPLICATION_ERROR(

                -20001,

                'Evento ID ' || p_id_evento || ' nao encontrado.'

            );

    END;

  

    DBMS_OUTPUT.PUT_LINE('=== RELATORIO DE DESEMPENHO ===');

    DBMS_OUTPUT.PUT_LINE('Evento: ' || v_nome_evento);

    DBMS_OUTPUT.PUT_LINE('-------------------------------');

  

    -- ── 2. Cursor principal: desempenho por competição ────

    OPEN p_cursor FOR

        SELECT

            c.id_competicao,

            c.nome                              AS competicao,

            c.fase,

            TO_CHAR(c.data_hora, 'DD/MM/YYYY HH24:MI') AS data_hora,

            es.nome                             AS esporte,

            es.tipo_esporte,

            COUNT(r.id)                         AS total_participantes,

            NVL(MAX(r.pontuacao), 0)            AS pontuacao_maxima,

            ROUND(NVL(AVG(r.pontuacao), 0), 2)  AS media_pontuacao,

            COUNT(arb.id_arbitro)               AS total_arbitros

        FROM TB_COMPETICAO   c

        INNER JOIN TB_ESPORTE    es  ON es.id_esporte    = c.id_esporte

        LEFT  JOIN TB_RESULTADO  r   ON r.id_competicao  = c.id_competicao

        LEFT  JOIN TB_ARBITRAGEM arb ON arb.id_competicao = c.id_competicao

        WHERE c.id_evento = p_id_evento

        GROUP BY

            c.id_competicao, c.nome, c.fase,

            c.data_hora, es.nome, es.tipo_esporte

        ORDER BY c.data_hora;

  

    -- ── 3. Alerta operacional: competições sem árbitros ───

    FOR reg IN c_sem_arbitros LOOP

        v_qtd_sem_arb := v_qtd_sem_arb + 1;

        DBMS_OUTPUT.PUT_LINE(

            '[ALERTA] Competicao sem arbitro: '

            || reg.nome || ' (Fase: ' || reg.fase || ')'

        );

    END LOOP;

  

    IF v_qtd_sem_arb = 0 THEN

        DBMS_OUTPUT.PUT_LINE('[OK] Todas as competicoes possuem arbitros.');

    END IF;

  

    -- ── 4. Total de patrocínios ativos do evento ──────────

    SELECT NVL(SUM(cp.valor), 0)

    INTO   v_total_patroc

    FROM   TB_CONTRATO_PATROCINIO cp

    WHERE  cp.id_evento = p_id_evento

      AND  cp.status    = 'ATIVO';

  

    DBMS_OUTPUT.PUT_LINE(

        'Total patrocinado (ativo): R$ '

        || TO_CHAR(v_total_patroc, 'FM999G999G990D00')

    );

    DBMS_OUTPUT.PUT_LINE('=== FIM DO RELATORIO ===');

  

EXCEPTION

    WHEN OTHERS THEN

        -- Garante que o cursor não fique aberto em caso de erro inesperado

        IF p_cursor%ISOPEN THEN

            CLOSE p_cursor;

        END IF;

        RAISE;

END PRC_RELATORIO_EVENTO;

/

  
  

-- ============================================================

-- EXECUÇÃO: PRC_RELATORIO_EVENTO

-- ============================================================

SET SERVEROUTPUT ON;

  

DECLARE

    v_cursor        SYS_REFCURSOR;

  

    v_id_comp       NUMBER;

    v_competicao    VARCHAR2(150);

    v_fase          VARCHAR2(30);

    v_data_hora     VARCHAR2(20);

    v_esporte       VARCHAR2(100);

    v_tipo_esporte  VARCHAR2(10);

    v_participantes NUMBER;

    v_pont_max      NUMBER;

    v_media_pont    NUMBER;

    v_arbitros      NUMBER;

  

BEGIN

    -- 1. Chama a procedure — ela abre o cursor e devolve aqui

    PRC_RELATORIO_EVENTO(

        p_id_evento => 2,    

        p_cursor    => v_cursor

    );

  

    DBMS_OUTPUT.PUT_LINE('');

    DBMS_OUTPUT.PUT_LINE('=== COMPETICOES DO EVENTO ===');

    DBMS_OUTPUT.PUT_LINE(

        RPAD('COMPETICAO',          25) || ' ' ||

        RPAD('FASE',                15) || ' ' ||

        RPAD('ESPORTE',             20) || ' ' ||

        LPAD('PARTICIPANTES', 13)  || ' ' ||

        LPAD('MAX PTS',        7)  || ' ' ||

        LPAD('MEDIA',          7)  || ' ' ||

        LPAD('ARBITROS',       8)

    );

    DBMS_OUTPUT.PUT_LINE(RPAD('-', 100, '-'));

  

    -- 2. Itera o cursor linha por linha com FETCH

    LOOP

        FETCH v_cursor INTO

            v_id_comp, v_competicao, v_fase, v_data_hora,

            v_esporte, v_tipo_esporte,

            v_participantes, v_pont_max, v_media_pont, v_arbitros;

  

        EXIT WHEN v_cursor%NOTFOUND;

  

        DBMS_OUTPUT.PUT_LINE(

            RPAD(v_competicao,  25) || ' ' ||

            RPAD(v_fase,        15) || ' ' ||

            RPAD(v_esporte,     20) || ' ' ||

            LPAD(v_participantes, 13) || ' ' ||

            LPAD(v_pont_max,    7) || ' ' ||

            LPAD(v_media_pont,  7) || ' ' ||

            LPAD(v_arbitros,    8)

        );

    END LOOP;

  

    -- 3. Fecha o cursor após consumir todos os dados

    CLOSE v_cursor;

  

END;

/
```