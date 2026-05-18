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
Uma transação é uma unidade lógica de trabalho que agrupa um conjunto de uma ou mais operações SQL (como inserções, atualizações ou exclusões). Para o banco de dados, esse grupo deve ser tratado de forma indivisível: ou todas as operações são executadas com sucesso, ou nenhuma delas é aplicada. O objetivo principal é garantir a integridade dos dados, impedindo estados intermediários ou corrompidos.

### Questão 26
Descreva a diferença entre `COMMIT` e `ROLLBACK`.
`COMMIT`: É o comando que finaliza uma transação com sucesso. Ele torna todas as alterações feitas durante a transação permanentes e visíveis para os outros usuários do banco de dados.
`ROLLBACK`: É o comando de aborto. Ele desfaz todas as alterações realizadas pela transação atual, retornando o banco de dados exatamente ao estado em que estava antes do início da transação.

### Questão 27
Explique por que uma transferência bancária deve ser tratada como transação.
Uma transferência envolve pelo menos duas etapas críticas: subtrair o dinheiro da conta A e somar o dinheiro na conta B. Se o sistema falhar no meio do caminho (após retirar o dinheiro de A, mas antes de depositar em B), o dinheiro simplesmente sumiria. Tratar o processo como uma transação garante que, se uma etapa falhar, todo o processo seja desfeito, evitando a perda de consistência do saldo.

### Questão 28
O que pode acontecer se duas transações alterarem o mesmo dado ao mesmo tempo sem controle de concorrência?
A falta de controle pode gerar sérios problemas de integridade, incluindo:
**Atualizações Perdidas** (Lost Updates): Uma transação sobrescreve as alterações da outra sem tomar conhecimento delas.
**Leituras Sujas** (Dirty Reads): Uma transação lê dados modificados por outra transação que ainda não foi confirmada (e que pode sofrer um `ROLLBACK`).
**Inconsistência de Dados**: O banco pode armazenar valores logicamente impossíveis ou contraditórios.

### Questão 29
Qual a relação entre transações e as propriedades ACID?
As propriedades ACID (Atomicidade, Consistência, Isolamento e Durabilidade) são os critérios e garantias que o Sistema Gerenciador de Banco de Dados (SGBD) deve cumprir para assegurar que as transações sejam processadas de forma confiável e segura. Elas definem o padrão de qualidade de uma transação.

### Questão 30
Explique o significado da propriedade de atomicidade no contexto de uma operação bancária.
A atomicidade dita que a transação é uma regra do "tudo ou nada". No contexto bancário, ao pagar um boleto, a operação inteira (retirar o saldo da sua conta e registrar o pagamento no sistema do beneficiário) é efetuada com sucesso ou, se houver qualquer erro (como queda de energia ou falta de saldo), o sistema desfaz tudo. Não existe "meio pagamento".

### Questão 31
Explique o que significa dizer que uma transação preserva a consistência do banco de dados.
Significa que uma transação só pode levar o banco de dados de um estado válido para outro estado válido. Ela deve respeitar todas as regras de integridade do sistema (como chaves primárias, chaves estrangeiras e restrições de verificação). Se as alterações violarem qualquer regra de negócio ou restrição técnica, a transação é rejeitada.

### Questão 32
Descreva o papel do isolamento em ambientes com múltiplos usuários acessando o mesmo banco.
O isolamento garante que a execução concorrente de várias transações não interfira umas nas outras. Ele faz com que cada transação pareça estar sendo executada de forma exclusiva no sistema. Isso impede que os efeitos parciais de uma transação inacabada fiquem visíveis para outros usuários, evitando decisões baseadas em dados provisórios ou incorretos.

### Questão 33
Explique a importância da durabilidade após a execução de um `COMMIT`.
A durabilidade garante que, uma vez emitido o `COMMIT`, as alterações se tornam permanentes. Mesmo que ocorra uma queda de energia, uma falha de hardware ou o servidor reinicie abruptamente logo em seguida, o banco de dados recuperará o estado confirmado e os dados não serão perdidos, pois foram gravados de forma não volátil (em disco ou logs de transação).

### Questão 34
O que é controle de concorrência e por que ele é necessário?
É o mecanismo utilizado pelo SGBD para coordenar os acessos simultâneos de múltiplos usuários aos mesmos dados. Ele é necessário para evitar conflitos e interferências entre transações concorrentes, garantindo que as propriedades de isolamento e consistência sejam mantidas sem sacrificar drasticamente o desempenho do sistema.

### Questão 35
Explique a função do lock em transações concorrentes.
O lock (bloqueio) funciona como uma trava de segurança. Quando uma transação precisa alterar (ou, às vezes, ler) um registro, ela coloca um lock nele. Isso avisa as outras transações de que aquele dado está sendo utilizado e que elas devem esperar até que a transação detentora do lock faça um `COMMIT` ou `ROLLBACK` para liberá-lo, impedindo modificações simultâneas destrutivas.

