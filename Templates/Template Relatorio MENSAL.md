---
tipo: relatorio
created: {{date:YYYY-MM-DD[T]HH:mm}}
---

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

# Questões Por Área


```dataview

TABLE length(rows) as Qtd, rows.file.link as "Questão"
FROM #questao 
WHERE file.frontmatter.area != "X" AND file.frontmatter.status_questao != "RESOLVIDO" AND file.frontmatter.status_questao != "CANCELADO" AND file.frontmatter.status_questao != "FECHADO" AND !contains(file.name, "Template")

GROUP BY list(file.frontmatter.area) AS Area

```



# Questões Por Semana

```dataview

TABLE length(rows) as Qtd, rows.file.link AS "Questão"
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


# Agenda




# metadado

[year:: {{date:YYYY}}] | [month:: {{date:MM}}] | [day:: {{date:DD}}] | [dayWeek:: {{date:dddd}}] | [dayWeekShort:: {{date:ddd}}] | [monthYear:: {{date:MMM}}] | [weekNumber:: {{date:ww}}] | [quarter:: {{date:Q}}] | [dayOfYear:: {{date:DDDD}}] | [weekNumber2:: {{date:ww-}}] | [month2:: {{date:MM-}}] | [day2:: {{date:DD-}}]
