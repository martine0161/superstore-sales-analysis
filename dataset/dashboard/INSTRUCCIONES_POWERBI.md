# 🎨 Guía de Creación del Dashboard en Power BI

## Paso 1: Cargar los datos

1. Abrir Power BI Desktop
2. Ir a **Inicio > Obtener datos > Texto/CSV**
3. Seleccionar `data/superstore_clean.csv`
4. Click en **Cargar**

---

## Paso 2: Verificar tipos de datos

En la vista **Modelo** o **Transformar datos**, verificar:

| Columna | Tipo |
|---------|------|
| Order Date | Fecha |
| Ship Date | Fecha |
| Sales | Número decimal |
| Profit | Número decimal |
| Quantity | Número entero |
| Discount | Número decimal |
| Year | Número entero |
| Month | Número entero |

---

## Paso 3: Crear medidas DAX

Ir a **Modelado > Nueva medida** y crear las medidas del archivo `medidas_dax.md`.

Medidas mínimas necesarias:
- Total Ventas
- Total Ganancias
- Margen %
- Total Órdenes

---

## Paso 4: Diseño del Dashboard

### Layout recomendado:

```
┌─────────────────────────────────────────────────────────────┐
│  TÍTULO: Análisis de Ventas - Superstore                   │
├─────────────┬─────────────┬─────────────┬─────────────┬─────┤
│   Ventas    │  Ganancias  │   Margen    │   Órdenes   │     │
│   $2.3M     │    $286K    │   12.5%     │    5,009    │     │
├─────────────┴─────────────┴─────────────┴─────────────┴─────┤
│                                                             │
│  [Gráfico de Líneas: Ventas por Mes/Año]                   │
│                                                             │
├──────────────────────────────┬──────────────────────────────┤
│                              │                              │
│  [Barras: Ventas x Categoría]│  [Mapa: Ventas x Estado]    │
│                              │                              │
├──────────────────────────────┼──────────────────────────────┤
│                              │                              │
│  [Donut: Ventas x Segmento]  │  [Tabla: Top 10 Productos]  │
│                              │                              │
├──────────────────────────────┴──────────────────────────────┤
│  FILTROS: [Año ▼] [Región ▼] [Categoría ▼]                 │
└─────────────────────────────────────────────────────────────┘
```

---

## Paso 5: Crear visualizaciones

### 5.1 Tarjetas KPI (4 tarjetas en la parte superior)

**Tarjeta 1 - Ventas:**
- Visualización: Tarjeta
- Campo: [Total Ventas]
- Formato: Moneda, 1 decimal

**Tarjeta 2 - Ganancias:**
- Visualización: Tarjeta
- Campo: [Total Ganancias]
- Formato: Moneda, 1 decimal

**Tarjeta 3 - Margen:**
- Visualización: Tarjeta
- Campo: [Margen %]
- Formato: Porcentaje, 1 decimal

**Tarjeta 4 - Órdenes:**
- Visualización: Tarjeta
- Campo: [Total Órdenes]
- Formato: Número entero con separador de miles

---

### 5.2 Gráfico de Líneas (Tendencia)

- Visualización: Gráfico de líneas
- Eje X: Order Date (nivel Mes o Año-Mes)
- Eje Y: [Total Ventas]
- Leyenda: Year (opcional, para comparar años)

---

### 5.3 Gráfico de Barras (Categorías)

- Visualización: Gráfico de barras agrupadas
- Eje Y: Category
- Eje X: [Total Ventas]
- Ordenar por: Total Ventas descendente
- Colores: Usar paleta consistente

---

### 5.4 Mapa (Ventas por Estado)

- Visualización: Mapa o Mapa coroplético
- Ubicación: State
- Tamaño/Color: [Total Ventas]
- Tooltip: State, [Total Ventas], [Margen %]

---

### 5.5 Gráfico de Dona (Segmentos)

- Visualización: Gráfico de anillos
- Leyenda: Segment
- Valores: [Total Ventas]
- Etiquetas: Mostrar porcentaje

---

### 5.6 Tabla Top Productos

- Visualización: Tabla
- Columnas: Product Name, [Total Ventas], [Total Ganancias], [Margen %]
- Filtro Top N: Top 10 por [Total Ventas]

---

## Paso 6: Agregar filtros (Slicers)

1. **Filtro de Año:**
   - Visualización: Segmentación
   - Campo: Year
   - Estilo: Lista o Dropdown

2. **Filtro de Región:**
   - Visualización: Segmentación
   - Campo: Region
   - Estilo: Lista o Botones

3. **Filtro de Categoría:**
   - Visualización: Segmentación
   - Campo: Category
   - Estilo: Botones

---

## Paso 7: Formato y estilo

### Colores recomendados:
- Primario: #1A365D (azul oscuro)
- Secundario: #2B6CB0 (azul medio)
- Acento: #48BB78 (verde para positivo)
- Alerta: #E53E3E (rojo para negativo)
- Fondo: #F7FAFC (gris muy claro)

### Tipografía:
- Títulos: Segoe UI Semibold, 14-16pt
- Datos: Segoe UI, 10-12pt
- KPIs: Segoe UI Bold, 24-28pt

### Tips de formato:
- Usar bordes sutiles entre secciones
- Agregar título en la parte superior
- Incluir fecha de actualización
- Mantener espaciado consistente

---

## Paso 8: Guardar y exportar

1. Guardar como: `superstore_dashboard.pbix`
2. Exportar imagen para GitHub:
   - Archivo > Exportar > Exportar a PDF
   - O usar Snipping Tool para captura PNG

---

## Checklist final

- [ ] Todas las tarjetas KPI funcionan
- [ ] Gráfico de líneas muestra tendencia correcta
- [ ] Mapa muestra todos los estados
- [ ] Filtros afectan todas las visualizaciones
- [ ] Colores son consistentes
- [ ] No hay errores en medidas DAX
- [ ] Tooltips muestran información útil
- [ ] Dashboard se ve bien en pantalla completa
