# 📘 Diccionario de Datos

Este documento describe las estructuras de datos utilizadas en el sistema, incluyendo tablas, columnas, tipos de datos, restricciones y procedimientos almacenados.

---

## 🗂️ Tablas y Columnas

### 🔹 Tabla: emp_Departamento

| Columna                | Tipo     | Longitud | Nulo | Descripción |
|------------------------|----------|----------|------|-------------|
| id_departamento        | int      | 4        | ❌   |             |
| nombre_departamento    | varchar  | 250      | ✅   |             |
| nombre_unidad_seccion  | varchar  | 250      | ✅   |             |
| activo                 | char     | 1        | ✅   |             |
| fecha_registro         | datetime | 8        | ✅   |             |
| fecha_actualiza        | datetime | 8        | ✅   |             |
| id_usuario_ingreso     | int      | 4        | ✅   |             |
| id_usuario_actualiza   | int      | 4        | ✅   |             |

---

### 🔹 Tabla: emp_puesto

| Columna                | Tipo     | Longitud | Nulo | Descripción |
|------------------------|----------|----------|------|-------------|
| id_puesto              | int      | 4        | ❌   |             |
| nombre_puesto          | varchar  | 100      | ✅   |             |
| activo                 | char     | 1        | ✅   |             |
| fecha_registro         | datetime | 8        | ✅   |             |
| fecha_actualiza        | datetime | 8        | ✅   |             |
| id_usuario_ingreso     | int      | 4        | ✅   |             |
| id_usuario_actualiza   | int      | 4        | ✅   |             |

---

### 🔹 Tabla: seg_menu_perfil

| Columna                | Tipo     | Longitud | Nulo | Descripción |
|------------------------|----------|----------|------|-------------|
| id_menu_perfil         | int      | 4        | ❌   |             |
| id_perfil              | int      | 4        | ✅   |             |
| id_menu                | int      | 4        | ✅   |             |
| nuevo                  | char     | 1        | ✅   |             |
| editar                 | char     | 1        | ✅   |             |
| eliminar               | char     | 1        | ✅   |             |
| imprimir               | char     | 1        | ✅   |             |
| consultar              | char     | 1        | ✅   |             |
| fecha_ingr             | datetime | 8        | ✅   |             |
| id_usuario_ingr        | int      | 4        | ✅   |             |
| activo                 | char     | 1        | ✅   |             |
| fecha_registro         | datetime | 8        | ✅   |             |
| fecha_actualiza        | datetime | 8        | ✅   |             |
| id_usuario_ingreso     | int      | 4        | ✅   |             |
| id_usuario_actualiza   | int      | 4        | ✅   |             |

---

### 🔹 Tabla: seg_usuarios

| Columna                | Tipo     | Longitud | Nulo | Descripción |
|------------------------|----------|----------|------|-------------|
| id_usuario             | int      | 4        | ❌   |             |
| usr_login              | varchar  | 50       | ✅   |             |
| usr_password           | varchar  | 50       | ✅   |             |
| usr_nombres            | varchar  | 100      | ✅   |             |
| usr_apellidos          | varchar  | 100      | ✅   |             |
| usr_Correo             | varchar  | 100      | ✅   |             |
| id_departamento        | int      | 4        | ✅   |             |
| id_puesto              | int      | 4        | ✅   |             |
| fecha_registro         | datetime | 8        | ✅   |             |
| fecha_actualiza        | datetime | 8        | ✅   |             |
| id_usuario_ingreso     | int      | 4        | ✅   |             |
| id_usuario_actualiza   | int      | 4        | ✅   |             |
| imagen_firma           | varchar  | 250      | ✅   |             |
| ruta_Icono             | varchar  | 250      | ✅   |             |
| Nombre_de_icono        | varchar  | 250      | ✅   |             |

---

## ⚙️ Procedimientos Almacenados

### sp_seg_cargar_perfil

Parámetros:
- @ID_SISTEMA int(4)
- @ID_OPCION int(4)
- @LOGIN varchar(50)
- @ACCION int(4)

---

### sp_seg_perfil_usuario

Parámetros:
- @ID_SISTEMA int(4)
- @LOGIN varchar(50)
- @ACCION int(4)

---

### sp_seg_Usuarios_CRUD

Parámetros:
- @Accion int(4)
- @id_usuario int(4)
- @usr_id_anterior char(4)
- (otros parámetros según operación)

---

### sp_sel_seg_Perfil

Carga de perfiles

---

### sp_sel_seg_Usuarios

Carga de usuarios

---

## 🧠 Convenciones Visuales

- ❌ → No permite nulo  
- ✅ → Permite nulo  
- Tablas agrupadas por módulo (`emp_`, `seg_`, etc.)  
- Auditoría estándar: `fecha_registro`, `fecha_actualiza`, `id_usuario_ingreso`, `id_usuario_actualiza`
