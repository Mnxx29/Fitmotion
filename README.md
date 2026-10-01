# FitMotion — Smart Sensor Workout

Aplicación móvil desarrollada en **MIT App Inventor** para la asignatura **Desarrollo de Aplicación Móvil** de la **Universidad de Los Lagos**.

---

## 📌 Descripción del Proyecto

**FitMotion** transforma un teléfono inteligente convencional en un asistente biomecánico capaz de registrar, auditar y retroalimentar entrenamientos físicos en tiempo real sin requerir accesorios externos ni intervención manual constante.

La aplicación utiliza los sensores inerciales del dispositivo móvil para cuantificar el movimiento del usuario, analizar la técnica postural en ejercicios funcionales (como sentadillas) y detectar zancadas en marcha o trote, brindando respuestas inmediatas visuales, auditivas (síntesis de voz) y hápticas (vibración).

---

## 🚀 Contenido del Repositorio

* **`FitMotion.aia`**: Archivo fuente del proyecto para importar en [MIT App Inventor](https://ai2.appinventor.mit.edu).
* **`DOCUMENTO_ENTREGA_FITMOTION.md`**: Informe técnico completo del proyecto (introducción, problema, solución, arquitectura de pantallas, sensores de hardware, lógica de bloques y guía de ejecución).
* **`Documento_Entrega_FitMotion_ULagos.docx`**: Versión formal en formato Microsoft Word del informe técnico.
* **`Evaluacion_App_Movil_App_Inventor_ULagos.docx`**: Pauta y requerimientos oficiales de la evaluación universitaria.

---

## 📱 Arquitectura de Pantallas

1. **Screen1 (Login):** Control de acceso seguro (`usuario` / `1234`), control de errores con alerta háptica y persistencia de sesión con `TinyDB`.
2. **Screen2 (Rutinas):** Catálogo de selección entre *Sentadillas Inteligentes* (meta: 10 reps) y *Podómetro & Trote Activo* (meta: 50 pasos).
3. **Screen3 (En Vivo):** Centro de telemetría inercial en tiempo real, cronómetro desacoplado, conteo biomecánico mediante máquina de estados y control de pausa/reanudación.
4. **Screen4 (Resumen):** Consola de resultados finales con métricas acumuladas recuperadas desde `TinyDB`.

---

## ⚙️ Hardware Integrado

* **Sensor de Orientación (`OrientationSensor`):** Mide la inclinación longitudinal (*Pitch*) para asegurar que la sentadilla alcance al menos 45° de flexión profunda antes de retornar a la posición erguida (< 25°).
* **Acelerómetro (`AccelerometerSensor`):** Mide la aceleración vertical (*YAccel*) con filtro anti-rebote (*debouncing*) para registrar el impacto de cada zancada.
* **Motor de Vibración (`Sound.Vibrate`):** Avisos táctiles de profundidad alcanzada, repetición completada y error de acceso.
* **Sintetizador de Voz (`TextToSpeech`):** Lectura en voz alta del número de repetición para entrenamiento manos libres.

---

## 🛠️ Ejecución con MIT AI2 Companion

1. Importar `FitMotion.aia` en [MIT App Inventor](https://ai2.appinventor.mit.edu).
2. En el menú superior seleccionar **Connect ➔ AI Companion**.
3. En el teléfono Android abrir la app **MIT AI2 Companion** y escanear el código QR.
