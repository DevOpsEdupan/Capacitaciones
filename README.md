# Guía de Tutoría de 20 Horas sobre Cloud Functions de Google Cloud Platform (GCP)

## Tabla de Contenidos

- [Introducción](#introducción)
- [Módulo 1: Introducción a GCP y Cloud Functions](#módulo-1-introducción-a-gcp-y-cloud-functions-2-horas)
- [Módulo 2: Configuración del Entorno](#módulo-2-configuración-del-entorno-2-horas)
- [Módulo 3: Fundamentos de Cloud Functions](#módulo-3-fundamentos-de-cloud-functions-4-horas)
- [Módulo 4: Cloud Functions y Eventos](#módulo-4-cloud-functions-y-eventos-3-horas)
- [Módulo 5: Desarrollo Avanzado](#módulo-5-desarrollo-avanzado-4-horas)
- [Módulo 6: Despliegue y Monitoreo](#módulo-6-despliegue-y-monitoreo-3-horas)
- [Módulo 7: Optimización y Costos](#módulo-7-optimizacion-y-costos-1-hora)
- [Módulo 8: Proyecto Final](#módulo-8-proyecto-final-1-hora)
- [Recursos Adicionales](#recursos-adicionales)
- [Conclusión](#conclusión)

## Introducción

Bienvenido a esta guía de tutoría de 20 horas sobre **Cloud Functions** de **Google Cloud Platform (GCP)**. Esta guía está diseñada para proporcionarte un recorrido completo desde los conceptos básicos hasta las prácticas avanzadas en el uso de Cloud Functions.

### Objetivos de la Tutoría

- Comprender los conceptos fundamentales de Cloud Functions en GCP.
- Configurar y administrar el entorno de desarrollo.
- Desarrollar, desplegar y monitorear funciones serverless.
- Integrar Cloud Functions con otros servicios de GCP.
- Optimizar el rendimiento y los costos.

### Requisitos Previos

- Conocimientos básicos de programación (JavaScript, Python, etc.).
- Familiaridad con la línea de comandos.
- Cuenta de Google Cloud Platform (se cubrirá en el Módulo 2).

---

## Módulo 1: Introducción a GCP y Cloud Functions (2 horas)

### 1.1 Introducción a Google Cloud Platform

- **¿Qué es GCP?**
  - Plataforma de servicios en la nube de Google.
- **Principales servicios de GCP**
  - Compute Engine, App Engine, Cloud Storage, etc.

### 1.2 Conceptos Básicos de Cloud Functions

- **¿Qué son las Cloud Functions?**
  - Funciones serverless que se ejecutan en respuesta a eventos.
- **Ventajas del modelo serverless**
  - Escalabilidad automática.
  - Pago por uso real.

### 1.3 Casos de Uso

- **Procesamiento de imágenes o videos al subirlos a Cloud Storage.**
- **Respondedores HTTP para aplicaciones web o móviles.**
- **Integraciones con APIs externas.**

**Actividad:** Investigar y discutir posibles casos de uso en proyectos personales o profesionales.

---

## Módulo 2: Configuración del Entorno (2 horas)

### 2.1 Creación de una Cuenta de GCP

- **Registro en GCP**
  - [Crear cuenta](https://cloud.google.com/free)
  - Uso del crédito gratuito inicial.

### 2.2 Configuración del Proyecto

- **Creación de un nuevo proyecto en la consola de GCP.**
- **Habilitación de facturación.**

### 2.3 Instalación de Google Cloud SDK

- **Descarga e instalación del SDK**
  - [Instrucciones de instalación](https://cloud.google.com/sdk/docs/install)
- **Inicialización y autenticación**
  ```bash
  gcloud init
  ```

### 2.4 Configuración del Entorno de Desarrollo

- **Elección del IDE (Visual Studio Code, IntelliJ, etc.).**
- **Instalación de extensiones útiles.**

**Actividad:** Configurar el entorno y validar la instalación ejecutando `gcloud --version`.

---

## Módulo 3: Fundamentos de Cloud Functions (4 horas)

### 3.1 Estructura de una Cloud Function

- **Componentes principales**
  - Código fuente.
  - Configuración de despliegue.
- **Anatomía de una función**

### 3.2 Lenguajes Soportados

- **Node.js, Python, Go, Java, .NET**
- **Selección del lenguaje según el caso de uso.**

### 3.3 Tipos de Cloud Functions

- **Funciones desencadenadas por HTTP**
  - Responden a solicitudes HTTP.
- **Funciones basadas en eventos**
  - Responden a eventos de GCP (Pub/Sub, Cloud Storage).

### 3.4 Primeros Pasos: Creación de una Función "Hello World"

- **Ejemplo en Node.js:**

  ```javascript
  exports.helloWorld = (req, res) => {
    res.send('¡Hola, Mundo!');
  };
  ```

- **Despliegue de la función:**

  ```bash
  gcloud functions deploy helloWorld --runtime nodejs14 --trigger-http --allow-unauthenticated
  ```

- **Prueba de la función:**

  ```bash
  gcloud functions call helloWorld
  ```

**Actividad:** Desplegar y probar una función "Hello World" en el lenguaje de preferencia.

---

## Módulo 4: Cloud Functions y Eventos (3 horas)

### 4.1 Comprensión de Eventos en GCP

- **¿Qué son los eventos?**
  - Acciones o cambios que ocurren en los servicios de GCP.
- **Event Triggers**
  - Configuración de funciones para responder a eventos específicos.

### 4.2 Integración con Pub/Sub

- **Configuración de un tópico de Pub/Sub.**
- **Desarrollo de una función que responda a mensajes.**

  ```python
  def hello_pubsub(event, context):
      import base64
      if 'data' in event:
          name = base64.b64decode(event['data']).decode('utf-8')
      else:
          name = 'Mundo'
      print(f'¡Hola, {name}!')
  ```

- **Despliegue:**

  ```bash
  gcloud functions deploy hello_pubsub --runtime python39 --trigger-topic mi-topico
  ```

### 4.3 Respondiendo a Cambios en Cloud Storage

- **Configuración de triggers para Cloud Storage.**
- **Ejemplo: Procesamiento de imágenes al subirlas.**

### 4.4 Trabajando con Firestore Triggers

- **Desencadenadores en cambios de base de datos.**
- **Ejemplo práctico.**

**Actividad:** Crear una función que responda a un evento de Pub/Sub o Cloud Storage.

---

## Módulo 5: Desarrollo Avanzado (4 horas)

### 5.1 Manejo de Dependencias

- **Uso de archivos `package.json` (Node.js) o `requirements.txt` (Python).**
- **Instalación de dependencias en el entorno de la función.**

### 5.2 Variables de Entorno y Configuración

- **Definición de variables de entorno en el despliegue.**
  ```bash
  gcloud functions deploy myFunction --set-env-vars "KEY=valor"
  ```
- **Acceso a variables en el código.**

### 5.3 Autenticación y Seguridad

- **Control de acceso con IAM.**
- **Protección de funciones con autenticación.**

### 5.4 Buenas Prácticas y Patrones Comunes

- **Estructuración del código.**
- **Manejo de errores y excepciones.**
- **Logs y seguimiento.**

**Actividad:** Refactorizar una función existente aplicando buenas prácticas.

---

## Módulo 6: Despliegue y Monitoreo (3 horas)

### 6.1 Desplegando Funciones con gcloud CLI

- **Comandos avanzados de despliegue.**
- **Automatización con scripts.**

### 6.2 Monitoreo y Logging

- **Visualización de logs en la consola de GCP.**
- **Uso de `console.log` o equivalentes.**

### 6.3 Uso de Cloud Monitoring

- **Creación de métricas personalizadas.**
- **Configuración de alertas.**

### 6.4 Manejo de Errores y Depuración

- **Herramientas de depuración en GCP.**
- **Estrategias para resolver problemas comunes.**

**Actividad:** Implementar monitoreo en una función y configurar una alerta básica.

---

## Módulo 7: Optimización y Costos (1 hora)

### 7.1 Escalabilidad y Rendimiento

- **Comprensión del modelo de escalado automático.**
- **Configuración de límites de concurrencia.**

### 7.2 Optimización de Costos

- **Análisis de factores que afectan los costos.**
- **Mejores prácticas para minimizar gastos.**

### 7.3 Límites y Cuotas

- **Revisión de cuotas por defecto.**
- **Solicitudes de aumento de cuotas si es necesario.**

**Actividad:** Analizar el costo estimado de una función y proponer optimizaciones.

---

## Módulo 8: Proyecto Final (1 hora)

### 8.1 Desarrollo de un Proyecto Integrado

- **Definición del proyecto (por ejemplo, una API RESTful).**
- **Integración de múltiples funciones y servicios de GCP.**

### 8.2 Revisión y Discusión

- **Presentación de soluciones.**
- **Feedback y mejoras sugeridas.**

---

## Recursos Adicionales

- **Documentación Oficial de Cloud Functions:**
  [Cloud Functions Documentation](https://cloud.google.com/functions/docs)
- **Cursos en Línea:**
  - [Google Cloud Training](https://cloud.google.com/training)
- **Comunidades y Foros:**
  - [Stack Overflow](https://stackoverflow.com/questions/tagged/google-cloud-functions)
  - [Google Cloud Community](https://www.googlecloudcommunity.com)

---

## Conclusión

A lo largo de esta tutoría de 20 horas, hemos explorado en profundidad las Cloud Functions de GCP, desde los conceptos básicos hasta las prácticas avanzadas. Has adquirido habilidades para desarrollar soluciones serverless eficientes y escalables.

**Próximos Pasos:**

- Aplicar lo aprendido en proyectos reales.
- Explorar otros servicios de GCP para ampliar tus habilidades.
- Continuar aprendiendo y manteniéndote actualizado con las novedades de GCP.

¡Gracias por tu participación y éxito en tus futuros proyectos con Google Cloud Platform!

---

# Licencia

Este material está licenciado bajo la [Licencia MIT](LICENSE).

# Contacto


Si tienes alguna pregunta o necesitas más información, no dudes en contactarme a través de [correo electrónico](mailto:leonardo_franco@edupan.com) o en [LinkedIn](https://www.linkedin.com/in/l-franco28/).

---

# Historias de Cambio

- **Versión 1.0** - Creación inicial de la guía.

---

*Esta guía fue creada para fines educativos y debe ser adaptada según las necesidades específicas de la audiencia.*
