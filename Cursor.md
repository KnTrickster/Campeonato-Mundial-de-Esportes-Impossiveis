```sql
SET SERVEROUTPUT ON;

  

-- ============================================================

-- Cursor Explícito com Parâmetro

-- Exibe o ranking oficial de uma competição específica.

-- ============================================================

DECLARE

  

    -- ── Declaração do cursor com parâmetro ────────────────

    CURSOR c_ranking (p_id_comp NUMBER) IS

        SELECT

            r.colocacao,

            NVL(a.nome_completo, eq.nome_equipe) AS participante,

            NVL(a.nacionalidade, eq.pais_origem) AS origem,

            es.nome                              AS esporte,

            c.fase,

            r.pontuacao,

            r.observacoes

        FROM TB_RESULTADO   r

        INNER JOIN TB_COMPETICAO c  ON c.id_competicao = r.id_competicao

        INNER JOIN TB_ESPORTE   es  ON es.id_esporte   = c.id_esporte

        LEFT  JOIN TB_ATLETA    a   ON a.id_atleta     = r.id_atleta

        LEFT  JOIN TB_EQUIPE    eq  ON eq.id_equipe    = r.id_equipe

        WHERE r.id_competicao = p_id_comp

          AND r.colocacao IS NOT NULL

        ORDER BY r.colocacao ASC;

  

    -- ── Variáveis de recepção (espelham o SELECT do cursor)

    v_colocacao    TB_RESULTADO.colocacao%TYPE;

    v_participante VARCHAR2(150);

    v_origem       VARCHAR2(100);

    v_esporte      TB_ESPORTE.nome%TYPE;

    v_fase         TB_COMPETICAO.fase%TYPE;

    v_pontuacao    TB_RESULTADO.pontuacao%TYPE;

    v_obs          TB_RESULTADO.observacoes%TYPE;

  

    -- ID da competição a consultar

    v_id_comp      NUMBER := 33;

  

    v_total_lidos  NUMBER := 0;

  

BEGIN

  

    DBMS_OUTPUT.PUT_LINE('=== RANKING OFICIAL ===');

    DBMS_OUTPUT.PUT_LINE('Competicao ID: ' || v_id_comp);

    DBMS_OUTPUT.PUT_LINE('-----------------------------------------');

  

    -- ── 1. Abre o cursor passando o parâmetro ─────────────

    OPEN c_ranking(v_id_comp);

  

    LOOP

        -- ── 2. Lê uma linha por vez para as variáveis locais

        FETCH c_ranking INTO

            v_colocacao, v_participante, v_origem,

            v_esporte, v_fase, v_pontuacao, v_obs;

  

        -- ── 3. Sai do loop quando não há mais linhas ──────

        EXIT WHEN c_ranking%NOTFOUND;

  

        -- Formata a saída conforme a colocação

        DBMS_OUTPUT.PUT_LINE(

            LPAD(v_colocacao, 2) || 'º  '

            || RPAD(v_participante, 30)

            || ' | ' || RPAD(v_origem, 15)

            || ' | ' || LPAD(TO_CHAR(v_pontuacao), 8) || ' pts'

            || CASE WHEN v_obs IS NOT NULL

                    THEN ' (' || v_obs || ')' ELSE '' END

        );

    END LOOP;

  

    v_total_lidos := c_ranking%ROWCOUNT;

  

    -- ── 4. Fecha o cursor e libera recursos ───────────────

    CLOSE c_ranking;

  

    DBMS_OUTPUT.PUT_LINE('-----------------------------------------');

    DBMS_OUTPUT.PUT_LINE('Total de colocados: ' || v_total_lidos);

  

    IF v_total_lidos = 0 THEN

        DBMS_OUTPUT.PUT_LINE('[AVISO] Nenhum resultado encontrado para esta competicao.');

    ELSE

        DBMS_OUTPUT.PUT_LINE('Esporte : ' || v_esporte);

        DBMS_OUTPUT.PUT_LINE('Fase    : ' || v_fase);

    END IF;

  

    DBMS_OUTPUT.PUT_LINE('=== FIM DO RANKING ===');

  

EXCEPTION

    WHEN OTHERS THEN

        IF c_ranking%ISOPEN THEN

            CLOSE c_ranking;

        END IF;

        DBMS_OUTPUT.PUT_LINE('ERRO: ' || SQLERRM);

        RAISE;

END;

/
```