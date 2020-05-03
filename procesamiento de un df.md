## Links a tutoriales:
* Pandas: https://colab.research.google.com/drive/1WG62-rGLkBujg0VJZ6iy1E3Ffi5xxwcH#scrollTo=mXvIQxsFM-qW
* Numpy: https://colab.research.google.com/drive/1_P-pi3ZuayPbmg5MqR6mb8H3UmIjoSCS
* Gráficos: https://colab.research.google.com/drive/15gvykYuokTVL6rIQQcZfcR50Osnx3u_I#scrollTo=xNzEBRkzL3B0

# Cheatsheet

### Obtener un valor de una columna específica
``` python
value = df.iloc[-1, df.columns.get_loc("column")]               # -1 para el último valor, 1 para el primero, etc
```

## Filtrar el df

### Filtrar filas
``` python
final = final[final.Precio_Alerta > 0]                          # Definiendo la condición entre paréntesis y con &, | se unen condiciones
```

### Filtrar columnas
``` python
final = final[['Fecha', 'Último_Precio']]                       # Definiendo cada una
df.filter(regex=("p.*b"))                                       # Con regex
```

## Columnas nuevas

### Crear columna con nombres de filas
``` python
df['rownames'] = df.index.values
```

### Crear columna con índices
``` python
df['Index'] = np.arange(len(df))
```

### Crear columna condicional
``` python
df.loc[(df['condición'] > 100), 'Tendencia'] = 1                  # En este caso, la columna serán 1s para los positivos y NaN para los negativos. Si se quiere 0 para los negativos hay que crear otra condición.
df['techo'] = np.where((df['Close']>df['maxb']) & (df['Close']>df['maxf']), 1, 0)    # En la misma condición defino 1 y 0
```

### Crear columna con sí misma pero una fila arriba
``` python
df['column_previous'] = df.column.shift(1)                        # 1 para una fila arriba, -1 para una fila abajo
```

### Crear columna con máximo entre otras columnas
``` python
df['maxA'] = df[["A", "B"]].max(axis=1)                           # Definiendo nombres de columnas
df['maxB'] = df.filter(regex=("p.*b")).max(axis=1)                # Con regex
```
