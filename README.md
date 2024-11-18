# MySQL Consultas Nivel Medio
## Introducción
La gestión y análisis de datos mediante sistemas de bases de datos relacionales se ha convertido en una herramienta fundamental en el mundo actual. MySQL, como uno de los sistemas de gestión de bases de datos más utilizados, permite realizar consultas y análisis de información de manera efectiva. Este trabajo presenta una serie de consultas realizadas sobre la base de datos "WORLD", la cual contiene información relevante sobre países, ciudades, idiomas y otros datos demográficos a nivel mundial.
El objetivo principal de este trabajo es demostrar diferentes niveles de complejidad en las consultas SQL, empezando desde las más básicas hasta llegar a algunas más avanzadas. Se han organizado las consultas en tres niveles: básico, intermedio y adicional, permitiendo así una progresión gradual en el aprendizaje y comprensión de los conceptos.
La base de datos "WORLD" resulta especialmente interesante para este ejercicio ya que contiene múltiples tablas relacionadas entre sí, lo que permite practicar diferentes tipos de consultas y operaciones. Además, al trabajar con datos reales sobre países y poblaciones, se pueden obtener resultados significativos y comprensibles que facilitan la verificación de la correcta ejecución de las consultas.
A lo largo del trabajo se explorarán diferentes aspectos de MySQL, como el uso de funciones de agregación, subconsultas, joins entre tablas y funciones de ventana, demostrando así la versatilidad y potencia de este sistema de gestión de bases de datos.

## Consultas 

### 1. Encuentra los países que tienen un idioma oficial.

```sql
SELECT DISTINCT CountryCode
FROM CountryLanguage
WHERE IsOfficial = 'T';
```

![Ejemplo1_Basicas](https://github.com/Bcamilo00/MySQL_1/blob/main/1.png)

### 2. Lista los países que tienen más de un idioma oficial.

```sql
SELECT CountryCode
FROM CountryLanguage
WHERE IsOfficial = 'T'
GROUP BY CountryCode
HAVING COUNT(*) > 1;
```

![Ejemplo1_Basicas](https://github.com/Bcamilo00/MySQL_1/blob/main/2.png)

### 3. Encuentra los países que tienen el mismo continente que Japón.

```sql
SELECT Name
FROM Country
WHERE Continent = (SELECT Continent FROM Country WHERE Name = 'Japan');
```

![Ejemplo1_Basicas](https://github.com/Bcamilo00/MySQL_1/blob/main/3.png)

### 4. Encuentra las ciudades que tienen población mayor a 5 millones y están en América del Sur.

```sql
SELECT City.Name
FROM City
JOIN Country ON City.CountryCode = Country.Code
WHERE City.Population > 5000000 AND Country.Continent = 'South America';
```

![Ejemplo1_Basicas](https://github.com/Bcamilo00/MySQL_1/blob/main/4.png)

### 5. Encuentra los países que no tienen ningún idioma oficial.

```sql
SELECT Code
FROM Country
WHERE Code NOT IN (
    SELECT CountryCode
    FROM CountryLanguage
    WHERE IsOfficial = 'T'
);
```

![Ejemplo1_Basicas](https://github.com/Bcamilo00/MySQL_1/blob/main/5.png)

### 6. Encuentra los idiomas que son oficiales en al menos dos países.

```sql
SELECT Language
FROM CountryLanguage
WHERE IsOfficial = 'T'
GROUP BY Language
HAVING COUNT(DISTINCT CountryCode) >= 2;
```

![Ejemplo1_Basicas](https://github.com/Bcamilo00/MySQL_1/blob/main/6.png)

### 7. Lista los países y su capital.

```sql
SELECT Country.Name AS CountryName, City.Name AS CapitalName
FROM Country
JOIN City ON Country.Capital = City.ID;
```

![Ejemplo1_Basicas](https://github.com/Bcamilo00/MySQL_1/blob/main/7.png)

### 8. Encuentra los países que tienen una población mayor que Alemania.

```sql
SELECT Name
FROM Country
WHERE Population > (SELECT Population FROM Country WHERE Name = 'Germany');
```

![Ejemplo1_Basicas](https://github.com/Bcamilo00/MySQL_1/blob/main/8.png)

### 9. Encuentra los idiomas oficiales de Europa.

```sql
SELECT DISTINCT Language
FROM CountryLanguage
JOIN Country ON CountryLanguage.CountryCode = Country.Code
WHERE IsOfficial = 'T' AND Country.Continent = 'Europe';
```

![Ejemplo1_Basicas](https://github.com/Bcamilo00/MySQL_1/blob/main/9.png)

### 10. Encuentra los países sin ciudades registradas en la tabla City.

```sql
SELECT Code
FROM Country
WHERE Code NOT IN (SELECT CountryCode FROM City);
```

![Ejemplo1_Basicas](https://github.com/Bcamilo00/MySQL_1/blob/main/10.png)

### 11. Muestra la población total de cada continente.

```sql
SELECT Continent, SUM(Population) AS TotalPopulation
FROM Country
GROUP BY Continent;
```

![Ejemplo1_Basicas](https://github.com/Bcamilo00/MySQL_1/blob/main/11.png)

### 12. Encuentra los países en los que la esperanza de vida es menor al promedio global.

```sql
SELECT Name
FROM Country
WHERE LifeExpectancy < (SELECT AVG(LifeExpectancy) FROM Country);
```

![Ejemplo1_Basicas](https://github.com/Bcamilo00/MySQL_1/blob/main/12.png)

### 13. Encuentra los países en Asia sin idioma oficial registrado.

```sql
SELECT Code
FROM Country
WHERE Continent = 'Asia' AND Code NOT IN (
    SELECT CountryCode
    FROM CountryLanguage
    WHERE IsOfficial = 'T'
);
```

![Ejemplo1_Basicas](https://github.com/Bcamilo00/MySQL_1/blob/main/13.png)

### 14. Lista los idiomas que son oficiales en países con esperanza de vida mayor a 80.

```sql
SELECT DISTINCT Language
FROM CountryLanguage
JOIN Country ON CountryLanguage.CountryCode = Country.Code
WHERE IsOfficial = 'T' AND Country.LifeExpectancy > 80;
```

![Ejemplo1_Basicas](https://github.com/Bcamilo00/MySQL_1/blob/main/14.png)

### 15. Encuentra los países con más de 10 ciudades en la tabla City.

```sql
SELECT CountryCode
FROM City
GROUP BY CountryCode
HAVING COUNT(*) > 10;
```

![Ejemplo1_Basicas](https://github.com/Bcamilo00/MySQL_1/blob/main/15.png)

## Consultas Adicionales

### 1. Encuentra los países que tienen al menos un idioma oficial y una población mayor a 20 millones.

π Name(σ Population>20000000 ∧ IsOfficial= ′T′
 
​
 (Country⋈CountryLanguage))
```sql
SELECT DISTINCT Continent
FROM Country;

```




```sql

```




```sql

```




```sql

```




```sql

```




```sql

```




```sql

```




```sql

```



```sql

```




```sql

```





```sql

```


```sql

```




```sql

```




```sql

```





```sql

```
