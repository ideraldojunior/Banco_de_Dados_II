### Questão 1  
Qual é o objetivo da tabela `contas` neste cenário prático?  
Armazenar contas de banco, com ID, Titular e Saldo.

### Questão 2  
Quais são os saldos iniciais de cada titular antes da execução das transações?  
Ana 1000.0  
Bruno 500.0  
Carlos 300.0  
Daniela 800.0  

### Questão 3  
O que aconteceu com os saldos após o `COMMIT`?  
O saldo da Ana ficou 900.0, já o saldo do Bruno ficou 600.0. As mudanças foram persistidas graças ao COMMIT.

### Questão 4  
Por que as duas instruções `UPDATE` devem fazer parte da mesma transação?  
Porque ambas fazem parte do mesmo conjunto de operações.

### Questão 5  
Por que os valores não foram alterados ao final?  
Por conta do ROLLBACK, que voltou atrás com as alterações feitas.

### Questão 6  
Em quais situações reais o uso de `ROLLBACK` seria essencial?  
Quando uma operação foi feita de forma errônea ou resulta em um resultado inválido, por exemplo.

### Questão 7  
Por que a transação foi desfeita neste caso?  
Porque o Carlos não tinha saldo suficiente em conta para subtrair 2000.0.

### Questão 8  
Qual problema de integridade poderia ocorrer se essa transação fosse confirmada?  
O titular poderia ficar com saldo negativo, sendo que provavelmente isso não é permitido para este tipo de conta.

### Questão 9  
Qual conta foi debitada e quais contas foram creditadas?  
Contas debitadas: Daniela  
Contas creditadas: Ana e Bruno

### Questão 10  
Por que esse conjunto de operações também deve ser tratado como uma única transação?  
Porque o saldo debitado da Daniela foi creditado à Ana e ao Bruno, portanto caso a transação seja desfeita, tudo volta como estava antes.

### Questão 11  
Qual era o objetivo de observar o valor da conta em outra sessão antes do `COMMIT`?  
Ver o valor antes modificado sem persisti-lo.

### Questão 12  
Como esse teste se relaciona com o conceito de isolamento?  
Enquanto a transação não for concluida outras sessões não conseguem acessar os dados envolvidos nela.

### Questão 13  
O que aconteceu com a segunda transação?  
A segunta transação entrou em um estado de espera.

### Questão 14  
Por que ela precisou esperar?  
Ela precisou esperar visto que a primeira ainda não havia sido concluída então o isolamento foi aplicado.

### Questão 15  
Qual a função do `FOR UPDATE`?  
Serve para evitar que outra sessão altere dados que já estão sofrendo modificações mas ainda não foram confirmadas.

### Questão 16  
Por que nesse caso as transações tendem a não disputar o mesmo recurso?  
Porque estão acessando partes diferentes do banco de dados.

### Questão 17  
O que esse teste mostra sobre concorrência em linhas diferentes da tabela?  
Que o isolamento se aplica somente quando os dados que estão em disputa são os mesmos.

### Questão 18  
Qual é a importância de registrar movimentações além de atualizar os saldos?  
A importância é manter registrado as contas de origens, destino, valor...

### Questão 19  
Por que o INSERT na tabela movimentacoes deve estar na mesma transação dos UPDATEs?  
Porque caso as mudanças não sejam confirmados a inserção na tabela movimentação também nao deve ser.

### Questão 20  
O que poderia acontecer se o histórico fosse gravado, mas os saldos não fossem atualizados, ou vice-versa?
O dado seria corrompido, não coerente com a realidade.

### Questão 21  
O que o ROLLBACK garantiu nesse cenário?  
O rollback garantiu que não fosse persistido um erro, e conservando a consistência dos dados

### Questão 22  
Como esse teste demonstra a propriedade de atomicidade?  
Demonstra que ao realizar uma transação que por algum motivo não foi possível concluir, garantimos que as alterações que estavam acontecendo não sejam concretizadas.

### Questão 23  
Como verificar se o banco permaneceu consistente após todas as operações realizadas?  
Podemos verificar se as mudanças dos valores das contas estão condizentes com as operações salvas na tabela de movimentações.

### Questão 24  
Por que a consistência do banco depende não apenas dos comandos SQL, mas também da forma como eles são agrupados em transações?  
Porque nem todos os comandos SQL são efetivamente concretizados no banco de dados final, dependendo se ao final de cada transação foi realizado um Rollback ou Commit.

## 7. Atividade dissertativa
### Questão 25
Explique o que é uma transação em banco de dados.

### Questão 26
Descreva a diferença entre `COMMIT` e `ROLLBACK`.

### Questão 27
Explique por que uma transferência bancária deve ser tratada como transação.

### Questão 28
O que pode acontecer se duas transações alterarem o mesmo dado ao mesmo tempo sem controle de concorrência?

### Questão 29
Qual a relação entre transações e as propriedades ACID?

### Questão 30
Explique o significado da propriedade de atomicidade no contexto de uma operação bancária.

### Questão 31
Explique o que significa dizer que uma transação preserva a consistência do banco de dados.

### Questão 32
Descreva o papel do isolamento em ambientes com múltiplos usuários acessando o mesmo banco.

### Questão 33
Explique a importância da durabilidade após a execução de um `COMMIT`.

### Questão 34
O que é controle de concorrência e por que ele é necessário?

### Questão 35
Explique a função do lock em transações concorrentes.

### Questão 36
Descreva um exemplo prático em que o `FOR UPDATE` seja necessário.

### Questão 37
O que é uma atualização perdida (*lost update*)?

### Questão 38
Explique por que nem toda leitura concorrente gera problema, mas algumas atualizações simultâneas sim.

### Questão 39
Qual é a importância de registrar operações em uma tabela de histórico dentro da mesma transação?

### Questão 40
Em um sistema acadêmico, cite um exemplo de operação que deveria ser tratada como transação.

### Questão 41
Em um sistema de estoque, cite um exemplo de falha que poderia justificar o uso de `ROLLBACK`.

### Questão 42
Como o processamento de transações contribui para a confiabilidade de sistemas de informação?

---

### Questão 43
Considerando todos os experimentos realizados, explique de forma integrada como atomicidade, consistência, isolamento e durabilidade atuam em conjunto no processamento de transações.

---
