# 🏗️ Estructura de Formulario
```csharp
    public partial class frm_Seg_Usuarios : Form
    {
      ConexionDB cn;                                                                      | <Controlador de conexion a DB>
      public frm_Seg_Usuarios()
      {
        InitializeComponent();                                                            | <Inicializa los componentes>
        this.Load += frm_Seg_Usuarios_Load;                                               | <Instancia el formulario y el metodo Load>
        cn = new ConexionDB(var_global.gs_cn_srv, var_global.gs_cn_usr, var_global.gs_cn_psw, var_global.gs_cn_dbs);
      }
      private void frm_Seg_Usuarios_Load(object sender, EventArgs e)                      | <Metodo Load /  aqui carga los elementos>
      {
        string rutaTema = Path.Combine(Application.StartupPath, "Scripts", "tema.json");  | <Busca la ruta del archivo Json que contiene propiedades de color>
        ThemeManager tema = ThemeLoader.CargarDesdeJson(rutaTema);                        | <Instancia el ThemeMAnager para el tema desde el archivo Json>
        tema.Aplicar(this);                                                               | <Aplica el tema con el metodo 'Aplicar'>

        // 🔁 Aplicar estilo a todos los LabelIn del formulario
        foreach (Control control in this.Controls)                                        | <Aplica Propiedades de fuente a los controles
        {                                                                                 | label dentro del contenedor de un card
            foreach (Control ctrl in this.Controls)                                       | el label debe llamarse 'lblNombreIn
            {                                                                             | debe comenzar con 'lbl' + nombre + 'In'>
                if (ctrl is Label lbl && lbl.Name.EndsWith("In"))
                {
                    lbl.ForeColor = tema.ColorTextoControlesLabel;
                    lbl.BackColor = tema.ColorFondoControlesLabel;
                    lbl.Font = new Font("Century Gothic", 11F, FontStyle.Bold);
                    lbl.UseCompatibleTextRendering = true;
                }
            }
        }

        // Card 1: contiene un ListView                                                    | Se agrega una card para mostrar listados
        CardControl card1 = new CardControl()                                              | se parametriza tamano y posicion
        {
            Title = "Listado",
            Description = " ",
            Location = new Point(40, 50),
            Size = new Size(590, 425),
            BorderColor = Color.DeepSkyBlue,
            BorderWidth = 1
        };
                                                                                            | El listview va dentro del contenedor de card
        ListView lvUsuarios = this.Controls.Find("lvUsuarios", true).FirstOrDefault() as ListView;
        if (lvUsuarios != null)                                                             | Se crea en modo diseno y se instancia para asignarlo
        {
            cn.CargarUsuariosEnLV(lvUsuarios);
            tema.AplicarEstiloEncabezadoListView(lvUsuarios);                               | Se le aplica el tema de encabezado
            // 🔁 Eventos para forzar redibujado durante hover                              | Se invalidan estos eventos para evitar redibujo
            lvUsuarios.MouseMove += (s, ev) => lvUsuarios.Invalidate();
            lvUsuarios.MouseLeave += (s, ev) => lvUsuarios.Invalidate();
            lvUsuarios.GotFocus += (s, ev) => lvUsuarios.Invalidate();
            lvUsuarios.LostFocus += (s, ev) => lvUsuarios.Invalidate();
            lvUsuarios.ItemSelectionChanged += (s, ev) => lvUsuarios.Invalidate();

            // 🔁 Refuerzo visual inmediato
            lvUsuarios.Invalidate();
            lvUsuarios.Update();
        }

        // Card 2: contiene un Panel (los controles se agregan visualmente)                  | Se agrega card2 para mantenimientos
        CardControl card2 = new CardControl()                                                | Se parametriza tamano y posicion
        {                                                                                    | CardControl contiene la aplicacion del tema de contenedor
            Title = "Mantenimiento",
            Description = " ",
            Location = new Point(680, 50),
            Size = new Size(430, 425),
            BorderColor = Color.DeepSkyBlue,
            BorderWidth = 1
        };
                                                                                             | Se crea un panel que servira de contenedor para los mantenimientos 
        Panel pnlFormulario = this.Controls.Find("pnlFormulario", true).FirstOrDefault() as Panel;
        if (pnlFormulario != null)
        {
            card2.EstablecerContenedor(pnlFormulario);                                       | Card2 recibe el panel dentro de su contenedor
            card2.AplicarTema(tema);                                                         | Card2 aplica el tema
            this.Controls.Add(card2);                                                        | Se carga el panel dentro del contenedor de Card2
        }

        this.Controls.Add(card1);                                                            | Se carga Card1 en el formulario
        this.Controls.Add(card2);                                                            | Se cargo Card2 en el formulario
    }
}
```
