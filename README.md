# 🧪 Nutriente Exótico: NLP árabe con diacríticos

**Región de origen:** Egipto  
**Cazado el:** 20260730011952  

---

## 📦 Tesoros encontrados en GitHub:
- No se encontraron repositorios relacionados.

---

## 🌍 ¿Por qué es valioso?
Este tema es escaso porque proviene de ecosistemas de desarrollo no occidentales. Contiene aproximaciones únicas a la IA que no están en los papers mainstream de EEUU/Europa.

---

## Corrección al stub (2026-11-09)

El stub de arriba se conserva íntegro. Dos de sus afirmaciones necesitan corrección, con fuente:

**1. "No se encontraron repositorios relacionados" — falso hoy.**
Existen repositorios relacionados, todos verificados el 2026-11-09:

- CAMeL Tools — `https://github.com/CAMeL-Lab/camel_tools.git` (NYU Abu Dhabi; PyPI `camel-tools` 1.5.7, 17-sep-2025, licencia MIT).
- Mishkal — `https://github.com/linuxscout/mishkal.git` (vocalizador árabe de código abierto, basado en reglas).
- Shakkala — `https://github.com/Barqawiz/Shakkala` (red neuronal recurrente para vocalizar texto árabe, Barqawi y Zerrouki 2017).
- CATT — `https://github.com/abjadai/catt` (modelos y benchmark del paper CATT, Abjad Ltd. 2024).
- arabic-diacritizer — `https://github.com/Z-Mahmood/arabic-diacritizer-public-release.git` (BiLSTM + atención, PyPI 1.0.0, 13-mar-2026).
- Farasa no es un repo GitHub abierto: es un servicio de QCRI con demo y API REST en `https://farasa.qcri.org/diacritization/` (la descarga exige registro).

El bot que cazó el tema en julio de 2026 no los encontró; hoy están ahí.

**2. "No están en los papers mainstream de EEUU/Europa" — impreciso.**
El tema SÍ está en los venues mainstream: EMNLP 2025 (Mohamed y Mubarak, QCRI), arXiv (CATT 2024, Sadeed 2026), ScienceDirect (Sukoun 2024), ACL Anthology (WANLP 2017). Lo que es verdad es la otra mitad de la frase: gran parte del trabajo puntero viene de instituciones del mundo árabe — QCRI (Catar), NYU Abu Dhabi, Universidad de Sharjah, Abjad Ltd. (Arabia Saudita) — no de laboratorios de EEUU/Europa. La escasez real no es de papers: es de datos. El texto árabe totalmente diacritizado es raro, y el mayor corpus del campo es 98,85% árabe clásico (ver §4).

**Nota de verificación:** la fecha del stub (`20260730011952`) coincide con el commit inicial: 01:19:52 -05 = 06:19:52 UTC; el commit es de las 06:20:05Z del 30-jul-2026.

---

## 1. Qué son los diacríticos

El árabe se escribe normalmente sin vocales cortas: las letras muestran las consonantes y las vocales largas, y las vocales cortas son marcas pequeñas sobre o debajo de la letra. Esas marcas se llaman **ḥarakāt** (حَرَكَات, singular *ḥaraka*); el sistema completo se llama **tashkeel** (تَشْكِيل). Toda ḥaraka es tashkeel, pero no todo tashkeel es ḥaraka.

| Marca | Nombre | Sonido / función |
|---|---|---|
| َ | fatḥa | vocal corta /a/ |
| ِ | kasra | vocal corta /i/ |
| ُ | ḍamma | vocal corta /u/ |
| ْ | sukūn | ninguna vocal tras la consonante |
| ّ | shadda | la consonante se duplica (geminación) |
| ً ٍ ٌ | tanwīn | -an / -in / -un al final de un nombre indefinido |

El árabe cotidiano —noticias, mensajes, novelas, letreros— omite casi todas estas marcas. Aparecen en el Corán, los libros infantiles, los diccionarios, la poesía y los materiales para estudiantes. Un lector nativo las rellena desde el contexto y el vocabulario; una máquina no puede, y ahí está el problema.

## 2. Por qué importan: la ambigüedad

El mismo esqueleto de consonantes puede ser varias palabras distintas. El ejemplo clásico:

