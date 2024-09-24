Este archivo Jupyter implementa un conjunto de ejemplos que demuestran el uso de la librería PyLaTeX para la generación de documentos en formato LaTeX. A continuación se describen los principales bloques de código y las funcionalidades que se desarrollan:

1. Generación básica de un documento LaTeX:
Se importa la librería pylatex para la creación de un documento en LaTeX.
Se define una función fill_document(doc) que inserta una sección y subsección con texto formateado (incluyendo cursivas).
Se crea un documento con el nombre "EjemploBasico.pdf" y "EjemploBasico.tex", donde se utiliza una estructura básica con el título, autor y fecha. El contenido incluye:
Una sección principal con texto normal y en cursiva.
Una subsección con caracteres especiales como %, &, y $.
2. Uso de herencia para extender el documento:
Se crea una clase MiDocumento, que hereda de Document de la librería pylatex.
La clase extiende la funcionalidad de Document para agregar más personalización, como texto en negrita y cursiva.
Además, se añade una nueva sección dentro del documento utilizando métodos de la clase.
El archivo generado es "Basico con herencia.pdf" y "Basico con Herencia.tex".
Documentación del código:
python
Copiar código
from pylatex import Command, Document, Section, Subsection
from pylatex.utils import NoEscape, italic

def fill_document(doc):
    """
    Función para llenar el documento con contenido estructurado.
    - Sección principal con texto en cursiva y subsección.
    """
    with doc.create(Section("Una Seccion")):
        doc.append("Texto interno de la seccion")
        doc.append(italic("Texto en cursiva"))
        with doc.create(Subsection("Una subseccion")):
            doc.append("Una Subseccion con otros caracteres: %&$&%$&()")

# Creación y configuración básica del documento
doc = Document("Basico")
doc.preamble.append(Command("title", "Cheatsheets ejemplo"))
doc.preamble.append(Command("author", "Raul Mamani Cusi"))
doc.preamble.append(Command("date", NoEscape(r"\today")))
doc.append(NoEscape(r"\maketitle"))

# Llenado del contenido y generación de archivos
fill_document(doc)
doc.generate_pdf("EjemploBasico.pdf")
doc.generate_tex("EjemploBasico.tex")

# Output del contenido en formato LaTeX
tex = doc.dumps()
tex
3. Herencia:
python
Copiar código
from pylatex import Command, Document, Section, Subsection
from pylatex.utils import NoEscape, italic, bold

class MiDocumento(Document):
    """
    Clase que hereda de Document para generar un documento personalizado.
    Añade más contenido y permite la reutilización del código base.
    """
    def __init__(self):
        super().__init__()
        self.preamble.append(Command("title", "Cheatsheets ejemplo 2 (Heredado)"))
        self.preamble.append(Command("author", "Raul Mamani Cusi"))
        self.preamble.append(Command("date", NoEscape(r"\today")))
        self.append(NoEscape(r"\maketitle"))

    def fill_document(self):
        with self.create(Section("Una Seccion")):
            self.append("Texto interno de la seccion")
            self.append(italic("Texto en cursiva"))
            self.append(bold("Texto en Negrilla"))
            with self.create(Subsection("Una subseccion")):
                self.append("Una Subseccion con otros caracteres: %&$&%$&()")

# Crear una instancia de la clase
doc = MiDocumento()
doc.fill_document()

# Añadir nueva sección
with doc.create(Section("Una nueva seccion")):
    doc.append("Otro texto añadido despues")

# Generar los archivos
doc.generate_pdf("Basico con herencia.pdf")
doc.generate_tex("Basico con Herencia.tex")
Este ejemplo demuestra cómo utilizar PyLaTeX para crear documentos con secciones, subsecciones, texto en negrita y cursiva, además de cómo gestionar la herencia para extender la funcionalidad
