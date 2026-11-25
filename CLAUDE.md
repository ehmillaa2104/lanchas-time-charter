# Estudio de lanchas: Time Charter

Guía para trabajar este repo con Claude Code.

## Qué hay aquí

- `index.html`: todo el estudio en un solo archivo (HTML, CSS y JavaScript). No hay build ni dependencias.
- Se publica solo con GitHub Pages desde `main`: https://ehmillaa2104.github.io/lanchas-time-charter/ (tarda cerca de un minuto en actualizarse después de cada cambio).
- La misma página existe como artefacto de Claude de Esteban Millaa. Los cambios de aquí no pasan solos al artefacto; Esteban los trae cuando lo pide.

## Cómo está armado `index.html`

- Pestañas: Presentación, Modelo, Modelo 2, Situación actual, Línea base y cobertura, Tareas de TT, Proveedores.
- `renderPres` arma la presentación: la portada (00 / 07, no cuenta) y 7 diapositivas principales numeradas con `num` (de 7) y 4 anexos numerados con `numA` (de 4). Usa los ayudantes `row` y `card` y los formatos `kf`, `money`, `nfp`.
- Orden (23 nov 2026): Portada (00), 1 Requerimientos, 2 Consideraciones, 3 Situación actual, 4 Cobertura estimada, 5 Comparativo de alternativas, 6 Precio del diésel y punto de equilibrio, 7 Recomendaciones para implementar. La diapositiva de barras "Costo anual por alternativa" (Yelko) se eliminó el 24 nov 2026. Anexos: 1 Time Charter: qué evaluar, 2 Propuesta de Arpón, 3 Estimación de 2 lanchas, 4 Licitación por paquete. Próximos pasos se eliminó.
- Pestaña Proveedores (`renderProv`, 24 nov 2026): solo muestra "Flota por proveedor", con la tabla de cada proveedor desplegable y la nota de fuente con la definición de L1 y L2. Se quitaron las tarjetas por proveedor, la conclusión y la tabla de naves que cumplen. Datos en `PROV`, del archivo Flota_Lanchas_Consolidado que envió Ramón Cardoze el 24 nov 2026: Arpón, BSS, Pacific Marine Supplies & Services (nuevo: Pacific Oasis II, IV y V; la IV es alternativa para L1 y L2), Marinet y OLS.
- `MODELS[0].plan` es el horario del modelo (lunes a domingo; `a` = lancha de 44, `b` = lancha de 20).
- Modelo 2 (`MODELS[1]`, id `modelo-2`, `pool:1`; 24 nov 2026, por viajes desde el 25 nov): los viajes del Modelo sin las rondas de mediodía, sin asignarlos a una lancha (`aViajes`; cada día es `{t:[...]}`). `renderPool` dibuja un solo carril por día (25 nov 2026): `pack` reparte los viajes no opcionales en niveles y `lane(...,rowOf)` baja dentro del mismo carril (`.lane.pl`, variables `--n` y `--r`) los que se juntan con otro; al lado del día dice cuántas lanchas trabajan a la vez. Las ventanas opcionales (`e[6]`) no empujan viajes: van de fondo en el primer nivel libre. En el editor no se elige lancha ("Cualquier lancha"), y doble clic y Borrar funcionan sobre los viajes. En Línea base y cobertura, el Modelo 2 muestra horas, viajes, lanchas a la vez y horas con más de una lancha en vez del uso por lancha. Si lo guardado trae el Modelo 2 por lancha o no lo trae, `setPlans` lo arma por viajes; desde que alguien guarda un cambio en la página, cada modelo queda guardado por separado. La presentación usa solo el Modelo (`MODELS[0]`).
- `SAVED_PLAN` es el horario guardado de los dos modelos (al 24 nov 2026, con Materiales del lunes de 9:30 a 14:30). En esta copia se aplica al cargar con `setPlans(SAVED_PLAN)`, porque GitHub Pages no tiene la base de datos del artefacto; antes del 24 nov se definía pero no se aplicaba, y GitHub mostraba el horario sin guardar (6,378 h). Si se cambia el horario de forma permanente, hay que actualizar `SAVED_PLAN`.
- `BASE_COST` es el costo anual actual sin Comanche; el punto de equilibrio es `BASE_COST / 365` (sin spot, desde el 23 nov 2026).
- Diapositiva 5 (comparativo de alternativas, 23 nov 2026, va justo después de Cobertura estimada): se ven de entrada hoy, Time Charter Arpón (3 lanchas) y paquete por horas a la tarifa actual. Las dos estimadas, Time Charter de 2 lanchas y paquete por horas negociado a $175/h (`NEG`), van a la derecha con la clase `cxe` y quedan ocultas hasta que se presiona el botón lateral "Ver estimados" (`CMP_OPEN`). Es el resumen para la junta directiva; usa las mismas cuentas que los anexos 2, 3 y 4. No lleva recomendación: el costo anual y la diferencia van en rojo si superan el costo actual y en verde si quedan por debajo. Se quitaron los renglones de costo por día y de galón para igualar; los precios de equilibrio del diésel están en la diapositiva 6 (con el horario guardado al 24 nov, 6,131 h al año: Arpón $2.63 contra hoy y $1.81 contra el paquete; 2 lanchas $4.04 y $3.23).
- Diapositiva 6 (precio del diésel y punto de equilibrio, 24 nov 2026): gráfica de líneas en SVG, costo anual contra precio del galón de $0 a $7. Los Time Charter suben con el diésel; Hoy y los paquetes por horas son líneas planas; los puntos marcan los cruces (los mismos precios del último renglón del comparativo) y una línea punteada marca el precio actual de $6. Rojo = Time Charter, verde = paquete por horas, punteado = estimado; colores validados con la skill de dataviz. Usa el mismo botón "Ver estimados": `CMP_OPEN` abre o cierra a la vez todos los `.cmx`. Al pasar el mouse muestra el costo de cada alternativa a ese precio.
- `COORD` = $30,000 al año de coordinador logístico; se suma en las tres alternativas nuevas, no en la situación actual.
- Anexo 2 (propuesta de Arpón, 19 nov 2026): $22,500 al mes por lancha x 3 lanchas x 12 meses, sin combustible. Combustible con el consumo informado por Arpón: Perseverance 2 x 480 HP, 48 a 52 gal/h (se usa 50); Arpón 1 e Infinity 2 x 385 HP, 40.2 gal/h. Cada lancha hace un tercio de las horas del modelo y el spot. Diésel a $6 por galón, consumo al 70% del máximo (23 nov 2026); se trabaja en galones, no en toneladas.
- Anexo 3 (estimación, 20 nov 2026): una lancha de 44 y una de carga, sin nombre, a $22,500 al mes cada una x 12 meses (mismo criterio que Arpón). Las horas del modelo y el spot se reparten según el uso de cada lancha en el modelo; consumo de referencia 50 gal/h (lancha de 44, como Perseverance) y 40.2 gal/h (carga, como Arpón 1), al 70%, con diésel a $6 por galón.

## Reglas de redacción

- Español, tono profesional y directo. Sin guiones largos.
- "Fijo" en vez de "línea base" para las tareas fijas actuales; "proveedor" en vez de "armador".
- La lancha grande siempre es de 44 pasajeros.

## Antes de subir un cambio

- Abrir la presentación en pantalla completa y revisar que cada diapositiva entre sin cortarse (1920x1080 y 1280x720).