- كتب sin diacríticos puede ser **كَتَبَ** *kataba* ("él escribió"), **كُتِبَ** *kutiba* ("fue escrito") o **كُتُب** *kutub* ("libros").

La vocal final, además, marca el caso gramatical (*iʿrāb*): el sujeto lleva ḍamma, el objeto fatḥa, el genitivo kasra. Equivocarse en la última vocal es equivocarse en la función de la palabra en la frase.

La ambigüedad no es un caso raro: en el benchmark WikiNews-2024, 785 palabras (el 7%) admiten más de una diacritización válida, revisada por lingüistas expertos. Incluso los expertos discrepan: la diacritización correcta depende del contexto y, a veces, de la interpretación.

## 3. La tarea: diacritización automática

La tarea es restaurar los diacríticos de un texto que no los trae. Se mide con dos métricas:

- **DER** (Diacritic Error Rate): porcentaje de diacríticos predichos mal, por marca.
- **WER** (Word Error Rate): porcentaje de palabras con al menos un diacrítico mal.

Regla de lectura: los números solo se comparan dentro del mismo benchmark. Cada benchmark tiene su propio género de texto y sus propias reglas de anotación; un 3% en WikiNews no es lo mismo que un 3% en Tashkeela.

Para qué sirve: síntesis de voz (TTS) que pronuncie bien, herramientas educativas para estudiantes de árabe, ayudas a la lectura, traducción automática y reconocimiento de voz.

## 4. Los datos

| Corpus / benchmark | Qué es | Tamaño |
|---|---|---|
| Tashkeela (Zerrouki y Balla 2017) | Corpus de textos árabes totalmente vocalizados, 97 libros | 75.629.921 palabras; 98,85% árabe clásico (74.762.008 palabras), 1,15% árabe estándar moderno (867.913 palabras); ~2,05 vocalizaciones por palabra de media |
| Subconjunto limpio de Tashkeela (Fadel et al. 2019) | Versión depurada y libre para comparar sistemas | 55.000 líneas, ~2,3 millones de palabras |
| WikiNews-2014 / WikiNews-2024 (Mohamed y Mubarak 2025) | Benchmark estándar, revisado por dos lingüistas expertos; el de 2024 añade evaluación multirreferencia | Corpus diacritizado de 5 millones de palabras liberado con el paper |
| CATT (Alasmary et al. 2024) | Benchmark de noticias, diacritizado a mano por dos nativos expertos y revisado por un tercero | 742 frases |
| SadeedDiac-25 (2026) | Benchmark nuevo, árabe clásico y estándar moderno, curado por expertos | Ver FUENTES.md |

El sesgo es el dato más importante de la tabla: casi todo el texto diacritizado que existe es árabe clásico (libros islámicos clásicos de la biblioteca Shamela). El árabe estándar moderno es el 1,15% del corpus mayor, y el árabe dialectal (egipcio, del Golfo, levantino) apenas aparece.

## 5. Modelos y herramientas

| Herramienta | Tipo | Qué es |
|---|---|---|
| Mishkal | Reglas | Vocalizador de código abierto (Taha Zerrouki). Analiza todos los casos morfológicos con Qalsadi y el diccionario Arramooz, genera las formas posibles y pondera por frecuencia. |
| Farasa | Estadístico | Diacritizador de QCRI. Demo web y API REST; paquete Java. |
| Shakkala | Red neuronal | RNN para vocalizar texto árabe (Barqawi y Zerrouki 2017). DER 2,88% en el test limpio de Tashkeela, frente a 13,78% de Mishkal. |
| CATT | Transformer | BERT a nivel de carácter + autoentrenamiento (Noisy-Student). Abjad Ltd. 2024. Código y benchmark abiertos. |
| Sukoun / SukounBERT.v2 | Transformer | Sistema basado en BERT (Univ. de Sharjah). El v2 se entrena con el corpus Sukoun: 5,2 millones de líneas, 71 millones de tokens. |
| Fine-Tashkeel | Transformer | ByT5 ajustado a nivel de byte; resiste las variaciones ortográficas de los dialectos. Dataset JODA de árabe jordano: 59.135 frases. |
| Sadeed | Modelo pequeño de lenguaje | Decoder-only ajustado desde Kuwain 1.5B, con datos diacritizados curados y limpiados. 2026. |
| CAMeL Tools | Toolkit | Suite de PLN árabe de NYU Abu Dhabi (preproceso, morfología, dialectos, NER, sentimiento). Incluye diacritización entre sus herramientas; sus modelos CAMeLBERT cubren MSA, dialectal y clásico. |

