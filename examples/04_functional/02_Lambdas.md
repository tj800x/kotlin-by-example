# Lambda Functions

[*Lambda functions*](https://kotlinlang.org/docs/reference/lambdas.html) ("lambdas") are a simple way to create functions ad-hoc. Lambdas can be denoted very concisely in many cases thanks to type inference and the implicit `it` variable.

```run-kotlin

    val upperCase6: (String) -> String = String::toUpperCase                  // 6
    
//sampleStart
typealias StringTransformFn = (String) -> String;

fun main() {

    val upperCase0: StringTransformFn =
        {it.toUpperCase()}
    val str0 : String = upperCase0("test0")

    // explicitly typed lambda
    // no type inference
    val upperCase1: StringTransformFn =
        {str: String -> str.toUpperCase() }
    val str1 : String = upperCase1("test1")


    // type of the str2 variable is inferred from type of the lambda
    val upperCase2: StringTransformFn =
        {str -> str.toUpperCase() }
    val str2 = upperCase2("test2")

    // type inference outside lambda
    // type of variable (str3) is inferred from BOTH the type
    // of the lambda parameter str (i.e. String)
    // and the return value (String)
    val upperCase3 =
        {str: String -> str.toUpperCase() }
    val str3 = upperCase3("test3")

    // This won't compile because you cannot infer both
    // the type of the lambda and the type of the variable
    //val upperCase4 =  // notice that there is no type here
    //    {str -> str.toUpperCase() }
    //val str4 : String = upperCase4("test4")

    // Can use "it" because there is a single parameter
    val upperCase5: StringTransformFn =
        {it.toUpperCase() }
    val str5: String = upperCase5("test5")

    // Function pointer only allowed for a single function call
    val upperCase6: StringTransformFn =
        String::toUpperCase
    val str6: String = upperCase6("test6")

    println(str0)
    println(str1)
    println(str2)
    println(str3)
    println(str5)
    println(str6)

}
//sampleEnd
```

1. A lambda in all its glory, with explicit types everywhere. The lambda is the part in curly braces, which is assigned to a variable of type `(String) -> String` (a function type).
2. Type inference inside lambda: the type of the lambda parameter is inferred from the type of the variable it's assigned to.
3. Type inference outside lambda: the type of the variable is inferred from the type of the lambda parameter and return value.
4. You cannot do both together, the compiler has no chance to infer the type that way.
5. For lambdas with a single parameter, you don't have to explicitly name it. Instead, you can use the implicit `it` variable. This is especially useful when the type of `it` can be inferred (which is often the case).
6. If your lambda consists of a single function call, you may use function pointers (`::`) .
