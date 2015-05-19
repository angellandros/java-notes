!# Singleton vs. Chameleon
Singleton is a famous design pattern. Singletons are usually identified with these three properties:

1. A private instance of themselves,
2. Private constructors,
3. A `getInstance` method.

We want to mention that, not all classes with these three propeties are actually singletons. For this pupose, we will mine into the concept a little deeper.

## Other definitions
We want to find the intuition behind the term, so we will gather definitons in different areas.

### Mathematics
A singleton in mathematics is a set with one member. These two terms are relation in this way: let a class be a set of all its elements, then a singelton class has one element.

This philosophical idea behind the classes is somehow ambigous. Which one a class is: a set of all _possible_ instances, or a set of all _existing_ ones? A Platonistic point of view would agree with the first one. The second definition has also difficulties with the term _existing_. Here is the first place that difference between _singleton_ and _chameleon_ gets into light.

### Scala
Scala is a language with strong philosophy behind it. In the language there is a concept for the singletons, namely `object`.
