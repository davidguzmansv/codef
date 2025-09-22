# Estructura de Formulario

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
        foreach (Control control in this.Controls)                                        | <Aplica Proiedades de fuente a los controles
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

        // Card 1: contiene un ListView
        CardControl card1 = new CardControl()
        {
            Title = "Listado",
            Description = " ",
            Location = new Point(40, 50),
            Size = new Size(590, 425),
            BorderColor = Color.DeepSkyBlue,
            BorderWidth = 1
        };

        ListView lvUsuarios = this.Controls.Find("lvUsuarios", true).FirstOrDefault() as ListView;
        if (lvUsuarios != null)
        {
            cn.CargarUsuariosEnLV(lvUsuarios);
            tema.AplicarEstiloEncabezadoListView(lvUsuarios);
            // 🔁 Eventos para forzar redibujado durante hover
            lvUsuarios.MouseMove += (s, ev) => lvUsuarios.Invalidate();
            lvUsuarios.MouseLeave += (s, ev) => lvUsuarios.Invalidate();
            lvUsuarios.GotFocus += (s, ev) => lvUsuarios.Invalidate();
            lvUsuarios.LostFocus += (s, ev) => lvUsuarios.Invalidate();
            lvUsuarios.ItemSelectionChanged += (s, ev) => lvUsuarios.Invalidate();

            // 🔁 Refuerzo visual inmediato
            lvUsuarios.Invalidate();
            lvUsuarios.Update();
        }

        // Card 2: contiene un Panel (los controles se agregan visualmente)
        CardControl card2 = new CardControl()
        {
            Title = "Mantenimiento",
            Description = " ",
            Location = new Point(680, 50),
            Size = new Size(430, 425),
            BorderColor = Color.DeepSkyBlue,
            BorderWidth = 1
        };

        Panel pnlFormulario = this.Controls.Find("pnlFormulario", true).FirstOrDefault() as Panel;
        if (pnlFormulario != null)
        {
            card2.EstablecerContenedor(pnlFormulario);
            card2.AplicarTema(tema);
            this.Controls.Add(card2);

            // 🔁 Aplicar estilo visual desde ThemeManager
            tema.AplicarEstiloLabelsIn(pnlFormulario);
        }

        this.Controls.Add(card1);
        this.Controls.Add(card2);

        // 🔁 Aplicar estilo visual a Labels "In" después de que todo esté cargado
        this.Shown += (s, ev) =>
        {
            if (card2.ContenedorInterno != null)
            {
                tema.AplicarEstiloLabelsIn(card2.ContenedorInterno);
            }
        };
    }
}
