# FitMotion — Entrenador de Bolsillo con Sensores

Aplicación móvil desarrollada en **MIT App Inventor** para la asignatura **Desarrollo de Aplicación Móvil** de la **Universidad de Los Lagos**.

---

## 📌 ¿Qué es FitMotion?

**FitMotion** es una aplicación diseñada para que cualquier persona pueda entrenar y registrar sus ejercicios (como sentadillas o caminata) usando únicamente los sensores de su teléfono celular, sin necesidad de pulseras ni accesorios externos.

La app mide de manera automática el movimiento y la inclinación del teléfono:
- **Tú pones la meta:** Puedes elegir cuántas sentadillas o cuántos pasos quieres hacer (por ejemplo, 15 sentadillas o 1.000 pasos).
- **Alarma al cumplir:** Al alcanzar tu objetivo, suena una alarma en el celular, vibra de forma prolongada y una voz te avisa que completaste tu meta.
- **Modo Bolsillo (Pantalla bloqueada):** Puedes activar el Modo Bolsillo, la pantalla se oscurece y se protege contra toques involuntarios, permitiéndote guardar el celular en el bolsillo mientras entrenas con total comodidad.

---

## 🚀 Contenido de la Carpeta

* **`FitMotion.aia`**: Archivo del proyecto listo para importar en [MIT App Inventor](https://ai2.appinventor.mit.edu).
* **`DOCUMENTO_ENTREGA_FITMOTION.md`**: Informe de entrega completo (problema, usuario, solución, pantallas, sensores utilizados y guía de prueba).
* **`Documento_Entrega_FitMotion_ULagos.docx`**: Versión en formato Microsoft Word del informe.
* **`Evaluacion_App_Movil_App_Inventor_ULagos.docx`**: Pauta y requerimientos de la evaluación universitaria.

---

<p align="center">
  <img src="Captura%20de%20pantalla%202026-10-01%20162438.png" alt="FitMotion - Vista de la Aplicación en Teléfono Móvil" width="280" />
</p>

---

## 📱 Pantallas de la Aplicación

1. **Screen1 (Iniciar Sesión):** Acceso rápido con usuario y clave (`usuario` / `1234`), aviso por vibración en caso de error y guardado de sesión con `TinyDB`.
2. **Screen2 (Elegir Ejercicio y Meta):** Selección entre *Sentadillas* y *Contador de Pasos*, permitiendo ingresar la meta que el usuario desea cumplir.
3. **Screen3 (Entrenamiento en Vivo):** Conteo automático con sensores, cronómetro, botón de *Modo Bolsillo* para guardar en el pantalón y alarma sonora al cumplir la meta.
4. **Screen4 (Resumen):** Resultados finales con repeticiones conseguidas, tiempo total y calorías aproximadas.

---

## ⚙️ Sensores de Hardware Integrados

* **Sensor de Inclinación (`OrientationSensor`):** Mide el ángulo del celular en el muslo o bolsillo para registrar sentadillas completas (flexión profunda de más de 45° y vuelta a posición de pie).
* **Sensor de Movimiento / Acelerómetro (`AccelerometerSensor`):** Registra cada paso al caminar o trotar mediante la fuerza de movimiento vertical.
* **Sonido de Alarma (`Sound`):** Hace sonar la alarma (`alarma.wav`) cuando se llega a la meta.
* **Vibración del teléfono:** Avisa cuando la flexión fue correcta y cuando se completó una repetición o el entrenamiento.
* **Voz del teléfono (`TextToSpeech`):** Dicta el número de repeticiones en voz alta para entrenar sin mirar la pantalla.

---

## 🛠️ Cómo Probar la App con MIT AI2 Companion

1. Abre [MIT App Inventor](https://ai2.appinventor.mit.edu) e importa el archivo `FitMotion.aia`.
2. En el menú superior haz clic en **Connect ➔ AI Companion**.
3. En tu teléfono Android abre la app **MIT AI2 Companion** y escanea el código QR en pantalla.
4. Inicia sesión con `usuario` / `1234`, fija tu objetivo, activa el *Modo Bolsillo* y prueba el ejercicio.
