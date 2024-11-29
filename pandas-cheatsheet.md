# Pandas 2.1.1 to 2.2.2 Migration Cheat Sheet

## Major New Features

### 1. ADBC Driver Support
- New support for Apache Arrow ADBC drivers in `read_sql` and `to_sql`
- Offers better performance and type support compared to SQLAlchemy
- Example:
```python
import adbc_driver_postgresql.dbapi as pg_dbapi

with pg_dbapi.connect("postgresql://...") as conn:
    df.to_sql("table_name", conn, index=False)
    df2 = pd.read_sql("table_name", conn)
```

### 2. New Series Methods
- `Series.case_when()`: Create Series based on conditions
```python
default = pd.Series('default', index=df.index)
default.case_when([
    (df.a == 1, 'first'),
    (df.b > 5, 'second'),
])
```

### 3. PyArrow Integration
- New `.struct` accessor for PyArrow structured data
```python
series_with_struct.struct.explode()  # Convert to DataFrame
series_with_struct.struct.field("field_name")  # Access field
```
- New `.list` accessor for PyArrow list data
```python
series_with_list.list[0]  # Access first element of each list
```

### 4. Excel Support
- New 'calamine' engine for `read_excel`
- Up to 5x faster than 'openpyxl'
- Supports .xlsx, .xlsm, .xls, .xlsb, and .ods files
```python
pd.read_excel("file.xlsb", engine="calamine")
```

## Improved Features

### 1. to_numpy() Enhancement
- Better dtype conversion for nullable and Arrow types
```python
# Old: ser.to_numpy() -> array([1, 2, 3], dtype=object)
# New: ser.to_numpy() -> array([1, 2, 3], dtype=int64)
```

### 2. DataFrame Operations
- `apply()` now supports Numba for potential speedups
```python
df.apply(func, engine="numba")
```
- Enhanced `interpolate()` support for ArrowDtype and masked dtypes
- Improved `value_counts()` for masked types

### 3. String and Date Operations
- `Series.str.extract()` now works with ArrowDtype
- Better datetime support in `.dt` accessor for PyArrow duration types

## Compatibility Notes

### NumPy 2.0 Support (as of 2.2.2)
- First version compatible with NumPy 2.0
- Works with both NumPy 1.x and 2.x
- Caveat: NumPy 2.0's StringDtype converts to object dtype in pandas
- Full StringDtype support expected in pandas 3.0

## Deprecated Features

- Reverted deprecation of `fill_method=None` in `pct_change()`
- Values 'backfill', 'bfill', 'pad', and 'ffill' remain deprecated

## Tips for Migration

1. Use ADBC drivers instead of SQLAlchemy when possible for better performance
2. Consider using `dtype_backend="pyarrow"` for better type preservation
3. Try the new 'calamine' engine for faster Excel file processing
4. Take advantage of the new `case_when()` for conditional operations
5. Use struct and list accessors when working with PyArrow data types