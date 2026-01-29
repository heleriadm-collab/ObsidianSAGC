---
tipo: tecnologia
created: 2026-01-05T09:59
---

# ato administrativo

```dataview
LIST "<br />" + rows.L.text + "<hr/>"
FROM #diario_heleri  
WHERE file.lists 
AND 
( 
1 = 1 
) 
FLATTEN file.lists as L 
WHERE 
contains(L.text, "ato administrativo") 

GROUP BY L.section as Secao
SORT Secao DESC
LIMIT 100
```



# registro configuração

```dataview
LIST "<br />" + rows.L.text + "<hr/>"
FROM #diario_heleri  
WHERE file.lists 
AND 
( 
1 = 1 
) 
FLATTEN file.lists as L 
WHERE 
contains(L.text, "registro configuração") 
OR
contains(L.text, "Livro de Registro de Item") 
GROUP BY L.section as Secao
SORT Secao DESC
LIMIT 100
```

# registro reunião

```dataview
LIST "<br />" + rows.L.text + "<hr/>"
FROM #diario_heleri  
WHERE file.lists 
AND 
( 
1 = 1 
) 
FLATTEN file.lists as L 
WHERE 
contains(L.text, "registro reunião") 

GROUP BY L.section as Secao
SORT Secao DESC
LIMIT 100
```

# teste simulação


```dataview
LIST "<br />" + rows.L.text + "<hr/>"
FROM #diario_heleri  
WHERE file.lists 
AND 
( 
1 = 1 
) 
FLATTEN file.lists as L 
WHERE 
contains(L.text, "teste simulação") 

GROUP BY L.section as Secao
SORT Secao DESC
LIMIT 100
```

# metadado

[year:: 2026] | [month:: 01] | [day:: 05] | [dayWeek:: Monday] | [dayWeekShort:: Mon] | [monthYear:: Jan] | [weekNumber:: 02] | [quarter:: 1] | [dayOfYear:: 005] | [weekNumber2:: 02-] | [month2:: 01-] | [day2:: 05-]



