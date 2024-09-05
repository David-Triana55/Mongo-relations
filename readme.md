# MongoDB Relationships Example

Este repositorio contiene ejemplos y apuntes sobre cómo implementar diferentes tipos de relaciones en MongoDB utilizando el driver nativo. Aquí presento ejemplos de relaciones uno a uno, uno a muchos y muchos a muchos, con ejemplos de embebido y referenciado.

## Introducción

En MongoDB, las relaciones entre colecciones se pueden manejar mediante dos enfoques principales: embebido y referenciado. Este repositorio ilustra cómo manejar estas relaciones con ejemplos prácticos y código en MongoDB.

## Relación Uno a Uno Embebida

En una relación uno a uno embebida, los datos relacionados se almacenan en un solo documento. Esto es útil cuando los datos se usan juntos y no son demasiado grandes.

### Ejemplo

Imaginemos que queremos almacenar el perfil de un usuario directamente en el documento del usuario.

```mongodb
// Crear un usuario con perfil embebido
db.users.insertOne({
  name: "John Doe",
  profile: {
    age: 30,
    address: "123 Main St"
  }
});

// Obtener el usuario
db.users.findOne({ name: "John Doe" });
```

## Relación Uno a Uno Referenciada

En una relación uno a uno referenciada, un documento en una colección contiene una referencia a un único documento en otra colección.

### Ejemplo

Imaginemos que tenemos dos colecciones: users y profiles. Cada usuario tiene un perfil asociado

```mongodb
// Crear perfil
const profileId = db.profiles.insertOne({
  age: 30,
  address: "123 Main St"
}).insertedId;

// Crear usuario con referencia al perfil
db.users.insertOne({
  name: "John Doe",
  profileId: profileId
});

// Obtener el usuario y su perfil
db.users.aggregate([
  {
    $lookup: {
      from: "profiles",
      localField: "profileId",
      foreignField: "_id",
      as: "profile"
    }
  },
  { $unwind: "$profile" }
]).toArray();
```

## Relación Uno a Muchos Embebida

En una relación uno a muchos embebida, un documento en una colección contiene una lista de documentos relacionados en un solo documento. Esto es útil cuando los datos relacionados tienen una relación de uno a muchos y se usan juntos frecuentemente.

### Ejemplo 

Imaginemos que queremos almacenar una lista de comentarios dentro de un documento de publicación.

```mongodb
// Crear una publicación con comentarios embebidos
db.posts.insertOne({
  title: "My First Post",
  comments: [
    { user: "Alice", comment: "Great post!" },
    { user: "Bob", comment: "Thanks for sharing!" }
  ]
});

// Obtener la publicación con comentarios
db.posts.findOne({ title: "My First Post" });
```

## Relación Uno a Muchos Referenciada

En una relación uno a muchos referenciada, un documento en una colección puede estar relacionado con varios documentos en otra colección. Los documentos relacionados se referencian mediante un campo en los documentos secundarios.

### Ejemplo

Imaginemos que tenemos dos colecciones: posts y comments. Cada publicación puede tener múltiples comentarios.

```mongodb
// Crear publicación
const postId = db.posts.insertOne({
  title: "My First Post"
}).insertedId;

// Crear comentarios con referencia a la publicación
db.comments.insertMany([
  { postId: postId, user: "Alice", comment: "Great post!" },
  { postId: postId, user: "Bob", comment: "Thanks for sharing!" }
]);

// Obtener la publicación con comentarios
db.posts.aggregate([
  {
    $lookup: {
      from: "comments",
      localField: "_id",
      foreignField: "postId",
      as: "comments"
    }
  }
]).toArray();
```

## Relación Muchos a Muchos Referenciada

En una relación muchos a muchos, se utiliza una colección intermedia para gestionar las relaciones entre los documentos de dos colecciones diferentes.

### Ejemplo

Imaginemos que tenemos dos colecciones: students y courses. Un estudiante puede estar inscrito en múltiples cursos y un curso puede tener múltiples estudiantes.

```mongodb
// Crear estudiante y curso
const studentId = db.students.insertOne({
  name: "Jane Doe"
}).insertedId;

const courseId = db.courses.insertOne({
  title: "Introduction to MongoDB"
}).insertedId;

// Crear relación entre estudiante y curso
db.studentCourses.insertOne({
  studentId: studentId,
  courseId: courseId
});

// Obtener estudiante con cursos
db.students.aggregate([
  {
    $lookup: {
      from: "studentCourses",
      localField: "_id",
      foreignField: "studentId",
      as: "enrollments"
    }
  },
  {
    $unwind: "$enrollments"
  },
  {
    $lookup: {
      from: "courses",
      localField: "enrollments.courseId",
      foreignField: "_id",
      as: "courses"
    }
  }
]).toArray();
```
