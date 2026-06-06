# Teste Caixa Cinza com Supabase e Postman

## Introdução

Este repositório contém a documentação e evidências da atividade de testes caixa cinza
realizada com as ferramentas Supabase e Postman, como parte do componente curricular 
UX/UI e Testes de Software da UniFacens.

**Aluno:** Márcio Soares de Brito

---

## Objetivo da Atividade

Compreender e aplicar testes de caixa cinza em APIs de autenticação, utilizando 
ferramentas modernas de mercado para configuração, execução e validação de testes 
funcionais.

---

## Configuração do Supabase

O projeto foi criado na plataforma Supabase, que oferece banco de dados PostgreSQL 
e autenticação gratuita.

**Passos realizados:**
- Criação de conta no Supabase via GitHub
- Criação do projeto chamado `foodexpress`
- Configuração da autenticação por e-mail (Email Provider habilitado)
- Desabilitação da confirmação de e-mail para facilitar os testes
- Criação do usuário de teste: `teste@foodexpress.com`
- Obtenção da API URL e API KEY (anon public)

**Evidências:** pasta `/prints`

---

## Configuração do Postman

O Postman Desktop foi utilizado para execução dos testes de API.

**Passos realizados:**
- Instalação do Postman Desktop
- Criação do Workspace `FoodExpress API Tests`
- Criação do Environment `FoodExpress Supabase` com as seguintes variáveis:

| Variável | Descrição |
|---|---|
| `base_url` | URL da API do Supabase |
| `api_key` | Chave anon public do Supabase |
| `email` | E-mail do usuário de teste |
| `password` | Senha do usuário de teste |

**Evidências:** pasta `/prints`

---

## Configuração das Requisições

**Endpoint utilizado:**

POST {{base_url}}/auth/v1/token?grant_type=password

**Headers:**

| Header | Valor |
|---|---|
| `apikey` | `{{api_key}}` |
| `Content-Type` | `application/json` |

**Body JSON:**
```json
{
  "email": "usuario@email.com",
  "password": "123456"
}
```

---

## Execução dos Testes

Foram executados 5 cenários de teste cobrindo situações válidas e inválidas 
de autenticação.

### Tabela de Cenários

| Cenário | Entrada Utilizada | Resultado Esperado | Resultado Obtido | Status |
|---|---|---|---|---|
| Login válido | Credenciais corretas | Status 200 + access token | Status 200 + access token retornado | ✅ OK |
| Senha incorreta | Senha errada | Erro de autenticação | Status 400 - invalid_credentials | ✅ OK |
| Usuário inexistente | E-mail não cadastrado | Acesso negado | Status 400 - invalid_credentials | ✅ OK |
| Campos vazios | E-mail e senha vazios | Erro de validação | Status 400 - validation_failed | ✅ OK |
| Credenciais inválidas | E-mail e senha falsos | Mensagem de erro | Status 400 - invalid_credentials | ✅ OK |

**Evidências:** pasta `/prints`

---

## Registro dos Testes

Os testes foram registrados em planilha disponível na pasta `/planilha`.

A documentação dos testes é fundamental para rastrear falhas, validar 
comportamentos esperados e garantir a qualidade do sistema. Nenhuma falha 
inesperada foi identificada durante a execução.

---

## Resultados Obtidos

- ✅ Autenticação com credenciais válidas retornou **Status 200** e **access token**
- ✅ Tentativas com credenciais inválidas retornaram **Status 400**
- ✅ Campos vazios retornaram erro de **validation_failed**
- ✅ Todos os 5 cenários executados com sucesso

---

## Conclusão

Os testes foram executados corretamente e a autenticação do Supabase funcionou 
conforme esperado em todos os cenários.

**Dificuldades encontradas:**
- A base_url precisou ser ajustada removendo o `/rest/v1/` do final

**Falhas identificadas:**
- Nenhuma falha inesperada foi encontrada

**Melhorias possíveis:**
- Adicionar testes automatizados com scripts no Postman
- Testar outros métodos de autenticação como OAuth

**Importância dos testes caixa cinza em APIs:**
Os testes caixa cinza permitem validar o comportamento da API conhecendo 
parcialmente sua estrutura, como endpoints, headers e respostas esperadas. 
Isso garante que a autenticação funciona corretamente antes de integrar 
com o frontend, evitando falhas em produção.
