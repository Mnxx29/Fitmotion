# FitMotion — Smart Sensor Workout
## Informe Técnico de Proyecto
**Universidad de Los Lagos** — Departamento de Ingeniería en Informática  
**Asignatura:** Desarrollo de Aplicación Móvil  
**Proyecto:** FitMotion  
**Estudiante:** Germán Ignacio Guillermo Aravena  

---

## 1. Introducción

FitMotion es una aplicación móvil desarrollada en **MIT App Inventor** orientada al acondicionamiento físico y la salud postural. Su propósito fundamental es transformar un teléfono inteligente convencional en un asistente biomecánico capaz de registrar, auditar y retroalimentar entrenamientos físicos en tiempo real sin requerir accesorios externos ni intervención manual constante.

A través del aprovechamiento directo de los sensores de hardware integrados en el dispositivo móvil, la aplicación cuantifica el movimiento del usuario, analiza la técnica de ejecución en ejercicios funcionales y entrega respuestas tanto visuales como auditivas y hápticas.

---

## 2. Problemática y Usuario Objetivo

En la actualidad, una proporción significativa de personas practica actividad física de manera autodidacta en sus hogares o en espacios públicos sin contar con la supervisión de un preparador físico. Esta situación suele generar dos dificultades recurrentes: la imprecisión en el registro manual de las series y repeticiones, y la ejecución deficiente de los ejercicios por falta de retroalimentación inmediata, lo cual incrementa el riesgo de sobrecargas articulares y lesiones lumbares.

FitMotion aborda esta necesidad ofreciendo una herramienta accesible que valida la calidad de cada movimiento mediante parámetros cinemáticos medidos por el propio teléfono.

El usuario objetivo comprende a jóvenes y adultos (entre 18 y 60 años) —incluyendo estudiantes y personas con rutinas laborales sedentarias— que desean incorporar pausas activas o entrenamientos estructurados en su vida diaria, requiriendo un sistema de monitoreo autónomo, confiable y que opere con manos libres.

---

## 3. Propuesta de Solución

La solución plantea un flujo de entrenamiento guiado donde el teléfono móvil actúa como sensor inercial adherido al cuerpo (ubicado en el muslo, bolsillo o sostenido en la mano). 

A diferencia de las aplicaciones tradicionales que se limitan a cronómetros estáticos o bitácoras manuales, FitMotion implementa algoritmos de detección cinemática que analizan en tiempo real los datos angulares y aceleraciones del usuario. De este modo, una repetición sólo se da por válida cuando se completa el rango articular biomecánico requerido, promoviendo una técnica correcta y manteniendo al usuario motivado mediante estímulos auditivos y táctiles continuos.

---

## 4. Estructura de Pantallas y Navegación

La aplicación está organizada en 4 pantallas secuenciales e interconectadas que cubren desde el acceso inicial hasta la entrega de resultados:

```
[Screen1: Acceso / Login]
           │
           ▼
[Screen2: Menú de Rutinas]
           │
           ▼
[Screen3: Entrenamiento en Vivo]
           │
           ▼
[Screen4: Resumen y Métricas]
    │                     │
    ▼                     ▼
[Nueva Rutina]       [Cerrar App]
```

### Screen1: Control de Acceso y Bienvenida
* **Propósito:** Brindar un punto de entrada seguro y presentar la identidad visual de la aplicación.
* **Componentes principales:** Logotipo institucional de la app (`imgLogo`), campos de texto para usuario y clave (`txtUsuario`, `txtClave`), botón de autenticación (`btnIngresar`) y etiqueta de retroalimentación en caso de error (`lblError`).
* **Lógica y eventos:** Valida las credenciales ingresadas (`usuario` / `1234`). Al ser correctas, almacena el identificador de sesión en la base de datos local `TinyDB` y avanza a `Screen2`. En caso de discordancia, despliega un aviso visual y acciona el actuador de vibración para advertir al usuario. El botón nativo de retorno (`Screen1.BackPressed`) finaliza la ejecución de forma ordenada.

### Screen2: Panel de Selección de Rutina
* **Propósito:** Permitir al deportista seleccionar el tipo de entrenamiento físico a desarrollar en la sesión.
* **Componentes principales:** Dos tarjetas de actividad claramente diferenciadas:
  * *Sentadillas Inteligentes:* Rutina enfocada en fuerza de tren inferior con meta predeterminada de 10 repeticiones.
  * *Podómetro y Trote Activo:* Rutina aeróbica orientada a cadencia y desplazamiento con meta predeterminada de 50 pasos.
  * Botón de cierre de sesión (`btnCerrarSesion`).
