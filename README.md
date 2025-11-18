# Guia Técnico e Explicação do Código: Sistema "Barbearia Etc"

Este documento detalha a arquitetura e a lógica de programação por trás do sistema web da Barbearia Etc. O foco é explicar como HTML, CSS e JavaScript interagem para criar as funcionalidades do site.

## 1. Arquitetura e Estilização Global

O sistema segue o padrão **MVC (Model-View-Controller) adaptado** para um contexto estático.
* **Views:** Pastas HTML (`/views`) contendo a estrutura.
* **Public:** Pasta de recursos (`/public`) contendo CSS e Imagens.

### O Arquivo `style.css` (O Motor Visual)
Todo o design é centralizado em um único arquivo para consistência.
* **Responsividade sem Media Queries:** Na classe `.service-list` e `.gallery-grid`, utilizamos uma técnica avançada de CSS Grid:
    ```css
    grid-template-columns: repeat(auto-fit, minmax(280px, 1fr));
    ```
    *Explicação:* Isso diz ao navegador: "Crie tantas colunas quanto couberem (`auto-fit`). Cada coluna deve ter no mínimo `280px`. Se sobrar espaço, divida-o igualmente (`1fr`)." Isso faz o layout se adaptar a celulares e PCs automaticamente.
* **Técnica "Visual Hidden":** Para atender à exigência de usar apenas a logo no cabeçalho sem prejudicar a semântica (SEO) da página, criamos a classe `.visual-hidden`:
    ```css
    .visual-hidden { display: none; }
    ```
    Isso mantém a tag `<h1>` no código (importante para a estrutura), mas a esconde visualmente.

---

## 2. Fluxo de Login e Cadastro

### `index.html` (Login)
A "mágica" do login simulado acontece no formulário HTML.
* **Código Chave:**
    ```html
    <form action="views/home.html" method="GET">
    ```
    *Explicação:* O atributo `action` define para onde o navegador deve ir quando o formulário for enviado. Ao apontar para `views/home.html`, criamos a ilusão de um login bem-sucedido sem precisar de um servidor real.

### `views/cadastro.html` e `cadastro_sucesso.html`
Aqui introduzimos a **passagem de dados via URL**.
1.  **Envio:** O formulário de cadastro usa `method="GET"`. Isso faz com que os dados digitados (ex: nome="Joao") apareçam na URL da próxima página: `...html?nome=Joao&email=...`.
2.  **Recepção (JavaScript):** Na página de sucesso, usamos JavaScript para ler essa URL:
    ```javascript
    const params = new URLSearchParams(window.location.search);
    document.getElementById('cad-nome').innerText = params.get('nome');
    ```
    *Explicação:* `URLSearchParams` é uma ferramenta nativa do navegador que "desempacota" a URL. O script pega o valor do campo 'nome' e o injeta na tag HTML com id `cad-nome`, personalizando a mensagem.

---

## 3. Funcionalidades Principais

### `views/agendamento.html` (Formulários Avançados)
Esta página demonstra o uso correto dos tipos de input do HTML5 para melhorar a experiência em dispositivos móveis.
* **Inputs Específicos:**
    * `<input type="date">`: Abre o calendário nativo do celular.
    * `<input type="time">`: Abre o seletor de hora.
    * `<input type="tel">`: Abre o teclado numérico no celular.
* **Select com Valores:**
    ```html
    <option value="corte">Corte de Cabelo (R$ 40,00)</option>
    ```
    Note que o `value` ("corte") é um código simples, diferente do texto que o usuário vê. Isso facilita o processamento dos dados depois.

### `views/sucesso.html` (Lógica de Dados)
Esta página contém a lógica mais complexa do sistema. Ela recebe os dados "crus" do agendamento e os formata.
* **Mapeamento de Dados (Dicionário):**
    Como o formulário envia apenas códigos como "corte" ou "pezinho", usamos um objeto JavaScript para traduzir isso:
    ```javascript
    const servicosMap = {
        'corte': 'Corte de Cabelo (R$ 40,00)',
        'pezinho': 'Pezinho (R$ 15,00)',
        // ...
    };
    ```
* **Tratamento de Datas:**
    Datas vindas de formulários podem ter problemas de fuso horário. O script inclui uma correção técnica:
    ```javascript
    dataObj.setMinutes(dataObj.getMinutes() + dataObj.getTimezoneOffset());
    ```
    Isso garante que o dia exibido na confirmação seja exatamente o dia que o usuário selecionou, sem voltar um dia devido ao fuso horário UTC.

### `views/galeria.html` e `views/detalhe.html` (Sistema Dinâmico)
Para evitar criar 8 arquivos HTML (um para cada foto), criamos um sistema de **Template Único**.
1.  **O Link Inteligente (Galeria):**
    ```html
    <a href="detalhe.html?id=1">...</a>
    ```
    Cada foto envia um número identificador (`id`) diferente.
2.  **O "Banco de Dados" Local (Detalhe):**
    Dentro do JavaScript da página de detalhes, existe um objeto `const portfolio` que guarda as informações de todos os cortes.
3.  **A Renderização:**
    O script lê o ID da URL (`params.get('id')`), busca as informações correspondentes no objeto `portfolio` e atualiza a imagem (`src`) e os textos (`innerText`) da página em tempo real.
    *Benefício:* Isso torna o site extremamente leve e fácil de manter. Para mudar a descrição de um corte, basta editar o script, sem mexer no HTML.

---

## 4. Estrutura Semântica

* **Header/Nav:** O uso da lista não ordenada (`<ul>`) dentro da tag `<nav>` é o padrão semântico correto para menus, garantindo acessibilidade.
* **Links Ativos:** A classe `.active` é aplicada manualmente no HTML de cada página para dar feedback visual ao usuário de onde ele está.