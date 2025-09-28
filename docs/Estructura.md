# Estructura  y Definiciones Generales
---
  ## 🧬 Estructura
  ### 🧩 Estructura Base de Formulario de Mantenimiento

  **Formulario**: `frm_[NombreFormulario]`  
  **Tipo**: Mantenimiento de [Entidad]  
  **Componentes principales**:
  - `CardControl` → Listado (`lvw_[Entidad]`) + Mantenimiento (`pnl_[NombreFormulario]`)
  - `ListView` → carga dinámica desde SP (`Cargar[Entidad]EnLV`)
  - `Panel` → contiene controles visuales (`TextBox`, `ComboBox`, `Buttons`)
  - `ThemeManager` → aplica estilos desde `tema.json`
  - `ModoAccion` → `"Nuevo"` / `"Editar"` para controlar flujo
  - `Botones`: `pbx_Nuevo`, `pbx_Editar`, `btn_GuardarIn`, `btn_Volver`
  - `SPs`: `Agregar[Entidad]`, `Actualizar[Entidad]`, `CargarDatos[Entidad]`

  **Funciones clave**:
  - `activarCampos()` / `desactivarCampos()` → control de edición
  - `LimpiarCampos()` → reset visual
  - `btn_GuardarIn_Click()` → lógica de inserción/actualización
  - `lvw_[Entidad]_SelectedIndexChanged()` → carga de datos al seleccionar

  ### 🎯 Convenciones de nombres por tipo de control

  **TextBox**  
  `tbx_Nom[NombreFormulario]`  
  `tbx_Pas[NombreFormulario]`  
  `tbx_Per[NombreFormulario]`
  
  **ComboBox**  
  `cbx_Est[NombreFormulario]`  
  `cbx_Tipo[NombreFormulario]`
  
  **Button**  
  `btn_GuardarIn[NombreFormulario]`  
  `btn_Volver[NombreFormulario]`
  **Label**  
  
  `lbl_Nombre[NombreFormulario]`  
  `lbl_PasswordIn[NombreFormulario]`
  **ListView**
  `lvw_[Entidad]`
  
  **Panel**  
  `pnl_[NombreFormulario]`
  
  **PictureBox**  
  `pbx_Nuevo[NombreFormulario]`  
  `pbx_Editar[NombreFormulario]`

  ## 📚 Definiciones
      
  ### 📱 Formularios
  **Size - (Max)**  :`1160; 600`   
  **Size - (Min)**  :`1280; 700`  
  **BackColor**     : `{Controlado por Json}`
  ### 🎚 Controles - `Exclusiones en Json`
  #### 🔖 Título - `Label`  
  **Name**: `lbl_Titulo`  
  **Posición**: `560, 1`
  
  #### ↩️ Volver   - `Button`
  **Name**: `btn_Volver`  
  **Posición**: `990, 510`  
  **Size**: `106, 39`  
  **BackColor**: `RGB(253, 184, 18)`  
  **ForeColor**: `White`  
  **FlatStyle**: `Flat`
  
  **FlatAppearance**  
   ***BorderColor**: `RGB(85, 159, 127)`  
   ***BorderSize**: `1`  
   ***MouseDownBackColor**: `RGB(20, 20, 20)`  
   ***MouseOverBackColor**: `Red`

  #### ➕ Nuevo   - `PictureBox`
  **Name**: `pbx_Nuevo`  
  **Posición**: `990, 90`  
  **Tamaño**: `30,30`  
  
  #### 📝 Editar   - `PictureBox`
  **Name**: `pbx_Editar`  
  **Posición**: `1040; 90`  
  **Tamaño**: `30,30`  
  
  .........................
  
  ### 🎚 Controles - 🖍 `Con Tema`
  #### 🧾 Listado - `ListView`
  **Name**: `lvw_Nombreform`  
  **Posición**: `1040; 90`  
  **Size**: `536, 304` 
 
  #### 💾 Guardar   - `Button`
  **Name**: `btn_Volver`  
  **Posición**: `990, 510`  
  **Size**: `106, 39`  
  **BackColor**: `RGB(253, 184, 18)`  
  **ForeColor**: `White`  
  **FlatStyle**: `Flat`
  
  **FlatAppearance**  
   ***BorderColor**: `RGB(85, 159, 127)`  
   ***BorderSize**: `1`  
   ***MouseDownBackColor**: `RGB(20, 20, 20)`  
   ***MouseOverBackColor**: `Red`
