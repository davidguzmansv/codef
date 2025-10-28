# 🧰 Diagrama del Proyecto

Este documento describe la estructura completa del proyecto desarrollado en **C# (Windows Forms)**.
Su objetivo es documentar la arquitectura general, carpetas, clases y módulos del sistema para facilitar la comprensión, mantenimiento y colaboración.

---

## 📁 Estructura General

```
Controlador/      Contiene la lógica de negocio, clases de seguridad y conexión con la base de datos. 
├─ Parser/        Encargado de interpretar y procesar los archivos **SAD
│  ├─ SADParserBinario.cs        → Procesa archivos SAD en formato binario.
│  ├─ SADParserFactory.cs        → Implementa el patrón *Factory* para instanciar parsers según el tipo de archivo.
│  ├─ SADParserFormalizacion.cs  → Maneja la formalización y validación de datos del documento SAD.
├─ Administracion.cs
├─ ButtonRounder.cs              → Personalización visual de formularios y botones.
├─ cls_Seg_Encriptamiento.cs     → Cifrado y descifrado de contrasenas.
├─ ConexionDB.cs                 → Gestiona la conexión y operaciones con la base de datos.
├─ FormRounder.cs                → Personalización visual de formularios y botones.
├─ IFormSeg.cs
├─ IntegracionParserSAD.cs       → Integra los resultados del parser con otros módulos del sistema.
├─ ListItemConId.cs
├─ OpcionItem.cs
├─ OpcionMenu.cs
├─ PerfilItem.cs
├─ seg_opciones_menu.cs          → Control de usuarios, roles y permisos.
└─ seg_usuarios.cs               → Control de usuarios, roles y permisos.

Css/              Contiene las clases de diseño visual, efectos y temas aplicables a la interfaz WinForms.
├─ AjustarConMargen.cs
├─ CardControl.cs                → Control visual estilo *card*.
├─ ClickEffect.cs                → Efectos visuales en botones o controles.
├─ ColorearTabs.cs               → Manejo de color dinámico en pestañas.
├─ estilosMenus.cs
├─ GridLayout.cs                 → Configuración y disposición de elementos visuales.
├─ ListViewIn.cs                 → Configuración y disposición de elementos visuales.
├─ MenuThemeConfig.cs
├─ ThemeConfig.cs                → Sistema de tematización completo.
├─ ThemeLoader.cs                → Sistema de tematización completo.
└─ ThemeManager.cs               → Sistema de tematización completo.

Modelos/          Contiene los modelos de datos del sistema, estructurados según las entidades pales de la appl aduanera.
├─ Parser/        Define las clases de mapeo de los documentos de declaración.
│  ├─ DeclaracionAduanera.cs     → Modelo principal de la declaración.
│  ├─ Impuesto.cs                → Estructura de impuestos asociados.
│  ├─ InfoDeclaracion.cs         → Información general de la declaración.   
│  ├─ InfoFactura.cs             → Datos de facturas de importación/exportación.
│  └─ ItemDeclaracion.cs         → Detalle de los ítems incluidos en la declaración.

Modulos/           Contiene las distintas áreas funcionales de la aplicación.
├─ Calidad/        Controles de calidad dentro del flujo de importación/exportación.
├─ Declaracion/    Manejo de declaraciones aduaneras y documentación relacionada.
├─ Documentacion/  Incluye formularios y herramientas internas para documentación.
│  └─ frm_Doc_Diccionario.cs     → Módulo de diccionario de datos/documentos.
├─ Inicio/         Contiene el flujo principal de autenticación y menús de acceso.
│  ├─ frm_Seg_Menu.cs            → Formulario principal de menú de seguridad.
│  ├─ GlobalesAplicacion.cs      → Variables y configuraciones globales.
│  ├─ Login.n.cs                 → Formulario de inicio de sesión.
│  └─ Menu.cs                    → Control de menú principal.
├─ Inventario/     Administración de inventarios, existencias y control de materiales.
├─ Mantenimiento/  Contiene formularios para gestión de catalogos
│  ├─ frm_Mto_MatPrima.cs        → Mantenimiento de materias primas.
│  ├─ frm_Mto_Motoristas.cs      → Mantenimiento de motoristas y transporte.
│  ├─ frm_Mto_Pais.cs            → Catálogo de países.
│  ├─ frm_Mto_Proveedores.cs     → Gestión de proveedores.
│  ├─ frm_Mto_TipProducto.cs     → Tipos de productos y categorías.
│  └─ FrmBase.cs                 → Clase base reutilizable para formularios.
├─ MateriaPrima/
├─ Quimicos/
├─ Reportes/        Generación de reportes
├─ Requerimientos/
├─ Seguridad/       Contiene todos los formularios relacionados con control de acceso, roles y usuarios.
│  ├─ frm_Seg_MenuPerfil.cs      → Administración de perfiles de menú.
│  ├─ frm_Seg_OpcionesMenu.cs    → Configuración de opciones por menú.
│  ├─ frm_Seg_Perfil.cs          → Gestión de perfiles.
│  ├─ frm_Seg_PerfilUsuario.cs   → Asignación de usuarios a perfiles.
│  └─ frm_Seg_Usuarios.cs        → Administración general de usuarios.
├─ Terminado/

Plantillas/
Recursos/           Carpetas destinadas a contener elementos de apoyo visual y configuraciones:
├─ Iconos/
├─ Imagenes/
├─ Logos/
Resources/
Scripts/
└─ tema.json

Archivos raíz:
├─ App.config
├─ Form1.cs
├─ packages.config
└─ Program.cs
```

