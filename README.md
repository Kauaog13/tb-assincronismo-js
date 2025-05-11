# 📘 Comparativo entre `XMLHttpRequest`, `fetch`, `Promises` e `async/await`

Este repositório contém um estudo comparativo entre diferentes abordagens para realizar requisições HTTP em JavaScript. A pesquisa foi desenvolvida como parte da disciplina de **Linguagem para Web** e visa esclarecer as diferenças em termos de **desempenho**, **facilidade de uso** e **legibilidade** entre `XMLHttpRequest`, `fetch`, `Promises` e `async/await`.

## 👥 Integrantes do Grupo

- [Kauã Oliveira](https://github.com/Kaua0g13)
- [Vitória Ferreira](https://github.com/victoriafe-sa)

---

## 📊 Tabela Comparativa

| Critério               | `XMLHttpRequest`                          | `fetch`                                   | `Promises`                                     | `async/await`                                      |
|------------------------|-------------------------------------------|-------------------------------------------|------------------------------------------------|-----------------------------------------------------|
| **Lançamento**         | 2000 (antigo, legado)                     | 2015 (moderno, padrão atual)              | 2015 (ES6)                                     | 2017 (ES8)                                           |
| **Facilidade de uso**  | Difícil e verboso                         | Simples e mais legível                    | Requer conhecimento de Promises               | Extremamente legível e próximo de código síncrono   |
| **Suporte a Promises** | ❌ Não                                     | ✅ Sim (nativo)                            | N/A                                            | ✅ Usa Promises por trás                             |
| **Controle de erros**  | Complexo (`onerror`, `onload`)           | Simples com `.catch()`                    | Sim, com `.then()` e `.catch()`               | Claro com `try/catch`                               |
| **Leitura de código**  | Pouco legível (boilerplate)              | Mais limpa e direta                       | Médio (pode ter muito `.then()`)              | Muito legível                                       |
| **Streaming**          | Limitado                                 | ✅ Sim (ReadableStream)                   | Depende da API                                | ✅ Sim                                               |
| **Compatibilidade**    | ✅ Alta (inclusive IE)                    | ✅ Boa (exceto IE)                         | ✅ Boa                                         | ✅ Boa (exceto IE)                                   |
| **Desempenho**         | Levemente mais rápido                    | Semelhante                                | Igual ao fetch                                | Igual ao fetch                                      |
| **Cancelamento**       | ✅ Nativo com `.abort()`                 | ✅ Com `AbortController`                  | Manual                                         | Com `AbortController`                               |

---

## 🧾 Resumo das Tecnologias

### 📦 XMLHttpRequest
`XMLHttpRequest` é a API tradicional do JavaScript para fazer requisições HTTP assíncronas. Embora seja funcional e compatível com navegadores antigos (como o Internet Explorer), seu uso é verboso e pouco intuitivo, exigindo múltiplos eventos (`onload`, `onerror`) e verificações manuais de status.

> ✅ Compatível com navegadores antigos  
> ⚠️ Menos legível e mais difícil de manter

---

### 🚀 fetch
`fetch` é a API moderna introduzida no ES6 que simplifica requisições HTTP. Ela retorna uma `Promise` e permite escrever código mais limpo e fácil de entender. Porém, não rejeita automaticamente respostas com status de erro (como 404), sendo necessário tratá-los manualmente.

> ✅ Sintaxe moderna e mais legível  
> ❗ Precisa de verificação manual do `response.ok`

---

### 🔄 Promises
As `Promises` permitem lidar com operações assíncronas de forma organizada. Elas fornecem os métodos `.then()` e `.catch()` para encadear ações após a conclusão (ou falha) de uma tarefa. São a base de APIs modernas como `fetch` e `async/await`.

> ✅ Boa estruturação de fluxo assíncrono  
> ⚠️ Pode ficar confuso com muitos encadeamentos

---

### ⏱️ async/await
`async/await` é uma evolução das Promises, permitindo escrever código assíncrono de forma semelhante ao código síncrono. Traz maior legibilidade, facilita o tratamento de erros com `try/catch` e melhora a manutenção em projetos maiores.

> ✅ Sintaxe simples e clara  
> ✅ Ideal para funções assíncronas complexas


## 🧠 Exemplos Técnicos Completos

```javascript
// === Exemplo 1: XMLHttpRequest ===
function exemploXMLHttpRequest() {
  const xhr = new XMLHttpRequest();
  xhr.open("GET", "https://api.exemplo.com/dados", true);
  xhr.onload = function () {
    if (xhr.status === 200) {
      console.log("XMLHttpRequest:", xhr.responseText);
    } else {
      console.error("Erro XMLHttpRequest:", xhr.status);
    }
  };
  xhr.onerror = function () {
    console.error("Erro de conexão com XMLHttpRequest");
  };
  xhr.send();
}

// === Exemplo 2: Fetch com Promises ===
function exemploFetch() {
  fetch("https://api.exemplo.com/dados")
    .then(response => {
      if (!response.ok) {
        throw new Error("Erro na resposta do fetch");
      }
      return response.json();
    })
    .then(data => {
      console.log("Fetch com Promises:", data);
    })
    .catch(error => {
      console.error("Erro no fetch:", error);
    });
}

// === Exemplo 3: Promises manuais ===
function exemploPromises() {
  const minhaPromise = new Promise((resolve, reject) => {
    const sucesso = true; // Simulação
    setTimeout(() => {
      if (sucesso) {
        resolve("Dados simulados recebidos com Promises");
      } else {
        reject("Erro ao obter dados simulados");
      }
    }, 1000);
  });

  minhaPromise
    .then(resultado => console.log("Promises manuais:", resultado))
    .catch(erro => console.error("Erro nas Promises:", erro));
}

// === Exemplo 4: Async/Await ===
async function exemploAsyncAwait() {
  try {
    const response = await fetch("https://api.exemplo.com/dados");
    if (!response.ok) {
      throw new Error("Erro na resposta do async/await");
    }
    const data = await response.json();
    console.log("Async/Await:", data);
  } catch (erro) {
    console.error("Erro no async/await:", erro);
  }
}

// Chamando todas as funções para demonstração
exemploXMLHttpRequest();
exemploFetch();
exemploPromises();
exemploAsyncAwait();

---
