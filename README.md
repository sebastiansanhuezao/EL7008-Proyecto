# Proyecto Final: Recuperación de Imágenes (Image Retrieval)

Este repositorio contiene el proyecto final para el curso **EL7008 - Procesamiento Avanzado de Imágenes** de la **Universidad de Chile**. El proyecto evaluó distintas estrategias para la tarea de **Recuperación de Imágenes (Image Retrieval)** utilizando los datasets **ROxford** y **RParis** [[1]](#referencias). Estos datasets fueron obtenidos del [repositorio oficial](https://github.com/filipradenovic/revisitop) del paper que los introdujo.

## Metodología
Se evaluaron tres estrategias principales para resolver la tarea de Recuperación de Imágenes:

1. **Bag-of-Visual-Words (BoVW)**: Técnica clásica inspirada en el modelo de **Bag-of-Words** del procesamiento de texto, donde las imágenes se representan como colecciones de características locales codificadas como "palabras visuales" [[2]](#referencias).

2. **Características de CNN**: Extracción de características a partir de un modelo **ResNet50 preentrenado**, capaz de capturar representaciones abstractas de las imágenes [[3]](#referencias).

3. **Mejoras sobre CNN**: Uso de capas avanzadas como **GeM Pooling** (*Generalized Mean Pooling*) y técnicas de **re-ranking** como **k-reciprocal encoding** para optimizar el rendimiento [[4]](#referencias)[[5]](#referencias).


El análisis se realizó mediante métricas como el mAP y una evaluación cualitativa de las consultas mejor y peor recuperadas. Adicionalmente, con las características extraídas del mejor modelo, se investigó el impacto de diferentes técnicas de indexación en la eficiencia y eficacia de la búsqueda, incluyendo métodos de reducción de dimensionalidad como PCA (*Principal Component Analysis*).

## Resultados

### Resultados Cuantitativos: Mean Average Precision (mAP)

La siguiente tabla muestra el desempeño promedio (*mean Average Precision*, mAP) de cada estrategia en la categoría *easy* de los datasets **ROxford** y **RParis**:

|          **Estrategia**         | **ROxford (mAP)** |  **RParis (mAP)** |
|:-------------------------------:|:-----------:|:-----------:|
|               BoVW              |    24.17%   |    50.87%   |
|        ResNet50 Features        |    38.95%   |    74.18%   |
| ResNet50 + R-MAC + k-reciprocal | **59.79%** | **81.87%** |

#### **Análisis:** 
- La estrategia más efectiva combinó características extraídas con **ResNet50**, una capa de **R-MAC Pooling** [[6]](#referencias), y la técnica de re-ranking **k-reciprocal encoding** [[5]](#referencias).
- El uso de estas técnicas mejoró significativamente el rendimiento sobre las estrategias más simples como BoVW.

### Resultados Cualitativos: Evaluación de Consultas

Se seleccionaron las mejores y peores consultas recuperadas para cada estrategia, extrayendo el top-5 de imágenes recuperadas. A continuación, se muestra un ejemplo del dataset **RParis**:

#### **Estrategia 1: Bag-of-Visual-Words (BoVW)**
![](/Figuras/queries_estrategia_1.png)

#### **Estrategia 2: ResNet50 Features**
![](/Figuras/queries_estrategia_2.png)

#### **Estrategia 3: ResNet50 + R-MAC + k-reciprocal**
![](/Figuras/queries_estrategia_3.png)



## Referencias
1. Radenović, F., Iscen, A., Tolias, G., Avrithis, Y., y Chum, O., "Revisiting oxford and paris: Large-scale image retrieval benchmarking", en Proceedings of the IEEE Conference on Computer Vision and Pattern Recognition (CVPR), pp. 5706–5715, 2018.
2. Csurka, G., Dance, C., Fan, L. X., Willamowski, J., y Bray, C., "Visual categorization with bags of keypoints", en Proceedings of the ECCV International Workshop on Statistical Learning in Computer Vision, pp. 1–22, 2004.
3. He, K., Zhang, X., Ren, S., y Sun, J., “Deep residual learning for image recognition”, arXiv preprint arXiv:1512.03385, 2015, [https://doi.org/10.48550/arXiv.1512.03385](https://doi.org/10.48550/arXiv.1512.03385). Tech report.
4. Radenović, F., Tolias, G., y Chum, O., "Fine-tuning cnn image retrieval with no human annotation", arXiv preprint arXiv:1711.02512, 2017, [https://arxiv.org/abs/1711.02512](https://arxiv.org/abs/1711.02512).
5. Zhong, Z., Zheng, L., Cao, D., y Li, S., "Re-ranking person re-identification with k-reciprocal encoding", en Proceedings of the IEEE Conference on Computer Vision and Pattern Recognition (CVPR), pp. 1318–1327, 2017.
6. Tolias, G., Sicre, R., y Jégou, H., “Particular object retrieval with integral max-pooling of cnn activations”, arXiv preprint arXiv:1511.05879, 2015, [https://arxiv.org/abs/1511.05879](https://arxiv.org/abs/1511.05879).
