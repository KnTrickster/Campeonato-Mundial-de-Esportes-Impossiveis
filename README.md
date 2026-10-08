# Campeonato-Mundial-de-Esportes-Impossiveis
Repositório destinado a um trabalho acadêmico para a matéria de Programação para Banco de Dados.

## 📌 Sobre o projeto
Este projeto apresenta a modelagem de um banco de dados para gerenciamento de uma liga de esportes não convencionais, envolvendo modalidades extremas e inovadoras, como competições em gravidade zero e ambientes simulados.

O sistema foi projetado para controlar toda a estrutura organizacional da liga, incluindo eventos, competições, atletas, equipes, arbitragem, resultados e contratos de patrocínio.

---

## 🎯 Objetivo
Desenvolver um modelo de banco de dados robusto e consistente capaz de:

- Organizar eventos esportivos e suas competições
- Gerenciar atletas e equipes
- Controlar arbitragem e desempenho dos árbitros
- Registrar resultados de forma flexível (individual ou coletivo)
- Administrar contratos de patrocínio
- Garantir integridade e consistência dos dados

---

## 🧱 Estrutura do Projeto

O projeto está dividido em:

- **Modelo Conceitual**  
  Representação das entidades e seus relacionamentos

- **Modelo Lógico**  
  Estrutura detalhada com tabelas, atributos e relacionamentos

- **Modelo Físico**  
  Implementação em SQL com tabelas, constraints e índices

- **Consultas SQL**
  Consultas analíticas para exploração e avaliação dos dados 

- **Procedures**  
  Rotinas em PL/SQL para manipulação e processamento de dados, geração de relatórios e cálculos agregados.

- **Imagens**  
  Diagrama do Modelo Conceitual 
  ![Modelo Conceitual](./Imagem%20Modelo%20Conceitual.png)
  Diagrama do Modelo Lógico
  ![Modelo Lógico](./Imagem%20Modelo%20Lógico.png)
---

## ⚙️ Recursos e Implementações em PL/SQL

Além da modelagem e implementação do banco de dados, o projeto conta com consultas e recursos avançados em Oracle PL/SQL:

**📊 Cursor Explícito com Parâmetro**

Consulta e exibe o ranking oficial de uma competição específica, recuperando colocação, participante, origem, esporte, fase, pontuação e observações. O cursor percorre os resultados ordenados por colocação e utiliza DBMS_OUTPUT para apresentar os dados de forma organizada, além de informar o total de colocados e tratar possíveis erros durante a execução.

**🔎 Consultas SQL da AV2**

Reúne consultas analíticas para exploração e avaliação dos dados do campeonato. As consultas identificam os atletas com maior pontuação, modalidades com melhores médias, atletas sem resultados registrados e competições de alta intensidade, além de apresentar um quadro geral das competições. Também são analisados eventos sem patrocínio ativo e patrocinadores com maiores investimentos em eventos encerrados, utilizando JOINs, agregações (COUNT, SUM, AVG, MAX), subconsultas, HAVING, ordenação e filtros.

**⚖️ Função Agregada de Média Ponderada**

Implementa uma função agregada personalizada em Oracle para calcular a média das pontuações considerando pesos diferentes para cada fase da competição. A solução utiliza um tipo objeto com o ciclo ODCIAggregate (Initialize, Iterate, Merge e Terminate), acumulando a soma ponderada e os pesos das fases. Ao final, a função retorna a média ponderada arredondada, permitindo comparar o desempenho dos atletas com a média simples de suas pontuações.

**📋 Procedure de Relatório de Evento**

Gera um relatório consolidado do desempenho das competições de um evento específico. A procedure valida a existência do evento, retorna os dados das competições por meio de um SYS_REFCURSOR e calcula informações como quantidade de participantes, pontuação máxima e média, esporte e número de árbitros. Também identifica competições sem árbitros e informa o valor total de patrocínios ativos do evento. A execução demonstra o consumo do REF CURSOR linha a linha e a formatação dos resultados com DBMS_OUTPUT.

## 🚀 Tecnologias Utilizadas

- SQL (Oracle)
- Modelagem de Banco de Dados

---

## 📎 Observações

Este projeto foi desenvolvido com foco acadêmico, visando demonstrar boas práticas em modelagem de banco de dados e organização de sistemas complexos.

---

## 👤 Autores

- Gustavo Borges
- Kevin Torquato
- Kleber Kauã
