**Pergunta 1**  
Qual é o objetivo da tabela `contas` neste cenário prático?  
Armazenar contas de banco, com ID, Titular e Saldo.

**Pergunta 2**  
Quais são os saldos iniciais de cada titular antes da execução das transações?  
Ana 1000.0  
Bruno 500.0  
Carlos 300.0  
Daniela 800.0  

**Pergunta 3**  
O que aconteceu com os saldos após o `COMMIT`?  
O saldo da Ana ficou 900.0, já o saldo do Bruno ficou 600.0. As mudanças foram persistidas graças ao COMMIT.

**Pergunta 4**  
Por que as duas instruções `UPDATE` devem fazer parte da mesma transação?  
Porque ambas fazem parte do mesmo conjunto de operações.

**Pergunta 5**  
Por que os valores não foram alterados ao final?  
Por conta do ROLLBACK, que voltou atrás com as alterações feitas.

**Pergunta 6**  
Em quais situações reais o uso de `ROLLBACK` seria essencial?  
Quando uma operação foi feita de forma errônea ou resulta em um resultado inválido, por exemplo.

**Pergunta 7**  
Por que a transação foi desfeita neste caso?  
Porque o Carlos não tinha saldo suficiente em conta para subtrair 2000.0.

**Pergunta 8**  
Qual problema de integridade poderia ocorrer se essa transação fosse confirmada?  
O titular poderia ficar com saldo negativo, sendo que provavelmente isso não é permitido para este tipo de conta.

**Pergunta 9**  
Qual conta foi debitada e quais contas foram creditadas?  
Contas debitadas: Daniela  
Contas creditadas: Ana e Bruno

**Pergunta 10**  
Por que esse conjunto de operações também deve ser tratado como uma única transação?  
Porque o saldo debitado da Daniela foi creditado à Ana e ao Bruno, portanto caso a transação seja desfeita, tudo volta como estava antes.

**Pergunta 11**  
Qual era o objetivo de observar o valor da conta em outra sessão antes do `COMMIT`?  
Ver o valor antes modificado sem persisti-lo.

**Pergunta 12**  
Como esse teste se relaciona com o conceito de isolamento?  
Enquanto a transação não for concluida outras sessões não conseguem acessar os dados envolvidos nela.

**Pergunta 13**  
O que aconteceu com a segunda transação?

**Pergunta 14**  
Por que ela precisou esperar?

**Pergunta 15**  
Qual a função do `FOR UPDATE`?



