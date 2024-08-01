# Web Scraping: Extracción de Datos de Wikipedia a un DataFrame de Pandas
Desarrollé una extracción de datos de una tabla en Wikipedia utilizando técnicas de web scraping. Los datos se almacenan en un DataFrame de Pandas y se exportan a un archivo CSV para su análisis posterior.
## Bibliotecas Utilizadas

- BeautifulSoup
- Requests
- Pandas

## Pasos del Proyecto

### Configuración Inicial

Primero, importé las bibliotecas necesarias:

```python
from bs4 import BeautifulSoup
import requests
import pandas as pd
```

### Obtención de la Página Web

Obtenemos el contenido de la página web usando:

```python
url = "https://en.wikipedia.org/wiki/List_of_largest_companies_in_the_United_States_by_revenue"
page = requests.get(url)
soup = BeautifulSoup(page.text, "html")
```

### Localización de la Tabla Objetivo

Encuentra la tabla con la clase "wikitable sortable":

```python
table = soup.find(“table”, class_=“wikitable sortable”)
```

### Extracción de los Encabezados de la Tabla

Extrae los encabezados de la tabla:

```python
world_titles=table.find_all("th")
world_table_titles=[title.text.strip() for title in world_titles]
```

### Creación del DataFrame de Pandas

Crea el DataFrame con los encabezados extraídos:

```python
df = pd.DataFrame(columns=world_table_titles)
```

### Extracción de Datos de la Tabla

Extrae los datos de cada fila:

```python
column_data = table.find_all(“tr”)[1:]

for row in column_data:
    row_data = row.find_all("td")
    individual_row_data = [data.text.strip() for data in row_data]
    length = len(df)
    df.loc[length] = row_data
```

### Exportación a CSV

Exporta el DataFrame a un archivo CSV:

```python
df.to_csv(“companies.csv”, index=False)
```

## Conclusión

He logrado extraer datos de una tabla en Wikipedia, almacenarlos en un DataFrame de Pandas y exportarlos a un archivo CSV. Este enfoque puede adaptarse para diversos proyectos de web scraping, permitiendo la recolección y análisis de datos de diferentes sitios web!
```
