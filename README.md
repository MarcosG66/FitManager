<div align="center">

# 🏋️‍♂️ FitManager

**Sistema Web de Gestão de Academia e Acompanhamento de Treinos**

[![Status](https://img.shields.io/badge/Status-Em_Desenvolvimento-blue.svg)](#-cronograma-e-etapas)
[![Node.js](https://img.shields.io/badge/Node.js-v18+-green.svg)](https://nodejs.org/)
[![React](https://img.shields.io/badge/React-18+-61DAFB.svg)](https://react.dev/)
[![MySQL](https://img.shields.io/badge/MySQL-8.0+-4479A1.svg)](https://www.mysql.com/)

---

*Centralizando o cadastro de alunos, a prescrição de treinos, o registro de cargas e o acompanhamento da evolução física em uma única plataforma web com foco no uso mobile durante o treino.*

</div>

---

## 📌 Sumário
- [Sobre o Projeto](#-sobre-o-projeto)
- [Funcionalidades Principais](#-funcionalidades-principais)
- [Perfis de Usuário](#-perfis-de-usuário)
- [Tecnologias Utilizadas](#-tecnologias-utilizadas)
- [Arquitetura do Sistema](#-arquitetura-do-sistema)
- [Modelo de Dados (MER)](#-modelo-de-dados-mer)
- [Rotas da API](#-rotas-da-api)
- [Requisitos do Sistema](#-requisitos-do-sistema)
- [Equipe e Divisão de Papéis](#-equipe-e-divisão-de-papéis)
- [Cronograma e Etapas](#-cronograma-e-etapas)

---

## 📖 Sobre o Projeto

O **FitManager** nasce de um problema real no dia a dia das academias: o uso de fichas de treino impressas em papel ou planilhas dispersas, que são difíceis de atualizar pelos instrutores e pouco práticas para a consulta dos alunos durante o treino.

A plataforma resolve isso oferecendo uma interface web responsiva (com foco mobile para os alunos) que permite a montagem rápida de fichas de treino, registro de carga usada série a série, acompanhamento do IMC e histórico visual da evolução do aluno.

---

## 🔥 Funcionalidades Principais

- 🔐 **Autenticação e Autorização:** Controle de acesso por perfil (Aluno, Instrutor e Administrador).
- 📋 **Gestão de Fichas de Treino:** Criação, edição e exclusão de fichas completas (exercícios, séries, repetições, descanso).
- 📊 **Registro de Cargas & Progresso:** Aluno marca os exercícios concluídos, registra cargas usadas e acompanha seu progresso em tempo real.
- 📈 **Evolução Corporal:** Cálculo automático de IMC a partir do registro de peso e altura, além de gráficos de evolução de carga por exercício.
- 🏋️ **Catálogo de Exercícios:** Organização e filtro de exercícios por grupo muscular.

---

## 👥 Perfis de Usuário

| Perfil | Descrição & Responsabilidades |
| :--- | :--- |
| **👨‍🎓 Aluno** | Visualiza treinos do dia, registra carga e conclusão de exercícios, registra peso e altura (com cálculo automático de IMC) e consulta histórico e evolução. |
| **👨‍🏫 Instrutor** | Cadastra, edita, ativa/inativa alunos; cria e gerencia fichas de treino personalizadas; consulta e organiza o banco de exercícios. |
| **⚙️ Administrador** | Gerencia o catálogo completo de exercícios, visualiza totais do sistema por perfil e realiza busca global de utilizadores. |

---

## 🛠️ Tecnologias Utilizadas

### **Front-end**
- **React:** Componentização dinâmica da interface do usuário.
- **Bootstrap / CSS:** Layout adaptável e responsivo com foco em dispositivos móveis.
- **JavaScript (ES6+):** Lógica da aplicação no cliente.

### **Back-end**
- **Node.js:** Ambiente de execução assíncrono.
- **Express.js:** Framework para construção da API REST.

### **Banco de Dados**
- **MySQL:** Banco de dados relacional para persistência de usuários, fichas, treinos e medições.

---

## 🏗️ Arquitetura do Sistema

O sistema adota uma arquitetura desacoplada em **3 camadas**, utilizando JSON para comunicação via REST:

```
┌─────────────────────────────────────────────────────────┐
│              Camada de Apresentação                      │
│        React + Bootstrap (Navegador / Mobile)           │
└──────────────────────────┬──────────────────────────────┘
                           │ API REST (JSON)
┌──────────────────────────▼──────────────────────────────┐
│               Camada de Aplicação                       │
│             Node.js + Express.js                        │
└──────────────────────────┬──────────────────────────────┘
                           │ SQL Queries
┌──────────────────────────▼──────────────────────────────┐
│                 Camada de Dados                         │
│                    MySQL Database                       │
└─────────────────────────────────────────────────────────┘
```

---

## 🗄️ Modelo de Dados (MER)

O banco de dados relacional é composto pelas seguintes entidades principais:

- **`USUARIO`**: Dados centralizados de acesso (`email`, `senha`, `perfil`).
- **`ALUNO`**: Dados específicos do aluno vinculados a um instrutor.
- **`INSTRUTOR`**: Cadastro de instrutores responsáveis.
- **`FICHA_TREINO`**: Fichas vinculadas a um aluno.
- **`ITEM_FICHA`**: Relação de exercícios, séries, repetições, descanso e carga prescrita.
- **`EXERCICIO`** & **`GRUPO_MUSCULAR`**: Catálogo estruturado por agrupamento.
- **`HISTORICO_CARGA`**: Registros semanais de cargas utilizadas pelos alunos.
- **`AVALIACAO_FISICA`**: Registros de peso e altura (IMC calculado em runtime).

---

## 🌐 Rotas da API

| Recurso | Método | Descrição |
| :--- | :---: | :--- |
| `/auth/login` | `POST` | Autenticação do usuário e geração de sessão |
| `/alunos` | `GET / POST / PUT / DELETE` | CRUD e listagem com filtros de alunos |
| `/fichas` | `GET / POST / PUT / DELETE` | Gerenciamento de fichas de treino |
| `/fichas/:id/itens` | `GET / POST / PUT / DELETE` | Gerenciamento dos exercícios de uma ficha |
| `/exercicios` | `GET / POST / PUT / DELETE` | CRUD do catálogo de exercícios |
| `/cargas` | `GET / POST` | Registro e consulta do histórico de carga |
| `/avaliacoes` | `GET / POST` | Registro de peso/altura e histórico de IMC |
| `/usuarios` | `GET` | Consulta e totais por perfil (Exclusivo Admin) |

---

## 📋 Requisitos do Sistema

### **Requisitos Funcionais (RFs)**
- **RF01:** Gestão completa de alunos (cadastrar, editar, ativar/inativar, excluir e pesquisar).
- **RF02:** Autenticação via login seguro direcionando para o painel específico do perfil.
- **RF03:** Montagem e edição de fichas de treino pelos instrutores.
- **RF04:** Organização do catálogo de exercícios por grupo muscular.
- **RF05/RF06:** Visualização de treinos diários pelo aluno, com marcação de concluído e registro de carga em kg.
- **RF07:** Registro de peso e altura com cálculo automático de IMC.
- **RF08:** Apresentação de gráficos de evolução de carga ao longo do tempo.

### **Requisitos Não Funcionais (RNFs)**
- **RNF01:** Interface **100% responsiva** otimizada para uso em smartphones nas academias.
- **RNF02:** Armazenamento seguro de senhas via **hash criptográfico**.
- **RNF03:** Comunicação exclusiva via JSON entre Front-end e Back-end.
- **RNF04:** Controle de acesso rígido por permissão de perfil (RBAC).

---

## 👥 Equipe e Divisão de Papéis

| Integrante | Função | Responsabilidades |
| :--- | :--- | :--- |
| **Valter Expedito Ribeiro da Silva** | Gerente de Projeto | Coordenação da equipe, gestão do cronograma, integração e documentação. |
| **Cairo Forte Ferreira Filho** | Dev Front-end | Desenvolvimento da interface no React, responsividade Bootstrap e telas de treinos/gráficos. |
| **Henrique José Barbosa V. C. Mello** | Dev Back-end | Configuração do servidor Node.js/Express, rotas da API REST e integração com MySQL. |
| **Marcos Gentili Oliveira** | UX/UI Designer | Wireframes, prototipação das telas no Figma e arquitetura da experiência de usuário. |

---

## 📅 Cronograma e Etapas

- [x] **Etapa 1: Plano de Trabalho e Modelagem**
  - Definição do escopo, requisitos, Casos de Uso, MER e Protótipo de Telas.
- [ ] **Etapa 2: Desenvolvimento MVP**
  - Implementação das telas responsivas em React/Bootstrap e integração do CRUD básico com Node.js/MySQL.
- [ ] **Etapa 3: Entrega Final & Publicação**
  - Módulo de autenticação/autorização, gráficos de evolução, refinamento de UI/UX e publicação (deploy).

---

<div align="center">

Desenvolvido para o Trabalho Final da Disciplina.  
© 2026 **FitManager** - Todos os direitos reservados.

</div>
