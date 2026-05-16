# ADR-01: Arquitectura – Grind Core

> **Estado:** `PROPUESTO`
> 
> **Autor:** Joshua Cruz
> 
> **Fecha:** Mayo 2026
> 
> **Dominio:** Gestión de Rendimiento en Gym y Powerlifting

---

## Contexto

En el ámbito del deporte de alto rendimiento, como el Powerlifting y el entrenamiento de fuerza avanzado, la gestión de la programación presenta un desafío logístico crítico que suele subestimarse. Los entrenadores frecuentemente gestionan una carga de atletas que supera su capacidad de organización manual, lo que convierte el seguimiento de rutinas en un proceso confuso y propenso a errores. Esta problemática se intensifica al intentar centralizar variables fundamentales como el registro de pesos, repeticiones, Esfuerzo Percibido (RPE), totales acumulados y el análisis de datos semanales o mensuales de cada individuo.

El objetivo de este sistema es digitalizar dicha interacción mediante una plataforma web donde atletas y entrenadores converjan en un ecosistema eficiente. El atleta dispone de una interfaz para adjuntar su rendimiento diario, permitiéndole consultar su intensidad máxima estimada (1RM) mediante una calculadora integrada que el entrenador supervisa en tiempo real. A su vez, el preparador cuenta con facultades para editar rutinas, configurar planes de entrenamiento en cualquier momento, consultar históricos de carga y añadir retroalimentación técnica sobre los ejercicios realizados.

Este proyecto se desarrolla bajo el entorno .NET, garantizando una arquitectura de datos robusta y una ejecución fiable que asegure la integridad de la información al momento de su entrega y puesta en producción.

---

## Decisión

Se ha seleccionado un ecosistema basado en **ASP.NET Core** bajo la arquitectura **Modelo-Vista-Controlador (MVC)**. Para la base de datos se emplea **PostgreSQL**, aprovechando su capacidad para manejar datos numéricos. La lógica de acceso a datos se implementa con **Entity Framework Core** mediante un enfoque de desarrollo basado en código, mientras que la interfaz visual utiliza **Razor Pages** y **Tailwind CSS** para consolidar una estética oscura y minimalista de alto rendimiento.

---

## Justificación 

La elección de esta ruta técnica responde principalmente a la necesidad de garantizar precisión absoluta en los cálculos de rendimiento. Al procesar los algoritmos de fatiga y las proyecciones de carga directamente en el servidor, aseguramos que los resultados sean exactos y consistentes, evitando los errores de redondeo que suelen ocurrir cuando los cálculos dependen del navegador del dispositivo móvil. Esta arquitectura se complementa con el patrón MVC, el cual permite una organización limpia donde la lógica de los levantamientos y la interfaz visual evolucionan de forma independiente, facilitando así la colaboración en el código sin generar conflictos técnicos. Finalmente, una característica esencial para que el atleta pueda registrar sus datos de manera fluida durante los breves periodos de descanso en el gimnasio.

---
## Alternativas

Se evaluaron opciones como el uso de PHP con Laravel o el desarrollo de una aplicación de página única con React (MERN Stack); sin embargo, se descartaron para priorizar el tipado fuerte de .NET y evitar la complejidad innecesaria en la sincronización de estados que presentan otros marcos de trabajo. Asimismo, se evitó una arquitectura de microservicios para prevenir latencias innecesarias, manteniendo un sistema monolítico bien estructurado que garantiza la fiabilidad requerida para este dominio deportivo.

---

##  Impacto y Proyecciones

La arquitectura actual garantiza una separación clara de responsabilidades, facilitando el mantenimiento futuro y la posible integración de módulos de análisis avanzados o dispositivos vestibles. Aunque el sistema realiza recargas de página controladas, se ha previsto el uso de scripts específicos para optimizar la interactividad en funciones críticas como cronómetros de descanso. Finalmente, la base técnica actual está preparada para exponer una interfaz de programación (API) si el crecimiento del proyecto requiere una transición hacia aplicaciones móviles nativas.
