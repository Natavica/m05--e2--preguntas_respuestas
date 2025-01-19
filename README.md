# m05--e2--preguntas_respuestas
Sesión Interactiva de Preguntas y Respuestas: Introducción a TypeScript en ReactJS

# Integrantes:
- Felipe Pineda
- Denisse Rossel
- Natalia Albornoz

## 1. Preguntas Teóricas sobre TypeScript

### - ¿Qué es TypeScript y para qué se utiliza?
TypeScript es un lenguaje de programación considerado una extensión de JavaScript, el cual agrega tipado estático, interfaces y decoradores. Esto significa que permite definir tipos de datos (como números o cadenas de texto) y proporciona herramientas para estructurar el código de manera más segura y organizada. TypeScript se utiliza para escribir aplicaciones más robustas y fáciles de mantener, y luego se compila a JavaScript para ser ejecutado en navegadores o servidores.

TypeScript es un lenguaje de programación, el cual es una extensión de JavaScript que principalmente añade tipado estático, interfaces y decoradores a JavaScript.

### - ¿Cuáles son las principales diferencias entre TypeScript y JavaScript?
- **Tipado Estático**: TypeScript permite definir tipos de datos (como números, cadenas de texto, objetos), lo que ayuda a detectar errores antes de ejecutar el código. En cambio, JavaScript es dinámico, permitiendo la asignación de cualquier tipo de datos a las variables, entendiendo por tipo de datos no solamente los tipos primitivos sino cualquier dato (tipos primitivos, arreglos, objetos, etc.). Estos al no ser detectados en una etapa temprana, puede generar errores que son detectados en tiempos de ejecución, incluso en entornos de producción.
  
- **Proceso de transpilación**: Antes de ejecutar el código en un navegador, TypeScript necesita ser transpilado a JavaScript, para posteriormente ser ejecutado por los distintos tipos de navegadores. En cambio, JavaScript es considerado un lenguaje de scripting, lo que significa que sus instrucciones son ejecutadas directamente en el entorno de ejecución (navegador o node) sin un proceso previo de compilación.

### - ¿Por qué es útil TypeScript en el desarrollo de aplicaciones ReactJS?
Ayuda a escribir código más claro y seguro.  
El tipado permite encontrar errores en tiempos de desarrollo, mientras que en JavaScript los errores por tipado de datos se encuentran en tiempo de ejecución.  
Además, facilita la organización del código y mejora la experiencia al trabajar con herramientas como editores de código, ya que ofrece sugerencias y documentación en tiempo real. Esto hace que sea más fácil de mantener, especialmente en proyectos grandes o cuando se trabaja en equipo.

### - ¿Qué es el sistema de tipos en TypeScript y cómo ayuda a evitar errores en tiempo de desarrollo?
El sistema de tipos en TypeScript permite especificar qué tipo de datos (como números, texto, listas o incluso propiedades de los objetos) puede manejar cada parte del código. Esto ayuda a evitar errores porque, antes de ejecutar el programa, TypeScript verifica que los datos sean del tipo esperado. Si, por ejemplo, se intenta sumar un número con un texto, TypeScript lo detecta de inmediato, alertando sobre el error antes de que cause problemas en la aplicación. Esto mejora la precisión y reduce fallos en el código.

A pesar de que esto permite detectar errores en tiempos de desarrollo, aún pueden haber casos donde un dato puede no tener el tipo definido. Un ejemplo común de este caso es cuando se solicitan datos desde una API. Si bien se puede definir qué estructura (propiedades y tipo de datos del objeto) debería tener la respuesta, esta puede ser diferente a lo esperado, ya que TypeScript solo indica la estructura que deberían tener los datos, pero no valida que esa estructura se cumpla. Para estos casos se puede complementar con un validador de esquemas, como por ejemplo “zod”.

## 2. Ejercicio Práctico: Definiendo Tipos e Inferencia

Se define un tipo de dato **Doctor**, el cual es un objeto que contiene la información de un doctor. Se usa este tipo de dato en una función que toma como parámetro un arreglo de datos sobre doctores. La función debe devolver los nombres de los doctores que tienen más de un cierto número de años de experiencia.

### Desarrollo:

