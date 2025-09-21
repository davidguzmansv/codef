##  UML
    +----------------------+
    |   CssThemeConfig     |  ← Se carga desde JSON
    +----------------------+
    | - FondoFormulario : string
    | - FondoControl : string
    | - FondoControlIn : string
    | - ForeColor : string
    | - FondoListViewIn : string
    | - EncabezadoListViewInBackColor : string
    | - EncabezadoListViewInForeColor : string
    | - FondoButtonIn : string
    | - ForeColorButtonIn : string
    | - FondoComboBoxIn : string
    | - ForeColorComboBoxIn : string
    | - FondoTabControlIn : string
    | - ForeColorTabControlIn : string
    | - FuenteTituloForm : Fuente
    | - FuenteControles : Fuente
    | - FuenteControlesIn : Fuente
    | - EstilosMenu : MenuThemeConfig
    +----------------------+

         |
         | deserializa en
         ▼

    +----------------------+
    |    ThemeManager      |  ← Aplica estilos a controles
    +----------------------+
    | - FondoFormulario : Color
    | - FondoControl : Color
    | - FondoControlesIn : Color
    | - ForeColor : Color
    | - FondoListViewIn : Color
    | - EncabezadoListViewInBackColor : Color
    | - EncabezadoListViewInForeColor : Color
    | - FondoButtonIn : Color
    | - ForeColorButtonIn : Color
    | - FondoComboBoxIn : Color
    | - ForeColorComboBoxIn : Color
    | - FondoTabControlIn : Color
    | - ForeColorTabControlIn : Color
    | - FuenteTituloForm : Font
    | - FuenteControles : Font
    | - FuenteControlesIn : Font
    | - EstilosMenu : MenuThemeConfig
    +----------------------+
    | + Aplicar(Control) : void
    | + AplicarEstiloEncabezadoListView(ListView) : void
    | + CargarDesdeJson(string) : ThemeManager
    +----------------------+

         ▲
         |
         | invocado desde
         |
    +----------------------+
    |   Formulario / UI    |  ← Tu WinForms
    +----------------------+
    | + tema.Aplicar(this)
    | + card1.AplicarTema(tema)
    | + tema.AplicarAControl(ctrl)
    +----------------------+


## ¿Cómo usar este UML?
  - CssThemeConfig define los estilos en el JSON.
  - ThemeManager convierte esos estilos en objetos Color y Font, y los aplica.
  - Aplicar(Control) detecta el tipo y nombre del control (ButtonIn, ListViewIn, etc.) y aplica el estilo correspondiente.
  - AplicarEstiloEncabezadoListView maneja el dibujo personalizado del encabezado.
  - Tu formulario solo invoca tema.Aplicar(...) y todo se configura automáticamente.

## Documentación interna sugerida
    Redibujado inteligente para controles OwnerDraw
    Para evitar pérdida de contenido en controles personalizados:
      Aplicar Invalidate() en eventos como MouseMove, MouseLeave, GotFocus, LostFocus, y ItemSelectionChanged. 
    Esto asegura que el contenido se mantenga visible y reactivo sin interferencias visuales.




