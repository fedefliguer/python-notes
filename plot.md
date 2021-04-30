## Matplotlib
* Figure o figura: contenedor de todos los objetos que representan al gráfico.
* Axes: area independiente donde se generan los gráficos. Puede haber uno o más en la figura.
``` python
import matplotlib.pyplot as plt
%matplotlib inline
fig = plt.figure()
ax = plt.axes()
ax.plot([1, 2, 3, 4], [1, 4, 2, 3])
```
* plt.subplot() permite crear simultáneamente la figura y los axes que lo componen

## Seaborn
* Se siguen usando los métodos de Matplotlib, ya que Seaborn extiende sus funcionalidades
* Persiste el plt.figure si queremos dar un tamaño o algo por el estilo
``` python
import seaborn as sns
iris = sns.load_dataset('iris')

sns.set_style('darkgrid')
plt.figure(figsize=(5, 2))
sns.boxplot(data=iris, x="species", y="sepal_width")

plt.xlabel("Species"); plt.ylabel("Sepal Width");plt.title("Box Plot")
plt.show()
```

## Bokeh
Pasos para trabajar:

1. Preparar el dataset. Una simple lista, tipos de datos de Numpy y Pandas.
2. Informar donde se genera la salida del gráfico. Se usa generalmente las funciones: output_file: genera archivos html para las visualizaciones Bokeh. output_notebook: las muestra como celdas de jupyter notebooks. Se debe realizar solo una vez salvo que se quiere modificar posteriormente la salida.
3. Llamar a la función figure(). Similar a Matplotlib, es el contenedor donde se definen el estilo general, los títulos, grillas, labels de los ejes y además los tools (la barra con los botones para actuar en forma interactiva).
4. Agregar los Glyphs (glifos). El término glyph en Bokeh se refiere a los puntos, líneas, áreas y otras figuras geométricas que representan a los datos.
5. Estos dos últimos pasos los podemos repetir para mostrar varios gráficos juntos.
6. Informar a Bokeh como mostramos los resultados. show() muestra en el browser el gráfico. save() lo graba en el file definido anteriormente.

``` python
from bokeh.plotting import figure, output_notebook, show
from bokeh.io import output_notebook
from bokeh.resources import INLINE

# Dataset
circle_x = [1, 2.5, 3, 2]; circle_y = [2, 3, 1, 1.5]
triangle_x = [1, 3, 2]; triangle_y = [3, 1, 1.5]

# Salida del gráfico
output_notebook(INLINE)

# Figure
p = figure(plot_width=250, plot_height=150, tools="pan,reset,save")

# Glyphs
p.triangle(x=triangle_x, y=triangle_y, color='red', size=20)
p.circle(x=circle_x, y=circle_y, radius=0.3, alpha=0.5)

show(p) # Mostrar los resultados
```

## Plotly

Plotly Express es una función de Plotly con una interfaz de alto nivel. Opera sobre una variedad de tipos de datos y genera figuras fáciles de trabajar en su estilo. Todos los gráficos de esta clase los vamos a generar usando Plotly Express. Las funciones de Plotly Express devuelven un objeto de tipo graph_objects.Figure cuyos datos y layout se definen de acuerdo a los argumentos provistos. Y que se muestra en la notebook con el método show. Con write_image se graba en un archivo.
El esquema general para crear gráficos es:

``` python
fig = px.chart_type(df, parameters) (chart_type: bar, scatter, etc. df: dataframe)
fig.update_layout(layout_parameters or add annotations)
fig.update_traces(further graph parameters)
fig.update_xaxis() # or update_yaxis
fig.show()
```
Por ejemplo,

``` python
import numpy as np
import pandas as pd
import plotly.express as px
import plotly as pl
pl.offline.init_notebook_mode(connected=True)

df_tips = px.data.tips() # Dataset de propinas
fig = px.bar(data_frame=df_tips, x="sex", y="total_bill", color='time', width=400, height=250)
fig.update_layout(
    title='Propinas por sexo y tiempo',
    xaxis_tickfont_size=10,
    yaxis=dict(title='Total Propinas',titlefont_size=14,tickfont_size=10))
fig.show()
```
