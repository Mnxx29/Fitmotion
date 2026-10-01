# FitMotion — Entrenador de Bolsillo con Sensores
## Informe de Entrega del Proyecto
**Universidad de Los Lagos** — Departamento de Ingeniería en Informática  
**Asignatura:** Desarrollo de Aplicación Móvil  
**Proyecto:** FitMotion  
**Estudiante:** Germán Ignacio Guillermo Aravena  

---

## 1. Introducción

**FitMotion** es una aplicación móvil desarrollada en **MIT App Inventor** creada para ayudar a las personas a hacer ejercicio de forma guiada y automática usando su propio teléfono celular, sin necesidad de comprar relojes inteligentes ni accesorios caros.

Aprovechando los **sensores de movimiento e inclinación** que ya vienen dentro de cualquier teléfono Android, la app cuenta automáticamente las repeticiones de ejercicios (como sentadillas) o los pasos al caminar o trotar, avisando con sonido de alarma, voz y vibraciones cuando se cumple el objetivo fijado por el usuario.

---

## 2. Problema y Usuario Objetivo

### El problema:
Muchas personas hacen ejercicio por su cuenta en casa o salen a caminar al aire libre sin la supervisión de un entrenador. Al hacerlo, suelen perder la cuenta de sus repeticiones, no saben si se están agachando lo suficiente en una sentadilla y tienen que estar mirando la pantalla o tocando el teléfono con las manos sudadas, lo cual resulta incómodo y corta el ritmo del entrenamiento.

### Usuario objetivo:
Estudiantes, trabajadores y cualquier persona (de 18 a 60 años) que quiera mantenerse activa, hacer pausas saludables durante el día o caminar para cuidar su salud, necesitando una app práctica, fácil de entender y que funcione con el celular guardado en el bolsillo.

---

## 3. Propuesta de Solución y Novedades

FitMotion permite que el celular funcione como un entrenador personal dentro del bolsillo:

1. **Objetivos personalizados:** El usuario puede ingresar la meta que desea lograr para su sesión (por ejemplo, una meta de 15 sentadillas o 1.000 pasos).
2. **Alarma al completar la meta:** Apenas se alcanza el número fijado, suena una **alarma sonora**, el teléfono **vibra** y una **voz** anuncia: *"¡Objetivo cumplido!"*, permitiendo saber de inmediato que la meta fue lograda sin tener que mirar la pantalla.
3. **Modo Bolsillo (Pantalla bloqueada):** Al iniciar la rutina, el usuario puede activar el botón de **Modo Bolsillo**. Esto coloca la pantalla en negro (ahorro de batería) y bloquea los toques accidentales de la tela del pantalón. De esta manera, el teléfono se guarda en el bolsillo y los sensores continúan contando el ejercicio de forma ininterrumpida.
4. **Lenguaje claro y directo:** La interfaz evita tecnicismos confusos y muestra la información que el usuario realmente necesita: repeticiones logradas, meta fijada, tiempo transcurrido y estado del ejercicio.

---

## 4. Estructura de Pantallas de la Aplicación

La aplicación se compone de 4 pantallas conectadas de manera ordenada y fácil de usar:

```
[Screen1: Iniciar Sesión]
           │
           ▼
[Screen2: Elegir Ejercicio y Meta]
           │
           ▼
[Screen3: Entrenamiento en Vivo (Modo Bolsillo + Alarma)]
           │
           ▼
[Screen4: Resumen de Resultados]
```

### Screen1: Iniciar Sesión
* **Qué hace:** Pantalla de bienvenida con el logo de la app. Permite el acceso seguro del usuario.
* **Componentes:** Logo institucional, campos para escribir usuario y contraseña, botón de inicio de sesión y mensaje de error si los datos son incorrectos.
* **Datos de prueba rápidos:** Usuario: `usuario` | Contraseña: `1234`.
* **Detalle:** Si los datos no coinciden, el celular vibra brevemente y muestra una advertencia visual. Si coinciden, guarda la sesión en `TinyDB` y pasa a `Screen2`.

