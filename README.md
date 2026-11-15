# MedAgenda — Sistema de Gestão de Consultas Médicas

[![Projeto Acadêmico](https://img.shields.io/badge/Projeto-Acadêmico-blue)](https://github.com/kaiojnsc/med.agenda)
[![Disciplina](https://img.shields.io/badge/Disciplina-Teste%20de%20Software-green)](https://github.com/kaiojnsc/med.agenda)

## 1. Apresentação

O **MedAgenda** é um sistema web destinado a apoiar a rotina administrativa e operacional de uma clínica médica. A proposta reúne funcionalidades de gerenciamento de usuários, cadastro de pacientes, agendamento e acompanhamento de consultas, registro de prontuários, emissão de documentos, notificações e relatórios.

O sistema contempla quatro perfis de acesso — administrador, secretária, médico e paciente —, cada um com responsabilidades e permissões específicas.

Este repositório está relacionado ao projeto acadêmico da disciplina **Teste de Software**, do curso de Sistemas de Informação, período 2026.2, cujo objetivo é elaborar o Plano de Testes e Validação do MedAgenda.

## 2. Objetivos do projeto

- Documentar a arquitetura e a organização técnica do sistema.
- Identificar requisitos funcionais e não funcionais.
- Descrever regras de negócio e permissões dos perfis de acesso.
- Representar os principais fluxos e funcionalidades por meio de diagramas.
- Elaborar o planejamento de testes e a análise de riscos.
- Definir critérios e condições para uma futura validação do software.

## 3. Funcionalidades do sistema

O MedAgenda contempla as seguintes áreas funcionais:

| Módulo | Funcionalidades |
|---|---|
| Autenticação | Login, logout, gerenciamento de sessão e perfil. |
| Usuários | Cadastro, edição, ativação, desativação e redefinição de senhas. |
| Pacientes | Cadastro, consulta, pesquisa e edição de fichas. |
| Médicos e agenda | Consulta de médicos, configuração de horários e disponibilidade. |
| Consultas | Agendamento, confirmação, cancelamento e registro de faltas. |
| Atendimento | Início e finalização de consultas e registro de prontuários. |
| Documentos | Emissão de comprovantes, receitas e atestados em PDF. |
| Comunicação | Notificações e assistente virtual. |
| Relatórios | Relatórios de consultas, indicadores e informações financeiras. |
| Painel | Informações e indicadores conforme o perfil de acesso. |

## 4. Perfis de acesso

O sistema possui quatro perfis:

- **Administrador:** gerencia contas de acesso, configura informações dos médicos e consulta relatórios da clínica.
- **Secretária:** cadastra e consulta pacientes, organiza agendamentos, confirma consultas, registra faltas e realiza cancelamentos conforme as regras.
- **Médico:** acompanha sua agenda, consulta pacientes vinculados aos atendimentos, registra prontuários e finaliza consultas.
- **Paciente:** consulta suas informações, agenda e acompanha consultas, realiza cancelamentos dentro do prazo permitido e acessa documentos disponíveis.

As permissões devem ser respeitadas tanto na interface quanto na API, conforme a matriz de permissões documentada no projeto.

## 5. Tecnologias utilizadas

As tecnologias identificadas nos arquivos de configuração e no código-fonte disponibilizado são:

| Tecnologia | Versão identificada | Aplicação |
|---|---|---|
| React | 18 | Construção da interface web. |
| React Router | — | Navegação entre páginas. |
| Vite | — | Desenvolvimento e compilação do frontend. |
| Node.js | 20 | Ambiente de execução do backend. |
| Express | 4 | Construção da API REST. |
| MongoDB | 7 | Banco de dados. |
| Mongoose | 8 | Modelagem e acesso aos dados. |
| Nginx | 1.27 | Servidor web e encaminhamento de requisições. |
| Docker | — | Conteinerização dos serviços. |
| Docker Compose | — | Orquestração do ambiente. |

O backend também utiliza bibliotecas como JWT, bcryptjs, PDFKit, cors e morgan.

*As versões apresentadas correspondem às identificadas nos arquivos analisados, não representando atualização das dependências.*

## 6. Arquitetura do sistema

A arquitetura está organizada em três serviços principais:

1. **Web:** disponibiliza a interface utilizada pelos usuários.
2. **API:** processa as requisições, aplica as regras de negócio e controla o acesso aos recursos.
3. **MongoDB:** armazena as informações utilizadas pela aplicação.

O fluxo de comunicação pode ser resumido da seguinte maneira:

```text
Navegador
    |
    v
Serviço Web (Nginx)
    |
    v
API REST (Node.js + Express)
    |
    v
Mongoose
    |
    v
MongoDB
```

O Nginx disponibiliza a interface e encaminha as requisições destinadas a `/api` para o serviço da API. A API utiliza o Mongoose para acessar e persistir os dados no MongoDB.

### Endereços locais identificados

| Componente | Endereço |
|---|---|
| Interface Web | http://localhost:8080 |
| API REST | http://localhost:3000/api |
| MongoDB | mongodb://localhost:27017/medagenda |

## 7. Modelo de dados

A análise do código identificou cinco estruturas principais:

- **Usuario:** armazena informações de acesso, perfil e dados específicos dos médicos.
- **Paciente:** mantém informações cadastrais e dados utilizados no atendimento.
- **Consulta:** relaciona pacientes e médicos, armazenando informações do agendamento e atendimento.
- **Notificacao:** registra notificações vinculadas aos usuários.
- **MensagemChat:** registra mensagens do usuário e do assistente virtual.

Duas características importantes da modelagem:

- O médico não possui uma entidade independente: é representado por um registro de Usuario com perfil MEDICO.
- O prontuário é armazenado como subdocumento de Consulta, não como uma coleção independente.

## 8. Estrutura do projeto

A aplicação está dividida em duas partes principais de código, além da infraestrutura de banco de dados:

```text
MedAgenda/
├── web/
│   └── src/
│       ├── pages/
│       └── api.js
│
├── api/
│   └── src/
│       ├── routes/
│       ├── services/
│       ├── middleware/
│       └── models.js
│
├── docker-compose.yml
└── README.md
```

*Representação resumida dos diretórios identificados na análise. Não substitui a estrutura completa do repositório.*

## 9. Execução do projeto

O ambiente de referência utiliza Docker Compose, com três serviços: `web`, `api` e `mongo`.

### Pré-requisitos

- Docker instalado.
- Docker Compose disponível.
- Repositório do MedAgenda obtido localmente.

### Endereços de acesso

Após a inicialização adequada dos serviços, os endereços locais documentados são:

- Interface: http://localhost:8080
- API: http://localhost:3000/api

**Importante:** consulte o guia de execução fornecido pelo professor e as configurações do repositório para os comandos de inicialização, configuração de ambiente e carga inicial de dados. Os procedimentos devem ser conferidos antes de sua utilização.

### Dados de demonstração

O material do instrutor prevê uma massa de dados fictícios, incluindo contas de demonstração, pacientes e consultas.

O comando de restauração indicado no material é:

```bash
docker compose exec api npm run seed
```

Esse procedimento está registrado como orientação documental e não foi executado pela equipe.

Não utilize dados reais de pacientes em ambientes de teste.

## 10. Documentação técnica e testes

Como parte do projeto acadêmico, foi elaborado um documento consolidado contendo:

- Introdução e caracterização do sistema.
- Análise da arquitetura e das tecnologias.
- Diagrama de arquitetura.
- Modelo de dados e relacionamentos.
- Inventário de módulos.
- Requisitos funcionais e não funcionais.
- Regras de negócio.
- Matriz de permissões.
- Diagrama de casos de uso.
- Fluxo do ciclo de vida das consultas.
- Plano de testes e definição do escopo.
- Análise de riscos.
- Estratégia, técnicas e níveis de teste.
- Critérios de entrada, saída e suspensão.
- Ambiente e dados de teste previstos.
- Gestão de defeitos e responsabilidades.

A documentação considera os requisitos RF01 a RF15, as regras de negócio RN01 a RN19 e os requisitos não funcionais RNF01 a RNF07.

## 11. Limitações da avaliação

A atividade acadêmica foi desenvolvida com foco na documentação técnica, análise estática e planejamento da validação.

A equipe realizou inspeção dos documentos, arquivos de configuração, modelos de dados, rotas, serviços e estrutura do código-fonte disponibilizado.

**O sistema não foi executado pela equipe e os testes não foram realizados.**

Consequentemente:

- Não foram produzidos resultados de execução.
- Não foram realizadas medições de desempenho.
- Não foram registrados defeitos reproduzidos.
- Não foi confirmada a integração dos componentes em ambiente de execução.
- As ferramentas de automação mencionadas no plano representam sugestões para uma eventual avaliação futura.

As informações documentadas representam características identificadas nos materiais analisados e não devem ser interpretadas como comprovação de funcionamento do software.

## 12. Equipe

Projeto desenvolvido por estudantes do curso de Sistemas de Informação:

| Integrante | Matrícula |
|---|---|
| Demóstenes Diniz Porto | 2313080098 |
| João Vitor Pereira da Silva | 2313080135 |
| Jonildo Pereira Araújo Júnior | 2313080067 |
| Kaio Jefferson do Nascimento Pereira | 2423080039 |
| Thomás Lopes Barbosa | 3213080127 |

**Disciplina:** Teste de Software — 2026.2  
**Professor:** Bruno Rafael Araújo Vasconcelos  
**Instituição:** UNIFACISA

## 13. Repositório

Código-fonte e arquivos do projeto:

[GitHub — MedAgenda](https://github.com/kaiojnsc/med.agenda)

## 14. Referências

- Projeto Plano de Testes e Validação do MedAgenda — modelo de entrega, fornecido pelo professor.
- Instruções de Entrega do Projeto Final — Primeira e Segunda Entregas.
- Guia de execução do projeto MedAgenda.
- Código-fonte e README original do MedAgenda.
- Documentação oficial do [React](https://react.dev/), [Vite](https://vite.dev/), [Express](https://expressjs.com/), [Mongoose](https://mongoosejs.com/docs/), [MongoDB](https://www.mongodb.com/docs/) e [Docker Compose](https://docs.docker.com/compose/).
- ISO/IEC/IEEE 29119-3:2021 — Software Testing — Test Documentation.
- WCAG 2.1 — Web Content Accessibility Guidelines.

---

**MedAgenda | Projeto acadêmico de Teste de Software | 2026.2**
