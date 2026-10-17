# HANDOUT — AULA 09

## Projete a Matriz de Acesso

*SisAcad — sistema acadêmico fictício — Arquitetura de Aplicações Web*

## 🎯 MISSÃO

Vocês são o time de segurança contratado para definir QUEM pode fazer O QUÊ no SisAcad, o novo sistema acadêmico da faculdade. Os papéis já existem: Aluno, Professor, Coordenador e Secretaria.

- Preencham a matriz abaixo com ✓ (pode) ou ✗ (não pode) para cada papel × ação
- Justifiquem por escrito os 3 casos que geraram mais discussão na dupla
- Respondam à pergunta-armadilha da Parte 03 — ela esconde o limite do modelo

*⏱️ Tempo: 25 minutos  |  👥 Formato: em duplas  |  Regra de ouro: na dúvida, NEGUE o acesso.*

> **Nomes:** filipe de Araujo Moira  **Turma:** 3001   **Data:** 15/10/2026

## PARTE 01 — A matriz papel × permissão

Marquem ✓ (pode) ou ✗ (não pode) em cada célula:

| **Ação** | **Aluno** | **Professor** | **Coordenador** | **Secretaria** |
| --- | --- | --- | --- | --- |
| 1. Ver as próprias notas | v | v | v | v |
| 2. Ver notas de toda a turma | x | v | v | v |
| 3. Lançar nota | x | v | v | x |
| 4. Alterar nota já lançada | x | x | v | x |
| 5. Matricular aluno em disciplina | x | x | x | v |
| 6. Trancar matrícula | x | x | x | v |
| 7. Criar nova disciplina | x | x | v | x |
| 8. Ver dados pessoais de aluno | v | x | v | v |
| 9. Emitir histórico escolar | x | x | x | v |
| 10. Aprovar colação de grau | x | x | v | v |

*Dica: pensem em consequências — quem responde perante o MEC se uma nota for alterada indevidamente? E perante a LGPD se dados pessoais vazarem?*

## PARTE 02 — Os casos polêmicos

Quais 3 células geraram mais discussão na dupla? Anotem a célula (ação + papel) e a justificativa da decisão final:

1. Caso 1: Alterar nota já lançada × Professor
   Negado (X). O professor pode lançar notas inicialmente, mas alterar a nota depois de ´ja ter lançado no sistema exige uma permição de um coordenador ou adminstrados com altorização de acesso que o professor não teria. 

2. Caso 2: Ver dados pessoais do aluno × Professor
   Negado (X). O professor não tem a necessidade de ter acesssos a informações censiveis do aluno como numero de CPF e Endereço do Aluno o professor necessita apenas dos dados académicos.

3. Caso 3: Lançar nota × Secretaria
   Negado (X). A avaliação e o lançamento de notas são responsabilidade exclusiva do professor.

## PARTE 03 — A pergunta-armadilha

Vocês marcaram que Professor pode “lançar nota”. Mas… de QUALQUER turma? O professor de Cálculo pode lançar nota na turma de Arquitetura de Aplicações Web?

1. O papel “Professor” sozinho é suficiente para decidir esse acesso? Por quê?
Não. O papel sozinho (RBAC estático) concede permissões globais. Se avaliarmos apenas o papel, um professor de Cálculo teria autorização para alterar notas em Arquitetura de Aplicações Web ou em qualquer outra disciplina do sistema.

2. Que informação ALÉM do papel o sistema precisa conhecer para decidir corretamente?
O sistema precisa de saber sobre o contexto/vínculo (relação entre o utilizador e a turma). Especificamente, precisa de verificar os atributos da requisição (ABAC): ID do Professor logado == ID do Professor responsável pela Turma/Disciplina.

3. Onde vocês já viram esse mesmo problema nesta disciplina? (dica: Aula 07…)
O sistema precisa de conhecer o contexto/vínculo (relação entre o utilizador e a turma). Especificamente, precisa de verificar os atributos da requisição (ABAC): ID do Professor logado == ID do Professor responsável pela Turma/Disciplina.

## DESAFIO

1. Chegou um pedido da coordenação: criar o papel “Monitor” — um aluno que ajuda o professor em uma disciplina. Que permissões vocês dariam ao Monitor? Que risco novo esse papel cria?

Permissões concedidas:
Ver notas da turma onde atua como monitor.
Lançar/Rascunhar notas de exercícios (sob aprovação/validação posterior do professor).
Riscos novos criados:
Conflito de Interesses / Elevação de Privilégios: O monitor é também um aluno. Se o escopo não for estritamente limitado à disciplina onde ele apoia, ele pode tentar alterar as suas próprias notas como aluno noutras disciplinas ou adulterar as notas dos seus colegas de turma.

Quebra do Princípio do Menor Privilégio: Conceder acesso de escrita/leitura ampla de dados de avaliação a um estudante aumenta a superfície de ataque para adulteração de dados académicos.