### Questão 36
Descreva um exemplo prático em que o `FOR UPDATE` seja necessário.
Imagine um sistema de reserva de poltronas de cinema. Dois usuários clicam no mesmo assento disponível exatamente no mesmo segundo. O sistema faz um `SELECT` para checar se a poltrona está livre. Utilizando o `SELECT ... FOR UPDATE`, o primeiro usuário que ler o registro bloqueia a linha imediatamente. Assim, o segundo usuário é obrigado a esperar até que o primeiro finalize a compra; quando a vez do segundo chegar, o sistema validará que o status mudou para "ocupado", impedindo a venda duplicada.

### Questão 37
O que é uma atualização perdida (*lost update*)?
Ocorre quando duas transações (T1 e T2) leem o mesmo valor de um dado (ex: Saldo = 100). T1 subtrai 20 (novo saldo = 80). Quase simultaneamente, T2 lê o saldo original (100) e soma 50 (novo saldo = 150). T1 salva seu resultado (80) e, logo depois, T2 salva seu resultado (150). A alteração feita por T1 (a subtração de 20) foi completamente sobrescritas e perdida por T2.

### Questão 38
Explique por que nem toda leitura concorrente gera problema, mas algumas atualizações simultâneas sim.
Leituras puras são operações idempotentes e seguras, pois não alteram o estado do banco de dados; mil pessoas podem ler o mesmo dado ao mesmo tempo sem que ele mude. Já as atualizações modificam o estado. Se ocorrerem simultaneamente no mesmo registro, elas competem para definir qual será a nova realidade daquele dado, gerando condições de corrida e corrupção se não forem ordenadas.

### Questão 39
Qual é a importância de registrar operações em uma tabela de histórico dentro da mesma transação?
Garante a rastreabilidade e a auditoria perfeita do sistema. Ao colocar a ação principal (ex: alterar o status de um pedido) e a gravação do histórico (ex: "Pedido alterado por Usuário X") na mesma transação, você elimina o risco de atualizar o dado e esquecer de registrar o histórico (ou vice-versa). Ou ambos acontecem, ou nada acontece.

### Questão 40
Em um sistema acadêmico, cite um exemplo de operação que deveria ser tratada como transação.
A matrícula de um aluno em uma disciplina com vagas limitadas. A operação envolve:
- Verificar se há vagas disponíveis na turma.
- Inserir a linha de vínculo do aluno na tabela de matrículas.
- Decrementar o número de vagas disponíveis na tabela da turma.
Tudo isso precisa ser uma única transação para evitar que a turma estoure o limite de alunos.

### Questão 41
Em um sistema de estoque, cite um exemplo de falha que poderia justificar o uso de `ROLLBACK`.
Durante a finalização de uma venda, o sistema dá baixa de 5 itens no estoque e tenta processar o pagamento no cartão de crédito do cliente. O gateway de pagamento retorna um erro de "cartão recusado". Como a venda não pôde ser concluída por falha financeira, o sistema aciona um `ROLLBACK` para estornar os itens ao estoque e não deixar a contagem de produtos incorreta.

### Questão 42
Como o processamento de transações contribui para a confiabilidade de sistemas de informação?
Ele transforma cenários caóticos, com milhares de usuários acessando os mesmos dados, quedas de energia repentinas e falhas de rede, em um ambiente previsível e estável. Ao garantir que as regras de integridade do negócio sejam rigidamente seguidas através de mecanismos de recuperação e isolamento, as transações blindam o sistema contra dados corrompidos, gerando confiança para os usuários e empresas.

---

### Questão 43
Considerando todos os experimentos realizados, explique de forma integrada como atomicidade, consistência, isolamento e durabilidade atuam em conjunto no processamento de transações.
As quatro propriedades do ACID operam como uma engrenagem única e integrada para proteger o ciclo de vida da informação:
A Atomicidade define a fronteira da operação, garantindo que o bloco de comandos seja indivisível (não deixando o trabalho "pela metade"). Enquanto essa unidade executa, o Isolamento age como uma barreira protetora, impedindo que o caos do acesso simultâneo de outros usuários contamine ou distorça os dados intermediários enquanto eles são manipulados.
Tudo isso ocorre sob o escopo da Consistência, que funciona como o tribunal de regras de negócio do banco, certificando-se de que, do início ao fim da transação, nenhuma lei ou restrição do sistema seja violada. Finalmente, quando a transação prova ser válida e segura, o comando COMMIT aciona a Durabilidade, que grava o resultado final em pedra (armazenamento persistente), assegurando que o novo estado consistente sobreviva ao tempo e a qualquer falha técnica.

---
