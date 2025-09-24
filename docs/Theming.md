# 🎨 Sistema de Tematización Dinámica para WinForms

Este sistema permite aplicar estilos visuales a formularios y controles de forma jerárquica, modular y automatizada, utilizando un archivo JSON externo (`tema.json`) como fuente de configuración.

---

## 📁 Estructura de Archivos
    /Theming
    │
    ├── Scripts/
    │   └── tema.json               # Archivo de configuración visual
    │
    ├── CssThemeConfig.cs           # Clase que representa el modelo del JSON
    ├── ThemeManager.cs             # Aplica estilos a formularios y controles
    ├── ThemeLoader.cs              # Carga y parsea el JSON
    │
    ├── Forms/
    │   └── frm_Seg_Menu.cs         # Formulario con menú dinámico y tema aplicado

---

## 🧠 Convenciones

- **Sufijo `In`**: Indica que el control debe recibir estilo automatizado.
- **Herencia visual**: Los estilos se aplican desde el contenedor hacia los hijos.
- **Controles excluidos**: Se definen en `ControlesExcluidos` para evitar aplicarles tema.
- **Configuración externa**: El archivo `tema.json` permite modificar estilos sin recompilar.

---

## 🧩 Componentes Clave

### `tema.json`
#### Archivo de configuración visual con colores, fuentes y estilos para cada tipo de control.

```json
{
  "FondoFormulario": "#F0F7FF",
  "FondoControl": "#F0F7FF",
  "FondoControlIn": "#1b2a49",
  "FondoButtonIn": "#007ACC",
  "ForeColorButtonIn": "#FFFFFF",
  "FondoComboBoxIn": "#F0F7FF",
  "ForeColorComboBoxIn": "#000000",
  "FondoTabControlIn": "#E8F0FF",
  "ForeColorTabControlIn": "#000000",
  "ColorFondoControlesLabel": "#1b2a49",
  "ColorTextoControlesLabel": "#FFFFFF",
  "ControlesExcluidos": ["btn_Volver"],
  "ListViewInBackColor": "#F0F7FF",
  "ForeColor": "#000000",
  "FuenteTituloForm": {
    "Nombre": "Century Gothic",
    "Tamaño": 18,
    "Estilo": "Bold"
  },
  "FuenteControles": {
    "Nombre": "Century Gothic",
    "Tamaño": 12,
    "Estilo": "Regular"
  },
  "FuenteControlesIn": {
    "Nombre": "Century Gothic",
    "Tamaño": 10,
    "Estilo": "Regular"
  },
  "EstilosMenu": {
    "FondoMenu": "#1B2A49",
    "FondoHover": "#3A506B",
    "FondoDropDown": "#0B132B",
    "ColorTexto": "#FFFFFF",
    "ColorTextoHover": "#F4D35E",
    "ColorBorde": "#5BC0BE",
    "FuenteMenu": {
      "Nombre": "Segoe UI",
      "Tamaño": 14,
      "Estilo": "Regular"
    },
    "FuenteMenuHover": {
      "Nombre": "Segoe UI",
      "Tamaño": 14,
      "Estilo": "Bold"
    }
  },
  "Form": {
    "BackColor": "#FFFFFF",
    "ForeColor": "#000000"
  },
  "Panel": {
    "BackColor": "#F5F5F5"
  },
  "PanelIn": {
    "BackColor": "#E8F0FF"
  },
  "ListView": {
    "BackColor": "#FFFFFF",
    "ForeColor": "#000000"
  },
  "ListViewIn": {
    "BackColor": "#F0F7FF",
    "ForeColor": "#000000",
    "HeaderBackColor": "#1E3C5A",
    "HeaderForeColor": "#FFFFFF"
  },
  "Label": {
    "ForeColor": "#333333"
  },
  "Button": {
    "BackColor": "#007ACC",
    "ForeColor": "#FFFFFF"
  }
}
```


### `CssThemeConfig.cs`
#### Clase que representa el modelo del JSON.
    
