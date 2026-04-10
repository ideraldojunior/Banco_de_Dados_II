## Questão 1
select * from aluno;

## Questão 2
select aluno.nome, aluno.curso from aluno;

## Questão 3
select * from aluno
where aluno.curso = 'Computacao';

## Questão 4
select * from aluno
where aluno.cidade = 'Maringa';

## Questão 5
select * from aluno
order by aluno.nome;

## Questão 6
select * from aluno
order by aluno.ano_ingresso;

## Questão 7
select * from aluno
where aluno.ano_ingresso >= 2022;

## Questão 8
select * from aluno
where aluno.nome like 'A%';

## Questão 9
select * from aluno
where aluno.curso = 'Computacao' or aluno.curso = 'Engenharia';

## Questão 10
select * from disciplina
where disciplina.carga_horaria >= 60 and disciplina.carga_horaria <= 80;

## Questão 11
select count(*) from aluno;

## Questão 12
select avg(nota) from matricula;

## Questão 13
select max(*) from aluno;

## Questão 14
select min(*) from aluno;

## Questão 15
select sum(carga_horaria) from disciplina;

## Questão 16
select curso, count(*) from aluno group by(curso);

## Questão 17
select cidade, count(*) from aluno group by(cidade);

## Questão 18
select situacao, avg(nota) from matricula group by(situacao);

## Questão 19
select semestre, count(*) from matricula group by(semestre);

## Questão 20
select curso from aluno
group by curso having count() > 1 

## Questão 21
select a.nome, m.situacao 
from aluno as a
join matricula as m on a.id = m.aluno_id 
group by a.nome, m.situacao;
