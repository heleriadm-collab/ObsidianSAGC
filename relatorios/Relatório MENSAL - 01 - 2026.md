---
tipo: relatorio
created: 2026-01-05T09:32
---


`$= 'Impresso em '+ moment(new Date(now())).format('DD/MM/YYYY HH:mm') + ' '`

Versão pdf A3 (computador) clique em => [[Relatório MENSAL - 01 - 2026_A3.pdf]]

Versão pdf A5 (celular) clique em => [[Relatório MENSAL - 01 - 2026_A5.pdf]]

# Questões Por Área

## FAZER

```dataview

TABLE length(rows) as Qtd, rows.file.link as Registro
FROM #questao 
WHERE file.frontmatter.area != "X" AND file.frontmatter.status_questao != "RESOLVIDO" AND file.frontmatter.status_questao != "CANCELADO" AND file.frontmatter.status_questao != "FECHADO" AND !contains(file.name, "Template")
AND any(file.tasks, (t) => !t.completed)

GROUP BY list(file.frontmatter.area) AS Area

```

## FEITO

```dataview

TABLE length(rows) as Qtd, rows.file.link as Registro
FROM #questao 
WHERE file.frontmatter.area != "X" AND file.frontmatter.status_questao != "RESOLVIDO" AND file.frontmatter.status_questao != "CANCELADO" AND file.frontmatter.status_questao != "FECHADO" AND !contains(file.name, "Template")
AND any(file.tasks, (t) => t.completed)

GROUP BY list(file.frontmatter.area) AS Area

```

# Fundo Manutenção

```dataview

TABLE length(rows) as Qtd, rows.file.link AS "Questões"
FROM #fundo_manutencao 
WHERE 
file.frontmatter.area != "INFORMAR" 
AND file.frontmatter.status_questao != "RESOLVIDO" 
AND file.frontmatter.status_questao != "CANCELADO" 
AND file.frontmatter.status_questao != "FECHADO" 
AND !contains(file.name, "Template")
GROUP BY "semana " + list( dateformat(created, "WW yyyy") ) AS "Semana/Ano"
SORT Mes DESC

```


# Questões Por Semana
```dataview

TABLE length(rows) as Qtd, rows.file.link AS "Questões"
FROM #questao 
WHERE 
file.frontmatter.area != "INFORMAR" 
AND file.frontmatter.status_questao != "RESOLVIDO" 
AND file.frontmatter.status_questao != "CANCELADO" 
AND file.frontmatter.status_questao != "FECHADO" 
AND !contains(file.name, "Template")
GROUP BY "semana " + list( dateformat(created, "WW yyyy") ) AS "Semana/Ano"
SORT Mes DESC

```

# Rotinas Derivadas de Tarefas

```dataview
TABLE WITHOUT ID
  qnd_mes AS "Mes",
  dateformat(quando, "dd/MM/yyyy") AS "Qnd",
  status AS "Status",
  descricao AS "Descr",
  responsavel AS "Resp.",
  file.link AS "Rotina"
FROM #rotina
WHERE
  tipo = "manutencao"
  AND qnd_ano = 2026
  AND any(file.tasks, (t) => !t.completed)
SORT quando ASC

```

# Lembretes - Em Aberto

```dataview
TASK
FROM #diario_heleri 
WHERE !completed
WHERE 
contains( dateformat(created, "MMyyyy"),  dateformat(this.created, "MMyyyy") ) 
AND
( 
contains(text, "registro lembrete")
OR 
contains(text, "próximos passos")
)
GROUP BY section as Secao
SORT Secao DESC
LIMIT 200
```


# Lembretes - Encerrados


```dataview
TASK
FROM #diario_heleri 
WHERE completed
WHERE 
contains( dateformat(created, "MMyyyy"),  dateformat(this.created, "MMyyyy") ) 
AND
( 
contains(text, "registro lembrete")
OR 
contains(text, "próximos passos")
)
GROUP BY section as Secao
SORT Secao DESC
LIMIT 200
```



# Diário Bordo do Mês


```dataview
LIST "<br />" + rows.L.text + "<hr /><br />"
FROM #diario_heleri  
WHERE file.lists AND month = this.month AND year = this.year 
FLATTEN file.lists as L 
GROUP BY L.section as Secao
SORT Secao DESC
LIMIT 200
```


# Agenda

%% COMPROMISSOS Q NOS TEMOS A FAZER %%

%% ROTINA RELACIONA OUTROS Q VAO EXECUTAR PRA GENTE %%

# metadado

[year:: 2026] [month:: 01] [day:: 05] [dayWeek:: Monday] [dayWeekShort:: Mon] [monthYear:: Jan] [weekNumber:: 02] [quarter:: 1] [dayOfYear:: 005] [weekNumber2:: 02-] [month2:: 01-] [day2:: 05-]
