# Implementação com SOLID

## Funcionalidade Implementada

Foi implementada a funcionalidade de busca de perguntas por palavra-chave.

A funcionalidade permite ao usuário pesquisar perguntas cadastradas utilizando um termo informado na URL da requisição.

Exemplo:

```
GET /buscar/javascript
```

---

## Aplicação do Single Responsibility Principle (SRP)

O princípio SRP foi aplicado mantendo responsabilidades separadas.

O arquivo `server.js` é responsável apenas por receber requisições HTTP e retornar respostas.

Exemplo:

```javascript
app.get('/buscar/:palavra', (req, res) => {
  const palavra = req.params.palavra;
  const perguntas = modelo.buscar_perguntas(palavra);
  res.json(perguntas);
});
```

Já o arquivo `modelo.js` concentra a lógica de acesso aos dados.

```javascript
function buscar_perguntas(palavra_chave) {
  return bd.queryAll(
    'select * from perguntas where lower(texto) like lower(?)',
    [`%${palavra_chave}%`]
  );
}
```

---

## Aplicação do Open/Closed Principle (OCP)

O sistema foi estendido com uma nova funcionalidade sem necessidade de alterar o comportamento das funcionalidades já existentes.

A função `buscar_perguntas()` foi adicionada ao modelo preservando todas as demais operações do sistema.

Dessa forma o sistema permanece aberto para extensão e fechado para modificações desnecessárias.

---

## Aplicação do Dependency Inversion Principle (DIP)

O modelo continua utilizando a abstração representada pelo módulo `bd`.

A nova funcionalidade utiliza os mesmos mecanismos de acesso a dados já existentes.

```javascript
return bd.queryAll(
  'select * from perguntas where lower(texto) like lower(?)',
  [`%${palavra_chave}%`]
);
```

Isso permite substituir a implementação do banco por versões simuladas durante testes, mantendo baixo acoplamento.

---

## Trechos de Código

### Modelo

```javascript
function buscar_perguntas(palavra_chave) {
  return bd.queryAll(
    'select * from perguntas where lower(texto) like lower(?)',
    [`%${palavra_chave}%`]
  );
}
```

### Rota

```javascript
app.get('/buscar/:palavra', (req, res) => {
  try {
    const palavra = req.params.palavra;
    const perguntas = modelo.buscar_perguntas(palavra);
    res.json(perguntas);
  }
  catch(erro) {
    res.status(500).json(erro.message);
  }
});
```

---

## Conclusão

A funcionalidade de busca por palavra-chave foi implementada seguindo os princípios SRP, OCP e DIP. A solução mantém a organização existente do sistema, reduz o acoplamento entre componentes e facilita futuras extensões.
