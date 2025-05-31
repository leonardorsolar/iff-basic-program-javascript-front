# Tutorial para Iniciantes: Projeto Frontend para Registrar Usuário

---

## 1. O que você vai aprender neste tutorial

-   Como baixar o projeto frontend do GitHub.
-   Como abrir e entender os arquivos HTML, CSS e JavaScript.
-   Como rodar o projeto localmente para testar no navegador.
-   Como funciona o código que envia dados do formulário para um servidor (backend).
-   Explicação simples do código para iniciantes.

---

## 2. O que você precisa ter instalado para começar

-   **Git**: Para baixar o projeto.
-   **Editor de texto**: Recomendado Visual Studio Code (VSCode).
-   **Navegador**: Google Chrome, Firefox, etc.

Se não tem o Git ou VSCode, pode instalar:

-   Git: [https://git-scm.com/downloads](https://git-scm.com/downloads)
-   VSCode: [https://code.visualstudio.com/download](https://code.visualstudio.com/download)

---

## 3. Baixando o projeto do GitHub

No terminal (Prompt de Comando ou Terminal):

```bash
git clone https://github.com/leonardorsolar/iff-basic-program-javascript-front.git
```

Entre na pasta do projeto:

```bash
cd iff-basic-program-javascript-front
```

---

## 4. Estrutura dos arquivos do projeto frontend

Dentro da pasta, você vai encontrar:

-   **index.html** — arquivo principal que mostra o formulário para registrar usuário.
-   **styles.css** — arquivo que deixa o site bonito, com cores, fontes, espaços etc.
-   **script.js** — arquivo que contém o código JavaScript para enviar os dados do formulário para o servidor.

---

## 5. Abrindo o projeto no navegador

-   Abra o VSCode.
-   No VSCode, abra a pasta do projeto: `Arquivo > Abrir Pasta > selecione iff-basic-program-javascript-front`.
-   Clique no arquivo `index.html`.
-   Clique com o botão direito na tela do editor e escolha "Abrir com Live Server" (se tiver essa extensão instalada).
-   Se não tiver o Live Server, basta abrir o arquivo `index.html` com seu navegador (clicar duas vezes no arquivo).

---

## 6. Como funciona o arquivo **index.html**

```html
<form id="registrationForm">
    <label for="name">Nome:</label>
    <input type="text" id="name" name="name" required />

    <label for="email">Email:</label>
    <input type="email" id="email" name="email" required />

    <label for="password">Senha:</label>
    <input type="password" id="password" name="password" required />

    <button type="submit">Registrar</button>
</form>
```

-   Esse é um formulário com 3 campos: nome, email e senha.
-   O botão "Registrar" envia os dados.
-   O `id="registrationForm"` é usado para o JavaScript identificar esse formulário.

---

## 7. Como funciona o arquivo **script.js**

Aqui está o que o código faz, linha a linha, de forma simples:

```js
document
    .getElementById("registrationForm")
    .addEventListener("submit", function (event) {
        event.preventDefault() // Não deixa a página recarregar ao enviar o formulário

        // Pega os valores digitados pelo usuário
        const name = document.getElementById("name").value
        const email = document.getElementById("email").value
        const password = document.getElementById("password").value

        // Cria um objeto com esses dados
        const userData = { name, email, password }

        console.log(userData) // Imprime os dados no console para verificação

        // Envia os dados para o servidor usando fetch (chamada HTTP)
        fetch("http://localhost:3000/criar-usuario", {
            method: "POST", // Tipo da requisição
            headers: {
                "Content-Type": "application/json", // Informamos que os dados são JSON
            },
            body: JSON.stringify(userData), // Converte o objeto para texto JSON
        })
            .then((response) => {
                if (!response.ok) {
                    return response.json().then((errorData) => {
                        throw new Error(
                            errorData.error || "Erro ao registrar usuário"
                        )
                    })
                }
                return response.json() // Se sucesso, pega os dados retornados do servidor
            })
            .then((data) => {
                // Mostra mensagem de sucesso na tela
                document.getElementById(
                    "responseMessage"
                ).innerText = `Usuário registrado com sucesso! Bem-vindo, ${data.name}.`
            })
            .catch((error) => {
                // Mostra mensagem de erro na tela
                document.getElementById("responseMessage").innerText =
                    "Erro ao registrar usuário - front."
                console.error("Erro:", error)
            })
    })
```

---

## 8. Como funciona o arquivo **styles.css**

Ele deixa seu formulário mais bonito com cores, espaçamento e fontes legíveis. Por exemplo:

-   Centraliza o formulário na tela.
-   Dá cor azul no botão.
-   Espaça os campos para não ficarem grudados.
-   Dá bordas arredondadas.

---

## 9. Importante: O backend (servidor)

O código do frontend **espera que exista um servidor rodando na sua máquina** no endereço:

```
http://localhost:3000/criar-usuario
```

Esse servidor deve aceitar o método POST e receber os dados do usuário para registrar.

Sem esse servidor funcionando, a chamada fetch vai falhar.

---

## 10. Como testar tudo funcionando

### a) Rodar o backend

Se você já tem o backend rodando (por exemplo seu projeto Node.js), execute ele na porta 3000.

Se não tem, precisará criar um backend para receber os dados.

---

### b) Rodar o frontend

-   Abra o arquivo `index.html` no navegador (via Live Server ou abrindo direto).
-   Preencha os campos do formulário.
-   Clique em "Registrar".
-   Veja as mensagens na tela e no console do navegador (aperte F12 e vá na aba Console).

---

## 11. Resumo dos comandos e passos

```bash
# Baixar o projeto frontend
git clone https://github.com/leonardorsolar/iff-basic-program-javascript-front.git
cd iff-basic-program-javascript-front

# Abrir no VSCode
code .

# Abrir index.html no navegador para testar
```

---

## 12. Dicas finais para iniciantes

-   Sempre veja o console do navegador (F12 > Console) para entender erros ou mensagens.
-   Se quiser aprender mais, comece testando pequenas mudanças no arquivo `script.js` ou `styles.css` para ver o que acontece.
-   O frontend envia dados para o backend, que deve processar e responder. Se o backend não existir, o frontend vai mostrar erro.

---
