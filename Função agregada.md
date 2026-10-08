```sql
  

-- ============================================================

-- OBJETO: MEDIA_POND_IMPL

-- Implementação interna da função agregada.

-- Armazena dois acumuladores:

--   soma_ponderada → soma de (pontuacao × peso_da_fase)

--   soma_pesos     → soma dos pesos acumulados

-- ============================================================

CREATE OR REPLACE TYPE MEDIA_POND_IMPL AS OBJECT (

    soma_ponderada NUMBER,

    soma_pesos     NUMBER,

  

    STATIC FUNCTION ODCIAggregateInitialize(

        ctx IN OUT MEDIA_POND_IMPL

    ) RETURN NUMBER,

  

    MEMBER FUNCTION ODCIAggregateIterate(

        self  IN OUT MEDIA_POND_IMPL,

        valor IN     VARCHAR2        

    ) RETURN NUMBER,

  

    MEMBER FUNCTION ODCIAggregateMerge(

        self IN OUT MEDIA_POND_IMPL,

        ctx2 IN     MEDIA_POND_IMPL

    ) RETURN NUMBER,

  

    MEMBER FUNCTION ODCIAggregateTerminate(

        self        IN  MEDIA_POND_IMPL,

        returnValue OUT NUMBER,

        flags       IN  NUMBER

    ) RETURN NUMBER

);

/

  

-- ============================================================

-- Implementar o BODY

-- ============================================================

CREATE OR REPLACE TYPE BODY MEDIA_POND_IMPL AS

  

    STATIC FUNCTION ODCIAggregateInitialize(

        ctx IN OUT MEDIA_POND_IMPL

    ) RETURN NUMBER IS

    BEGIN

        ctx := MEDIA_POND_IMPL(0, 0);

        RETURN ODCIConst.Success;

    END;

  

    MEMBER FUNCTION ODCIAggregateIterate(

        self  IN OUT MEDIA_POND_IMPL,

        valor IN     VARCHAR2

    ) RETURN NUMBER IS

        v_pontuacao NUMBER;

        v_fase      VARCHAR2(30);

        v_peso      NUMBER;

        v_sep       NUMBER;

    BEGIN

        -- Ignora entradas nulas

        IF valor IS NULL THEN

            RETURN ODCIConst.Success;

        END IF;

  

        -- Separa 'pontuacao|fase' pelo pipe

        v_sep       := INSTR(valor, '|');

        v_pontuacao := TO_NUMBER(SUBSTR(valor, 1, v_sep - 1));

        v_fase      := UPPER(SUBSTR(valor, v_sep + 1));

  

        -- Define o peso da fase

        v_peso := CASE v_fase

                      WHEN 'CLASSIFICATORIA' THEN 1

                      WHEN 'QUARTAS'         THEN 2

                      WHEN 'SEMIFINAL'       THEN 3

                      WHEN 'FINAL'           THEN 4

                      WHEN 'UNICA'           THEN 2

                      ELSE 1

                  END;

  

        self.soma_ponderada := self.soma_ponderada + (v_pontuacao * v_peso);

        self.soma_pesos     := self.soma_pesos     + v_peso;

  

        RETURN ODCIConst.Success;

    END;

  

    MEMBER FUNCTION ODCIAggregateMerge(

        self IN OUT MEDIA_POND_IMPL,

        ctx2 IN     MEDIA_POND_IMPL

    ) RETURN NUMBER IS

    BEGIN

        self.soma_ponderada := self.soma_ponderada + ctx2.soma_ponderada;

        self.soma_pesos     := self.soma_pesos     + ctx2.soma_pesos;

        RETURN ODCIConst.Success;

    END;

  

    MEMBER FUNCTION ODCIAggregateTerminate(

        self        IN  MEDIA_POND_IMPL,

        returnValue OUT NUMBER,

        flags       IN  NUMBER

    ) RETURN NUMBER IS

    BEGIN

        IF self.soma_pesos = 0 THEN

            returnValue := NULL;

        ELSE

            returnValue := ROUND(self.soma_ponderada / self.soma_pesos, 2);

        END IF;

        RETURN ODCIConst.Success;

    END;

  

END;

/

  

-- ============================================================

-- Criar a função pública

-- ============================================================

CREATE OR REPLACE FUNCTION MEDIA_PONDERADA_FASE(

    p_valor VARCHAR2        

) RETURN NUMBER

PARALLEL_ENABLE AGGREGATE USING MEDIA_POND_IMPL;

/

  

-- ============================================================

-- USO: concatenar pontuacao e fase com pipe na chamada

-- ============================================================

SELECT

    a.nome_completo                                              AS atleta,

    ROUND(AVG(r.pontuacao), 2)                                  AS media_simples,

    MEDIA_PONDERADA_FASE(TO_CHAR(r.pontuacao) || '|' || c.fase) AS media_ponderada

FROM TB_ATLETA      a

INNER JOIN TB_RESULTADO  r ON r.id_atleta     = a.id_atleta

INNER JOIN TB_COMPETICAO c ON c.id_competicao = r.id_competicao

GROUP BY a.nome_completo

ORDER BY media_ponderada DESC NULLS LAST;
```