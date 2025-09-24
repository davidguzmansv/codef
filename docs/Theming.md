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

  Archivo de configuración visual con colores, fuentes y estilos para cada tipo de control.

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

  
### `CssThemeConfig.cs`
Clase que representa el modelo del JSON
```
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

ThemeLoader.cs
Carga el JSON y lo convierte en una instancia de ThemeManager.
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

ThemeManager.cs
Aplica los estilos a cada control del formulario, incluyendo lógica específica para:
• 	 con encabezado personalizado
• 	, , 
• 	 con fondo heredado del contenedor
Incluye métodos:
• 	
• 	
• 	
• 	


Formulario MDI que:
• 	Carga el tema desde 
• 	Aplica estilo visual al área cliente (`Mdi
