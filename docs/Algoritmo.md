# 📔 Algoritmo

## 💡Definicion
En terminos de programación , un algoritmo es como un guía para indicarle paso a paso a una computador, equipo o máquina la secuencia que debe seguir para realizar operaciones y mostrar resultados
Este pseudo-codigo consta de las siguientes parte importantes :
  1. Inicio del Algoritmo
  2. Definicion de Variables
  3. Operaciones
  4. Resultados
  5. Fin del Algoritmo

### 🔎 Consideraciones previas
Antes de iniciar debemos saber:  
    - Qué variables tenemos?             Ej: Nos dan: radio=0.75, altura=1.5  
    - Qué operaciones vamos a realizar?  Ej: Necesitamos la generatriz, area, volumen  (fórmulas)  
    - Cómo se mostrarán los resultatos?  Ej: [Mostrar nombre] : `Escribir "Nombre completo: ", nombre` esto mostrará: `Nombre completo: Morales Barahona, Ana Rebeca`

### ⌨️ Comandos a utilizar  
Algoritmo: `Con esto se indica el inicio del proceso`  
Definir : `con este comando o palabra se crean los nombres de las variables, tanto las que nos dan como las que necesitamos para la operacion`  
Escribir: `es la forma como mostramos los resultados, puede mostrarse tanto numeros como letras, las letras o palabras van entre comillas dobles " "`  
FinAlgoritmo: ` Con esto se indica la finalizacion del proceso luego de haber mostrado el resultado`  

### 🟰 Asignaciones
Para asignar un valor a una variable no se utiliza el signo 🟰, sino ⬅️, formado por el signo `<` y un `-`   asi:  `nombre<-"Morales Barahona, Ana Rebeca"`   recordando que las palabras(no variables, area, volumen van sin comillas por ser operaciones) en comillas dobles ""  




### 📲 Codigo

```
Algoritmo Cono
	// Declaración de variables
	Definir nombre Como Cadena
	Definir radio, altura, generatriz, area, volumen Como Real
	
	// Se guarda el nombre completo en la variable nombre
	nombre <- "Morales Barahona, Ana Rebeca"
	
	// Asignamos los valores dados en el enunciado
	radio <- 0.75
	altura <- 1.5
	
	// Se calcula la generatriz (g) con la fórmula ?(r^2 + h^2)
	generatriz <- raiz(radio*radio + altura*altura)
	
	// Se calcula el área de la superficie del cono
	// Fórmula: PI * r * (r + g)
	area <- PI * radio * (radio + generatriz)
	
	// Se calula el volumen del cono
	// Fórmula: (PI * r^2 * h) / 3
	volumen <- (PI * radio*radio * altura) / 3
	
	// Se muestran los resultados en pantalla
	Escribir "Nombre completo: ", nombre
	Escribir "Area: ", area
	Escribir "Volumen: ", volumen
FinAlgoritmo

```
<img width="554" height="344" alt="image" src="https://github.com/user-attachments/assets/69896752-b100-4358-8996-a0fd213abaff" />
