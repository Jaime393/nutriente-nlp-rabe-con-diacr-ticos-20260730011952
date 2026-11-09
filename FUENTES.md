# Fuentes — NLP árabe con diacríticos

Verificadas el 2026-11-09. Cada número del README viene de una de estas fuentes; nada más se afirma.

## Corpus y datos

1. **Zerrouki y Balla (2017), "Tashkeela: Novel corpus of Arabic vocalized texts"**, *Data in Brief* 11, pp. 147–151.
   URL: https://pmc.ncbi.nlm.nih.gov/articles/PMC5310197/
   Afirma: 75.629.921 palabras en 97 libros; 98,85% árabe clásico (74.762.008 palabras), 1,15% árabe estándar moderno (867.913 palabras); ~2,05 vocalizaciones por palabra de media; corpus libre en tashkeela.sourceforge.net.

2. **Fadel et al. (2019), "Arabic Text Diacritization Using Deep Neural Networks"**, 2nd International Conference on Computer Applications & Information Security (ICCAIS).
   URL: https://explore.openaire.eu/search/result?id=doi_dedup___::dc6ade34fc741ee3e7dfd0ab8d61e04f
   Afirma: subconjunto limpio de Tashkeela de 55.000 líneas y ~2,3 millones de palabras; en su test, Shakkala DER 2,88% frente a Mishkal 13,78% (mejor no-neuronal).

## Papers de modelos y benchmarks

3. **Mohamed y Mubarak (2025), "Advancing Arabic Diacritization: Improved Datasets, Benchmarking, and State-of-the-Art Models"**, *Proceedings of EMNLP 2025*, pp. 16707–16719, 4–9 nov 2025.
   URL: https://preview.aclanthology.org/dashboard/2025.emnlp-main.846.pdf
   Afirma: benchmark WikiNews-2024 con evaluación multirreferencia; modelo BiLSTM con WER 3,12% (WikiNews-2014) y 2,70% (WikiNews-2024); corpus diacritizado de 5 millones de palabras liberado; 785 palabras (7%) de WikiNews-2024 admiten varias diacritizaciones válidas; comparativa de referencia única (sistema propio 3,61%/0,93%; Farasa 11,50%/3,06%; GPT-4o 8,55%/3,31%; Seq2Seq Mubarak 2019 4,49%/1,21%).

4. **Alasmary, Zaafarani y Ghannam (2024), "CATT: Character-based Arabic Tashkeel Transformer"**, arXiv:2407.03236, 3-jul-2024.
   URL: https://arxiv.org/pdf/2407.03236
   Afirma: BERT a nivel de carácter + Noisy-Student; supera al mejor de 11 modelos en 30,83% (WikiNews) y 35,21% (CATT) de DER relativa; supera a GPT-4-turbo en 9,36% de DER relativa en el dataset CATT; benchmark CATT de 742 frases, diacritizado por dos expertos nativos y revisado por un tercero; entrenamiento con todo Tashkeela (1.658.325 muestras); código en https://github.com/abjadai/catt.

5. **Kharsa et al. (2024), "BERT-Based Arabic Diacritization"**, *ScienceDirect* (Expert Systems with Applications).
   URL: https://www.sciencedirect.com/science/article/pii/S0957417424002811
   Afirma: sistema Sukoun basado en BERT; DER sintáctica 1,14% y WER 3,34% en el conjunto AD (Fadel et al. 2019); compara cinco BERT (Multi-BERT, CAMeLBERT-MSA, CAMeLBERT-MIX, CAMeLBERT-CA, AraBERTv0.2-base).

6. **Universidad de Sharjah (2026), "SukounBERT.v2"**, nota en Scimex, 4-feb-2026. Publicado en *Information Processing and Management*.
   URL: https://www.scimex.org/newsfeed/new-ai-model-enables-native-speakers-and-foreign-learners-to-read-undiacritized-arabic-texts-with-greater-fluency
   Afirma: corpus Sukoun de más de 5,2 millones de líneas y 71 millones de tokens; reducción relativa de DER y WER superior al 55% frente a los modelos líderes.

