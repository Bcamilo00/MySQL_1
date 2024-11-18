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

π Name(σ Population>20000000 ∧ IsOfficial= ′T′(Country⋈CountryLanguage))

```sql
SELECT DISTINCT Continent
FROM Country;

```

![Ejemplo1_Basicas](https://github.com/Bcamilo00/MySQL_1/blob/main/a1.png)

### 2. Lista los países que tienen más de 2 idiomas oficiales.

π Name(σ count(Language)>2(Country⋈CountryLanguage WHERE IsOfficial=’T’ GROUP BY Country.Name))

```sql
SELECT Country.Name
FROM Country
JOIN CountryLanguage ON Country.Code = CountryLanguage.CountryCode
WHERE CountryLanguage.IsOfficial = 'T'
GROUP BY Country.Name
HAVING COUNT(DISTINCT CountryLanguage.Language) > 2;
```

![Ejemplo1_Basicas](https://github.com/Bcamilo00/MySQL_1/blob/main/a2.png)

### 3. Encuentra los países que tienen el mismo idioma oficial que México.

π Name(σ Language∈(π Language​(σ CountryCode= ′MEX′(CountryLanguage)))(Country⋈CountryLanguage))

```sql
SELECT DISTINCT Country.Name
FROM Country
JOIN CountryLanguage ON Country.Code = CountryLanguage.CountryCode
WHERE CountryLanguage.Language IN (
    SELECT Language
    FROM CountryLanguage
    WHERE CountryCode = 'MEX'
);
```

![Ejemplo1_Basicas](https://github.com/Bcamilo00/MySQL_1/blob/main/a3.png)

### 4. Encuentra las ciudades que tienen una población entre 1 y 2 millones y están en Europa.

π City.Name (σ Continent= ′ Europe ′ ∧ Population≥1000000 ∧ Population≤2000000​(City⋈Country))

```sql
SELECT City.Name
FROM City
JOIN Country ON City.CountryCode = Country.Code
WHERE Country.Continent = 'Europe' AND City.Population BETWEEN 1000000 AND 2000000;
```

![Ejemplo1_Basicas](https://github.com/Bcamilo00/MySQL_1/blob/main/a4.png)

### 5. Encuentra los países con una superficie menor que la de Japón.

π Name(σ SurfaceArea<(SELECTSurfaceAreaFROMCountryWHEREName= ′ Japan ′)​(Country))

```sql
SELECT Name
FROM Country
WHERE SurfaceArea < (SELECT SurfaceArea FROM Country WHERE Name = 'Japan');
```

![Ejemplo1_Basicas](https://github.com/Bcamilo00/MySQL_1/blob/main/a5.png)

### 6. Lista los idiomas que son oficiales en más de 3 países en América.

π Language​(σ IsOfficial= ′T′ ​(CountryLanguage⋈Country) GROUP BY Language HAVING count(CountryCode)>3 ∧ Continent= ′ America ′)

```sql
SELECT CountryLanguage.Language
FROM CountryLanguage
JOIN Country ON CountryLanguage.CountryCode = Country.Code
WHERE Country.Continent = 'North America' OR Country.Continent = 'South America'
AND CountryLanguage.IsOfficial = 'T'
GROUP BY CountryLanguage.Language
HAVING COUNT(DISTINCT Country.Code) > 3;
```

![Ejemplo1_Basicas](https://github.com/Bcamilo00/MySQL_1/blob/main/a6.png)

### 7. Lista los países que tienen una capital con población mayor a 1 millón.

π Name(σ City.Population>1000000 ∧ City.ID=Country.Capital​(City⋈Country))

```sql
SELECT Country.Name
FROM Country
JOIN City ON Country.Capital = City.ID
WHERE City.Population > 1000000;

```

![Ejemplo1_Basicas](https://github.com/Bcamilo00/MySQL_1/blob/main/a7.png)

### 8. Encuentra los países que tienen más de 50% de su población viviendo en ciudades registradas.

π Name​(σ urban population ratio>0.5​(Country JOIN with city population data))

```sql
SELECT Country.Name
FROM Country
JOIN City ON Country.Code = City.CountryCode
GROUP BY Country.Name, Country.Population
HAVING SUM(City.Population) > 0.5 * Country.Population;
```

![Ejemplo1_Basicas](https://github.com/Bcamilo00/MySQL_1/blob/main/a8.png)

### 9. Encuentra las ciudades que son capitales en países de Asia y tienen una población menor a 500,000.

πCity.Name​(σ Continent= ′Asia′ ∧ City.ID=Country.Capital ∧ City.Population<500000​(City⋈Country))

```sql
SELECT City.Name
FROM City
JOIN Country ON City.ID = Country.Capital
WHERE Country.Continent = 'Asia' AND City.Population < 500000;
```

![Ejemplo1_Basicas](https://github.com/Bcamilo00/MySQL_1/blob/main/a9.png)

### 10. Lista los países que tienen más de 10 idiomas registrados, sin importar si son oficiales o no.

π Name​(σcount(Language)>10(Country⋈CountryLanguage GROUP BY Country.Name))

```sql
SELECT Country.Name
FROM Country
JOIN CountryLanguage ON Country.Code = CountryLanguage.CountryCode
GROUP BY Country.Name
HAVING COUNT(CountryLanguage.Language) > 10;
```

![Ejemplo1_Basicas](https://github.com/Bcamilo00/MySQL_1/blob/main/a10.png)

## Conclusiones

- Comprensión de las Relaciones y Consultas: Hemos aprendido a traducir problemas del mundo real en consultas formales usando álgebra relacional y luego implementarlas en SQL. Esto fortalece nuestra capacidad para analizar y estructurar datos de manera lógica y precisa.

- Manejo de Operaciones Complejas: Desarrollar consultas avanzadas, como las que involucran funciones de agregación, operaciones de unión, y subconsultas, nos ayuda a comprender cómo manipular grandes volúmenes de datos y extraer información relevante de manera eficiente.

- Optimización de Consultas: Aprender a usar condiciones específicas y funciones de filtrado nos enseña la importancia de optimizar consultas, lo que es fundamental para el rendimiento de las bases de datos. Esta habilidad se vuelve especialmente útil cuando trabajamos con datos a gran escala.

- Conexiones y Relaciones entre Tablas: Trabajar con operadores como JOIN y entender cómo las tablas se relacionan en una base de datos nos permite desarrollar consultas más complejas y extraer datos significativos de múltiples fuentes.

- Pensamiento Lógico y Análisis de Datos: Resolver problemas a través de consultas fomenta un pensamiento lógico y estructurado. Nos obliga a descomponer problemas complejos en pasos más pequeños y manejables, lo que es esencial para el análisis de datos.

## Referencias

https://chatgpt.com/?model=auto

https://claude.ai/new
