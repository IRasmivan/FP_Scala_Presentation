---
theme: gaia
_class: lead
paginate: true
backgroundColor: #fff
---

![bg left:40% 80%](https://www.lightbend.com/assets/images/brand/scala/scala-logos/svg/scala-full-color.svg)

# **Functional Programming Learning**
## In Scala
ரஸ்மிவன் கன்னிப்பேச்சு

---
# Whats is Functional Programming?

Its a Programming paradigm!

Some Programing paradigm are `Object-Oriented Programming`, `imperative programming`

---
# Whats is Functional Programming?

    A coding style
    A mindset
---
![bg left](https://upload.wikimedia.org/wikipedia/commons/3/3c/Size_planets_comparison.jpg)

# In this Presentaion

Maybe an electron.

Share few programs!

---
# Whats Qualifys as Functional Programming for Scala?

![bg right:20%](https://img.freepik.com/free-vector/groovy-psychedelic-hand-drawn-background_23-2149086296.jpg?w=2000&t=st=1666009683~exp=1666010283~hmac=ef9b4bc1a5075d0a987709bce54e58b914de4a2add262ca37e64cd5427786c3a)
- Higher-order functions
- Immutability
- First class modules
- Currying
- Lambdas
- Closures
- Pattern matching
- Laziness

---
# Whats Qualifys as Functional Programming for Scala?
![bg right:20%](https://img.freepik.com/free-vector/abstract-hand-painted-background_23-2148426728.jpg?w=2000&t=st=1666009990~exp=1666010590~hmac=1910641302eb071d079ebae3e0b24be50df7894a56733a6d15b8ecbdfe7a3abf)

- Monadic comprehensions
- Algebraic data types
- Type classes
- Higher-kinded types
- Phantom types
- Existential types
- Type-level programming

---

# How to do it?

Do Everything as Function

```
Input => Output
````

---
# Non Functional:

    public class CubeSquare {
        public static void main(String args[]) {
            int number = 3;
            int square;
            int cube;

            System.out.println("\nNumber\tSquare\tCubes");
            square = number * number;
            cube = square * number;
            System.out.printf(" %d\t \t%d\t \t%d\n", number, square, cube);
        }//end main
    }

    Output:
        Number	Square	    Cubes
        3	 	9	 	27
---
# Functional Way:
    def square(num: Int): Int = num * num
    def cube(num: Int): Int = square(num) * num
    def display(number: Int): Unit = {
        println(s"\nNumber\tSquare\tCubes")
        println(s"$number \t ${square(number)}\t ${cube(number)}")
    }

    display(3)

    Output:
        Number	Square	Cubes
        3 	    9	        27

---
# Impure Function

    In general, you should watch out for functions with a return type of Unit.
    Because those functions do not return anything, logically the only reason you ever call it is to achieve some side effect. 
    In consequence, often the usage of those functions is impure.

    def display(number: Int): Unit // Is Impure

https://docs.scala-lang.org/overviews/scala-book/pure-functions.html


---
# Pure Function

    def square(num: Int): Int = num * num
    def cube(num: Int): Int = square(num) * num

    def getSqrCub(number: Int): String = {
        s"$number \t ${square(number)}\t ${cube(number)}"
    }

    getSqrCub(3) //3 	    9	    27

---
# Higher-order functions
![bg left](https://www.callcentrehelper.com/images/stories/2011/02/concentric-circles-760.jpg)

---

![bg 65%](https://thecodebytes.com/wp-content/webpc-passthru.php?src=https://thecodebytes.com/wp-content/uploads/2022/03/functional-programming-meme-8.jpeg&nocache=1)

---
    def HOF_sqr_cub(num: Int, fn:Int => Int): Int = fn(num)
    
    def square(num: Int): Int = num * num
    def cube(num: Int): Int = square(num) * num

    def getSqrCub(number: Int): String = {
        s"$number \t ${HOF_sqr_cub(number, square)}\t ${HOF_sqr_cub(number, cube)}"
    }

    getSqrCub(3) //3 	    9	    27

---
    def urlBuilder(ssl: Boolean, domainName: String): (String, String) => String = {
    val schema = if (ssl) "https://" else "http://"
    (endpoint: String, query: String) => s"$schema$domainName/$endpoint?$query"
    }

    val domainName = "www.example.com"
    def getURL = urlBuilder(ssl=true, domainName)
    val endpoint = "users"
    val query = "id=1"
    val url = getURL(endpoint, query) // "https://www.example.com/users?id=1": String

---
# Don't Iterate using `LOOP`, Insted Use `HOF`:
*Map*

    val salaries = Seq(20000, 70000, 40000)
    val doubleSalary = (x: Int) => x * 2
    val newSalaries = salaries.map(doubleSalary) // List(40000, 140000, 80000)

*FoldLeft*

    val l = List(1, 3, 5, 11, -1, -3, -5)
    l.foldLeft(0)(_ + _) // 11: Int

---
# `HOF` in Options:

*Default Value:*

	option match {
        case Some(i) => i
        case None => default
    }

    option.getOrElse(default) // This is HOF

---

*Checking If Empty*:

    option match {
        case Some(a) => false
        case None => true
    }

    option.isEmpty // This is HOF

Ref: https://alvinalexander.com/scala/how-use-higher-order-functions-option-some-none-match-expressions/

---
# Avoid mutability
    use immutable data

---
# Mutation (bad!):
    var numbers = Array(2000, 7000, 4000)

    println("Number before Update")
    for ( x <- numbers ) {
        println( x )
    }
    numbers(1) = 3000; // This is BAD
    println("Number After Update")
    for ( x <- numbers ) {
        println( x )
    }

    Number before Update
    2000 7000 4000
    Number After Update
    2000 3000 4000

---
# No mutation (good!):

    val numbers = Seq(20000, 70000, 40000)
    val new_numbers = numbers.updated(1,30000)
    new_numbers //List(20000, 30000, 40000)
    numbers //List(20000, 70000, 40000)

---

# Resources

![w:72 h:90](https://images.manning.com/360/480/resize/book/2/a2ed920-d6ed-48fb-8f18-b051b7a09a2a/bjarnason.png) Functional Programming in Scala

![w:72 h:90](https://d2sofvawe08yqg.cloudfront.net/pfp-scala/s_hero2x?1622576566) Practical FP in Scala A hands-on approach

![w:80 h:80](https://scala.love/wp-content/uploads/2020/04/5-3-400x400xc.png)Zainab Sessions

---
![bg 50%](https://thumbs.dreamstime.com/b/questions-colorful-overlapping-question-marks-banner-vector-119765863.jpg)
