# Design Simples (YAGNI)

## Análise do Código Atual

O backend do ESM Forum possui uma implementação simples e direta, seguindo o princípio YAGNI (You Aren't Gonna Need It), que recomenda implementar apenas o que é necessário para atender aos requisitos atuais.

Os arquivos analisados foram:

- server.js
- modelo.js

---

## Exemplos de Aplicação do Design Simples

### 1. Rotas Objetivas e Diretas

As rotas implementadas em `server.js` possuem responsabilidades claras e específicas.

Exemplo:

```javascript
app.post('/perguntas', (req, res) => {
  const id_pergunta = modelo.cadastrar_pergunta(req.body.pergunta);
  res.json({id_pergunta: id_pergunta});
});
```

A rota apenas recebe a requisição, delega a lógica ao modelo e retorna a resposta, evitando complexidade desnecessária.

---

### 2. Separação entre API e Regras de Negócio

O arquivo `server.js` concentra apenas o tratamento das requisições HTTP.

A lógica de acesso aos dados está centralizada em `modelo.js`.

Exemplo:

```javascript
const perguntas = modelo.listar_perguntas();
```

Essa separação facilita a manutenção e evita duplicação de código.

---

### 3. Consultas Simples ao Banco de Dados

As consultas SQL utilizam apenas os dados necessários para cada operação.

Exemplo:

```javascript
return bd.queryAll(
  'select * from respostas where id_pergunta = ?',
  [id_pergunta]
);
```

Não existem consultas complexas ou abstrações prematuras que aumentariam a dificuldade de manutenção.

---

### 4. Funções Pequenas e Focadas

As funções possuem responsabilidades únicas.

Exemplo:

```javascript
function get_respostas(id_pergunta) {
  return bd.queryAll(
    'select * from respostas where id_pergunta = ?',
    [id_pergunta]
  );
}
```

Cada função executa apenas uma tarefa específica.

---

## Oportunidades de Simplificação

### 1. Repetição de Tratamento de Erros

Atualmente cada rota possui um bloco `try/catch`.

Exemplo:

```javascript
try {
  ...
}
catch(erro) {
  res.status(500).json(erro.message);
}
```

Uma possível melhoria seria criar um middleware global para tratamento de erros, reduzindo repetição de código.

---

### 2. Usuário Fixo na Criação de Perguntas

No método:

```javascript
const params = [texto, 1];
```

O identificador do usuário está fixo como valor `1`.

Atualmente isso atende aos requisitos do sistema, mas em futuras evoluções poderá ser substituído por um mecanismo real de autenticação.

---

## Conclusão

O sistema apresenta um design simples, com baixo acoplamento entre as camadas e funções pequenas que executam responsabilidades específicas. A implementação segue os princípios do YAGNI ao evitar abstrações complexas e desenvolver apenas os recursos necessários para os requisitos atuais.
