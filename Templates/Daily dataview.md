
```dataview-Off
LIST rows.L.text 
FROM #diario_heleri  
WHERE file.lists FLATTEN file.lists as L 
WHERE 
contains(L.text, "SOS Elevadores") 
OR 
contains(L.text, "SOS Elevadores")

GROUP BY L.section as Secao
SORT Secao DESC
LIMIT 50
```
