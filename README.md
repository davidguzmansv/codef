# Formularios
1. Estructura de formulario


       ├── pnlCards (Panel principal con CssGridLayout)
           ├── cardCliente (CardControl)
           |   ├── Icono (PictureBox)
           |   ├── Titulo (Label)
           |   ├── Descripcion (Label)
           |   └── ControlesIn (PanelIn)
           |       ├── lstOpcionesIn (ListBox)
           |       ├── txtNombreIn (TextBox)
           |       └── btnGuardarIn (Button)
           ├── cardProducto
           |   └── ControlesIn
           |       ├── cmbCategoriaIn (ComboBox)
           |       ├── lblPrecioIn (Label)
           |       └── btnAgregarIn (Button)
           └── cardResumen
               └── ControlesIn
                   ├── lblTotalIn (Label)
                   └── btnFinalizarIn (Button)


## Codigo
1. Ejemplo de codigo:

       public partial class frm_EjemploVisual : Form
        {
            private ThemeManager tema;
            private Panel pnlCards;

            public frm_EjemploVisual()
            {
                InitializeComponent();
                this.Load += frm_EjemploVisual_Load;
            }    

            private void frm_EjemploVisual_Load(object sender, EventArgs e)
            {
            // Cargar tema
            string ruta = Path.Combine(Application.StartupPath, "Scripts", "tema.json");
            tema = CssThemeLoader.CargarDesdeJson(ruta);
            tema.Aplicar(this);

            // Panel principal
            pnlCards = new Panel
            {
               Dock = DockStyle.Fill,
               Name = "pnlCards",
               Padding = new Padding(20),
               AutoScroll = true
            };
            this.Controls.Add(pnlCards);

            // Card Cliente
            var cardCliente = new CardControl { Title = "Cliente", Description = "Datos del cliente", Name = "cardCliente", Size = new Size(300, 200) };
            cardCliente.ControlesIn.Controls.Add(new ListBox { Name = "lstOpcionesIn", Dock = DockStyle.Top, Height = 60 });
            cardCliente.ControlesIn.Controls.Add(new TextBox { Name = "txtNombreIn", Dock = DockStyle.Top, PlaceholderText = "Nombre" });
            cardCliente.ControlesIn.Controls.Add(new Button { Name = "btnGuardarIn", Text = "Guardar", Dock = DockStyle.Bottom });
            cardCliente.AplicarTema(tema);
            pnlCards.Controls.Add(cardCliente);

            // Card Producto
            var cardProducto = new CardControl { Title = "Producto", Description = "Información del producto", Name = "cardProducto", Size = new Size(300, 200) };
            cardProducto.ControlesIn.Controls.Add(new ComboBox { Name = "cmbCategoriaIn", Dock = DockStyle.Top });
            cardProducto.ControlesIn.Controls.Add(new Label { Name = "lblPrecioIn", Text = "Precio: $0.00", Dock = DockStyle.Top });
            cardProducto.ControlesIn.Controls.Add(new Button { Name = "btnAgregarIn", Text = "Agregar", Dock = DockStyle.Bottom });
            cardProducto.AplicarTema(tema);
            pnlCards.Controls.Add(cardProducto);

            // Card Resumen
            var cardResumen = new CardControl { Title = "Resumen", Description = "Totales y acciones", Name = "cardResumen", Size = new Size(300, 200) };
            cardResumen.ControlesIn.Controls.Add(new Label { Name = "lblTotalIn", Text = "Total: $0.00", Dock = DockStyle.Top });
            cardResumen.ControlesIn.Controls.Add(new Button { Name = "btnFinalizarIn", Text = "Finalizar", Dock = DockStyle.Bottom });
            cardResumen.AplicarTema(tema);
            pnlCards.Controls.Add(cardResumen);

            // Distribuir visualmente
            CssGridLayout.Aplicar(pnlCards, columnas: 2);
            }
        }

## Reglas para nuevos formularios
    1. 	Todos los controles internos deben tener el sufijo  para que reciban estilos diferenciados.
    2. 	Aplica  a cada  después de agregar sus hijos.
    3. 	Usa  para distribuir los cards automáticamente.
    4. 	Evita aplicar fuentes al formulario completo; usa  si necesitas aplicar a un control específico.


    
