# Programación orientada a objetos (parte 2)

## Clases abstractas e interfaces
Nuestra última discusión se quedó en una clase Mesa y dos subclases suyas:
MesaCircular y MesaRectangular. ¿Se acuerdan del problema que había? En realidad
no tenía sentido instanciar un objeto de clase Mesa porque no puede tener
significación alguna.

Estas clases son comunes cuando programamos orientado a objetos, por lo que
Java nos permite modelarlo con dos maneras diferentes. El primero son las
**clases abstractas**, de las cuales _no_ podemos instanciar ningún objeto. Una
clase se declara abstracta poniend `abstract` en su declaración.  Otra cosa que
caracteriza a las clases abstractas es que pueden tener **métodos abstractos**,
métodos especificados sin implementarse, entendiéndose que cuando una clase
extienda a la clase abstracta, debe especificar la implementación.

En el ejemplo, anterior, podríamos convertir la clase Mesa en abastracta como
sigue:

```Java
public abstract class Mesa{

      //Atributos
      private String material;
      private int añosDeUso;

      //Métodos
      public Mesa(){}

      public Mesa(String material, int años){
       material = material;
       añosDeUso = años;
      }

      public void setAñosDeUso(int años){
       añosDeUso = años;
      }

      public String getAñosDeUso(){
       return añosDeUso;
      }

      public abstract double calcularArea();
}
```
¿Ven qué es nuevo en este código? la clase y el método `calcularArea` se
especificaron explícitamente como `abstract`. Noten que a diferencia del
constructor trivial, un método abstracto _no_ tiene llaves. Las llaves defininen
la implementación del método, y no es lo mismo poner llaves vacías (la implementación
es nada) a no ponerlas (la implemenetación se especificará después.) Podemos
completar entonces la clase MesaCircular exctamente como lo hicimos en el
documento anterior.

Antes de Java 1.8, las clases sólamente podían extender a _una_ otra clase. Por ejemplo,
la clase MesaRectangular podía extender a Mesa o a Rectángulo, pero sólamente a una
de ellas. Si se quiere usar **herencia múltiple** (es decir, extender a más de una
clase), utilizamos **Interfaces**. Pueden pensar en una interface como una clase
abstracta que no permitía _ninguna_ implementación. Básicamente es un contrato, un
caparazón vacío que especifica todo lo que debería poder hacer una clase que **implemente**
(como se pueden imaginar, aquí no usamos `extends` sino `implement`) la interfase,
pero todo es diferente entre ellos.

No quiero entrar mucho en detalle ahora para no confundirlos, pero desde Java 1.8
las Interfaces ya permiten implementación de los llamados **métodos default**.
¿Cuándo usar interfaces y cuándo clases abastractas? En general, yo prefiero
usar interfaces con métodos default, pero las clases abstractas son más flexibles
con la visibildad (ya casi llegamos a eso).

## Estructura de un documento de Java
Por fin llegamos a entender la letanía de `public static void main(String[] args)`.
Primero hablaremos de la **visibilidad** de una clase y sus miembros. Cuando declaramos
a una clase como `public`, todas las clases pueden verla; mientras que si la nombramos
`private`, sólo pueden hacerlo las clases dentro de su paquete.

Para los métodos y atributos funciona más o menos igual: los declarados `public`
le son accesibles a todas las clases y los `private` sólo lo son al objeto mismo.
Por ejemplo, todos los atributos los hemos declarados siempre como privados, y es
porque sólo un objeto debería ser capaz de cambiarlos y leerlos (recuerden el
principio de encapsulamiento). Hay una tercera capa de visibilada, `protected`,
que da acceso a todas las clases del paquete.

La otra palabra que no saben interpretar es `static`. Para no entrar mucho en
detalle, y comor regla rápida de decisión, los métodos y atributos estáticos
son los que _deben asociarse a toda la clase y no a un objeto particular_. Por
ejemplo, un método estático debe tener sentido incluso cuando no haya ningún
objeto de la clase instanciada, y un atributo estático debe ser compartido
entre todos los objetos instanciados de esa clase.

## Polimorfismo
El último concepto de programación orientada a objetos que quiero revisar es
el de **polimorfismo**. Del griego 'muchas formas', en POO polimorfismo se refiere
a la idea de que una clase puede compartir comportmiento con su superclase pero
también añadirle algo propio.

Para poner un ejemplo, imaginen que tenemos una clase Bicicleta con atributos
color y material. Supongan también que la clase bicicleta tiene el siguiente
método

```Java
public toString(){
 return "La bicicleta es de color " + this.getColor() + " y es de " + this.getMaterial();
}
```

Digamos que BicicletaDeMontaña extiende a la clase Bicicleta. En este caso,