### Screen2: Elige tu Ejercicio y Configura tu Meta
* **Qué hace:** Menú principal donde el usuario elige qué ejercicio quiere realizar y puede escribir su propio objetivo numérico.
* **Opciones disponibles:**
  * **🏋️ Sentadillas:** Mide la inclinación del celular en el muslo o bolsillo para contar cada flexión bien hecha. Incluye una casilla para escribir la meta deseada (por defecto: 15 repeticiones).
  * **🚶 Contador de Pasos:** Detecta el impacto de cada zancada al caminar o trotar. Incluye una casilla para escribir la meta de pasos (por defecto: 1.000 pasos).
* **Botón de Cerrar Sesión:** Permite salir y volver a la pantalla de login.

### Screen3: Entrenamiento en Vivo
* **Qué hace:** Es la pantalla donde transcurre la actividad física. Registra las lecturas de los sensores en tiempo real, suma las repeticiones, lleva el tiempo y avisa al cumplir la meta.
* **Elementos en pantalla:**
  * **Cronómetro:** Muestra los minutos y segundos transcurridos.
  * **Número grande:** Indica las repeticiones o pasos completados hasta el momento.
  * **Etiqueta de meta:** Muestra el objetivo configurado (ej: *Meta: 15*).
  * **Tarjeta de consejos:** Indica la fase del movimiento (*"Coloca el móvil en tu bolsillo"*, *"¡Buena flexión! Ahora sube..."*, *"¡Repetición completada!"*).
  * **Datos del sensor en vivo:** Muestra de forma simple los grados de inclinación y la fuerza de movimiento detectada.
  * **Botón 🔒 Modo Bolsillo (Bloquear Pantalla):** Activa la pantalla de protección oscura para meter el teléfono al bolsillo sin miedo a toques involuntarios.
  * **Botón 🔓 Desbloquear Pantalla:** Permite volver a la vista normal en cualquier momento para ver las estadísticas en detalle.
  * **Botones Pausar / Reanudar y Finalizar:** Para controlar la sesión manualmente cuando se desee.
* **Comportamiento de la Alarma:** Al llegar o superar la meta configurada (ej: repetición 15), se activa la alarma sonora (`alarma.wav`), el celular vibra con un pulso largo (1,5 segundos) y la voz del teléfono felicita al usuario.

### Screen4: Resumen de Resultados
* **Qué hace:** Muestra la tarjeta final con las estadísticas consolidadas de la rutina que se acaba de terminar.
* **Datos mostrados:**
  * Tipo de ejercicio realizado (Sentadillas o Caminata).
  * Total de repeticiones o pasos conseguidos.
  * Tiempo total invertido en segundos.
  * Estimación simple de calorías quemadas.
  * Mensaje de felicitación por el logro.
* **Botones de acción:**
  * **Nuevo Entrenamiento:** Vuelve a la pantalla de selección de rutinas (`Screen2`).
  * **Cerrar Aplicación:** Finaliza la app ordenadamente.

---

## 5. Sensores de Hardware Utilizados

Cumpliendo con los requisitos de la evaluación, FitMotion utiliza de forma real y funcional los siguientes recursos de hardware del teléfono:

### 1. Sensor de Orientación (`OrientationSensor`)
* **Qué mide:** Los grados de inclinación del teléfono (*Pitch*).
* **Para qué sirve en la app:** Al guardar el teléfono en el bolsillo delantero o sobre el muslo, el celular se inclina hacia adelante al agacharse.
* **Cómo funciona la cuenta:** Cuando la inclinación supera los **45°**, la app reconoce que la persona bajó lo suficiente y emite una vibración corta de aviso. Cuando la persona vuelve a ponerse de pie (menos de **25°**), se suma una repetición válida, vibra de confirmación y el teléfono dice el número en voz alta.

### 2. Sensor de Aceleración / Movimiento (`AccelerometerSensor`)
* **Qué mide:** Los cambios de velocidad y fuerza vertical del teléfono en cada paso.
* **Para qué sirve en la app:** En el modo de caminata o trote, detecta el impacto del pie contra el piso al dar una zancada.
* **Cómo funciona la cuenta:** Al superar un umbral de movimiento suave (12 m/s²), la app suma un paso. Cuenta con un filtro de tiempo para evitar que un solo rebote cuente dos veces.

