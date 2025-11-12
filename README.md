# trabalho-dev-web
trabalho desenvolvido durante o curso tecnico. Gerenciamento e agendamento de uma barbearia.

# 🏛️ Resumo do Sistema: Barbearia Estático (README.md)

Este documento serve como um guia para futuras manutenções, garantindo que a essência visual e estrutural do site seja preservada.

## 1. Visão Geral do Projeto

* **Objetivo:** Website estático (HTML/CSS) para uma barbearia, simulando um sistema de agendamento.
* **Tecnologia:** HTML5 e CSS3.
* **Estrutura:** O projeto segue uma estrutura **MVC adaptada** (a pedido acadêmico) para organizar os arquivos, mesmo sendo estático.
    * `index.html`: É a tela de **Login** (ponto de entrada).
    * `views/`: Contém todas as **páginas** de conteúdo (`home.html`, `servicos.html`, etc.).
    * `public/`: Contém os **assets** (um único `style.css`, imagens, etc.).
    * `models/` e `controllers/`: Pastas vazias, prontas para uma futura expansão *back-end*.

## 2. Identidade Visual (A Essência)

A identidade do site foi construída sobre três pilares: **Profissionalismo, Energia e Legibilidade.**

* **Profissionalismo (Fundos Escuros):** A cor `#333` (cinza-escuro/quase preto) é usada no `header` e `footer` para "ancorar" o site, dando um visual sofisticado e unificado em todas as páginhas.
* **Energia (Acento Vermelho):** A cor `#E63946` (vermelho) é o ponto focal. Ela **NÃO** deve ser usada em excesso. Sua função é guiar o usuário para ações importantes (botões, links ativos, destaques).
* **Legibilidade (Fundos Claros):** O conteúdo principal (`.main-content`) usa fundos `#f4f4f4` (body) e `#ffffff` (cards, formulários) para garantir que o texto seja fácil de ler e o visual seja limpo.
* **Fluxo Visual Distinto:** Há uma separação clara entre o fluxo de "Autenticação" e o de "Conteúdo".
    * **Autenticação (`index.html`, `views/cadastro.html`):** Usam um fundo escuro (`#333`) que preenche a tela inteira.
    * **Conteúdo (`views/home.html`, etc.):** Usam o layout padrão (Header escuro, Conteúdo claro, Footer escuro).

## 3. Paleta de Cores (Guia Rápido)

| Cor | Hexcode | Papel Principal | Onde é usado |
| :--- | :--- | :--- | :--- |
| **Vermelho (Acento)** | `#E63946` | Ação e Destaque | Botões, Links, `a.active`, Preços |
| **Vermelho (Hover)** | `#b82834` | Interação de Botão | `.btn-login:hover`, `.btn-cta:hover` |
| **Cinza Escuro (Base)** | `#333` | Estrutura e Foco | `header`, `footer`, fundos de Login/Cadastro |
| **Cinza Médio** | `#555` | Descrições | Subtítulos (`.main-content h2 + p`) |
| **Branco (Conteúdo)** | `#ffffff` | Fundo de Conteúdo | Cards (`.service-item`), Formulários, `.intro-text` |
| **Cinza Claro (Fundo)** | `#f4f4f4` | Fundo do Site | `body` (páginas de conteúdo) |

## 4. Guia de Funcionalidades (Páginas)

| Página (Arquivo) | Propósito | Classes/Componentes Chave |
| :--- | :--- | :--- |
| `index.html` | **Login:** Ponto de entrada. | `.login-page`, `.login-container` |
| `views/cadastro.html` | **Cadastro:** Página com estilo espelhado no Login. | `.cadastro-page`, `.cadastro-container` |
| `views/home.html` | **Home:** Introdução ao site após o "login". | `.welcome-banner`, `.btn-cta` |
| `views/servicos.html` | **Serviços:** Lista de serviços em formato de *grid*. | `.service-list`, `.service-item` |
| `views/agendamento.html`| **Agendamento:** Formulário (simulado) para marcar horário. | `.agendamento-form`, (reúsa `.input-group`) |
| `views/galeria.html` | **Galeria:** *Grid* responsivo de imagens. | `.gallery-grid`, `.gallery-item` |
| `views/contato.html` | **Contato:** Layout de 2 colunas para Info + Mapa. | `.contact-container`, `.contact-details` |

## 5. Componentes Reutilizáveis (CSS)

Para manter a consistência, sempre que possível, utilize estas classes globais:

* `.btn-login`: O botão de ação padrão (vermelho).
* `.input-group`: O *wrapper* padrão para `label` e `input`/`select`/`textarea`.
* `.main-content`: O *wrapper* principal de todo o conteúdo das páginas (define o `padding` padrão).