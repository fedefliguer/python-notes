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

### Trasponer
``` python
df.T                                  
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

## SettingwithCopyWarning
Este warning aparece cuando se asigna un valor en una copia

## Caso 1
``` python
data[data.bidder == 'parakeet2004'] # Tres filas de las que queremos reemplazar el valor de la columna bidderrate

data[data.bidder == 'parakeet2004']['bidderrate'] = 100 # Tira el warning. La modificación no se hace en data, 
data[data.bidder == 'parakeet2004'] # No tiene modificaciones

data.loc[data.bidder == 'parakeet2004', 'bidderrate'] = 100 # No tira el warning
data[data.bidder == 'parakeet2004'] # Tiene modificaciones
```
Esto sucedió porque en el primer caso hay dos operaciones que se hacen en forma consecutiva, por lo que la asignación = 100 no se hace sobre data sino sobre el df generado a partir del filtro, que es una copia. En el segundo caso se hace en el mismo movimiento todo.

## Caso 2
``` python
winners = data.loc[data.bid == data.price] # Creo un df a partir de otro
winners.loc[304, 'bidder'] = 'therealname' # Asigno un valor faltante en una celda. Tira el warning.
print(winners.loc[304, 'bidder']) # Hizo el cambio que le dije

winners = data.loc[data.bid == data.price].copy() # Creo un df a partir de otro, explicitando la copia
winners.loc[304, 'bidder'] = 'therealname' # Asigno un valor faltante en una celda. No tira el warning.
print(winners.loc[304, 'bidder']) # Hizo el cambio que le dije

winners = data.loc[data.bid == data.price]
winners.is_copy = None
winners.loc[304, 'bidder'] = 'therealname'
```
En los dos casos hace lo mismo, pero en uno tira el warning y en otro no. El warning viene de que la creación de winners no explicitó la copia. El tercer caso es lo mismo, con el paso is_copy = None evito el warning.
