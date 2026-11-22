# Los productos naturales en la base de datos LOTUS

LOTUS es una base de datos abierta creada por el grupo de  ***Quimioinformática y metabolómica computacional*** de la **Universidad Friedich Schiller** en Jena, Alemania; con el propósito de crear un repositorio de moléculas de origen natural disponible para todas las personas que deseen realizar investigaciones relacionadas con los productos naturales de plantas, hongos y animales.<sup>1</sup> LOTUS contiene más de 270 mil entradas, reportando datos de estructuras, nombres científicos, nombres comunes, el organismo en el cual aparece, su taxonomía, propiedades físicas, etcétera. 

> Esta base de datos está construida sobre **MongoDB**, es de tipo ***no relacional*** y está disponible para su consulta [aquí](https://lotus.naturalproducts.net/)

No solo eso, LOTUS cuenta con una API REST para realizar consultas. Se pueden hacer búsquedas de tres maneras diferentes:

**1. Búsqueda exacta**

---

Se ingresa un código SMILES (una estrategia de abstracción para las estructuras químicas) de la molécula que se quiere buscar por la base de datos. Esta API tiene dos métodos de búsqueda: 1. Usando InChI (Identificador Químico Internacional) como método de coincidencia, y 2. Usando el SMILES como método de coincidencia.

- Caso 1: `https://lotus.naturalproducts.net/api/search/exact-structure?type=inchi&smiles=O=C1OC(C(O)=C1O)CO` 

- Caso 2: 
`https://lotus.naturalproducts.net/api/search/exact-structure?type=smiles&smiles=O=C1OC(C(O)=C1O)CO`  

**2. Búsqueda simple**

---

En este caso, se emplean querys sencillas, como preguntar el LOTUS ID, la clave InChI, el código InChI o el nombre de la molécula:

- `https://lotus.naturalproducts.net/api/search/simple?query=LTS0253154`

**3. Búsqueda por subestructura**

---

Los productos naturales son como una torre de LEGOs: están construidos por bloques representados por un SMILES (un trocito de molécula), y esos bloques son las subestructuras. La API REST de LOTUS permite buscar moléculas por subestructura, ajustando el algoritmo de búsqueda por:
- a) `type`:
    - `default` (Algoritmo de Ullmann): La opción por defecto
    - `df` (Búsqueda en profundidad): Grafos y árboles (*backtracing*)
    - `vf` (Algoritmo de Vento-Foggia)
- b) `max-hits`:
    - Es el máximo de productos naturales a mostrar (tipo `int`)

Ejemplo: `https://lotus.naturalproducts.net/api/search/substructure?type=default&max-hits=100&smiles=O=C1OC(C(O)=C1O)CO`

# Graficando las moléculas con RDKit y Py3DMol


**RDKit** es un programa de acceso abierto (Open Source) para quimioinformática y machine learning, desarrollado por Greg Landrum y los contribuidores de la comunidad de RDKit. Este programa permite manipular moléculas, calcular sus propiedades, visualizarlas, compararlas y ejecutar reacciones químicas.<sup>2</sup>

Repositorio de RDKit: https://github.com/rdkit 

Por otro lado, **Py3DMol** es un motor de visualización de estructuras moleculares en 3D de forma interactiva. Está diseñado a partir de 3Dmol.js para integrarse en Jupyter Notebooks, Google Colab o scripts de Python.<sup>3</sup>

Todo sobre Py3DMol: https://colab.research.google.com/drive/1T2zR59TXyWRcNxRgOAiqVPJWhep83NV_?usp=sharing

# ¿Cómo usar los notebooks?

Creé un notebook principal que funciona como un circuito: cada consulta puede ejecutarse de manera independiente, ya que la notebook está pensada para poder utilizar datos provenientes de una consulta por SMILES o por nombre. 

# Referencias

1) Rutz, A.; Sorokina, M.; Galgonek, J.; Mietchen, D.; Willighagen, E.; Gaudry, A.; Graham, J. G.; Stephan, R.; Page, R.; Vondrášek, J.; Steinbeck, C.; Pauli, G. F.; Wolfender, J.-L.; Bisson, J.; Allard, P.-M. The LOTUS Initiative for Open Knowledge Management in Natural Products Research. eLife **2022**, *11*, e70780. https://doi.org/10.7554/eLife.70780

2) RDKit: Open Source cheminformatics. https://www.rdkit.org 

3) Rego, N.; Koes, D. 3Dmol.Js: Molecular Visualization with WebGL. Bioinformatics **2015**, *31* (8), 1322–1324. https://doi.org/10.1093/bioinformatics/btu829
