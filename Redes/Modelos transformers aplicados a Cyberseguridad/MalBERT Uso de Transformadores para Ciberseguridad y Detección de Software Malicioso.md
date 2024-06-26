
# Abstrac

> [!summary] +
Se propone el uso de una arquitectura de Transformers para detectar automáticamente software malicioso. Se propone un modelo basado en BERT (Bidireccional Encoder. Representations from Transformers) que realiza un análisis estático sobre el código fuente de las aplicaciones Android utilizando características preprocesadas para caracterizar el malware existente y clasificarlo en diferentes categorías de malware representativo 

# Introduction

> [!summary]
> IBM informó que el costo promedio de una violación de datos es de $3.86 millones a partir de 2020, sin embargo, el tiempo promedio para identificar una violación fue de 207 días [[1](https://ar5iv.labs.arxiv.org/html/2103.03806#bib.bib1)]. Como resultado, los profesionales e investigadores de seguridad de TI deben actualizar las herramientas disponibles para detectar automáticamente nuevos ataques de malware.
> Se realizaron una serie de estudios para resolver este problema. Se utilizaron diferentes experimentos de análisis a nivel estático, dinámico e híbrido [[2](https://ar5iv.labs.arxiv.org/html/2103.03806#bib.bib2)] para extraer varios tipos de características
> El tipo ampliamente utilizado es el análisis estático. Para el análisis estático, existen principalmente tres prácticas para detectar y clasificar malware: Basado en permisos (verifique si los permisos solicitados son necesarios para que la aplicación garantice el comportamiento normal en el acceso a la aplicación y el uso de los datos del usuario), Basado en firmas (identifique si la firma de la aplicación coincide con una de las firmas de malware entre la biblioteca recopilada de antemano),y basado en especificaciones (verifique si la aplicación viola las reglas establecidas por los expertos para decidir la malicia de un programa bajo inspección).
> En este documento, proponemos un enfoque de detección de malware utilizando un algoritmo basado en Transformer. Experimentamos con diferentes arquitecturas de modelos Transformer en nuestros datos. El conjunto de datos incluye 11 categorías diferentes de malware, a saber, adware, spyware, ransomware, clicker, dropper, downloader, riskware, SMS-sender, horse-trojan, backdoor y banker [[9](https://ar5iv.labs.arxiv.org/html/2103.03806#bib.bib9)].

