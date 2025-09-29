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

  ### 🧩 Guía Estructural Secuencial para Formularios de Mantenimiento

  Esta plantilla define el orden lógico y técnico que deben seguir los formularios tipo mantenimiento (frm_[Modulo]_[Entidad]), como usuarios, perfiles, menú, etc.

  #### ▸ Definición de clase

    public partial class frm_[Modulo]_[Entidad] : Form
    - Declara conexión a BD → ConexionDB cn
    - Define modo de acción → string modoAccion = "" ("Nuevo" / "Editar")

  #### ▸ Constructor del formulario

    public frm_[Modulo]_[Entidad]()
    - Ejecuta InitializeComponent()
    - Asocia evento Load → frm_[Modulo]_[Entidad]_Load
    - Instancia conexión → cn = new ConexionDB()

  #### ▸ Evento Load

    private void frm_[Modulo]_[Entidad]_Load(object sender, EventArgs e)
    - Carga el tema desde archivo JSON
        ThemeManager tema = ThemeLoader.CargarDesdeJson(rutaTema);
        tema.Aplicar(this);

    - Aplica estilo visual a todos los LabelIn del formulario
      (color, fuente, renderizado compatible)

  #### ▸ Define los CardControl

    Card 1: Listado
    - Crea CardControl card1 con título "Listado"
    - Busca y referencia ListView lvw_[Entidad]
    - Carga datos desde SP → cn.Cargar[Entidad]EnLV(lvw_[Entidad])
    - Aplica estilo de encabezado → tema.AplicarEstiloEncabezadoListView(lvw_[Entidad])
    - Asocia eventos visuales (Invalidate() en hover, focus, selección)

    Card 2: Mantenimiento

    - Crea CardControl card2 con título "Mantenimiento"
    - Busca y referencia Panel pnl_[Modulo]_[Entidad]
    - Establece contenedor visual → card2.EstablecerContenedor(pnl...)
    - Aplica tema visual → card2.AplicarTema(tema)

  #### ▸ Agrega los CardControl al formulario

    this.Controls.Add(card1);
    this.Controls.Add(card2);

  #### ▸ Inicializa estado visual

    desactivarCampos();
    - Deshabilita campos de entrada y oculta botón de guardar

  #### ▸ Métodos de control de estado

    activarCampos()
    desactivarCampos()
    LimpiarCampos()

    - Activan/desactivan campos según modo (Nuevo / Editar)
    - Limpian contenido de los controles visuales

  #### ▸ Eventos de acción

    pbx_Nuevo_Click()
    - Establece modo "Nuevo"
    - Activa campos y limpia contenido
    - Muestra botón de guardar

    pbx_Editar_Click()
    - Verifica selección en ListView
    - Establece modo "Editar"
    - Activa campos y muestra botón de guardar

    btn_GuardarIn_Click()
    - Verifica modo (Nuevo / Editar)
    - Cifra contraseña si aplica
    - Ejecuta SP → Agregar[Entidad] o Actualizar[Entidad]
    - Recarga ListView, resetea estado visual

    btn_Volver_Click()
    - Cierra el formulario

  #### ▸ Evento de selección en ListView

    lvw_[Entidad]_SelectedIndexChanged()
    - Verifica selección
    - Ejecuta SP → CargarDatos[Entidad]
    - Carga datos en los controles del panel

  #### 🎯 Convenciones de nombres por tipo de control

  TextBox  :    `tbx_Nom[Entidad], tbx_Pas[Entidad], tbx_Per[Entidad]`  
  ComboBox :    `cbx_Est[Entidad]`  
  Button  : `btn_GuardarIn[Entidad], btn_Volver[Entidad]`  
  Label  : `lbl_Nombre[Entidad], lbl_PasswordIn[Entidad]`  
  ListView  : `lvw_[Entidad]`  
  Panel  : `pnl_[Modulo]_[Entidad]`  
  PictureBox  : `pbx_Nuevo[Entidad], pbx_Editar[Entidad]`  
  
  ---

  ## 📚 Definiciones
      
  ### 📱 Formularios
  **Size - (Max)**  :`1160; 600`   
  **Size - (Min)**  :`1280; 700`  
  **BackColor**     : `{Controlado por Json}`  
  **FormBorderStyle**: `None`  
  **ControlBox**: `False`  
  **StartPosition**: `CenterScreen`  
  
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