```typescript
// Tipo de dato Doctor
type Doctor = {
  id: number; // Número identificador único
  name: string; // Nombre del doctor
  specialty: string; // Especialidad
  yearsOfExperience: number; // Años de experiencia
  image?: string; // (opcional) Ruta a la imagen
};

// Función para filtrar doctores con experiencia mínima
const filterExperiencedDoctors = (
  doctors: Doctor[], // Arreglo de datos de doctores
  minExperience: number // Mínimo de años de experiencia requeridos
) => {
  return doctors.filter((doctor) => doctor.yearsOfExperience >= minExperience);
};

/*
 Cómo todos los elementos del array doctors son del tipo Doctor, el
 array retornado por método filter también será un array del tipo
 doctor y además como este es el único return, Typescript infiere que
 esta función retorna un array de elementos Doctor, por lo que no es
 necesario indicarlo explícitamente al inicio de la definición de la
 función.
*/

// Ejemplo de uso
const doctors: Doctor[] = [
  {
    id: 1,
    name: 'Ana Pérez',
    specialty: 'Cardiología',
    yearsOfExperience: 10,
  },
  {
    id: 2,
    name: 'Juan López',
    specialty: 'Neurología',
    yearsOfExperience: 5,
  },
  {
    id: 3,
    name: 'María González',
    specialty: 'Pediatría',
    yearsOfExperience: 15,
  },
];

const experiencedDoctors = filterExperiencedDoctors(doctors, 8);
console.log(experiencedDoctors.map(({ name }) => name));

// ["Ana Pérez", "María González"] 

```

## 3. Definición de Interfaces y Clases en TypeScript

Podemos integrar esta función en la clase **HospitalDoctor** para hacerla más robusta, utilizando los datos de los doctores definidos en la clase.

- **Interfaz**: Representa la forma que debe tener un objeto o clase (indicando sus propiedades y métodos), como los datos de un doctor (nombre, especialidad, años de experiencia, etc.). Es un contrato que garantiza que los objetos sigan un formato específico.
  
- **Clase**: Implementa la interfaz y puede contener lógica adicional.  
  Por ejemplo:
  - Métodos para obtener información detallada de un doctor.
  - Métodos para actualizar su especialidad.

### Ejemplo de uso:

```typescript
const hospital = new MyHospital(doctors);

// Obtener doctores con más de 8 años de experiencia
console.log(hospital.getExperiencedDoctors(8)); // ["Ana Pérez", "María González"]

// Buscar doctores especializados en "Neurología"
console.log(hospital.findDoctorsBySpecialty('Neurología')); // [{ id: 2, name: "Juan López", specialty: "Neurología", yearsOfExperience: 5 }]

// Agregar un nuevo doctor
hospital.addDoctor({
  id: 4,
  name: 'Carlos Ramírez',
  specialty: 'Dermatología',
  yearsOfExperience: 12,
});

// Actualizar la especialidad de un doctor
hospital.updateDoctorSpecialty(2, 'Psiquiatría');

// Calcular experiencia promedio de los doctores
console.log(hospital.calculateAverageExperience()); // Calcula el promedio de años

```

## 4. TypeScript y ReactJS: Implementación Básica en un Componente

Aquí se muestra un componente, el cual corresponde a una **Card** básica que muestra solo el nombre y la especialidad de un doctor en particular. De forma adicional, se otorga un segundo parámetro (`onPress`) con el fin de realizar alguna acción usando la información del doctor si la card es presionada (por ejemplo, mostrar un modal con información más detallada del doctor).


```typescript
const DoctorCard = ({
  doctor,
  onPress,
}: { 
  doctor: { 
    name: string; 
    specialty: string; 
  }; 
  onPress: () => void; 
}) => {
  return (
    <div onClick={onPress}>
      <h3>{doctor.name}</h3>
      <p>{doctor.specialty}</p>
    </div>
  );
};

```

## 5. Ventajas de TypeScript en el Desarrollo con ReactJS

- Se evaluará la comprensión de los estudiantes sobre las ventajas de utilizar TypeScript en proyectos basados en ReactJS. Esto puede incluir la detección temprana de errores, la autocompletación en editores de código, y la mejora en la productividad y el mantenimiento del código.

- Se pedirá a los estudiantes que den ejemplos de cómo TypeScript mejora el desarrollo en React en comparación con JavaScript puro.

La ventaja de utilizar TypeScript es la facilidad que entrega al momento de codificar y detectar errores tempranos, permitiendo la corrección antes de llegar a la implementación y ejecución (producción) del proyecto.

Además, en **VSCode** su integración es casi automática, ya que contiene un autocompletado cuando se trabaja en **TypeScript/JavaScript**, a medida que se va codificando un proyecto. Esto mejora la productividad del desarrollador. Ejemplo: cuando se utiliza un Array, sugiere métodos exclusivos del tipo o alerta cuando no es compatible.

Entrega beneficios para el mantenimiento, haciendo que el código sea más fácil de entender y modificar con el tiempo.

TypeScript ofrece integración y soporte con librerías de React mediante definiciones tipo `@types`, como por ejemplo rutas dinámicas con `react-router`.

Permite crear componentes altamente reutilizables.