* **Lógica y eventos:** Al seleccionar cualquiera de las dos actividades, la aplicación parametriza y almacena en `TinyDB` las etiquetas correspondientes al modo de entrenamiento y la meta cuantitativa elegida, realizando la transición inmediata hacia `Screen3`. La tecla física de retroceso retorna a `Screen1`.

### Screen3: Centro de Telemetría y Ejecución en Vivo
* **Propósito:** Constituye el núcleo biomecánico de la app; procesa en segundo plano las señales de los sensores, evalúa los ángulos posturales, administra el tiempo transcurrido y retroalimenta al usuario.
* **Componentes principales:** 
  * Encabezado con visualización del modo y cronómetro en segundos (`lblTiempoLive`).
  * Indicador numérico de repeticiones en tamaño prominente para lectura a distancia (`lblGranNumero`).
  * Tarjeta de instrucción postural dinámica (`lblEstadoFase`).
  * Consola de telemetría de sensores (`lblValOrientacion` y `lblValAceleracion`).
  * Botones de control operativo: Pausa/Reanudación (`btnPausa`) y Finalización (`btnFinalizarLive`).
* **Componentes no visuales:** `AccelerometerSensor1`, `OrientationSensor1`, `ClockCrono`, `ClockSensores`, `Sound1`, `TextToSpeech1` y `TinyDB1`.
* **Lógica y eventos:** En el inicio (`Screen3.Initialize`), recupera las metas desde `TinyDB`, inicializa variables de estado y emite un mensaje de voz anunciando el inicio. El algoritmo analiza continuamente los datos de los sensores para registrar repeticiones válidas. Al presionar finalizar, guarda las métricas consolidadas en `TinyDB` y transfiere el control a `Screen4`.

### Screen4: Resumen Post-Entrenamiento
* **Propósito:** Exhibir los resultados cuantitativos consolidados de la actividad física recién finalizada.
* **Componentes principales:** Encabezado con distintivo de sesión completada, panel de métricas donde se desglosa la rutina efectuada (`lblModoRealizado`), repeticiones o pasos alcanzados (`lblTotalLogrado`), tiempo total invertido (`lblTiempoInvertido`), estimación calórica y mensaje de rendimiento. Botones para comenzar un nuevo entrenamiento (`btnNuevaRutina`) o salir de la aplicación (`btnCerrarApp`).
* **Lógica y eventos:** En `Screen4.Initialize`, consulta los registros almacenados en `TinyDB`, renderiza los datos en pantalla y emite una vibración de logro. El usuario puede volver al catálogo de rutinas (`Screen2`) o cerrar el aplicativo.

---

## 5. Integración de Recursos de Hardware

FitMotion incorpora hardware nativo del teléfono inteligente para garantizar que la recolección de datos sea completamente funcional dentro de la solución:

### A. Sensor de Orientación (`OrientationSensor`)
* **Parámetro utilizado:** Grados de inclinación angular longitudinal (*Pitch*).
* **Función en el sistema:** Al colocar el teléfono en el bolsillo lateral del pantalón o sujeto al muslo, el sensor registra directamente la inclinación del fémur. Durante la flexión de una sentadilla, el ángulo respecto a la vertical cambia de manera proporcional al descenso.
* **Criterio cinemático:** Se estableció que para considerar una flexión adecuada, la inclinación debe alcanzar o superar los **45°** de *Pitch*. La repetición se valida únicamente cuando el usuario retorna a la posición erguida (inclinación inferior a **25°**). Este umbral evita conteos fraudulentos causados por simples balanceos de tronco.

### B. Sensor de Aceleración (`AccelerometerSensor`)
* **Parámetro utilizado:** Aceleración lineal en el eje vertical (*YAccel*, medido en $\text{m/s}^2$).
* **Función en el sistema:** En la rutina de caminata y trote, el sensor monitorea las fuerzas reactivas del suelo que se transmiten al cuerpo en cada zancada.
* **Criterio cinemático:** Al registrarse un impacto que exceda los **12 $\text{m/s}^2$** en el eje vertical, el sistema reconoce la existencia de un paso y lo procesa a través del filtro de estabilidad.

### C. Actuadores de Retroalimentación Complementarios
* **Motor de Vibración (`Sound.Vibrate`):** Suministra una interfaz háptica esencial para el uso a ciegas del dispositivo:
  * Pulso suave (40 ms): Notifica al usuario que alcanzó la profundidad correcta en sentadilla y ya puede iniciar el ascenso.
  * Pulso medio (100 ms): Confirma la repetición completada y contabilizada.
  * Pulso corto (30 ms): Confirma la detección de paso en trote.
  * Pulso largo (250 ms): Alerta sobre error en credenciales de acceso.
