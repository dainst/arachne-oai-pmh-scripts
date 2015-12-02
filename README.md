## Workflow

### 1. Arachne-DB harvesten

#### 1.1 Verknüpfungen

##### 1.1.1 semantic connections einlesen

in der Arachne-DB:

```
SELECT * INTO OUTFILE '/usr/local/arachne-oai-pmh-data/raw/verknuepfungen/SemanticConnection.csv'
FROM `SemanticConnection`
```

Beispiel-Zeilen:
```
1	16705	gruppen	400000	1076425	objekt	16628	P46_is_composed_of	
2	1076425	objekt	16628	16705	gruppen	400000	P46i_forms_part_of	
```

lokal speichern als
`arachne-oai-pmh-data/raw/verknuepfungen/SemanticConnection.csv`

##### 1.1.2 nach Datensätzen sortieren

```
cd .../arachne-oai-pmh-data/harvesting
perl .../arachne-oai-pmh-scripts/harvesting/01_connections-tabelle-verkuerzen.pl raw/SemanticConnection.csv
```


erzeugt SemanticConnection-kurz.txt:
* seriennummer nur wenn es keine ArachneEntityID gibt (also nur bei Datierung?); Markierung mit "fk" vor der Zahl (in Schritt 3 wird daraus eine URI)
* Übergangsverben werden auf ihre Nummer verkürzt (der volle Name wird später wieder ergänzt)

Beispiel-Zeile: Verküpfungen von Datensatz 5384:
```
5384 P53 1213534 or # P62i 41319 mb # P62i 41320 mb # P62i 41321 mb
```
