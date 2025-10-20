# 🧠 Convenciones y Nombres
Se definen las convenciones a utilizar en el proyecto

## 🧩 Prefijos por Módulo
Esta tabla resume los prefijos utilizados para identificar componentes clave en el sistema, organizados por módulo. Incluye los prefijos para tablas, procedimientos almacenados (SP), formularios (Form), funciones (FN) y vistas (VW), facilitando la estandarización y el mantenimiento del código.

| 🗂️ Módulo  y otros      | 🔤 Prefijo | 📊 Tabla   | ⚙️ SP         | 🧾 Form | 🧠 Función (FN) | 👁️ Vista (VW) |
|------------------------|-----------|------------|---------------|----------------|------------------|----------------|
| **Mantenimiento**       | `mto`     | `mto`       | `sp_mto`      | `frm_mto`      | `fn_mto`         | `vw_mto`       |
| **Catálogos**           | `ctlg`    | `ctlg`      | `N/A`         | N/A            | `N/A`            | `N/A`          |
| **Inventario**          | `inv`     | `inv`       | `sp_inv`      | `frm_inv`      | `fn_inv`         | `vw_inv`       |
| **Materia Prima**       | `mtp`     | `mtp`       | `sp_mtp`      | `frm_mtp`      | `fn_mtp`         | `vw_mtp`       |
| **Químicos**            | `qmc`     | `qmc`       | `sp_qmc`      | `frm_qmc`      | `fn_qmc`         | `vw_qmc`       |
| **Requerimientos**      | `req`     | `req`       | `sp_req`      | `frm_req`      | `fn_req`         | `vw_req`       |
| **Seguridad**           | `seg`     | `seg`       | `sp_seg`      | `frm_seg`      | `fn_seg`         | `vw_seg`       |
| **Producto Terminado**  | `ptr`     | `ptr`       | `sp_ptr`      | `frm_ptr`      | `fn_ptr`         | `vw_ptr`       |
| **Documentación**       | `doc`     | `doc`       | `sp_doc`      | `frm_doc`      | `fn_doc`         | `vw_doc`       |
| **Reportes**            | `rpt`     | `rpt`       | `rpt`         | `N/A`          | `N/A`            | `N/A`          |
| **Declaración**         | `dcl`     | `dcl`       | `sp_dcl`      | `frm_dcl`      | `fn_dcl`         | `vw_dcl`       |
| **Calidad**             | `cld`     | `cld`       | `sp_cld`      | `frm_cld`      | `fn_cld`         | `vw_cld`       |
| **Bodegas**             | `bdg`     | `bdg`       | `sp_bdg`      | `N/A`          | `N/A`            | `N/A`          | 
| **Unidad de Medida**    | `udm`     | `udm`       | `N/A`         | `N/A`          | `N/A`            | `N/A`          |  
| **Inciso Arancelario**  | `ina`     | `ina`       | `N/A`         | `N/A`          | `N/A`            | `N/A`          |  
| **Tipo Producto**       | `tpd`     | `tpd`       | `N/A`         | `N/A`          | `N/A`            | `N/A`          |  


## 🔑 Tablas, Vistas, SP y funciones
- Nombres `todo` en minúsculas  Ej: `sp_seg_opciones_menu_crud`
- Para SP y FN agregar autor, fecha de creacion, Description (Esto con el fin de documentacion dinámica)
    Ej:  
          <Author: Nombre autor>  
          <Create date: <27/09/2025>  
          <Description: <CRUD de Opciones - Menu>  

## 🎚 Controles
**[ Botones ]**  
Convención: `btn_NombreBoton`  
Ejemplos:  
🟩 `btn_Guardar`  
🟩 `btn_Volver`  
🖍 Con tema: `btn_NombreBotonIn`  
🟦 `btn_GuardarIn`  
🟦 `btn_VolverIn`


**[ TextBox ]**  
Convención: `tbx_CampoOpcionMenu`  
Ejemplos:  
🔲 `tbx_NomUsuarios`  
🔲 `tbx_PasUsuarios`


**[ ComboBox ]**  
Convención: `cbx_CampoOpcionMenu`  
Ejemplos:  
🔽 `cbx_EstUsuarios`  
🔽 `cbx_EstPais`


**[ ListView ]**  
Convención: `lvw_NombreOpcion`  
Ejemplos:  
📋 `lvw_Usuarios`  
📋 `lvw_Pais`


**[ ListBox ]**  
Convención: `lbx_NombreOpcion`  
Ejemplo:  
📦 `lbx_Producto`

---

**[ TabControl ]**  
Convención: `tbc_NombreTabOpcion`  
Ejemplos:  
🗂️ `tbc_MtoMatPrima`  
🗂️ `tbc_LstMatPrima`


**[ Label ]**  
Convención: `lbl_NombreCampo`  
Ejemplos:  
🏷️ `lbl_Nombre`  
🏷️ `lbl_Password`  
🖍 Con tema:  `lbl_NombreCampoIn`  
🏷️ `lbl_PasswordIn`