---

## 🧩 Descripción de Carpetas y Módulos

### 🔹 Controlador/
Contiene la lógica de negocio y control del flujo del sistema.  
Incluye clases de seguridad, manejo de formularios y conexión con la base de datos.

#### Subcarpeta `Parser/`
Módulo encargado de interpretar y procesar los archivos **SAD (Single Administrative Document)** en distintos formatos.
- **SADParserBinario.cs** → Procesa archivos SAD en formato binario.
- **SADParserFactory.cs** → Implementa el patrón *Factory* para instanciar parsers según el tipo de archivo.
- **SADParserFormalizacion.cs** → Maneja la formalización y validación de datos del documento SAD.

Otros controladores relevantes:
- **ConexionDB.cs** → Gestiona la conexión y operaciones con la base de datos.
- **cls_Seg_Encriptamiento.cs** → Cifrado y descifrado de información sensible.
- **FormRounder.cs / ButtonRounder.cs** → Personalización visual de formularios y botones.
- **IntegracionParserSAD.cs** → Integra los resultados del parser con otros módulos del sistema.
- **seg_usuarios.cs / seg_opciones_menu.cs** → Control de usuarios, roles y permisos.

---

### 🔹 Css/
Contiene las clases de diseño visual, efectos y temas aplicables a la interfaz WinForms.
- **CardControl.cs** → Control visual estilo *card*.
- **ClickEffect.cs** → Efectos visuales en botones o controles.
- **ColorearTabs.cs** → Manejo de color dinámico en pestañas.
- **ThemeManager.cs / ThemeLoader.cs / ThemeConfig.cs** → Sistema de tematización completo.
- **GridLayout.cs / ListViewIn.cs** → Configuración y disposición de elementos visuales.

---

### 🔹 Modelos/
Contiene los modelos de datos del sistema, estructurados según las entidades principales de la aplicación aduanera.

#### Subcarpeta `Parser/`
Define las clases de mapeo de los documentos de declaración.
- **DeclaracionAduanera.cs** → Modelo principal de la declaración.
- **Impuesto.cs** → Estructura de impuestos asociados.
- **InfoDeclaracion.cs** → Información general de la declaración.
- **InfoFactura.cs** → Datos de facturas de importación/exportación.
- **ItemDeclaracion.cs** → Detalle de los ítems incluidos en la declaración.

---

### 🔹 Modulos/
Contiene las distintas áreas funcionales de la aplicación.

#### Calidad/
Gestión de procesos y controles de calidad dentro del flujo de importación/exportación.

#### Declaracion/
Manejo de declaraciones aduaneras y documentación relacionada.

#### Documentacion/
Incluye formularios y herramientas internas para documentación.
- **frm_Doc_Diccionario.cs** → Módulo de diccionario de datos/documentos.

#### Inicio/
Contiene el flujo principal de autenticación y menús de acceso.
- **frm_Seg_Menu.cs** → Formulario principal de menú de seguridad.
- **GlobalesAplicacion.cs** → Variables y configuraciones globales.
- **Login.n.cs** → Formulario de inicio de sesión.
- **Menu.cs** → Control de menú principal.

#### Inventario/
Administración de inventarios, existencias y control de materiales.

#### Mantenimiento/
Agrupa formularios para gestión de entidades maestras.
- **frm_Mto_MatPrima.cs** → Mantenimiento de materias primas.
- **frm_Mto_Motoristas.cs** → Mantenimiento de motoristas y transporte.
- **frm_Mto_Pais.cs** → Catálogo de países.
- **frm_Mto_Proveedores.cs** → Gestión de proveedores.
- **frm_Mto_TipProducto.cs** → Tipos de productos y categorías.
- **FrmBase.cs** → Clase base reutilizable para formularios.

#### Seguridad/
Contiene todos los formularios relacionados con control de acceso, roles y usuarios.
- **frm_Seg_MenuPerfil.cs** → Administración de perfiles de menú.
- **frm_Seg_OpcionesMenu.cs** → Configuración de opciones por menú.
- **frm_Seg_Perfil.cs** → Gestión de perfiles.
- **frm_Seg_PerfilUsuario.cs** → Asignación de usuarios a perfiles.
- **frm_Seg_Usuarios.cs** → Administración general de usuarios.

#### Reportes / Requerimientos / Terminado
Módulos reservados para la generación de reportes, requisitos del sistema y flujo de procesos terminados.

---

### 🔹 Recursos, Resources y Scripts
Carpetas destinadas a contener elementos de apoyo visual y configuraciones:
- **Recursos/Iconos**, **Recursos/Imagenes**, **Recursos/Logos** → Recursos gráficos.
- **Resources/** → Recursos internos de compilación.
- **Scripts/tema.json** → Archivo de configuración de tema visual y estilos.

---

### 🔹 Archivos raíz
Configuraciones base del proyecto:
- **App.config** → Configuración de conexión, dependencias y entorno.
- **Form1.cs** → Formulario principal o inicial del proyecto.
- **packages.config** → Paquetes NuGet utilizados.
- **Program.cs** → Punto de entrada principal del programa (Main).

---

## 📘 Notas finales
- Proyecto basado en **WinForms C#**.
- Arquitectura modular con separación de lógica, datos y presentación.
- Uso de clases personalizadas para UI moderna y adaptable.
- Integración con parser SAD para gestión aduanera automatizada.

---