```csharp
    public class CssThemeConfig
    {
      public string FondoFormulario { get; set; }
      public string FondoControl { get; set; }
      public string FondoControlIn { get; set; }
      public string ForeColor { get; set; }

      public string FondoButtonIn { get; set; } = "#007ACC";
      public string ForeColorButtonIn { get; set; } = "#FFFFFF";
      public string FondoComboBoxIn { get; set; } = "#F0F7FF";
      public string ForeColorComboBoxIn { get; set; } = "#000000";
      public string FondoTabControlIn { get; set; } = "#E8F0FF";
      public string ForeColorTabControlIn { get; set; } = "#000000";

      public Fuente FuenteTituloForm { get; set; }
      public Fuente FuenteControles { get; set; }
      public Fuente FuenteControlesIn { get; set; }

      public MenuThemeConfig EstilosMenu { get; set; }

      public string FondoListViewIn { get; set; } = "#F0F7FF";
      public string EncabezadoListViewInBackColor { get; set; } = "#1E3C5A";
      public string EncabezadoListViewInForeColor { get; set; } = "#FFFFFF";

      public List<string> ControlesExcluidos { get; set; } = new List<string>();

      public class Fuente
      {
        public string Nombre { get; set; }
        public float Tamaño { get; set; }
        public string Estilo { get; set; }
      }
    }
```

### `ThemeLoader.cs`
#### Carga el JSON y lo convierte en una instancia de ThemeManager.
```csharp
public static class ThemeLoader
{
    public static ThemeManager CargarDesdeJson(string ruta)
    {
        if (!File.Exists(ruta))
            throw new FileNotFoundException("No se encontró el archivo de tema.", ruta);

        string json = File.ReadAllText(ruta);
        var config = JsonSerializer.Deserialize<CssThemeConfig>(json, new JsonSerializerOptions
        {
            PropertyNameCaseInsensitive = true
        });

        Enum.TryParse(config.FuenteTituloForm.Estilo, true, out FontStyle estiloTitulo);
        Enum.TryParse(config.FuenteControles.Estilo, true, out FontStyle estiloControles);
        Enum.TryParse(config.FuenteControlesIn.Estilo, true, out FontStyle estiloControlesIn);

        return new ThemeManager
        {
            FondoFormulario = ColorTranslator.FromHtml(config.FondoFormulario),
            FondoControl = ColorTranslator.FromHtml(config.FondoControl),
            FondoControlesIn = ColorTranslator.FromHtml(config.FondoControlIn),
            FondoListViewIn = ColorTranslator.FromHtml(config.FondoListViewIn),
            EncabezadoListViewInBackColor = ColorTranslator.FromHtml(config.EncabezadoListViewInBackColor),
            EncabezadoListViewInForeColor = ColorTranslator.FromHtml(config.EncabezadoListViewInForeColor),
            ForeColor = ColorTranslator.FromHtml(config.ForeColor),
            FuenteTituloForm = new Font(config.FuenteTituloForm.Nombre, config.FuenteTituloForm.Tamaño, estiloTitulo),
            FuenteControles = new Font(config.FuenteControles.Nombre, config.FuenteControles.Tamaño, estiloControles),
            FuenteControlesIn = new Font(config.FuenteControlesIn.Nombre, config.FuenteControlesIn.Tamaño, estiloControlesIn),
            FondoButtonIn = ColorTranslator.FromHtml(config.FondoButtonIn),
            ForeColorButtonIn = ColorTranslator.FromHtml(config.ForeColorButtonIn),
            FondoComboBoxIn = ColorTranslator.FromHtml(config.FondoComboBoxIn),
            ForeColorComboBoxIn = ColorTranslator.FromHtml(config.ForeColorComboBoxIn),
            FondoTabControlIn = ColorTranslator.FromHtml(config.FondoTabControlIn),
            ForeColorTabControlIn = ColorTranslator.FromHtml(config.ForeColorTabControlIn),
            EstilosMenu = config.EstilosMenu,
            ControlesExcluidos = config.ControlesExcluidos
        };
    }
}
```