7. **"Fine-Tashkeel: Fine-Tuning Byte-Level Models for Accurate Arabic Text Diacritization"** (ResearchGate).
   URL: https://www.researchgate.net/publication/372616004_Fine-Tashkeel_Fine-Tuning_Byte-Level_Models_for_Accurate_Arabic_Text_Diacritization
   Afirma: ByT5 ajustado a nivel de byte; dataset JODA de árabe jordano con 59.135 frases; CER 4,64% en Test-200; compara seis herramientas (CAMeL Tools, Farasa, Mishkal, i2Text 2, Fine-Tashkeel, Shakkelha).

8. **"Sadeed: Advancing Arabic Diacritization Through Small Language Model"**, arXiv:2504.21635, 24-ago-2026.
   URL: https://arxiv.org/html/2504.21635v1
   Afirma: modelo decoder-only ajustado desde Kuwain 1.5B con datos diacritizados curados y limpiados; benchmark nuevo SadeedDiac-25 (árabe clásico y estándar moderno, curado por expertos); SOTA en WER en el dataset Fadel.

## Herramientas

9. **Mishkal**, PyPI 0.1.
   URL: https://pypi.org/project/mishkal/0.1/
   Afirma: vocalizador árabe de código abierto, basado en reglas; repo https://github.com/linuxscout/mishkal.git; usa Qalsadi (analizador morfológico) y Arramooz (diccionario); corpus Tashkeela.

10. **Shakkala**, PyPI.
    URL: https://pypi.org/project/shakkala/
    Afirma: red neuronal recurrente para vocalizar texto árabe; repo https://github.com/Barqawiz/Shakkala; Barqawi y Zerrouki (2017); probado con TensorFlow 2.9.3.

11. **Farasa — Diacritization Module**, QCRI.
    URL: https://farasa.qcri.org/diacritization/
    Afirma: módulo de diacritización con demo web y API REST (`/webapi/diacritize/`); paquete Java (`FarasaDiacritizeJar.jar`); la descarga exige registro.

12. **CAMeL Tools**, PyPI 1.5.7, 17-sep-2025.
    URL: https://pypi.org/project/camel-tools/1.5.7/
    Afirma: suite de PLN árabe del CAMeL Lab, New York University Abu Dhabi; repo https://github.com/CAMeL-Lab/camel_tools.git; licencia MIT; preproceso, morfología, dialectos, NER y sentimiento.

13. **CAMeLBERT**, Hugging Face.
    URL: https://huggingface.co/CAMeL-Lab/bert-base-arabic-camelbert-msa-half
    Afirma: colección de modelos BERT preentrenados para árabe: MSA, dialectal, clásico y mezcla; pensados para ajuste fino en tareas de PLN.

14. **arabic-diacritizer**, PyPI 1.0.0, 13-mar-2026.
    URL: https://pypi.org/project/arabic-diacritizer/1.0.0/
    Afirma (autoinforme del autor, no verificación independiente): BiLSTM + atención Bahdanau, DER 6,6% frente a 20,9% de GPT-5.3 en el test de Tashkeela; repo https://github.com/Z-Mahmood/arabic-diacritizer-public-release.git; rendimiento en dialectos no probado.

## Lengua (inventario de marcas y ejemplos)

15. **"Short Vowels (Harakat) in Arabic"**, SettemilaLingue.
    URL: https://www.settemilalingue.com/en/languages/ar/grammar/short-vowels-harakat
    Afirma: fatḥa /a/, kasra /i/, ḍamma /u/, sukūn (sin vocal), shadda (consonante doble); el árabe cotidiano se escribe sin ellas; كتب puede ser كَتَبَ *kataba*, كُتِبَ *kutiba* o كُتُب *kutub*.

16. **"Arabic Vowels & Diacritics"**, Fahm.
    URL: https://www.fahm.app/grammar/g002/
    Afirma: corrobora el inventario (fatḥa, ḍamma, kasra, sukūn, shadda, tanwīn con -an/-in/-un) y los ejemplos كَتَبَ / كُتُب.
