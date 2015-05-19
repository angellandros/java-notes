# Singleton vs. Chameleon
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
Scala is a language with strong philosophy behind it. In the language there is a concept for the singletons, namely `object`. Singleton objects in Scala have only one instance and there are multiple restrictions to prevent the instance to change. A list of them of some of them:

1. Singleton objects in Scala could not have parameters in their constructor,
2. They could not have any uninitialized fields,
3. etc.

These all show that singleton objects are immutable in Scala's philosophy.

## Chameleon
Our first example is a class implemented in Java language. This class is appearently singleton, but actually not.

```java
public class SingleInt
{
	private static SingleInt instance;
	private int theInt;
	
	private SingleInt()
	{
		theInt = 1;
	}
	
	public static SingleInt getInstance()
	{
		if(instance == null)
			instance = new SingleInt();
		return instance;
	}
	
	public void setInt(int theInt)
	{
		this.theInt = theInt;
	}
	
	public int getInt()
	{
		return theInt;
	}
}
```

Test the program somewhere with this code:

```java
	public static void main (String[] args)
	{
		SingleInt one = SingleInt.getInstance();
		System.out.println(one.getInt());
		
		SingleInt two = SingleInt.getInstance();
		two.setInt(2);
		System.out.println(two.getInt());
	}
```

There will be a 1 and a 2 in the output:

```txt
1
2
```

The `SingleInt` class here does not have one _possible_ member as a set. But the at a time cannot have two different instances. This is difference between _chameleon_ and _singleton_. A singleton is a class with one possible member, but a chameleon is a class with more than one possible member, but with one existing member at all times.

### Chameleon in Scala
Scala wanted to prevent this usecase of object, but people are careless:

```scala
object SingleInt {
	var x: Int = 1
	def set(y: Int) = {
		x = y
	}
}

object Main extends App {
	println(SingleInt.x)
	SingleInt.set(2)
	println(SingleInt.x)
}
```