### 3. Actuadores de Sonido, Voz y Vibración
* **Sonido de Alarma (`Sound`):** Reproduce el archivo de audio `alarma.wav` al alcanzar el objetivo fijado.
* **Vibración del teléfono:** Permite sentir cuándo la sentadilla llegó abajo y cuándo se completó la repetición o la meta, sin tener que mirar la pantalla.
* **Sintetizador de Voz (`TextToSpeech`):** Dicta en voz alta las repeticiones y avisa verbalmente cuando la meta fue completada.

---

## 6. ¿Cómo Funciona el Modo Bolsillo?

En los sistemas Android, cuando se apaga físicamente la pantalla con el botón de encendido, el sistema operativo congela los sensores de las aplicaciones comunes para ahorrar batería. 

Para resolver este problema y permitir que la app funcione dentro del bolsillo sin romperse ni requerir permisos raros en MIT AI2 Companion:

1. FitMotion incorpora el **Modo Bolsillo**: un botón directo que activa una pantalla en negro absoluto (estilo pantalla de bloqueo de bajo consumo).
2. Se **bloquean todos los botones interactivos** para que la fricción de la tela del bolsillo no pause el ejercicio ni toque botones por error.
3. Los sensores de movimiento e inclinación, los relojes internos con `TimerAlwaysFires` y el motor de sonido y voz **permanecen 100% activos**.
4. El usuario guarda el teléfono en el bolsillo, realiza sus sentadillas o su caminata, escucha el conteo por voz y, al llegar al objetivo (por ejemplo la sentadilla 15), la **alarma suena fuerte desde el bolsillo**.
5. Al sacarlo, solo pulsa **"🔓 Desbloquear Pantalla"** para revisar su resumen final.

---

## 7. Guía Paso a Paso para Probar la App (con MIT AI2 Companion)

Para probar la aplicación en un teléfono Android real mediante el Companion oficial:

1. **Importar el proyecto:**
   * Entrar a [ai2.appinventor.mit.edu](https://ai2.appinventor.mit.edu).
   * Ir a *Projects ➔ Import project (.aia) from my computer* y seleccionar el archivo `FitMotion.aia`.
2. **Conectar el teléfono:**
   * En el menú superior de App Inventor, hacer clic en *Connect ➔ AI Companion*.
   * Abrir la app **MIT AI2 Companion** en el teléfono y escanear el código QR que aparece en pantalla.
3. **Probar el flujo completo:**
   * **Paso 1 (Login):** Ingresar con `usuario` y `1234`. Presionar *Iniciar Sesión*.
   * **Paso 2 (Elegir ejercicio y meta):** En *Sentadillas*, revisar la casilla de meta (por ejemplo, cambiarla a 5 para una prueba rápida o dejar 15). Presionar *Iniciar Sentadillas*.
   * **Paso 3 (Probar el Modo Bolsillo):** En la pantalla de entrenamiento, presionar *🔒 MODO BOLSILLO*. La pantalla se pondrá negra con protección táctil.
   * **Paso 4 (Hacer el ejercicio):** Con el celular en posición vertical (en el bolsillo o en la mano simulando el muslo), inclinar el teléfono hacia adelante más de 45° (sentadilla abajo) y volver a enderezarlo (sentadilla arriba). Notar la vibración y el conteo por voz.
   * **Paso 5 (Alarma de meta):** Al completar la última repetición de la meta, escuchar cómo suena la alarma sonora, la vibración larga y el mensaje de voz.
   * **Paso 6 (Desbloquear y finalizar):** Presionar *🔓 Desbloquear Pantalla* y luego *🏁 Finalizar* para ver el resumen de tiempo y calorías en la pantalla 4.

---

## 8. Conclusión

FitMotion demuestra cómo herramientas accesibles como **MIT App Inventor** permiten crear soluciones móviles prácticas y de alto impacto para la vida diaria. Al conectar directamente el acelerómetro y el sensor de inclinación con respuestas sonoras, por voz y de vibración, se logra una experiencia de ejercicio fluida, manos libres y pensada para la comodidad del usuario común.
