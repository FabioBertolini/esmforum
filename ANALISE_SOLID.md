# Análise SOLID

## Pontos Positivos

### 1. Single Responsibility Principle (SRP)

O arquivo `modelo.js` concentra as operações relacionadas ao acesso e manipulação dos dados do sistema, enquanto o arquivo `server.js` é responsável pelo tratamento das requisições HTTP.

Exemplo:

```javascript
const perguntas = modelo.listar_perguntas();
```

Essa separação demonstra o princípio da responsabilidade única, pois cada módulo possui uma função bem definida.

---

### 2. Open/Closed Principle (OCP)

O sistema permite adicionar novas funções ao módulo `modelo.js` sem modificar as funcionalidades já existentes.

Exemplo:

```javascript
function get_respostas(id_pergunta) {
  return bd.queryAll(
    'select * from respostas where id_pergunta = ?',
    [id_pergunta]
  );
}
```

Novas operações podem ser adicionadas ao modelo sem alterar o comportamento das funções já implementadas.

---

### 3. Dependency Inversion Principle (DIP)

O método `reconfig_bd()` permite substituir a implementação do banco de dados por uma versão simulada durante os testes.

Exemplo:

```javascript
function reconfig_bd(mock_bd) {
  bd = mock_bd;
}
```

Dessa forma, o modelo depende de uma abstração do acesso aos dados e não diretamente de uma implementação específica.

---

## Oportunidades de Melhoria

### 1. Violação do Single Responsibility Principle (SRP)

O arquivo `server.js` contém repetição de tratamento de erros em praticamente todas as rotas.

Exemplo:

```javascript
try {
  ...
}
catch(erro) {
  res.status(500).json(erro.message);
}
```

Uma melhoria seria criar um middleware global de tratamento de erros, centralizando essa responsabilidade em um único local.

---

### 2. Violação do Dependency Inversion Principle (DIP)

No método `cadastrar_pergunta()`, o identificador do usuário é definido diretamente no código.

Exemplo:

```javascript
const params = [texto, 1];
```

Essa abordagem cria dependência de um valor fixo.

Uma melhoria seria receber o identificador do usuário como parâmetro da aplicação ou por meio de autenticação, reduzindo o acoplamento e aumentando a flexibilidade.

---

## Conclusão

O sistema apresenta características positivas relacionadas aos princípios SRP, OCP e DIP, principalmente pela separação entre as camadas de API e modelo e pela possibilidade de utilização de objetos simulados nos testes.

As principais oportunidades de melhoria estão relacionadas à centralização do tratamento de erros e à remoção de dependências fixas presentes no código, tornando a aplicação mais flexível e aderente aos princípios SOLID.
