# Regular expressions in Kotlin

In this guide, you will learn how to use regular expressions in Kotlin in practice and see a number of examples. 

We will not focus much on theory. 
For details about functions and options described below, refer to the [Kotlin Documentation](https://kotlinlang.org/api/latest/jvm/stdlib/kotlin.text/-regex/). 

## Prerequisites

We assume that you are already familiar with the following:

- The Kotlin basics.
- The concept of regular expressions and their syntax. 

## Overview

To use regular expressions in Kotlin,
you invoke functions and options of the `Regex` class, which you do not need to import explicitly. 
The `Regex` class belongs to the `kotlin.text` package imported by default. 

Using regular expressions comes down to the following steps:

1. Coming up with a search pattern in the form of a string.
   
    **Note:** Search patterns often contain characters Kotlin interprets as escape ones (for example, `\d`).
    To avoid errors, double escape these characters or define search patterns as raw strings with triple quotes (`"""`), for example:
    
    ```kotlin
    val pattern = """\d{3}-\d{3}-\d{4}""" 
    ```
2. [Creating a regular expression from the pattern](https://kotlinlang.org/api/latest/jvm/stdlib/kotlin.text/-regex/#constructors).
3. Invoking a [function](https://kotlinlang.org/api/latest/jvm/stdlib/kotlin.text/-regex/#functions) of the `Regex` class on the regular expression.
4. Passing the string you want to manipulate with regular expressions to the function. 

With regular expressions in Kotlin, you can do the following:

- [Find out if a string contains matches of a pattern](#find-out-if-a-string-contains-matches).
- [Search for matches of a pattern in a string](#search-for-matches).
- [Check if the entire string matches a pattern](#check-if-the-entire-string-matches-a-pattern). 
- [Replace matches with the given replacement](#replace-matches-with-the-given-replacement).
- [Split a string around matches](#split-a-string-around-matches).

## Find out if a string contains matches 

To do so, use the `containsMatchIn()` function.
If `containsMatchIn()` finds at least one match, the function returns `true`.
If the function finds no matches, it returns `false`:

```kotlin
fun main() {
    val pattern = Regex("""\W\d{3}\W\s\d{3}-\d{4}""")
    println(pattern.containsMatchIn("her phone number is (555) 123-4567"))
    println(pattern.containsMatchIn("her phone number is 555-123-4567"))
}
```

## Search for matches

To do so, use the `find()` and `findAll()` functions.

`find()` returns only the first match of the specified pattern:

```kotlin
fun main() {
    val pattern = Regex("apples")
    println(pattern.find("2 apples plus 3 apples make 5 apples")?.value)
}
```
while `findAll()` returns all matches:

```kotlin
fun main() {
    val pattern = Regex("apples")
    pattern.findAll("2 apples plus 3 apples make 5 apples").forEach {
        println(it.value)
    }
}
```

With both `find()` and `findAll()`, you can specify the character index to start the search from: `startIndex`.
In the example below, `startIndex` is `10`:

```kotlin
fun main() {
    val pattern = Regex("apples")
    pattern.findAll("2 apples plus 3 apples make 5 apples",10).forEach {
        println(it.value)
    }
}
```

If you omit `startIndex`, the search starts from the beginning of the string.

## Check if the entire string matches a pattern

To do so, use either the `matchEntire()` or `matches()` functions.

If the entire string matches the pattern, the `matchEntire()` will return the string.
Otherwise, the function will return `null`:

```kotlin
fun main() {
    val pattern = Regex("""\d+ oranges""")
    println(pattern.matchEntire("2 oranges")?.value)
    println(pattern.matchEntire("2 oranges in the basket")?.value)
}
```

Unlike `matchEntire()`, `matches()` is a boolean function. 
If the entire string matches the pattern, the `matches()` function will return `true`.
Otherwise, the function will return `false`:

```kotlin
fun main() {
    val pattern = Regex("""\d+ oranges""")
    println(pattern.matches("20 oranges"))
    println(pattern.matches("20 oranges in the basket"))
}
```

## Replace matches with the given replacement

To do so, use either the `replace()` or `replaceFirst()` functions.

`replace()` replaces all matches with the replacement string you specify.
In the example below, the replacement string is `jane_doe@example.com`:

```kotlin
fun main() {
    val pattern = Regex("""\w+@\w+.com""")
    println(pattern.replace("anna_pavlova@gmail.com and grace_hopper@yahoo.com","jane_doe@example.com"))
}
```
Unlike `replace()`, `replaceFirst()` replaces only the first match:

```kotlin
fun main() {
    val pattern = Regex("""\d+""")
    println(pattern.replaceFirst("phone number is 555-123-4567","xxx"))
}
```

## Split a string around matches

To do so, use the `split()` function:

```kotlin
fun main() {
    val pattern = Regex("""\s""")
    println(pattern.split("The quick brown fox jumps over the lazy dog"))
}
```
By default, the maximum number of substrings `split()` can return is not limited. 

To limit the maximum number of substrings, specify `limit`.
In the example below, `limit` is `2`:

```kotlin
fun main() {
    val pattern = Regex("""\s""")
    println(pattern.split("The quick brown fox jumps over the lazy dog",5))
}
```

## Conclusion

We learned how to use regular expressions in Kotlin and saw the examples. 
For details about `Regex` functions and options, refer to the [Kotlin Documentation](https://kotlinlang.org/api/latest/jvm/stdlib/kotlin.text/-regex/). 









