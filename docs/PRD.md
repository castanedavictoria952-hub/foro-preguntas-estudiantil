# PRD · <Nombre de tu producto>

> Documento de requisitos del producto (Product Requirements Document).
> Complétalo en el Sprint 0 (historia H0.3) y pide la aprobación del profesor en un Issue.
> Cada requisito funcional (RF) se convierte en un Issue con la plantilla "Historia de usuario".

| Campo               | Valor                                       |
| ------------------- | ------------------------------------------- |
| Alumno              | Victoria de los Ángeles Castañeda Gutiérrez |
| Proyecto n.º        | Foro de preguntas estudiantiles             |
| Sitio de referencia | Stack Overflow                              |
| Compañero revisor   | _(Ente248)_                                 |
| URL desplegada      | (se completa en el Sprint 5)                |

## 1. Problema

¿Qué problema real resuelve y a quién le duele? (3 a 5 líneas) : Los estudiantes universitarios suelen resolver dudas de programación y materias técnicas a través de chats informales (WhatsApp, Discord o Telegram), donde las respuestas útiles se pierden en el historial, se repiten las mismas preguntas cada semestre y no existe forma de validar cuál solución es correcta.

## 2. Usuarios

- **Usuario principal:** quién es, qué necesita, desde qué dispositivo entra. : Estudiantes universitarios (autores y colaboradores) que necesitan publicar dudas técnicas con contexto o fragmentos de código, responder consultas de compañeros, votar por las mejores soluciones y marcar una respuesta como aceptada; acceden desde computadora de escritorio/laptop y teléfono móvil.
- **Usuario secundario:** : Docentes o moderadores académicos que revisan la calidad de las publicaciones y supervisan el cumplimiento de las normas de la comunidad.

## 3. Objetivo y métrica de éxito

Ejemplo: «Un estudiante publica una pregunta técnica o encuentra una solución verificada mediante búsqueda por palabras clave, etiquetas y ordenamiento por votos en menos de 15 segundos».

## 4. Alcance del MVP

Entre 5 y 8 funcionalidades que SÍ entran este semestre.

1.Publicación, listado y consulta detallada de preguntas académicas.
2.Publicación de respuestas asociadas a una pregunta y marcado de respuesta aceptada por el autor.
3.Sistema de votación (votos positivos y negativos) para preguntas y respuestas.
4.Clasificación y filtrado de preguntas mediante etiquetas temáticas (materias y tecnologías). 5. Búsqueda de preguntas por texto y ordenamiento por votos o actividad reciente.

### Funcionalidades → carpetas de `src/` (screaming architecture)

Cada funcionalidad del alcance será una carpeta en `src/`. Nómbralas en inglés y en plural.

| Funcionalidad | Carpeta         |
| ------------- | --------------- |
| Preguntas     | `src/questions` |
| Respuestas    | `src/answers`   |
| Votos         | `src/votes`     |
| Etiquetas     | `src/tags`      |

## 5. Fuera de alcance

Lo que NO vas a construir.

- Chat privado en tiempo real o mensajería directa entre estudiantes.
- Notificaciones push móviles o integración directa con aulas virtuales externas (LMS).
- Edición colaborativa simultánea tipo wiki o subida de archivos multimedia pesados.

## 6. Requisitos funcionales

| ID    | Requisito                                                                                    | Prioridad (alta, media, baja) |
| ----- | -------------------------------------------------------------------------------------------- | ----------------------------- |
| RF-01 | Crear, listar y consultar el detalle de preguntas estudiantiles con título, cuerpo y autor.  | alta                          |
| RF-02 | Publicar respuestas dentro de una pregunta existente.                                        | alta                          |
| RF-03 | Permitir al autor de una pregunta marcar una respuesta como solución aceptada.               | alta                          |
| RF-04 | Emitir votos positivos o negativos en preguntas y respuestas para calcular su puntuación.    | media                         |
| RF-05 | Asociar etiquetas temáticas a cada pregunta y filtrar el listado por etiqueta.               | media                         |
| RF-06 | Buscar preguntas por palabras clave y ordenar los resultados por votos o actividad reciente. | alta                          |

## 7. Requisitos no funcionales

- Responsive, móvil primero (375 px y 1280 px).
- Lighthouse ≥ 90 en Accesibilidad y Buenas prácticas.
- 0 errores en la consola del navegador.
- Funciona con 10.000 registros sin congelarse.
- Consultas SQL escritas a mano y parametrizadas en PostgreSQL sin ORM, con entradas validadas mediante Zod.

## 8. Modelo de datos

Diagrama entidad-relación y tablas PostgreSQL con tipos, claves y restricciones.
GitHub dibuja diagramas Mermaid; edita este ejemplo:

```mermaid
erDiagram
  QUESTION ||--o{ ANSWER : tiene
  QUESTION ||--o{ VOTE : recibe
  ANSWER ||--o{ VOTE : recibe
  QUESTION }o--o{ TAG : clasifica_con
  QUESTION {
    int id PK
    text titulo
    text cuerpo
    text autor
    int votos
    timestamptz creado_en
    timestamptz actualizado_en
  }
  ANSWER {
    int id PK
    int question_id FK
    text cuerpo
    text autor
    boolean aceptada
    int votos
    timestamptz creado_en
  }
  VOTE {
    int id PK
    int question_id FK
    int answer_id FK
    int valor
    text votante
    timestamptz creado_en
  }
  TAG {
    int id PK
    text nombre UK
  }


## 9. Reto técnico distintivo

El que te tocó en el catálogo y cómo piensas resolverlo.

## 10. Riesgos y preguntas abiertas

-
```
