# 📐 Medidas DAX - Superstore Dashboard

Este documento contiene todas las medidas DAX utilizadas en el dashboard.

---

## 📊 KPIs Principales

### Total Ventas
```dax
Total Ventas = SUM(superstore[Sales])
```

### Total Ganancias
```dax
Total Ganancias = SUM(superstore[Profit])
```

### Total Órdenes
```dax
Total Órdenes = DISTINCTCOUNT(superstore[Order ID])
```

### Total Cantidad
```dax
Total Cantidad = SUM(superstore[Quantity])
```

---

## 📈 Métricas Calculadas

### Margen de Ganancia (%)
```dax
Margen % = 
DIVIDE(
    [Total Ganancias],
    [Total Ventas],
    0
) * 100
```

### Ticket Promedio
```dax
Ticket Promedio = 
DIVIDE(
    [Total Ventas],
    [Total Órdenes],
    0
)
```

### Ganancia por Unidad
```dax
Ganancia por Unidad = 
DIVIDE(
    [Total Ganancias],
    [Total Cantidad],
    0
)
```

### Precio Promedio
```dax
Precio Promedio = 
DIVIDE(
    [Total Ventas],
    [Total Cantidad],
    0
)
```

---

## 📅 Comparativas Temporales

### Ventas Año Anterior
```dax
Ventas YoY = 
CALCULATE(
    [Total Ventas],
    SAMEPERIODLASTYEAR(superstore[Order Date])
)
```

### Variación Año Anterior (%)
```dax
Var YoY % = 
VAR VentasActual = [Total Ventas]
VAR VentasAnterior = [Ventas YoY]
RETURN
DIVIDE(
    VentasActual - VentasAnterior,
    VentasAnterior,
    0
) * 100
```

### Ventas Mes Anterior
```dax
Ventas MoM = 
CALCULATE(
    [Total Ventas],
    PREVIOUSMONTH(superstore[Order Date])
)
```

### Variación Mes Anterior (%)
```dax
Var MoM % = 
VAR VentasActual = [Total Ventas]
VAR VentasMesAnterior = [Ventas MoM]
RETURN
DIVIDE(
    VentasActual - VentasMesAnterior,
    VentasMesAnterior,
    0
) * 100
```

---

## 🎯 Acumulados

### Ventas YTD (Año a la fecha)
```dax
Ventas YTD = 
TOTALYTD(
    [Total Ventas],
    superstore[Order Date]
)
```

### Ganancias YTD
```dax
Ganancias YTD = 
TOTALYTD(
    [Total Ganancias],
    superstore[Order Date]
)
```

### Ventas Acumuladas
```dax
Ventas Acumuladas = 
CALCULATE(
    [Total Ventas],
    FILTER(
        ALLSELECTED(superstore[Order Date]),
        superstore[Order Date] <= MAX(superstore[Order Date])
    )
)
```

---

## 🏆 Rankings

### Ranking Productos por Ventas
```dax
Rank Producto = 
RANKX(
    ALL(superstore[Product Name]),
    [Total Ventas],
    ,
    DESC,
    DENSE
)
```

### Ranking Categorías por Margen
```dax
Rank Categoria Margen = 
RANKX(
    ALL(superstore[Category]),
    [Margen %],
    ,
    DESC,
    DENSE
)
```

---

## 🔢 Conteos

### Total Clientes
```dax
Total Clientes = DISTINCTCOUNT(superstore[Customer ID])
```

### Total Productos
```dax
Total Productos = DISTINCTCOUNT(superstore[Product ID])
```

### Órdenes con Pérdida
```dax
Órdenes con Pérdida = 
CALCULATE(
    [Total Órdenes],
    superstore[Profit] < 0
)
```

### % Órdenes con Pérdida
```dax
% Órdenes Pérdida = 
DIVIDE(
    [Órdenes con Pérdida],
    [Total Órdenes],
    0
) * 100
```

---

## 🎨 Formato Condicional

### Indicador Margen (para colores)
```dax
Indicador Margen = 
SWITCH(
    TRUE(),
    [Margen %] >= 15, "Alto",
    [Margen %] >= 5, "Medio",
    [Margen %] >= 0, "Bajo",
    "Negativo"
)
```

### Indicador Tendencia
```dax
Indicador Tendencia = 
IF(
    [Var YoY %] > 0,
    "▲ Crecimiento",
    "▼ Decrecimiento"
)
```

---

## 📝 Notas

- Todas las medidas asumen que la tabla principal se llama `superstore`
- La columna de fecha debe llamarse `Order Date`
- Ajustar nombres de columnas según tu dataset si es necesario
