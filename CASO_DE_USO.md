# Caso de Uso: Buscar Perguntas por Palavra-chave

## Atores

- Usuário do fórum

---

## Pré-condições

- O sistema está disponível.
- Existem perguntas cadastradas no fórum.
- O usuário possui acesso à página principal.

---

## Fluxo Principal

1. O usuário acessa a página principal do fórum.
2. O sistema exibe o campo de busca.
3. O usuário informa uma palavra-chave.
4. O usuário solicita a pesquisa.
5. O sistema consulta as perguntas cadastradas.
6. O sistema localiza perguntas relacionadas ao termo informado.
7. O sistema exibe a lista de resultados encontrados.
8. O usuário visualiza as perguntas retornadas.

---

## Fluxo Alternativo 1: Nenhum Resultado Encontrado

6a. O sistema não encontra perguntas relacionadas ao termo pesquisado.

6b. O sistema exibe a mensagem:

> Nenhuma pergunta encontrada.

6c. O usuário pode realizar uma nova pesquisa.

---

## Fluxo Alternativo 2: Campo de Busca Vazio

3a. O usuário não informa nenhum termo.

3b. O sistema solicita o preenchimento do campo de busca.

3c. O usuário informa um termo válido.

3d. O fluxo retorna ao passo 4 do fluxo principal.

---

## Pós-condições

- Os resultados da pesquisa são apresentados ao usuário.
- Nenhuma informação cadastrada no sistema é alterada.
- O usuário pode acessar qualquer pergunta retornada pela busca.
