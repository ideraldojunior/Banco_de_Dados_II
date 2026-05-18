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

## Questão 22
select nome, curso from aluno;

## Questão 23
select aluno.nome, aluno.curso, matricula.nota
from aluno 
inner join matricula on aluno.id = matricula.aluno_id;

## Questão 24
select nome  
from aluno   
where id in (
    select matricula.aluno_id   
    from matricula  
    inner join disciplina on matricula.disciplina_id = disciplina.id  
    where disciplina.departamento = 'Computacao'  
);

## Questão 25
select aluno.nome   
from aluno   
inner join matricula on aluno.id = matricula.aluno_id  
where matricula.situacao = 'Reprovado';  

## Questão 26
select aluno.nome, disciplina.nome  
from aluno  
inner join matricula on aluno.id = matricula.aluno_id  
inner join disciplina on matricula.disciplina_id = disciplina.id  
where aluno.curso = 'Computacao';  

## Questão 27
select aluno.nome, avg(matricula.nota)  
from aluno  
inner join matricula on aluno.id = matricula.aluno_id  
group by aluno.nome;  

## Questão 28
select aluno.nome, count(matricula.disciplina_id)  
from aluno  
inner join matricula on aluno.id = matricula.aluno_id  
group by aluno.nome;  

## Questão 29
select aluno.nome  
from aluno  
inner join matricula on aluno.id = matricula.aluno_id  
group by aluno.nome  
having avg(matricula.nota) > 8;  

## Questão 30
select disciplina.departamento, count(matricula.id)  
from disciplina  
inner join matricula on disciplina.id = matricula.disciplina_id  
group by disciplina.departamento; 