### `ThemeManager.cs`
#### Aplica los estilos a cada control del formulario, incluyendo lógica específica para:
        • 	 con encabezado personalizado
        • 	 , , 
        • 	 con fondo heredado del contenedor
    
    Incluye métodos:
        • 	Aplicar(Form form)
        • 	AplicarAControl(Control ctrl)
        • 	AplicarEstiloEncabezadoListView(ListView lv)
        • 	AplicarEstiloLabelsIn(Control raiz)
 ```csharp
public class ThemeManager
{
    public Color FondoFormulario { get; set; }
    public Color FondoControl { get; set; }
    public Color FondoControlesIn { get; set; }
    public Color ForeColor { get; set; }

    public Font FuenteTituloForm { get; set; }
    public Font FuenteControles { get; set; }
    public Font FuenteControlesIn { get; set; }
    public Color FondoButtonIn { get; set; }
    public Color ForeColorButtonIn { get; set; }
    public Color FondoComboBoxIn { get; set; }
    public Color ForeColorComboBoxIn { get; set; }
    public Color FondoTabControlIn { get; set; }
    public Color ForeColorTabControlIn { get; set; }
    public Color ColorFondoControlesLabel { get; set; } = Color.FromArgb(21,42,75);
    public Color ColorTextoControlesLabel { get; set; } = Color.White;


    public MenuThemeConfig EstilosMenu { get; set; } // ✅ Esta es la propiedad que faltaba
    public Color ListViewInBackColor { get; set; } = Color.FromArgb(240, 247, 255);
    public Color FondoListViewIn { get; set; } = Color.FromArgb(240, 247, 255);
    public Color EncabezadoListViewInBackColor { get; set; } = Color.FromArgb(30, 60, 90); // fondo oscuro por defecto
    public Color EncabezadoListViewInForeColor { get; set; } = Color.White;                // texto blanco por defecto
    public List<string> ControlesExcluidos { get; set; } = new List<string>();


    public void Aplicar(Form form)
    {
        Size tamañoOriginal = form.Size;
        form.BackColor = FondoFormulario;
        form.ForeColor = ForeColor;

        foreach (Control ctrl in form.Controls)
            AplicarAControl(ctrl);

        form.Size = tamañoOriginal;
    }

    public void AplicarAControl(Control ctrl)
    {
        if (ControlesExcluidos.Contains(ctrl.Name))
            return; // ❌ No aplicar tema a este control

        if (ctrl.Name.EndsWith("In"))
        {
            ctrl.BackColor = FondoControlesIn;
            ctrl.ForeColor = ForeColor;
            ctrl.Font = FuenteControlesIn;
        }
        else
        {
            ctrl.BackColor = FondoControl;
            ctrl.ForeColor = ForeColor;
            ctrl.Font = FuenteControles;
        }

        if (ctrl is ListView lv && ctrl.Name.EndsWith("In"))
        {
            lv.BackColor = FondoListViewIn;
            lv.ForeColor = ForeColor;
            AplicarEstiloEncabezadoListView(lv); // ✅ se aplica automáticamente
            return;
        }

        if (ctrl is Button && ctrl.Name.EndsWith("In"))
        {
            ctrl.BackColor = FondoButtonIn;
            ctrl.ForeColor = ForeColorButtonIn;
            return;
        }

        if (ctrl is ComboBox && ctrl.Name.EndsWith("In"))
        {
            ctrl.BackColor = FondoComboBoxIn;
            ctrl.ForeColor = ForeColorComboBoxIn;
            return;
        }

        if (ctrl is TabControl && ctrl.Name.EndsWith("In"))
        {
            ctrl.BackColor = FondoTabControlIn;
            ctrl.ForeColor = ForeColorTabControlIn;
            return;
        }

        // Aplicar recursivamente si es contenedor
        foreach (Control child in ctrl.Controls)
        {
            AplicarAControl(child);
        }
    }
    public void AplicarEstiloEncabezadoListView(ListView lv)
    {
        if (lv == null) return;

        lv.FullRowSelect = true;
        lv.View = View.Details;
        lv.OwnerDraw = true;

        // Activar doble búfer incluso si fue creado en diseñador
        typeof(Control).GetProperty("DoubleBuffered", BindingFlags.Instance | BindingFlags.NonPublic)
            ?.SetValue(lv, true, null);

        lv.DrawColumnHeader += (sender, e) =>
        {
            using (SolidBrush backBrush = new SolidBrush(EncabezadoListViewInBackColor))
            using (SolidBrush textBrush = new SolidBrush(EncabezadoListViewInForeColor))
            using (StringFormat sf = new StringFormat { Alignment = StringAlignment.Near, LineAlignment = StringAlignment.Center })
            {
                e.Graphics.FillRectangle(backBrush, e.Bounds);
                e.Graphics.DrawString(e.Header?.Text ?? "", lv.Font, textBrush, e.Bounds, sf);
                e.DrawDefault = false;
            }
        };

        lv.DrawItem += (sender, e) =>
        {
            bool isSelected = (e.State & ListViewItemStates.Selected) != 0;
            Color backColor = isSelected ? SystemColors.Highlight : lv.BackColor;
            Color textColor = isSelected ? SystemColors.HighlightText : lv.ForeColor;

            using (SolidBrush backBrush = new SolidBrush(backColor))
            using (SolidBrush textBrush = new SolidBrush(textColor))
            {
                e.Graphics.FillRectangle(backBrush, e.Bounds);
            }

            // No dibujamos texto aquí si hay subitems
            if (lv.View != View.Details || e.Item.SubItems.Count <= 1)
            {
                e.Graphics.DrawString(e.Item.Text, lv.Font, new SolidBrush(textColor), e.Bounds);
            }

            if ((e.State & ListViewItemStates.Focused) != 0)
                e.DrawFocusRectangle();
        };

        lv.DrawSubItem += (sender, e) =>
        {
            bool isSelected = e.Item.Selected;
            Color backColor = isSelected ? SystemColors.Highlight : lv.BackColor;
            Color textColor = isSelected ? SystemColors.HighlightText : lv.ForeColor;

            using (SolidBrush backBrush = new SolidBrush(backColor))
            using (SolidBrush textBrush = new SolidBrush(textColor))
            {
                e.Graphics.FillRectangle(backBrush, e.Bounds);
                e.Graphics.DrawString(e.SubItem.Text, lv.Font, textBrush, e.Bounds);
            }

            if (e.Item.Focused)
                e.DrawFocusRectangle(e.Bounds);
        };

        // Eventos para forzar redibujado durante hover y foco
        lv.MouseMove += (s, ev) => lv.Invalidate();
        lv.MouseLeave += (s, ev) => lv.Invalidate();
        lv.GotFocus += (s, ev) => lv.Invalidate();
        lv.LostFocus += (s, ev) => lv.Invalidate();
        lv.ItemSelectionChanged += (s, ev) => lv.Invalidate();
    }

    public void AplicarEstiloLabelsIn(Control raiz)
    {
        foreach (Control ctrl in raiz.Controls)
        {
            if (ctrl is Label lbl && lbl.Name.EndsWith("In"))
            {
                // 🔁 Tomar el fondo del contenedor real
                lbl.BackColor = lbl.Parent?.BackColor ?? raiz.BackColor;
                lbl.ForeColor = Color.White;
                lbl.UseCompatibleTextRendering = true;
                lbl.Font = new Font("Segoe UI", 9F, FontStyle.Bold);
            }

            if (ctrl.HasChildren)
            {
                AplicarEstiloLabelsIn(ctrl);
            }
        }
    }
}
```
### `frm_Seg_Usuarios.cs`
#### Formulario MDI que:
    • 	Carga el tema desde 
    • 	Aplica estilo visual al área cliente (`Mdi

```csharp
 public partial class frm_Seg_Menu : Form, IFormSeg
 {
     public ToolStripMenuItem MnuStripItem { get; private set; }
     public int li_id_sistema;
     public int li_id_opcion;
     public int li_accion;
     public string li_nombre_opcion;
     public string li_nombre_frm;
     private string aux_li_nombre_frm = "prueba";

     public void CambiarNombreFormulario(string text)
     {
         aux_li_nombre_frm = text;
     }

     ConexionDB cn;

     public frm_Seg_Menu()
     {
         cn = new ConexionDB(var_global.gs_cn_srv, var_global.gs_cn_usr, var_global.gs_cn_psw, var_global.gs_cn_dbs);
         InitializeComponent(); 
         this.BackColor = Color.FromArgb(240, 247, 255);
     }

     private void salirToolStripMenuItem_Click(object sender, EventArgs e) => System.Environment.Exit(1);

     private void tileLayout1_Paint(object sender, PaintEventArgs e)
     {
     }

     private void salir_tmp_Click(object sender, EventArgs e) => System.Environment.Exit(1);

     public void frm_Seg_Menu_Load(object sender, EventArgs e)
     {
         this.IsMdiContainer = true;

         // ✅ Aplicar color al área cliente real (MdiClient)
         foreach (Control ctrl in this.Controls)
         {
             if (ctrl is MdiClient)
             {
                 ctrl.BackColor = Color.FromArgb(240, 247, 255);
             }
         }

         // ✅ Cargar tema visual desde JSON
         string rutaTema = Path.Combine(Application.StartupPath, "Scripts", "tema.json");
         var tema = ThemeLoader.CargarDesdeJson(rutaTema);

         // ✅ Crear MenuStrip con renderer desde tema
         MenuStrip Menu_Mnu_Strip = new MenuStrip
         {
             Dock = DockStyle.Top,
             RenderMode = ToolStripRenderMode.Professional,
             Renderer = new AecMenuRenderer(tema.EstilosMenu),
             Font = new Font(tema.EstilosMenu.FuenteMenu.Nombre, tema.EstilosMenu.FuenteMenu.Tamaño,
                             Enum.TryParse(tema.EstilosMenu.FuenteMenu.Estilo, true, out FontStyle estilo) ? estilo : FontStyle.Regular)
         };

         this.Controls.Add(Menu_Mnu_Strip);
         this.MainMenuStrip = Menu_Mnu_Strip;

         // ✅ Cargar menú desde base de datos
         li_id_sistema = 1;
         li_id_opcion = 1;
         li_accion = 1;

         ConexionDB cn = new ConexionDB(var_global.gs_cn_srv, var_global.gs_cn_usr, var_global.gs_cn_psw, var_global.gs_cn_dbs);
         DataSet dsetpam = cn.CargarMenu(var_global.gs_sistema, 2, var_global.gs_usuario, 1);

         foreach (DataRow dr in dsetpam.Tables["Seg_Opciones_Menu"].Rows)
         {
             ToolStripMenuItem MnuStripItem = new ToolStripMenuItem(dr["NOMBRE_OPCION"].ToString());
             SubMenu(MnuStripItem, Convert.ToInt32(dr["ID_OPCION"]));
             Menu_Mnu_Strip.Items.Add(MnuStripItem);
         }

         // ✅ Posicionamiento visual
         int margen = 20;
         int margen_f = 40;

         btn_Salir.Location = new Point(
             this.ClientSize.Width - btn_Salir.Width - margen,
             this.ClientSize.Height - btn_Salir.Height - margen
         );

         pbx_Fondo.Width = 300;
         pbx_Fondo.Location = new Point(
             this.ClientSize.Width - pbx_Fondo.Width,
             margen_f
         );

         pbx_Fondo.Height = this.ClientSize.Height - margen_f - btn_Salir.Height - margen;
         this.BackColor = Color.FromArgb(240, 247, 255);
         this.Invalidate();

         this.MdiChildActivate += frm_Seg_Menu_MdiChildActivate;
     }

     public void SubMenu(ToolStripMenuItem mnu, int submenu)                                  //Recibe Nombre_Opcion y ID_Opcion
     {
         ConexionDB cn;
         cn = new ConexionDB(var_global.gs_cn_srv, var_global.gs_cn_usr, var_global.gs_cn_psw, var_global.gs_cn_dbs);
         DataSet dsetpam_s1;
         dsetpam_s1 = cn.CargarMenu(var_global.gs_sistema, submenu, var_global.gs_usuario, 2);       //Retorna datos para el Submenu : NIVEL 2

         if (dsetpam_s1 == null)
         {
         }
         else
         {   
             foreach (DataRow dr in dsetpam_s1.Tables["Seg_Opciones_Menu"].Rows)
             {
                 ToolStripMenuItem SSMenu = new ToolStripMenuItem(dr["NOMBRE_OPCION"].ToString(), null, new EventHandler(ChildClick));

                 // 🎨 Estilo de los submenús
                 //SSMenu.BackColor = Color.DarkBlue;
                 //SSMenu.ForeColor = Color.LightYellow;
                 //SSMenu.Font = new Font("Segoe UI", 10, FontStyle.Regular);

                 mnu.DropDownItems.Add(SSMenu);

                 SubMenu(SSMenu, Convert.ToInt32(dr["ID_OPCION"]));
             }
         }
     }

     private void ChildClick(object sender, EventArgs e)
     {
         var menuItem = sender as ToolStripMenuItem;
         if (menuItem == null) return;

         // Traer la URL del form desde la BD
         ConexionDB cn = new ConexionDB(var_global.gs_cn_srv, var_global.gs_cn_usr, var_global.gs_cn_psw, var_global.gs_cn_dbs);
         DataTable dsetpam_s_url = cn.CargarMenu_dt(menuItem.Text); // O usa el ID, mejor que Text
         string formPath = dsetpam_s_url.Rows[0][0].ToString();

         if (aux_li_nombre_frm == formPath)
         {
             MessageBox.Show("Formulario Abierto");
             return;
         }

         // Buscar el tipo del formulario
         Type type = Type.GetType(formPath);

         if (type == null)
         {
             MessageBox.Show($"No se encontró el formulario: {formPath}");
             return;
         }

         Form frmShow = (Form)Activator.CreateInstance(type);

         // Cuando el hijo se cierre, limpiar la variable cache
         frmShow.FormClosed += (s, ev) =>
         {
             aux_li_nombre_frm = null;
         };

         // Cerrar otros hijos si quieres que solo uno esté abierto
         foreach (Form form in this.MdiChildren)
         {
             form.Close();
         }

         frmShow.MdiParent = this;
         frmShow.Show();

         aux_li_nombre_frm = formPath; // actualizar cache
     }
    // Se desactiva el boton Salir del MDI mientas el formulario hijo esta abierto
     private void frm_Seg_Menu_MdiChildActivate(object sender, EventArgs e)
     {
         btn_Salir.Visible = this.ActiveMdiChild == null;
     }
 }
```
