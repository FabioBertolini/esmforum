# Padrões de Projeto Existentes

## 1. MVC (Model-View-Controller)

### Onde está aplicado

- Models: pasta `models/`
- Controllers/Rotas: pasta `routes/`
- Views: respostas HTML e JSON enviadas pelo Express

### Como funciona

O sistema separa os dados (Models), o controle das requisições (Routes/Controllers) e a apresentação das respostas (Views).

### Possíveis melhorias

A implementação pode ser aprimorada com uma separação mais explícita entre Controllers e Routes.

---

## 2. Repository (Parcial)

### Onde está aplicado

- Arquivos da pasta `models/`

### Como funciona

Os Models concentram operações de acesso aos dados, funcionando de forma semelhante ao padrão Repository.

### Possíveis melhorias

Criar uma camada Repository específica para separar completamente o acesso aos dados da lógica de negócio.

---

## 3. Singleton (Implícito)

### Onde está aplicado

- Instância única do servidor Express
- Configuração única do banco de dados

### Como funciona

Existe apenas uma instância do servidor durante a execução da aplicação.

### Possíveis melhorias

Formalizar a implementação através de uma classe Singleton.
