```sql
-- ============================================================

-- PROJETO: Campeonato Mundial de Esportes Impossiveis

-- ARQUIVO: Procedures minimas - VERSAO CORRIGIDA

-- OBSERVACAO:

--   Esta versao evita chamar funcao local diretamente dentro do INSERT,

--   pois em alguns ambientes Oracle isso gera PLS-00231.

-- ============================================================

  

CREATE OR REPLACE PROCEDURE PRC_CARGA_FIXA AS

BEGIN

    INSERT INTO TB_ESPORTE (nome, tipo_esporte, descricao, regras, unidade_pontuacao)

    VALUES (

        'Corrida em Gravidade Zero',

        'INDIVIDUAL',

        'Corrida simulada em ambiente sem gravidade.',

        'Vence quem concluir o percurso no menor tempo, evitando obstaculos orbitais.',

        'TEMPO'

    );

  

    INSERT INTO TB_ESPORTE (nome, tipo_esporte, descricao, regras, unidade_pontuacao)

    VALUES (

        'Natacao em Lava Simulada',

        'INDIVIDUAL',

        'Prova aquatica em ambiente extremo simulado.',

        'Vence quem atingir maior pontuacao tecnica sem tocar nas bordas de seguranca.',

        'PONTOS'

    );

  

    INSERT INTO TB_ESPORTE (nome, tipo_esporte, descricao, regras, unidade_pontuacao)

    VALUES (

        'Futebol com Campo Elastico',

        'COLETIVO',

        'Jogo coletivo em campo instavel com superficie elastica.',

        'Vence a equipe com maior pontuacao ao final do tempo regulamentar.',

        'PONTOS'

    );

  

    INSERT INTO TB_ESPORTE (nome, tipo_esporte, descricao, regras, unidade_pontuacao)

    VALUES (

        'Salto em Profundidade Inversa',

        'INDIVIDUAL',

        'Salto de dentro da terra para fora, usando propulsores.',

        'Pontuacao baseada na altura atingida apos sair da escavacao.',

        'METROS'

    );

  

    INSERT INTO TB_ESPORTE (nome, tipo_esporte, descricao, regras, unidade_pontuacao)

    VALUES (

        'Corrida de Obstaculos Magneticos',

        'INDIVIDUAL',

        'Pista com obstaculos magnetizados que repelem e atraem o atleta.',

        'Vence quem concluir o percurso sem ser ejetado pela pista.',

        'TEMPO'

    );

  

    INSERT INTO TB_ESPORTE (nome, tipo_esporte, descricao, regras, unidade_pontuacao)

    VALUES (

        'Arco e Flecha Subaquatico',

        'INDIVIDUAL',

        'Prova de precisao realizada completamente debaixo dagua.',

        'Pontuacao acumulada por alvos atingidos. Penalidade por boiar.',

        'PONTOS'

    );

  

    INSERT INTO TB_ESPORTE (nome, tipo_esporte, descricao, regras, unidade_pontuacao)

    VALUES (

        'Levantamento de Peso em Camara de Vacuo',

        'INDIVIDUAL',

        'Levantamento de pesos em ambiente sem pressao atmosferica.',

        'Vence quem levantar maior carga sem perder o traje de pressao.',

        'QUILOGRAMAS'

    );

  

    INSERT INTO TB_ESPORTE (nome, tipo_esporte, descricao, regras, unidade_pontuacao)

    VALUES (

        'Slalom em Buraco Negro Simulado',

        'INDIVIDUAL',

        'Manobras em torno de um campo gravitacional artificialmente gerado.',

        'Pontuacao por velocidade e precisao nas passagens pelas portas.',

        'PONTOS'

    );

  

    INSERT INTO TB_ESPORTE (nome, tipo_esporte, descricao, regras, unidade_pontuacao)

    VALUES (

        'Ginastica em Superficie Lunar',

        'INDIVIDUAL',

        'Execucao de movimentos ginasticos em superfice de baixa gravidade.',

        'Juizes avaliam tecnica, criatividade e pouso. Sem tocar no teto.',

        'PONTOS'

    );

  

    INSERT INTO TB_ESPORTE (nome, tipo_esporte, descricao, regras, unidade_pontuacao)

    VALUES (

        'Triatlo do Caos',

        'INDIVIDUAL',

        'Tres etapas: natacao em gelatina, ciclismo em esteira movel e corrida inversa.',

        'Tempo total das tres etapas. Penalidade de 30s por cada queda na gelatina.',

        'TEMPO'

    );

  

    INSERT INTO TB_ESPORTE (nome, tipo_esporte, descricao, regras, unidade_pontuacao)

    VALUES (

        'Escalada de Parede Invertida',

        'INDIVIDUAL',

        'Escalada no teto de uma estrutura usando apenas luvas adesivas.',

        'Vence quem concluir o percurso no menor tempo sem cair.',

        'TEMPO'

    );

  

    INSERT INTO TB_ESPORTE (nome, tipo_esporte, descricao, regras, unidade_pontuacao)

    VALUES (

        'Tiro ao Alvo Termico',

        'INDIVIDUAL',

        'Alvos que mudam de posicao conforme a temperatura do ambiente.',

        'Pontuacao maxima por acertos em alvos de alta temperatura.',

        'PONTOS'

    );

  

    INSERT INTO TB_ESPORTE (nome, tipo_esporte, descricao, regras, unidade_pontuacao)

    VALUES (

        'Volei em Camara de Gelo',

        'COLETIVO',

        'Partida de volei em quadra completamente congelada.',

        'Regras do volei tradicional. Ponto extra por placar de joelho.',

        'PONTOS'

    );

  

    INSERT INTO TB_ESPORTE (nome, tipo_esporte, descricao, regras, unidade_pontuacao)

    VALUES (

        'Cabo de Guerra em Lama Magnetica',

        'COLETIVO',

        'Disputa de forca com corda em lama com propriedades magneticas.',

        'Vence a equipe que puxar o adversario alem da linha em 3 de 5 rodadas.',

        'PONTOS'

    );

  

    INSERT INTO TB_ESPORTE (nome, tipo_esporte, descricao, regras, unidade_pontuacao)

    VALUES (

        'Basquete em Plataforma Rotativa',

        'COLETIVO',

        'Partida de basquete em quadra que gira 360 graus a cada minuto.',

        'Regras do basquete tradicional. Cesta durante a rotacao vale dobrado.',

        'PONTOS'

    );

  

    INSERT INTO TB_ESPORTE (nome, tipo_esporte, descricao, regras, unidade_pontuacao)

    VALUES (

        'Revezamento Subaquatico',

        'COLETIVO',

        'Corrida de revezamento onde cada membro da equipe completa um trecho debaixo dagua.',

        'Menor tempo total vence. Penalidade de 15s por respiro nao autorizado.',

        'TEMPO'

    );

  

    INSERT INTO TB_ESPORTE (nome, tipo_esporte, descricao, regras, unidade_pontuacao)

    VALUES (

        'Remo em Sal Grosso',

        'COLETIVO',

        'Corrida de barcos em pista preenchida com sal grosso compactado.',

        'Vence a equipe que cruzar a linha de chegada primeiro com o barco intacto.',

        'TEMPO'

    );

  

    INSERT INTO TB_ESPORTE (nome, tipo_esporte, descricao, regras, unidade_pontuacao)

    VALUES (

        'Polo Aquatico Gravitacional',

        'COLETIVO',

        'Polo aquatico em piscina com gravidade alternada a cada 2 minutos.',

        'Gols marcados durante gravidade normal valem 1 ponto, invertida valem 3.',

        'PONTOS'

    );

  

    INSERT INTO TB_ESPORTE (nome, tipo_esporte, descricao, regras, unidade_pontuacao)

    VALUES (

        'Corrida de Estafetas Caotica',

        'COLETIVO',

        'Revezamento com obstaculos aleatorios sorteados ao vivo.',

        'Menor tempo total vence. Obstaculos sao revelados apenas no inicio de cada trecho.',

        'TEMPO'

    );

  

    INSERT INTO TB_ESPORTE (nome, tipo_esporte, descricao, regras, unidade_pontuacao)

    VALUES (

        'Hoquei em Superficie de Espuma',

        'COLETIVO',

        'Partida de hoquei em pista coberta por 20cm de espuma.',

        'Regras do hoquei tradicional. Penalidade extra por afundar completamente na espuma.',

        'PONTOS'

    );

  

    COMMIT;

  

    INSERT INTO TB_EVENTO (nome, cidade, pais, data_inicio, data_fim, status_evento, descricao)

    VALUES (

        'Campeonato Mundial de Esportes Impossiveis 2025',

        'Sao Paulo',

        'Brasil',

        DATE '2025-03-10',

        DATE '2025-03-17',

        'ENCERRADO',

        'Primeira edicao do campeonato mundial. Evento inaugural com 10 modalidades.'

    );

  

    INSERT INTO TB_EVENTO (nome, cidade, pais, data_inicio, data_fim, status_evento, descricao)

    VALUES (

        'Copa Intercontinental de Esportes Impossiveis 2025',

        'Toquio',

        'Japao',

        DATE '2025-08-01',

        DATE '2025-08-10',

        'ENCERRADO',

        'Edicao intercontinental com equipes da Asia, Europa e Americas.'

    );

  

    INSERT INTO TB_EVENTO (nome, cidade, pais, data_inicio, data_fim, status_evento, descricao)

    VALUES (

        'Campeonato Mundial de Esportes Impossiveis 2026',

        'Berlin',

        'Alemanha',

        DATE '2026-06-15',

        DATE '2026-06-25',

        'PLANEJADO',

        'Segunda edicao do campeonato mundial. Estreia de 5 novas modalidades.'

    );

  

    INSERT INTO TB_ARBITRO (nome_completo, data_nascimento, nacionalidade, especialidade)

    VALUES ('Carlos Orbitais',  DATE '1980-05-10', 'Brasil',          'Gravidade Zero');

  

    INSERT INTO TB_ARBITRO (nome_completo, data_nascimento, nacionalidade, especialidade)

    VALUES ('Marina Vulcanica', DATE '1985-09-20', 'Chile',           'Lava Simulada');

  

    INSERT INTO TB_ARBITRO (nome_completo, data_nascimento, nacionalidade, especialidade)

    VALUES ('Joao Elastico',    DATE '1978-03-15', 'Portugal',        'Esportes Coletivos');

  

    INSERT INTO TB_ARBITRO (nome_completo, data_nascimento, nacionalidade, especialidade)

    VALUES ('Yuki Tanaka',      DATE '1990-11-02', 'Japao',           'Esportes Aquaticos');

  

    INSERT INTO TB_ARBITRO (nome_completo, data_nascimento, nacionalidade, especialidade)

    VALUES ('Amara Diallo',     DATE '1983-07-18', 'Senegal',         'Atletismo Extremo');

  

    INSERT INTO TB_ARBITRO (nome_completo, data_nascimento, nacionalidade, especialidade)

    VALUES ('Erik Nordstrom',   DATE '1976-01-30', 'Suecia',          'Esportes de Forca');

  

    INSERT INTO TB_ARBITRO (nome_completo, data_nascimento, nacionalidade, especialidade)

    VALUES ('Sofia Reyes',      DATE '1992-04-25', 'Mexico',          'Ginastica e Acrobacia');

  

    INSERT INTO TB_ARBITRO (nome_completo, data_nascimento, nacionalidade, especialidade)

    VALUES ('Liang Wei',        DATE '1988-08-14', 'China',           'Esportes de Precisao');

  

    INSERT INTO TB_ARBITRO (nome_completo, data_nascimento, nacionalidade, especialidade)

    VALUES ('Fatima Al-Hassan', DATE '1981-12-03', 'Emirados Arabes', 'Esportes Coletivos');

  

    INSERT INTO TB_ARBITRO (nome_completo, data_nascimento, nacionalidade, especialidade)

    VALUES ('Bruno Ferreira',   DATE '1995-06-09', 'Brasil',          'Velocidade e Cronometragem');

  

    INSERT INTO TB_COMPETICAO (id_evento, id_esporte, nome, fase, data_hora, local_competicao, status_competicao)

    VALUES (1, 1, 'Corrida em Gravidade Zero - Classificatoria',    'CLASSIFICATORIA', TIMESTAMP '2025-03-10 09:00:00', 'Arena Orbital',      'FINALIZADA');

  

    INSERT INTO TB_COMPETICAO (id_evento, id_esporte, nome, fase, data_hora, local_competicao, status_competicao)

    VALUES (1, 1, 'Corrida em Gravidade Zero - Final',              'FINAL',           TIMESTAMP '2025-03-11 15:00:00', 'Arena Orbital',      'FINALIZADA');

  

    INSERT INTO TB_COMPETICAO (id_evento, id_esporte, nome, fase, data_hora, local_competicao, status_competicao)

    VALUES (1, 2, 'Natacao em Lava Simulada - Classificatoria',     'CLASSIFICATORIA', TIMESTAMP '2025-03-10 11:00:00', 'Piscina Vulcanica',  'FINALIZADA');

  

    INSERT INTO TB_COMPETICAO (id_evento, id_esporte, nome, fase, data_hora, local_competicao, status_competicao)

    VALUES (1, 2, 'Natacao em Lava Simulada - Final',               'FINAL',           TIMESTAMP '2025-03-12 14:00:00', 'Piscina Vulcanica',  'FINALIZADA');

  

    INSERT INTO TB_COMPETICAO (id_evento, id_esporte, nome, fase, data_hora, local_competicao, status_competicao)

    VALUES (1, 3, 'Futebol com Campo Elastico - Fase de Grupos A',  'CLASSIFICATORIA', TIMESTAMP '2025-03-11 10:00:00', 'Arena Elastika',     'FINALIZADA');

  

    INSERT INTO TB_COMPETICAO (id_evento, id_esporte, nome, fase, data_hora, local_competicao, status_competicao)

    VALUES (1, 3, 'Futebol com Campo Elastico - Fase de Grupos B',  'CLASSIFICATORIA', TIMESTAMP '2025-03-11 13:00:00', 'Arena Elastika',     'FINALIZADA');

  

    INSERT INTO TB_COMPETICAO (id_evento, id_esporte, nome, fase, data_hora, local_competicao, status_competicao)

    VALUES (1, 3, 'Futebol com Campo Elastico - Final',             'FINAL',           TIMESTAMP '2025-03-15 16:00:00', 'Arena Elastika',     'FINALIZADA');

  

    INSERT INTO TB_COMPETICAO (id_evento, id_esporte, nome, fase, data_hora, local_competicao, status_competicao)

    VALUES (1, 5, 'Corrida de Obstaculos Magneticos - Unica',       'UNICA',           TIMESTAMP '2025-03-12 09:00:00', 'Pista Magnetica',    'FINALIZADA');

  

    INSERT INTO TB_COMPETICAO (id_evento, id_esporte, nome, fase, data_hora, local_competicao, status_competicao)

    VALUES (1, 7, 'Levantamento de Peso em Vacuo - Classificatoria','CLASSIFICATORIA', TIMESTAMP '2025-03-13 10:00:00', 'Camara de Vacuo',    'FINALIZADA');

  

    INSERT INTO TB_COMPETICAO (id_evento, id_esporte, nome, fase, data_hora, local_competicao, status_competicao)

    VALUES (1, 7, 'Levantamento de Peso em Vacuo - Final',          'FINAL',           TIMESTAMP '2025-03-14 14:00:00', 'Camara de Vacuo',    'FINALIZADA');

  

    INSERT INTO TB_COMPETICAO (id_evento, id_esporte, nome, fase, data_hora, local_competicao, status_competicao)

    VALUES (1, 9, 'Ginastica em Superficie Lunar - Unica',          'UNICA',           TIMESTAMP '2025-03-13 16:00:00', 'Dome Lunar',         'FINALIZADA');

  

    INSERT INTO TB_COMPETICAO (id_evento, id_esporte, nome, fase, data_hora, local_competicao, status_competicao)

    VALUES (1, 13, 'Volei em Camara de Gelo - Semifinal 1',         'SEMIFINAL',       TIMESTAMP '2025-03-14 10:00:00', 'Quadra Glacial',     'FINALIZADA');

  

    INSERT INTO TB_COMPETICAO (id_evento, id_esporte, nome, fase, data_hora, local_competicao, status_competicao)

    VALUES (1, 13, 'Volei em Camara de Gelo - Semifinal 2',         'SEMIFINAL',       TIMESTAMP '2025-03-14 13:00:00', 'Quadra Glacial',     'FINALIZADA');

  

    INSERT INTO TB_COMPETICAO (id_evento, id_esporte, nome, fase, data_hora, local_competicao, status_competicao)

    VALUES (1, 13, 'Volei em Camara de Gelo - Final',               'FINAL',           TIMESTAMP '2025-03-16 15:00:00', 'Quadra Glacial',     'FINALIZADA');

  

    INSERT INTO TB_COMPETICAO (id_evento, id_esporte, nome, fase, data_hora, local_competicao, status_competicao)

    VALUES (1, 15, 'Basquete em Plataforma Rotativa - Final',       'FINAL',           TIMESTAMP '2025-03-17 14:00:00', 'Arena Rotativa SP',  'FINALIZADA');

  

    INSERT INTO TB_COMPETICAO (id_evento, id_esporte, nome, fase, data_hora, local_competicao, status_competicao)

    VALUES (2, 1, 'Corrida em Gravidade Zero - Copa Intercont.',     'UNICA',           TIMESTAMP '2025-08-01 10:00:00', 'Dome Orbital Tokyo', 'FINALIZADA');

  

    INSERT INTO TB_COMPETICAO (id_evento, id_esporte, nome, fase, data_hora, local_competicao, status_competicao)

    VALUES (2, 4, 'Salto em Profundidade Inversa - Classificatoria', 'CLASSIFICATORIA', TIMESTAMP '2025-08-02 09:00:00', 'Poco Meiji',         'FINALIZADA');

  

    INSERT INTO TB_COMPETICAO (id_evento, id_esporte, nome, fase, data_hora, local_competicao, status_competicao)

    VALUES (2, 4, 'Salto em Profundidade Inversa - Final',           'FINAL',           TIMESTAMP '2025-08-04 14:00:00', 'Poco Meiji',         'FINALIZADA');

  

    INSERT INTO TB_COMPETICAO (id_evento, id_esporte, nome, fase, data_hora, local_competicao, status_competicao)

    VALUES (2, 6, 'Arco e Flecha Subaquatico - Classificatoria',     'CLASSIFICATORIA', TIMESTAMP '2025-08-02 11:00:00', 'Piscina Olimpica TK','FINALIZADA');

  

    INSERT INTO TB_COMPETICAO (id_evento, id_esporte, nome, fase, data_hora, local_competicao, status_competicao)

    VALUES (2, 6, 'Arco e Flecha Subaquatico - Final',               'FINAL',           TIMESTAMP '2025-08-05 15:00:00', 'Piscina Olimpica TK','FINALIZADA');

  

    INSERT INTO TB_COMPETICAO (id_evento, id_esporte, nome, fase, data_hora, local_competicao, status_competicao)

    VALUES (2, 8, 'Slalom em Buraco Negro Simulado - Unica',         'UNICA',           TIMESTAMP '2025-08-03 10:00:00', 'Camara Gravitacional','FINALIZADA');

  

    INSERT INTO TB_COMPETICAO (id_evento, id_esporte, nome, fase, data_hora, local_competicao, status_competicao)

    VALUES (2, 10, 'Triatlo do Caos - Unica',                        'UNICA',           TIMESTAMP '2025-08-04 08:00:00', 'Complexo do Caos',   'FINALIZADA');

  

    INSERT INTO TB_COMPETICAO (id_evento, id_esporte, nome, fase, data_hora, local_competicao, status_competicao)

    VALUES (2, 11, 'Escalada de Parede Invertida - Classificatoria', 'CLASSIFICATORIA', TIMESTAMP '2025-08-05 09:00:00', 'Estrutura Teto TK',  'FINALIZADA');

  

    INSERT INTO TB_COMPETICAO (id_evento, id_esporte, nome, fase, data_hora, local_competicao, status_competicao)

    VALUES (2, 11, 'Escalada de Parede Invertida - Final',           'FINAL',           TIMESTAMP '2025-08-07 11:00:00', 'Estrutura Teto TK',  'FINALIZADA');

  

    INSERT INTO TB_COMPETICAO (id_evento, id_esporte, nome, fase, data_hora, local_competicao, status_competicao)

    VALUES (2, 14, 'Cabo de Guerra em Lama Magnetica - Semifinal',   'SEMIFINAL',       TIMESTAMP '2025-08-06 14:00:00', 'Arena Lama',         'FINALIZADA');

  

    INSERT INTO TB_COMPETICAO (id_evento, id_esporte, nome, fase, data_hora, local_competicao, status_competicao)

    VALUES (2, 14, 'Cabo de Guerra em Lama Magnetica - Final',       'FINAL',           TIMESTAMP '2025-08-08 16:00:00', 'Arena Lama',         'FINALIZADA');

  

    INSERT INTO TB_COMPETICAO (id_evento, id_esporte, nome, fase, data_hora, local_competicao, status_competicao)

    VALUES (2, 16, 'Revezamento Subaquatico - Unica',                'UNICA',           TIMESTAMP '2025-08-07 13:00:00', 'Piscina Olimpica TK','FINALIZADA');

  

    INSERT INTO TB_COMPETICAO (id_evento, id_esporte, nome, fase, data_hora, local_competicao, status_competicao)

    VALUES (2, 18, 'Polo Aquatico Gravitacional - Semifinal',        'SEMIFINAL',       TIMESTAMP '2025-08-08 10:00:00', 'Arena Aqua Grav TK', 'FINALIZADA');

  

    INSERT INTO TB_COMPETICAO (id_evento, id_esporte, nome, fase, data_hora, local_competicao, status_competicao)

    VALUES (2, 18, 'Polo Aquatico Gravitacional - Final',            'FINAL',           TIMESTAMP '2025-08-09 15:00:00', 'Arena Aqua Grav TK', 'FINALIZADA');

  

    INSERT INTO TB_COMPETICAO (id_evento, id_esporte, nome, fase, data_hora, local_competicao, status_competicao)

    VALUES (2, 20, 'Hoquei em Superficie de Espuma - Final',         'FINAL',           TIMESTAMP '2025-08-10 14:00:00', 'Rink de Espuma TK',  'FINALIZADA');

  

    INSERT INTO TB_COMPETICAO (id_evento, id_esporte, nome, fase, data_hora, local_competicao, status_competicao)

    VALUES (3, 1, 'Corrida em Gravidade Zero - Mundial 2026',        'FINAL',           TIMESTAMP '2026-06-15 10:00:00', 'Dome Orbital Berlin','AGENDADA');

  

    INSERT INTO TB_COMPETICAO (id_evento, id_esporte, nome, fase, data_hora, local_competicao, status_competicao)

    VALUES (3, 2, 'Natacao em Lava Simulada - Mundial 2026',         'FINAL',           TIMESTAMP '2026-06-16 11:00:00', 'Piscina Vulcanica BE','AGENDADA');

  

    INSERT INTO TB_COMPETICAO (id_evento, id_esporte, nome, fase, data_hora, local_competicao, status_competicao)

    VALUES (3, 12, 'Tiro ao Alvo Termico - Classificatoria',         'CLASSIFICATORIA', TIMESTAMP '2026-06-17 09:00:00', 'Campo Termico',      'AGENDADA');

  

    INSERT INTO TB_COMPETICAO (id_evento, id_esporte, nome, fase, data_hora, local_competicao, status_competicao)

    VALUES (3, 12, 'Tiro ao Alvo Termico - Final',                   'FINAL',           TIMESTAMP '2026-06-20 14:00:00', 'Campo Termico',      'AGENDADA');

  

    INSERT INTO TB_COMPETICAO (id_evento, id_esporte, nome, fase, data_hora, local_competicao, status_competicao)

    VALUES (3, 17, 'Remo em Sal Grosso - Semifinal',                 'SEMIFINAL',       TIMESTAMP '2026-06-18 10:00:00', 'Canal Salgado',      'AGENDADA');

  

    INSERT INTO TB_COMPETICAO (id_evento, id_esporte, nome, fase, data_hora, local_competicao, status_competicao)

    VALUES (3, 17, 'Remo em Sal Grosso - Final',                     'FINAL',           TIMESTAMP '2026-06-21 15:00:00', 'Canal Salgado',      'AGENDADA');

  

    INSERT INTO TB_COMPETICAO (id_evento, id_esporte, nome, fase, data_hora, local_competicao, status_competicao)

    VALUES (3, 19, 'Corrida de Estafetas Caotica - Unica',           'UNICA',           TIMESTAMP '2026-06-22 09:00:00', 'Pista do Caos',      'AGENDADA');

  

    INSERT INTO TB_COMPETICAO (id_evento, id_esporte, nome, fase, data_hora, local_competicao, status_competicao)

    VALUES (3, 3, 'Futebol com Campo Elastico - Mundial 2026',       'FINAL',           TIMESTAMP '2026-06-23 16:00:00', 'Arena Elastika BE',  'AGENDADA');

  

    INSERT INTO TB_COMPETICAO (id_evento, id_esporte, nome, fase, data_hora, local_competicao, status_competicao)

    VALUES (3, 15, 'Basquete em Plataforma Rotativa - Semifinal',    'SEMIFINAL',       TIMESTAMP '2026-06-24 14:00:00', 'Arena Rotativa BE',  'AGENDADA');

  

    INSERT INTO TB_COMPETICAO (id_evento, id_esporte, nome, fase, data_hora, local_competicao, status_competicao)

    VALUES (3, 15, 'Basquete em Plataforma Rotativa - Final',        'FINAL',           TIMESTAMP '2026-06-25 17:00:00', 'Arena Rotativa BE',  'AGENDADA');

  

    INSERT INTO TB_PATROCINADOR (nome, cnpj, pais_origem, email_contato)

    VALUES ('Impossivel Sports',    '11111111000111', 'Brasil',          'contato@impossivel.com');

  

    INSERT INTO TB_PATROCINADOR (nome, cnpj, pais_origem, email_contato)

    VALUES ('Gravity Company',      '22222222000122', 'Estados Unidos',  'contato@gravity.com');

  

    INSERT INTO TB_PATROCINADOR (nome, cnpj, pais_origem, email_contato)

    VALUES ('Lava Safe Corp',       '33333333000133', 'Japao',           'contato@lavasafe.com');

  

    INSERT INTO TB_PATROCINADOR (nome, cnpj, pais_origem, email_contato, website)

    VALUES ('Zero G Technologies',  '44444444000144', 'Estados Unidos',  'sponsor@zerog.com',    'www.zerog.com');

  

    INSERT INTO TB_PATROCINADOR (nome, cnpj, pais_origem, email_contato, website)

    VALUES ('Polar Extreme Gear',   '55555555000155', 'Noruega',         'hi@polarextreme.no',   'www.polarextreme.no');

  

    INSERT INTO TB_PATROCINADOR (nome, cnpj, pais_origem, email_contato, telefone_contato)

    VALUES ('Magnetix Corp',        '66666666000166', 'Alemanha',        'info@magnetix.de',     '+49 30 12345678');

  

    INSERT INTO TB_PATROCINADOR (nome, cnpj, pais_origem, email_contato, website)

    VALUES ('AquaVenture Ltd',      '77777777000177', 'Australia',       'info@aquaventure.au',  'www.aquaventure.au');

  

    INSERT INTO TB_PATROCINADOR (nome, cnpj, pais_origem, email_contato, telefone_contato)

    VALUES ('Chaos Energy Drink',   '88888888000188', 'Brasil',          'patrocinio@chaos.com', '+55 11 99999999');

  

    INSERT INTO TB_PATROCINADOR (nome, cnpj, pais_origem, email_contato, website)

    VALUES ('Orbital Vision Media', '99999999000199', 'Reino Unido',     'media@orbital.co.uk',  'www.orbital.co.uk');

  

    INSERT INTO TB_PATROCINADOR (nome, cnpj, pais_origem, email_contato, website)

    VALUES ('Elastic World Inc',    '10101010000100', 'Canada',          'hello@elasticworld.ca','www.elasticworld.ca');

  

    INSERT INTO TB_ARBITRAGEM (id_arbitro, id_competicao, papel, avaliacao_desempenho, observacoes)

    VALUES (1, 1,  'PRINCIPAL',     9, 'Arbitro principal da Corrida em Gravidade Zero - Classificatoria.');

  

    INSERT INTO TB_ARBITRAGEM (id_arbitro, id_competicao, papel, avaliacao_desempenho, observacoes)

    VALUES (2, 3,  'PRINCIPAL',     8, 'Arbitro principal da Natacao em Lava Simulada - Classificatoria.');

  

    INSERT INTO TB_ARBITRAGEM (id_arbitro, id_competicao, papel, avaliacao_desempenho, observacoes)

    VALUES (3, 5,  'PRINCIPAL',    10, 'Arbitro principal do Futebol com Campo Elastico - Grupos A.');

  

    INSERT INTO TB_ARBITRAGEM (id_arbitro, id_competicao, papel, avaliacao_desempenho, observacoes)

    VALUES (10, 1, 'CRONOMETRISTA',  9, 'Responsavel pela cronometragem oficial da classificatoria.');

  

    INSERT INTO TB_ARBITRAGEM (id_arbitro, id_competicao, papel, avaliacao_desempenho, observacoes)

    VALUES (1,  2, 'PRINCIPAL',     10, 'Arbitro principal da Final da Corrida em Gravidade Zero.');

  

    INSERT INTO TB_ARBITRAGEM (id_arbitro, id_competicao, papel, avaliacao_desempenho, observacoes)

    VALUES (10, 2, 'CRONOMETRISTA',  9, 'Cronometragem da final.');

  

    INSERT INTO TB_ARBITRAGEM (id_arbitro, id_competicao, papel, avaliacao_desempenho, observacoes)

    VALUES (2,  4, 'PRINCIPAL',      9, 'Arbitro principal da Final da Natacao em Lava Simulada.');

  

    INSERT INTO TB_ARBITRAGEM (id_arbitro, id_competicao, papel, avaliacao_desempenho, observacoes)

    VALUES (3,  6, 'PRINCIPAL',      8, 'Arbitro principal do Futebol com Campo Elastico - Grupos B.');

  

    INSERT INTO TB_ARBITRAGEM (id_arbitro, id_competicao, papel, avaliacao_desempenho, observacoes)

    VALUES (9,  6, 'AUXILIAR',       7, 'Auxiliou no controle de irregularidades de campo.');

  

    INSERT INTO TB_ARBITRAGEM (id_arbitro, id_competicao, papel, avaliacao_desempenho, observacoes)

    VALUES (3,  7, 'PRINCIPAL',     10, 'Arbitro principal da Grande Final do Futebol Elastico.');

  

    INSERT INTO TB_ARBITRAGEM (id_arbitro, id_competicao, papel, avaliacao_desempenho, observacoes)

    VALUES (9,  7, 'AUXILIAR',       9, 'Auxiliar de linha na final.');

  

    INSERT INTO TB_ARBITRAGEM (id_arbitro, id_competicao, papel, avaliacao_desempenho, observacoes)

    VALUES (5,  8, 'PRINCIPAL',      8, 'Arbitro principal da Corrida de Obstaculos Magneticos.');

  

    INSERT INTO TB_ARBITRAGEM (id_arbitro, id_competicao, papel, avaliacao_desempenho, observacoes)

    VALUES (6,  9, 'PRINCIPAL',      9, 'Arbitro principal do Levantamento de Peso em Vacuo - Classif.');

  

    INSERT INTO TB_ARBITRAGEM (id_arbitro, id_competicao, papel, avaliacao_desempenho, observacoes)

    VALUES (6, 10, 'PRINCIPAL',     10, 'Arbitro principal da Final do Levantamento de Peso em Vacuo.');

  

    INSERT INTO TB_ARBITRAGEM (id_arbitro, id_competicao, papel, avaliacao_desempenho, observacoes)

    VALUES (7, 11, 'PRINCIPAL',      9, 'Arbitro principal da Ginastica em Superficie Lunar.');

  

    INSERT INTO TB_ARBITRAGEM (id_arbitro, id_competicao, papel, avaliacao_desempenho, observacoes)

    VALUES (9, 12, 'PRINCIPAL',      8, 'Arbitro principal do Volei em Camara de Gelo - Semifinal 1.');

  

    INSERT INTO TB_ARBITRAGEM (id_arbitro, id_competicao, papel, avaliacao_desempenho, observacoes)

    VALUES (9, 13, 'PRINCIPAL',      9, 'Arbitro principal do Volei em Camara de Gelo - Semifinal 2.');

  

    INSERT INTO TB_ARBITRAGEM (id_arbitro, id_competicao, papel, avaliacao_desempenho, observacoes)

    VALUES (9, 14, 'PRINCIPAL',     10, 'Arbitro principal da Final do Volei em Camara de Gelo.');

  

    INSERT INTO TB_ARBITRAGEM (id_arbitro, id_competicao, papel, avaliacao_desempenho, observacoes)

    VALUES (3, 15, 'PRINCIPAL',      9, 'Arbitro principal da Final do Basquete em Plataforma Rotativa.');

  

    INSERT INTO TB_ARBITRAGEM (id_arbitro, id_competicao, papel, avaliacao_desempenho, observacoes)

    VALUES (4, 16, 'PRINCIPAL',      8, 'Arbitro principal da Corrida em Gravidade Zero - Copa Intercont.');

  

    COMMIT;

END;

/

  

CREATE OR REPLACE PROCEDURE PRC_GERA_DADOS (

    p_qtd_equipes    IN NUMBER,

    p_qtd_atletas    IN NUMBER,

    p_qtd_resultados IN NUMBER,

    p_qtd_contratos  IN NUMBER

) AS

    v_alvo NUMBER;

  

    v_id_equipe NUMBER;

    v_id_atleta NUMBER;

    v_id_competicao NUMBER;

    v_id_patrocinador NUMBER;

    v_id_evento NUMBER;

    v_id_arbitro NUMBER;

BEGIN

    FOR i IN 1..p_qtd_equipes LOOP

        INSERT INTO TB_EQUIPE (nome_equipe, sigla, pais_origem, tecnico)

        VALUES ('Equipe ' || TRUNC(DBMS_RANDOM.VALUE(1,3000)), 'EQ' || TRUNC(DBMS_RANDOM.VALUE(1,3000)), 'Pais ' || TRUNC(DBMS_RANDOM.VALUE(1,3000)), 'Tecnico ' || TRUNC(DBMS_RANDOM.VALUE(1,3000)));

    END LOOP;

  

    FOR i IN 1..p_qtd_atletas LOOP

        SELECT id_equipe

        INTO v_id_equipe

        FROM (

            SELECT id_equipe

            FROM TB_EQUIPE

            ORDER BY DBMS_RANDOM.VALUE

        )

        WHERE ROWNUM = 1;

  

        INSERT INTO TB_ATLETA (

            id_equipe, nome_completo, apelido, data_nascimento,

            nacionalidade, sexo_biologico, status

        )

        VALUES (

            CASE TRUNC(DBMS_RANDOM.VALUE(1,2))

                WHEN 1 THEN v_id_equipe

                WHEN 2 THEN null

            END,

            'Atleta ' || TRUNC(DBMS_RANDOM.VALUE(1,3000)),

            'Apelido ' || TRUNC(DBMS_RANDOM.VALUE(1,3000)),

            TRUNC(SYSDATE - DBMS_RANDOM.VALUE(7000, 15000)),

            'Pais ' || TRUNC(DBMS_RANDOM.VALUE(1, 6)),

            CASE TRUNC(DBMS_RANDOM.VALUE(1, 4))

                WHEN 1 THEN 'M'

                WHEN 2 THEN 'F'

                ELSE 'O'

            END,

            'ATIVO'

        );

    END LOOP;

  

    FOR i IN 1..p_qtd_resultados LOOP

        v_alvo := TRUNC(DBMS_RANDOM.VALUE(1, 3));

  

        SELECT id_competicao

        INTO v_id_competicao

        FROM (

            SELECT id_competicao

            FROM TB_COMPETICAO

            ORDER BY DBMS_RANDOM.VALUE

        )

        WHERE ROWNUM = 1;

  

        IF v_alvo = 1 THEN

            SELECT id_atleta

            INTO v_id_atleta

            FROM (

                SELECT id_atleta

                FROM TB_ATLETA

                ORDER BY DBMS_RANDOM.VALUE

            )

            WHERE ROWNUM = 1;

  

            v_id_equipe := NULL;

        ELSE

            SELECT id_equipe

            INTO v_id_equipe

            FROM (

                SELECT id_equipe

                FROM TB_EQUIPE

                ORDER BY DBMS_RANDOM.VALUE

            )

            WHERE ROWNUM = 1;

  

            v_id_atleta := NULL;

        END IF;

  

        INSERT INTO TB_RESULTADO (

            id_competicao, id_atleta, id_equipe,

            colocacao, pontuacao, observacoes

        )

        VALUES (

            v_id_competicao,

            v_id_atleta,

            v_id_equipe,

            TRUNC(DBMS_RANDOM.VALUE(1, 11)),

            ROUND(DBMS_RANDOM.VALUE(1, 1000), 2),

            'Resultado gerado automaticamente'

        );

    END LOOP;

  

    FOR i IN 1..p_qtd_contratos LOOP

        v_alvo := TRUNC(DBMS_RANDOM.VALUE(1, 5));

  

        SELECT id_patrocinador

        INTO v_id_patrocinador

        FROM (

            SELECT id_patrocinador

            FROM TB_PATROCINADOR

            ORDER BY DBMS_RANDOM.VALUE

        )

        WHERE ROWNUM = 1;

  

        v_id_atleta := NULL;

        v_id_equipe := NULL;

        v_id_evento := NULL;

        v_id_arbitro := NULL;

  

        IF v_alvo = 1 THEN

            SELECT id_atleta

            INTO v_id_atleta

            FROM (

                SELECT id_atleta

                FROM TB_ATLETA

                ORDER BY DBMS_RANDOM.VALUE

            )

            WHERE ROWNUM = 1;

        ELSIF v_alvo = 2 THEN

            SELECT id_equipe

            INTO v_id_equipe

            FROM (

                SELECT id_equipe

                FROM TB_EQUIPE

                ORDER BY DBMS_RANDOM.VALUE

            )

            WHERE ROWNUM = 1;

        ELSIF v_alvo = 3 THEN

            SELECT id_evento

            INTO v_id_evento

            FROM (

                SELECT id_evento

                FROM TB_EVENTO

                ORDER BY DBMS_RANDOM.VALUE

            )

            WHERE ROWNUM = 1;

        ELSE

            SELECT id_arbitro

            INTO v_id_arbitro

            FROM (

                SELECT id_arbitro

                FROM TB_ARBITRO

                ORDER BY DBMS_RANDOM.VALUE

            )

            WHERE ROWNUM = 1;

        END IF;

  

        INSERT INTO TB_CONTRATO_PATROCINIO (

            id_patrocinador, id_atleta, id_equipe, id_evento, id_arbitro,

            tipo_patrocinio, valor, vigencia_inicio, vigencia_fim, status

        )

        VALUES (

            v_id_patrocinador,

            v_id_atleta,

            v_id_equipe,

            v_id_evento,

            v_id_arbitro,

            CASE TRUNC(DBMS_RANDOM.VALUE(1, 5))

                WHEN 1 THEN 'COTA_OURO'

                WHEN 2 THEN 'NAMING_RIGHTS'

                WHEN 3 THEN 'COTA_PRATA'

                WHEN 4 THEN 'COTA_BRONZE'

                WHEN 5 THEN 'FORNECEDOR'

            END,

            ROUND(DBMS_RANDOM.VALUE(1000, 100000), 2),

            SYSDATE,

            SYSDATE + 365,

            CASE TRUNC(DBMS_RANDOM.VALUE(1, 4))

                WHEN 1 THEN 'ATIVO'

                WHEN 2 THEN 'ENCERRADO'

                WHEN 3 THEN 'SUSPENSO'

                WHEN 4 THEN 'EM_NEGOCIACAO'

            END

        );

    END LOOP;

  

    COMMIT;

END;

/
```