* **Sintetizador de Voz (`TextToSpeech`):** Verbaliza el inicio del ejercicio y canta en voz alta el número de repetición completada, posibilitando el entrenamiento con manos libres y sin necesidad de observar la pantalla.

---

## 6. Lógica de Programación y Arquitectura de Bloques

La programación en bloques de FitMotion fue diseñada con criterios de modularidad, eficiencia y robustez:

### 1. Máquina de Estados Finitos para Conteo de Repeticiones
Para prevenir que un usuario que permanezca en posición agachada active múltiples conteos involuntarios, se implementó una máquina de estados controlada por la variable global `fase`:

```
                 Inclinación Pitch >= 45°
           ┌──────────────────────────────────┐
           │                                  ▼
    ┌──────────────┐                  ┌──────────────┐
    │ FASE ARRIBA  │                  │  FASE ABAJO  │
    └──────────────┘                  └──────────────┘
           ▲                                  │
           └──────────────────────────────────┘
                 Inclinación Pitch <= 25°
              (Suma 1 Repetición + Voz + Haptic)
```

1. **Estado Inicial (`ARRIBA`):** El usuario se encuentra de pie.
2. **Transición a Descenso:** Cuando `Pitch >= 45°` y la fase es `ARRIBA`, el estado conmuta a `ABAJO`, se actualiza la interfaz indicando profundidad lograda y se emite un pulso háptico de 40 ms.
3. **Transición a Ascenso:** Cuando `Pitch <= 25°` y la fase es `ABAJO`, el estado regresa a `ARRIBA`, se incrementa el contador general en 1, se genera la vibración de 100 ms y se pronuncia la repetición por síntesis de voz.

### 2. Filtro Temporal de Rebote (Debouncing) en Podómetro
Durante la zancada, el choque del pie suele producir oscilaciones secundarias en el acelerómetro en cuestión de milisegundos. Para evitar que un único impacto cuente dos o tres pasos:
* Al detectar un pico de aceleración válido, se incrementa el contador y se fija la variable `cooldown = 2`.
* Mientras `cooldown` sea mayor a 0, se descartan lecturas subsecuentes, decrementando la variable en cada ciclo de muestreo hasta que el sensor retorne a un rango estable.

### 3. Persistencia de Datos con TinyDB
La información transita entre pantallas de manera desacoplada mediante etiquetas clave en `TinyDB`:
* `UsuarioActivo`: Mantiene la identidad del deportista autenticado.
* `Modo` y `Meta`: Almacenan la rutina configurada en `Screen2` para inicializar `Screen3`.
* `RepsFinales`, `TiempoFinal` y `ModoFinal`: Consolidados en `Screen3` para ser proyectados en el informe de `Screen4`.

### 4. Doble Reloj Asíncrono
Se configuraron dos componentes `Clock` con responsabilidades separadas para optimizar el rendimiento del hilo principal:
* `ClockCrono` (Intervalo de 1000 ms): Gestiona estrictamente la cadencia del cronómetro general en segundos.
* `ClockSensores` (Intervalo de 250 ms / 4 Hz): Dedicado al muestreo de telemetría inercial y ejecución de condicionales de movimiento, garantizando una respuesta ágil sin saturar el procesamiento del teléfono.

---

## 7. Guía de Ejecución y Demostración en MIT AI2 Companion

Para realizar la comprobación funcional de la aplicación en un dispositivo Android real, se sigue el procedimiento estándar:

1. **Carga del Proyecto:**
   * Importar el archivo `FitMotion.aia` en la plataforma web de MIT App Inventor.
   * En el menú superior, seleccionar **Connect ➔ AI Companion**.
2. **Enlace con el Dispositivo:**
   * Abrir la aplicación **MIT AI2 Companion** en el teléfono Android e ingresar el código alfanumérico o escanear el código QR en pantalla.
3. **Flujo de Prueba en Vivo:**
   * **Ingreso:** Probar credenciales (`usuario` / `1234`) y observar el control de acceso con vibración de confirmación.
   * **Configuración:** En el panel de rutinas, seleccionar *Sentadillas Inteligentes*.
   * **Biomecánica:** Con el teléfono orientado en posición vertical simulando el muslo, realizar la flexión hacia adelante superando los 45°. Se observará el cambio de estado a *¡BUENA PROFUNDIDAD!* y la vibración de aviso. Al erguirse por debajo de 25°, el contador sumará la unidad y el teléfono verbalizará el conteo.
   * **Control de Sesión:** Probar la alternancia del botón *Pausar / Reanudar*.
   * **Cierre y Resultados:** Pulsar *Finalizar* para verificar la recepción de métricas consolidadas en la pantalla de resumen.
