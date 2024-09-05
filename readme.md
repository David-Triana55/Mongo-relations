# MongoDB Relationships Example

Este repositorio contiene ejemplos y apuntes sobre cómo implementar diferentes tipos de relaciones en MongoDB utilizando el driver nativo. Aquí presento ejemplos de relaciones uno a uno, uno a muchos, y muchos a muchos, con ejemplos de referencias completas.

## Introducción

En MongoDB, las relaciones entre colecciones se pueden manejar mediante referencias utilizando el driver nativo. Este repositorio ilustra cómo manejar estas relaciones con ejemplos prácticos y código en JavaScript.

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

### Relación Uno a Uno Referenciada

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