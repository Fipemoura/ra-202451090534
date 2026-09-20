# Aula 07 — Caça às Vulnerabilidades (OWASP)

**Nome:** Filipe de Araújo Moura  
**Disciplina:** Arquitetura de Aplicações Web  

---

## Vulnerabilidade 01 — A busca de clientes
1. **Qual é a falha?** Concatenação direta de strings na consulta SQL (SQL Injection).
2. **Qual o dano possível?** Acesso não autorizado, vazamento ou exclusão de dados do banco de dados.
3. **Como corrigir?** Utilizar consultas parametrizadas (`FromSqlRaw("SELECT * FROM Clientes WHERE Nome = {0}", nome)`).

---

## Vulnerabilidade 02 — A consulta de faturas
1. **Qual é a falha?** Ausência de verificação de propriedade do recurso (IDOR / BOLA).
2. **Qual o dano possível?** Um usuário logado pode visualizar faturas de outros clientes alterando o ID no endpoint.
3. **Como corrigir?** Validar se o ID da fatura pertence ao ID do usuário autenticado no token.

---

## Vulnerabilidade 03 — A configuração do servidor
1. **Qual é a falha?** Credenciais expostas no código (Hardcoded Credentials) e modo de depuração ativo em produção.
2. **Qual o dano possível?** Acesso de administrador ao banco de dados e exposição de estrutura interna do sistema em erros.
3. **Como corrigir?** Mover credenciais para variáveis de ambiente (`appsettings.json`) e ativar `UseDeveloperExceptionPage()` apenas em ambiente de desenvolvimento.

---

## Vulnerabilidade 04 — A atualização de perfil
1. **Qual é a falha?** Atribuição em massa (Mass Assignment / Over-posting).
2. **Qual o dano possível?** Elevação de privilégios (usuário comum pode se promover a `admin`).
3. **Como corrigir?** Remover o campo `Role` do DTO de atualização.

---

## Desafio
1. **Qual das 4 falhas um scanner teria MAIS dificuldade de encontrar?**
   A Vulnerabilidade 02 (IDOR / BOLA). Scanners automáticos analisam sintaxe e não entendem regras de negócio/autorização.
