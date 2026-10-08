```sql
CREATE TABLE TB_ESPORTE (

  id_esporte NUMBER GENERATED ALWAYS AS IDENTITY PRIMARY KEY NOT NULL,

  nome VARCHAR2(100) NOT NULL UNIQUE,

  tipo_esporte VARCHAR2(10) NOT NULL CHECK (tipo_esporte IN ('INDIVIDUAL', 'COLETIVO')),

  descricao VARCHAR2(500) NOT NULL,

  regras CLOB NOT NULL,

  unidade_pontuacao VARCHAR2(50) NOT NULL

);

  

CREATE TABLE TB_EVENTO (

    id_evento NUMBER GENERATED ALWAYS AS IDENTITY PRIMARY KEY NOT NULL,

    nome VARCHAR2(150) NOT NULL,

    cidade VARCHAR2(100) NOT NULL,

    pais VARCHAR2(100) NOT NULL,

    data_inicio DATE NOT NULL,

    data_fim DATE NOT NULL,

    status_evento VARCHAR2(20) NOT NULL,

    descricao VARCHAR2(500) NOT NULL,

    CONSTRAINT chk_evento_status CHECK (status_evento IN ('PLANEJADO', 'EM_ANDAMENTO', 'ENCERRADO', 'CANCELADO')),

    CONSTRAINT chk_evento_datas  CHECK (data_fim >= data_inicio)

);

  

CREATE TABLE TB_COMPETICAO (

  id_competicao NUMBER GENERATED ALWAYS AS IDENTITY PRIMARY KEY NOT NULL,

  id_esporte NUMBER NOT NULL,

  id_evento NUMBER NOT NULL,

  nome VARCHAR2(150) NOT NULL,

  fase VARCHAR2(30) NOT NULL,

  data_hora TIMESTAMP NOT NULL,

  local_competicao VARCHAR2(100) NOT NULL,

  status_competicao VARCHAR2(20) NOT NULL,

  CONSTRAINT fk_comp_evento FOREIGN KEY (id_evento)  REFERENCES TB_EVENTO(id_evento),

  CONSTRAINT fk_comp_esporte  FOREIGN KEY (id_esporte) REFERENCES TB_ESPORTE(id_esporte),

  CONSTRAINT chk_comp_status CHECK (status_competicao IN ('AGENDADA', 'EM_ANDAMENTO', 'FINALIZADA', 'CANCELADA')),

  CONSTRAINT chk_comp_fase CHECK (fase IN ('CLASSIFICATORIA', 'QUARTAS', 'SEMIFINAL', 'FINAL', 'UNICA'))

);

  

CREATE TABLE TB_ARBITRO (

  id_arbitro NUMBER GENERATED ALWAYS AS IDENTITY PRIMARY KEY NOT NULL,

  nome_completo VARCHAR2(150) NOT NULL,

  data_nascimento DATE NOT NULL,

  nacionalidade VARCHAR2(100) NOT NULL,

  especialidade VARCHAR2(100) NOT NULL,

  status_ativo BOOLEAN DEFAULT TRUE NOT NULL

);

  

CREATE TABLE TB_ARBITRAGEM (

  id_arbitro NUMBER NOT NULL,

  id_competicao NUMBER NOT NULL,

  papel VARCHAR2(30) NOT NULL,

  avaliacao_desempenho NUMBER,

  observacoes VARCHAR2(500),

  CONSTRAINT pk_arbitragem PRIMARY KEY (id_arbitro, id_competicao),

  CONSTRAINT fk_arb_arbitro FOREIGN KEY (id_arbitro) REFERENCES TB_ARBITRO(id_arbitro),

  CONSTRAINT fk_arb_competicao FOREIGN KEY (id_competicao) REFERENCES TB_COMPETICAO(id_competicao),

  CONSTRAINT ck_arb_avaliacao CHECK (avaliacao_desempenho BETWEEN 0 AND 10),

  CONSTRAINT ck_arb_papel CHECK (papel IN('PRINCIPAL', 'AUXILIAR', 'CRONOMETRISTA', 'FISCAL'))

);

  

CREATE TABLE TB_EQUIPE (

  id_equipe NUMBER GENERATED ALWAYS AS IDENTITY PRIMARY KEY NOT NULL,

  nome_equipe VARCHAR2(100) NOT NULL UNIQUE,

  sigla VARCHAR2(10),

  pais_origem VARCHAR2(100),

  tecnico VARCHAR2(100),

  status VARCHAR2(30) DEFAULT 'ATIVA' NOT NULL,

  CONSTRAINT ck_equipe_status CHECK (status IN ('ATIVA', 'SUSPENSA', 'INATIVA', 'DESCLASSIFICADA'))

);

  

CREATE TABLE TB_ATLETA (

  id_atleta NUMBER GENERATED ALWAYS AS IDENTITY PRIMARY KEY NOT NULL,

  id_equipe NUMBER,

  nome_completo VARCHAR2(150) NOT NULL,

  apelido VARCHAR2(100),

  data_nascimento DATE NOT NULL,

  nacionalidade VARCHAR2(100) NOT NULL,

  sexo_biologico VARCHAR2(1) NOT NULL,

  status VARCHAR2(30) DEFAULT 'ATIVO' NOT NULL,

  data_cadastro TIMESTAMP DEFAULT SYSTIMESTAMP NOT NULL,

  CONSTRAINT fk_atleta_equipe FOREIGN KEY (id_equipe) REFERENCES TB_EQUIPE(id_equipe),

  CONSTRAINT ck_atleta_sexo CHECK (sexo_biologico IN ('M', 'F', 'O')),

  CONSTRAINT ck_atleta_status CHECK (status IN ('ATIVO', 'SUSPENSO', 'INATIVO', 'APOSENTADO'))

);

  

CREATE TABLE TB_RESULTADO (

  id NUMBER GENERATED ALWAYS AS IDENTITY PRIMARY KEY NOT NULL,

  id_equipe NUMBER,

  id_competicao NUMBER NOT NULL,

  id_atleta NUMBER,

  colocacao NUMBER,

  pontuacao NUMBER,

  observacoes VARCHAR2(500),

  data_registro TIMESTAMP DEFAULT SYSTIMESTAMP NOT NULL,

  CONSTRAINT fk_resultado_equipe FOREIGN KEY (id_equipe) REFERENCES TB_EQUIPE (id_equipe),

  CONSTRAINT fk_resultado_atleta FOREIGN KEY (id_atleta) REFERENCES TB_ATLETA (id_atleta),

  CONSTRAINT fk_resultado_competicao FOREIGN KEY (id_competicao) REFERENCES TB_COMPETICAO (id_competicao),

  CONSTRAINT chk_resultado_participante CHECK (

        (id_atleta IS NOT NULL AND id_equipe IS NULL) OR

        (id_atleta IS NULL AND id_equipe IS NOT NULL)

    ),

  CONSTRAINT chk_resultado_pontos CHECK (

    (pontuacao IS NOT NULL OR colocacao IS NOT NULL)

    ),

  CONSTRAINT chk_resultado_pontuacao CHECK (

    pontuacao > 0

    )

);

  

CREATE TABLE TB_PATROCINADOR (

  id_patrocinador NUMBER GENERATED ALWAYS AS IDENTITY PRIMARY KEY NOT NULL,

  nome VARCHAR2(100) NOT NULL,

  cnpj VARCHAR2(14) UNIQUE NOT NULL,

  pais_origem VARCHAR2(100) NOT NULL,

  email_contato VARCHAR2(150),

  telefone_contato VARCHAR2(30),

  website VARCHAR2(200),

  status BOOLEAN DEFAULT TRUE NOT NULL,

  CONSTRAINT chk_patrocinador_contato CHECK (

  email_contato IS NOT NULL OR telefone_contato IS NOT NULL

  )

);

  

CREATE TABLE TB_CONTRATO_PATROCINIO (

  id_contrato NUMBER GENERATED ALWAYS AS IDENTITY PRIMARY KEY NOT NULL,

  id_patrocinador NUMBER NOT NULL,

  id_equipe NUMBER,

  id_atleta NUMBER,

  id_arbitro NUMBER,

  id_evento NUMBER,

  tipo_patrocinio VARCHAR2(30) NOT NULL,

  valor NUMBER NOT NULL,

  moeda VARCHAR2(5) DEFAULT 'BRL' NOT NULL,

  data_assinatura DATE DEFAULT SYSDATE NOT NULL,

  vigencia_inicio DATE NOT NULL,

  vigencia_fim DATE,

  status VARCHAR2(20) DEFAULT 'ATIVO' NOT NULL,

  CONSTRAINT fk_contrato_patrocinador  FOREIGN KEY (id_patrocinador) REFERENCES TB_PATROCINADOR(id_patrocinador),

  CONSTRAINT fk_contrato_atleta FOREIGN KEY (id_atleta) REFERENCES TB_ATLETA(id_atleta),

  CONSTRAINT fk_contrato_equipe FOREIGN KEY (id_equipe) REFERENCES TB_EQUIPE(id_equipe),

  CONSTRAINT fk_contrato_evento FOREIGN KEY (id_evento) REFERENCES TB_EVENTO(id_evento),

  CONSTRAINT fk_contrato_arbitro FOREIGN KEY (id_arbitro) REFERENCES TB_ARBITRO(id_arbitro),

  CONSTRAINT chk_contrato_exclusividade CHECK (

        (

            CASE WHEN id_atleta  IS NOT NULL THEN 1 ELSE 0 END +

            CASE WHEN id_equipe  IS NOT NULL THEN 1 ELSE 0 END +

            CASE WHEN id_evento  IS NOT NULL THEN 1 ELSE 0 END +

            CASE WHEN id_arbitro IS NOT NULL THEN 1 ELSE 0 END

        ) = 1

    ),

  

  CONSTRAINT chk_contrato_tipo CHECK (

        tipo_patrocinio IN ('NAMING_RIGHTS', 'COTA_OURO', 'COTA_PRATA', 'COTA_BRONZE', 'FORNECEDOR')

    ),

  CONSTRAINT chk_contrato_status CHECK (

        status IN ('ATIVO', 'ENCERRADO', 'SUSPENSO', 'EM_NEGOCIACAO')

    ),

  CONSTRAINT chk_contrato_vigencia CHECK (vigencia_fim IS NULL OR vigencia_fim >= vigencia_inicio),

  CONSTRAINT chk_contrato_valor CHECK (valor >= 0)

);

  

-- ÍNDICES — TB_COMPETICAO

CREATE INDEX idx_comp_evento    ON TB_COMPETICAO(id_evento);

CREATE INDEX idx_comp_esporte   ON TB_COMPETICAO(id_esporte);

CREATE INDEX idx_comp_status    ON TB_COMPETICAO(status_competicao);

CREATE INDEX idx_comp_fase      ON TB_COMPETICAO(fase);

CREATE INDEX idx_comp_data      ON TB_COMPETICAO(data_hora);

  

-- ÍNDICES — TB_ARBITRAGEM

CREATE INDEX idx_arb_competicao ON TB_ARBITRAGEM(id_competicao);

  

-- ÍNDICES — TB_ATLETA

CREATE INDEX idx_atleta_equipe      ON TB_ATLETA(id_equipe);

CREATE INDEX idx_atleta_status      ON TB_ATLETA(status);

CREATE INDEX idx_atleta_nac         ON TB_ATLETA(nacionalidade);

  

-- ÍNDICES — TB_RESULTADO

CREATE INDEX idx_res_competicao ON TB_RESULTADO(id_competicao);

CREATE INDEX idx_res_atleta     ON TB_RESULTADO(id_atleta);

CREATE INDEX idx_res_equipe     ON TB_RESULTADO(id_equipe);

-- Índice composto para ranking dentro de uma competição

-- Cobre queries ORDER BY colocacao WHERE id_competicao = X

CREATE INDEX idx_res_comp_col   ON TB_RESULTADO(id_competicao, colocacao);

  

-- ÍNDICES — TB_CONTRATO_PATROCINIO

CREATE INDEX idx_cont_patrocinador  ON TB_CONTRATO_PATROCINIO(id_patrocinador);

CREATE INDEX idx_cont_atleta        ON TB_CONTRATO_PATROCINIO(id_atleta);

CREATE INDEX idx_cont_equipe        ON TB_CONTRATO_PATROCINIO(id_equipe);

CREATE INDEX idx_cont_evento        ON TB_CONTRATO_PATROCINIO(id_evento);

CREATE INDEX idx_cont_arbitro       ON TB_CONTRATO_PATROCINIO(id_arbitro);

CREATE INDEX idx_cont_status        ON TB_CONTRATO_PATROCINIO(status);

-- Índice composto para buscar contratos ativos por patrocinador

CREATE INDEX idx_cont_pat_status    ON TB_CONTRATO_PATROCINIO(id_patrocinador, status);

  

-- ÍNDICES — TB_EVENTO

CREATE INDEX idx_evento_status      ON TB_EVENTO(status_evento);

CREATE INDEX idx_evento_pais        ON TB_EVENTO(pais);

CREATE INDEX idx_evento_datas       ON TB_EVENTO(data_inicio, data_fim);

  

-- ÍNDICES — TB_PATROCINADOR

CREATE INDEX idx_pat_status         ON TB_PATROCINADOR(status);

CREATE INDEX idx_pat_pais           ON TB_PATROCINADOR(pais_origem);

  

-- ÍNDICES — TB_EQUIPE

CREATE INDEX idx_equipe_status      ON TB_EQUIPE(status);

CREATE INDEX idx_equipe_pais        ON TB_EQUIPE(pais_origem);

  

-- ÍNDICES — TB_ARBITRO

CREATE INDEX idx_arbitro_status     ON TB_ARBITRO(status_ativo);

CREATE INDEX idx_arbitro_nac        ON TB_ARBITRO(nacionalidade);
```