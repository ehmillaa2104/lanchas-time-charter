# Estudio de lanchas: Time Charter

Guía para trabajar este repo con Claude Code.

## Qué hay aquí

- `index.html`: todo el estudio en un solo archivo (HTML, CSS y JavaScript). No hay build ni dependencias.
- Se publica solo con GitHub Pages desde `main`: https://ehmillaa2104.github.io/lanchas-time-charter/ (tarda cerca de un minuto en actualizarse después de cada cambio).
- La misma página existe como artefacto de Claude de Esteban Millaa. Los cambios de aquí no pasan solos al artefacto; Esteban los trae cuando lo pide.

## Cómo está armado `index.html`

- Pestañas: Presentación, Modelo, Situación actual, Línea base y cobertura, Tareas de TT, Proveedores.
- `renderPres` arma la presentación: 7 diapositivas principales numeradas con `num` (de 7) y 4 anexos numerados con `numA` (de 4). Usa los ayudantes `row` y `card` y los formatos `kf`, `money`, `nfp`.
- Orden (23 nov 2026): 1 Portada, 2 Requerimientos, 3 Consideraciones, 4 Situación actual, 5 Cobertura estimada, 6 Comparativo de alternativas, 7 Recomendaciones para implementar. Anexos: 1 Time Charter: qué evaluar, 2 Propuesta de Arpón, 3 Estimación de 2 lanchas, 4 Licitación por paquete. Próximos pasos se eliminó.
- `MODELS[0].plan` es el horario del modelo (lunes a domingo; `a` = lancha de 44, `b` = lancha de 20).
- `SAVED_PLAN` carga el horario guardado al 19 nov 2026. Si se cambia el horario de forma permanente, hay que actualizar `SAVED_PLAN`.
- `BASE_COST` es el costo anual actual sin Comanche; el punto de equilibrio es `BASE_COST / 365` (sin spot, desde el 23 nov 2026).
- Diapositiva 6 (comparativo de alternativas, 23 nov 2026, va justo después de Cobertura estimada): hoy, Time Charter Arpón (3 lanchas), Time Charter estimado (2 lanchas), paquete por horas a la tarifa actual y paquete por horas negociado a $175/h (`NEG`). Es el resumen para la junta directiva; usa las mismas cuentas que los anexos 2, 3 y 4. No lleva recomendación: el costo anual y la diferencia van en rojo si superan el costo actual y en verde si quedan por debajo.
- `COORD` = $30,000 al año de coordinador logístico; se suma en las tres alternativas nuevas, no en la situación actual.
- Anexo 2 (propuesta de Arpón, 19 nov 2026): $22,500 al mes por lancha x 3 lanchas x 12 meses, sin combustible. Combustible con el consumo informado por Arpón: Perseverance 2 x 480 HP, 48 a 52 gal/h (se usa 50); Arpón 1 e Infinity 2 x 385 HP, 40.2 gal/h. Cada lancha hace un tercio de las horas del modelo y el spot. Diésel a $6 por galón, consumo al 70% del máximo (23 nov 2026); se trabaja en galones, no en toneladas.
- Anexo 3 (estimación, 20 nov 2026): una lancha de 44 y una de carga, sin nombre, a $22,500 al mes cada una x 12 meses (mismo criterio que Arpón). Las horas del modelo y el spot se reparten según el uso de cada lancha en el modelo; consumo de referencia 50 gal/h (lancha de 44, como Perseverance) y 40.2 gal/h (carga, como Arpón 1), al 70%, con diésel a $6 por galón.

## Reglas de redacción

- Español, tono profesional y directo. Sin guiones largos.
- "Fijo" en vez de "línea base" para las tareas fijas actuales; "proveedor" en vez de "armador".
- La lancha grande siempre es de 44 pasajeros.

## Antes de subir un cambio

- Abrir la presentación en pantalla completa y revisar que cada diapositiva entre sin cortarse (1920x1080 y 1280x720).