## 6. Estado del arte, por benchmark

| Benchmark | Mejor resultado reportado | Sistema |
|---|---|---|
| WikiNews-2014 | WER 3,12%, DER 0,90% | BiLSTM de Mohamed y Mubarak (EMNLP 2025) |
| WikiNews-2024 | WER 2,70%, DER 0,94% | Mismo sistema |
| WikiNews-2014, referencia única | Sistema 3,61% WER / 0,93% DER; Farasa 11,50% / 3,06%; GPT-4o 8,55% / 3,31%; Seq2Seq (Mubarak 2019) 4,49% / 1,21% | Comparativa de Mohamed y Mubarak 2025 |
| Conjunto AD (Fadel 2019) | DER sintáctica 1,14%, WER 3,34% | Sukoun (Kharsa et al. 2024) |
| Test limpio de Tashkeela | DER 2,88% (Shakkala) frente a 13,78% (Mishkal) | Fadel et al. 2019 |
| CATT | Supera al mejor de 11 modelos en 30,83% (WikiNews) y 35,21% (CATT) de DER relativa; supera a GPT-4-turbo en 9,36% de DER relativa en CATT | Alasmary et al. 2024 |
| SukounBERT.v2 | Reducción relativa de DER y WER superior al 55% frente a los modelos líderes | Univ. de Sharjah, 2026 |

Dos lecturas que importan más que los números:

1. **Los modelos generales de lenguaje son mucho peores que los especializados.** GPT-4o tiene 8,55% de WER donde el sistema especializado tiene 3,61% (WikiNews-2014). En Tashkeela, un BiLSTM especializado reporta 6,6% de DER frente a 20,9% de GPT-5.3 (cifras de la propia página del modelo, no verificación independiente).
2. **Los números no se comparan entre benchmarks.** Cada fila de la tabla es un mundo: distinto texto, distintas reglas. Lo que sí se puede decir es que el estado del arte en noticias (MSA) ronda el 3% de WER, y que lo basado en reglas (Mishkal ~14-15% de DER) quedó atrás de lo neuronal.

## 7. Límites

- **Sesgo clásico.** El 98,85% de Tashkeela es árabe clásico. El rendimiento en árabe estándar moderno es peor, y en dialectos (egipcio, del Golfo, levantino) no está medido en la mayoría de los modelos: la propia página de arabic-diacritizer dice que su rendimiento en dialectos no está probado. Fine-Tashkeel es la excepción que intenta cubrir dialecto (jordano).
- **La terminación de caso es lo más difícil.** La vocal final depende de la sintaxis de toda la frase, no de la palabra sola.
- **El usuario ya trae marcas.** Un texto real puede venir parcialmente diacritizado; el sistema debe respetar las marcas que el usuario ya puso. El modelo de Mohamed y Mubarak 2025 es robusto a eso; no todos lo son.
- **Diacritizar no es pronunciar bien.** Restaurar las marcas no garantiza la pronunciación correcta de palabras dialectales ni de nombres propios.
- **Farasa exige registro** para descargar; su demo web es la vía libre.

## 8. NO SÉ

- Si existe un dataset diacritizado de árabe dialectal egipcio. El stub sitúa el tema en Egipto, y no encontré ningún benchmark ni corpus diacritizado de árabe egipcio. Es el hueco más claro de este nutriente.
- El coste y la latencia de correr estos modelos en producción: no hay números medidos en las fuentes consultadas.
- Si la demo y la API de Farasa siguen vivas hoy: la página exige registro para descargar y la demo no se probó en vivo.
- El rendimiento real de cualquiera de estos sistemas sobre texto egipcio cotidiano (redes sociales, prensa egipcia).
- Qué herramienta conviene hoy para un caso concreto: las comparativas citadas usan benchmarks distintos, así que no hay un ganador único con fuente. Por benchmark: en noticias MSA, el BiLSTM de Mohamed y Mubarak 2025; en código abierto usable, CATT, Shakkala y Mishkal.

---

*Fuentes con URL y fecha en [FUENTES.md](FUENTES.md). Solo SÉ con fuente; lo demás, NO SÉ.*
