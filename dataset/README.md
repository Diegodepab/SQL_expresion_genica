Nuestra base de datos está compuesta por las siguientes tablas:
1. Pacientes
- id_paciente: este atributo es la primary key (valor de tipo integer). Servirá para identificar de manera única a los pacientes.
- nombre: este atributo hace referencia al nombre del paciente (valor de tipo varchar). Nos será útil a la hora de realizar las consultas para saber información pertinente de un paciente.
- apellidos: este atributo almacena los apellidos del paciente (valor de tipo varchar). Cumple la misma función que ‘nombre’.
- edad: este atributo almacena la edad del paciente en años (valor de tipo integer). Factor importante para el diagnóstico del cáncer de mama CDI a la hora de llevar a cabo decisiones clínicas.
- género: este atributo almacena el género del paciente (valor de tipo ENUM). Ciertos tratamientos pueden ser más efectivos o tener diferentes efectos secundarios según el género del paciente.
2.Muestras
- id_muestras: este atributo es la primary key (valor de tipo integer). Almacena el código asignado a la muestra. Servirá para identificar de manera única cada muestra.
- descripcion: proporciona una descripción detallada de la muestra (valor de tipo varchar). Puede incluir información como el tipo de tejido, la ubicación de la recolección o cualquier otro detalle relevante de la muestra. 
- fecha_recoleccion: Almacena la fecha en la que se recolectó la muestra (valor de tipo date). Este atributo es importante para registrar el momento en que se tomó la muestra. Relevante para registrar la vida útil de la muestra.
- condiciones: describe las condiciones bajo las que se recolectó la muestra , como el estado de salud del paciente, el tratamiento recibido, la etapa de la enfermedad, etc... (valor de tipo varchar).
- Pacientes_id_paciente: este atributo es la foreign key heredada de los Pacientes. Almacena el id del paciente sobre el que se recolectó la muestra.
3.Genes (relacionados con el cáncer de mama CDI)
- id_gen: este atributo es la primary key. Servirá para identificar de manera única cada gen (valor de tipo integer).
- gen_symbol: Almacena el símbolo o nombre del gen (valor de tipo varchar). Útil para identificar y referirse a un gen específico de manera abreviada.
4.ExpresionGenica:
- Genes_id_gen y Muestras_id_muestras: estos atributos son las foreign key heredadas de Muestras y Genes, además de ser una primary key compuesta de la tabla.
- Nivel_expresion:  se refiere a la cantidad relativa de ARN mensajero producido a partir de un gen en particular en una muestra (valor de tipo varchar).
5.   GenesInteres
- Genes_id_gen: este atributo es la primary key. Servirá para identificar de manera única cada gen (valor de tipo integer).
- description: proporciona una descripción detallada de los genes de los cuales se están haciendo un estudios (valor de tipo varchar). 
- Cromosoma: Este atributo ubica el gen con su respectivo número de cromosoma  (valor de tipo integer).

Relaciones entre las tablas.
- Pacientes y Muestras: relación débil de 1 a N, dado que las muestras sólo pueden tener un paciente asociado, pero se pueden sacar varias muestras del mismo (No puede existir una muestra que no esté vinculada a un paciente).
- Muestras y ExpresionGenica: relación débil de 1 a N, dado que una muestra puede contener distintos niveles de expresión de varios genes. Y la expresión génica es relativa a cada muestra. (No sé puede catalogar la expresión de un gen en una muestra sin esta).
- Genes y ExpresionGenica: relación débil de 1 a N, dado que un gen puede tener distintos niveles de expresión para cada muestra. (Necesitas un gen al cual estudiar su Expresion Genica).
- Genes y GenesInteres: relación débil de 1 a N, dado que un gen puede tener distintos niveles de expresión para cada muestra.

Funcionalidades que debería cumplir:
1. Registro y Gestión de Pacientes:
- Permitir la creación, actualización y eliminación de registros de pacientes, incluyendo información como nombre, apellidos, edad y género.
- Facilitar la búsqueda y recuperación de información de pacientes para apoyar la toma de decisiones clínicas.
 
2. Registro y Gestión de Muestras:
- Permitir el registro de nuevas muestras, incluyendo información detallada como nombre, descripción, fecha de recolección, condiciones de recolección y genes presentes.
- Facilitar la búsqueda y recuperación de muestras basadas en criterios como el paciente asociado, la fecha de recolección o los genes presentes.
 
3. Registro y Gestión de Genes:
- Permitir el registro de nuevos genes relacionados con el cáncer de mama, incluyendo información como símbolo, descripción, cromosoma y posición.
-  Facilitar la búsqueda y recuperación de información de genes para apoyar la investigación y el análisis de datos.
 
4. Registro y Gestión de Expresión Génica:
- Registrar los niveles de expresión génica para cada gen en cada muestra, incluyendo información sobre la cantidad relativa de ARN mensajero producido.
- Mantener una relación adecuada entre las muestras, los genes y los niveles de expresión para permitir un análisis detallado de los datos de expresión génica.
 
Restricciones:
Restricciones de Integridad:
- Garantizar que las relaciones entre las tablas se mantengan correctamente. Por ejemplo, cada muestra debe estar asociada con un paciente válido y cada gen presente en la tabla de Expresión Genética debe existir en la tabla de Genes.
- Utilizar claves foráneas para establecer y mantener estas relaciones, y configurar acciones de restricción (como ON DELETE CASCADE o ON UPDATE CASCADE) (esto es básicamente para evitar errores, como el caso de que algunos atributos que sean heredados se eliminen del padre, pero no de los hijos y lo evitamos con ON DELETE CASCADE).
Restricciones de Unicidad:
- Evitar la duplicación de datos y garantizar que ciertos atributos sean únicos. Por ejemplo, una restricción de unicidad en el dni de un paciente para evitar que se registren pacientes con el mismo dni más de una vez.
- Utilizar restricciones de clave única en los atributos que deben ser únicos, como dni o códigos de muestras.
Restricciones de Valor:
- Asegurarse de que los valores ingresados en ciertos campos cumplan con ciertos criterios específicos. Por ejemplo, la edad de un paciente no debería ser un número negativo u overflow.
- Utilizar restricciones de verificación o comprobaciones de integridad para validar los valores ingresados en la base de datos.

