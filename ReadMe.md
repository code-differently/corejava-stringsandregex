# All you need to know about Regular Expressions

## Part I: Demystifying Regular Expressions

![](./assets/img01.png)

### What are Regular Expressions and why should you know about them?

Regular expressions are a generalized way to match patterns with sequences of characters. They define a search pattern, mainly for use in pattern matching with strings, or string matching, i.e. “find and replace” like operations.

Let’s say you have to search a corpus and return all the email addresses mentioned in it. A pretty straightforward task for a human as every email address can be generalized as a string of alphanumeric characters with some permissible special characters like . (dot), _(underscore), -(hyphen), followed by a ‘@{domainName}.com’.

But how do you pass such a template to a computer? The fact that email addresses can be of variable length, don’t have a fixed location for numeric/special characters (could be in the beginning, the end, or anywhere in between), doesn’t make the task any easier for a computer.

This is where regular expressions come to our rescue! By using them we can easily create a generalized template that a not only a computer will understand but will satisfy all of our restrictions.

![](./assets/img03.png)

### Where did the term Regular Expressions come from?

The term *regular expression* comes from mathematics and computer science theory, where it reflects a trait of mathematical expressions called **regularity**. The text patterns used by the earliest grep tools were regular expressions in the mathematical sense. Though the name has stuck, modern-day Perl-style regular expressions (which we still use with other programming languages) are not regular expressions at all in the mathematical sense.

They are often called **REs**, or **regexes**, or **regex** patterns.


### How to write a regular expression?

#### Basics:

##### **1)** Most characters match with themselves. 

So if you have to write a regular expression for the word “wubbaLubbaDubDub”, the regex for it would be ‘wubbaLubbaDubDub’. Keep in mind that REs are case-sensitive.

But there are some characters called meta-characters which don’t match to themselves rather signal that some out-of-the-ordinary thing should be matched, or they affect other portions of the RE by repeating them or changing their meaning. These meta-characters make regular expressions the powerful tool they are.

##### **2) Repeaters *,+,{}.** 

A lot of time you’ll face a scenario where you don't know how many times a character will be repeated or if it will be repeated at all. Repeaters allow us to tackle such cases.

**The asterisk (*):** It implies that the preceding character is present 0 or more times. There is no upper bound on the number of occurrences of the preceding character.

```
In ‘a*b’, ‘a’ precedes the *, which means ‘a’ can occur 0/0+ times. 
So it will match to ‘b’, ‘ab’, ‘aab’, ‘aaab’, ‘aa..(infinite a’s)..b’.
```

**The plus(+):** It is the same as * but implies at least 1 occurrence of the previous character.

```
‘a+b’ will match to ‘ab’, ‘aab’, ‘aaab’, ‘aaa…aab’ but not just ‘b’.
```

**The curly braces {}:** These are used to define a range of occurrences of the previous character.

```
‘a{3},b’: will match ‘aaab’ only. 
‘a{min,}b’: restricting minimum occurrences of ‘a’, no upper limit restrictions. 
‘a{3,}b’ will match ‘aaab’, ‘aaaab’, ‘aaa…aab’.
‘a{min, max}b’: ‘a’ should occur at least min times and at most max times. ‘a{3,5}b’ will match ‘aaab’, ‘aaaab’, ‘aaaaab’.
```

##### 3) The wildcard(.): 

Knowing the order of characters in a string is not always feasible. A wildcard comes in really handy in these situations.
It implies that any character can take its place in the sequence.

```
‘.’ will match all strings with just one character.
‘.*’ will match all possible strings of any length.
‘a.b’ will match ‘aab’, ‘abb’, ‘acb’, ‘adb’, …. ‘a b’ [a(space)b], ‘a/b’ and so on. Basically, any sequence of length 3 starting with ‘a’ and ending with ‘b’.
```

##### 4) The Optional character(?): 

Sometimes multiple variations of a word are possible. Like ‘color’ (American English) and ‘colour’ (British English) are different spellings of the same word and both are correct, the only difference being an extra ‘u’ in the British version.
The ‘?’ implies that the previous character may or may not be present in the final string. In a way, ‘?’ implies a 0 or 1 occurrence.

```
‘colou?r’ will match both ‘color’ and ‘colour’.
‘docx?’ will match both ‘doc’ and ‘docx’.
```

##### 5) The Caret(^):

It implies the first character of a string.

```
‘^a.*’ will match all strings starting with ‘a’.
‘^a{2}.*’ will match all strings starting with ‘aa’.
```

##### 6) The dollar($): 

It implies the last character of a string.

```
‘.*b$’ will match all strings ending with a ‘b’.
```

##### 7) Character classes([]):

More often than not, for a particular position in a string, there will be more than one possible character.
To accommodate all the possible characters we use character classes. They specify a set of characters that you wish to match. Characters can be listed individually, or a range of characters can be indicated by giving two characters and separating them by a ‘-’.

```
‘[abc]’: will match ‘a’, ‘b’, or ‘c’. 
‘[^abc]’:Negation will match any character except ‘a’, ‘b’, and ‘c’. Note -- Not to be confused with caret where ^ implies begins with. If inside a character class ^ implies negation.
Character range: ‘[a-zA-Z]’ will match any character from a-z or A-Z. 
```
| Metacharacter | Description |
| ------------- | ----------- |
|`\d` | matches any decimal digit; this is equivalent to the class [0–9].|
|`\D` | Matches any non-digit character; this is equivalent to the class [^0–9].|
|`\s`| Matches any whitespace character; this is equivalent to the class[\t\n\r\f\v].|
|`\S` |Matches any non-whitespace character; this is equivalent to the class[^\t\n\r\f\v].|
|`\w `|Matches any alphanumeric character; this is equivalent to the class [a-zA-Z0–9].|
|`\W `|Matches any non-alphanumeric character; this is equivalent to the class [^a-zA-Z0–9].|
| `\b`| Find a match at the beginning of a word like this: \bWORD, or at the end of a word like this: WORD\b|
| `|` | Find a match for any one of the patterns separated by \| as in: cat \| dog \| fish|
| `.` | Find just one instance of any character |
| `^` | Finds a match as the beginning of a string as in: ^Hello|

##### 9) Grouping character:

A set of different symbols of a regular expression can be grouped together to act as a single unit and behave as a block, for this, you need to wrap the regular expression in the parenthesis( ).

```
‘(ab)+’ will match ‘ab’, ‘abab’,’abab…’.
‘^(th).*” will match all string starting with ‘th’.
```

#### 10) Vertical Bar ( | ):

Matches any one element separated by the (|).

```
th(e|is|at) will match words - the, this and that.
```

##### 11) The Escape character (\):

What if you want to match a meta-character with itself i.e match ‘*’ with a ‘*’ and not use it is a wild card?
You can do so by adding a backslash( \ ) before that character. This will allow special characters to be used without invoking their special meaning.

```
\d+[\+-x\*]\d+ will match patterns like "2+2" and "3*9" in "(2+2)*3*9".
```

## Writing Regex for an email address

In order to write a regex for any email address, we need to keep in mind the following constraints:

* It can only start with an alphabet. `^([a-zA-Z])`
* It is of variable length and can contain any alphanumeric character along with ‘.’, ‘_’, ‘-’. `([a-zA-Z0–9_\-\.]*)`
* It should have a ‘@’ followed by a domain name. `@([a-zA-Z0–9_\-\.]+)`
* It should end with a .(dot) something, usually 2/3 character long.
`\.([a-zA-Z]){2,3}$`
Our final regular expression for an email address :
`^([a-zA-Z])([a-zA-Z0–9_\-\.]*)@([a-zA-Z0–9_\-\.]+)\.([a-zA-Z]){2,3}$
`


## Example In Java

```
import java.util.regex.Matcher;
import java.util.regex.Pattern;

public class RegexMatches {

   private static final String REGEX = "\\bcat\\b";
   private static final String INPUT = "cat cat cat cattie cat";

   public static void main( String args[] ) {
      Pattern p = Pattern.compile(REGEX);
      Matcher m = p.matcher(INPUT);   // get a matcher object
      int count = 0;

      while(m.find()) {
         count++;
         System.out.println("Match number "+count);
         System.out.println("start(): "+m.start());
         System.out.println("end(): "+m.end());
      }
   }
}
```



## Let's Try it out Part 1

### Implementation

In the package `com.codedifferentlty.regex.practice.countingword` :

Let's complete the following files :

* RegexWordCounter
* RegexWordCounterDriver

`RegexWordCounter`

```
import java.util.regex.Matcher;
import java.util.regex.Pattern;

public class RegexWordCounter {

    public static Integer countWordOccurrences(String REGEX, String input){
        Pattern p = Pattern.compile(REGEX);
        Matcher m = p.matcher(input);
        int count = 0;
        while(m.find()){
            count++;
        }
        return count;
    }


}
```

`RegexWordCounterDriver`

```
public class RegexWordCounterDriver {
    public static void main(String[] args) {
        String REGEX = "\\bcat\\b";
        String input = "cat cat cat cattie cat";
        Integer occurences = RegexWordCounter.countWordOccurrences(REGEX, input);
        System.out.println("This is the original string: "+ input );
        String output = String.format("It appears %d times.", occurences);
        System.out.println(output);
    }
}
```

### Unit Test


`RegexWordCounterTest`

* Create unit test for the following scenerios
	*  finding one word
	*  finding multiple words 
	*  finding words that start with a prefix



## Let's Try it out Part 2

In the package `com.codedifferentlty.regex.practice.replacing` :

* RegexReplaceWord
* RegexReplaceWordDriver

`RegexReplaceWord`

```
import java.util.regex.Matcher;
import java.util.regex.Pattern;

public class RegexReplaceWord {

    public static String replaceFirst(String regex, String replace, String input){
        Pattern p = Pattern.compile(regex);
        Matcher m = p.matcher(input);
        return m.replaceFirst(replace);
    }

    public static String replaceAll(String regex, String replace, String input){
        Pattern p = Pattern.compile(regex);
        Matcher m = p.matcher(input);
        return m.replaceAll(replace);
    }

}
```

`RegexReplaceWordDriver`

```
public class RegexReplaceWordDriver {

    public static void main(String[] args) {
        String regex = "\\bdog";
        String input = "The dog says meow. All dogs say meow.";
        String replace = "cat";
        String out1 = RegexReplaceWord.replaceFirst(regex, replace, input);
        System.out.println(out1);
        String out2 = RegexReplaceWord.replaceAll(regex, replace, input);
        System.out.println(out2);
    }
}
```

### Unit Test

`RegexWordCounterTest`

* Create unit test for the following scenerios
	*  replacing one word
	*  replacing multiple 
	*  replacing prefix words that start with a prefix


### Challenge

Create a function called `replaceNthWord`  :

* the function should take in these inputs
	* the regex pattern
	* the word to replace
	* the input sentence
	* a integer reprecented the nth occurence of that word to replace 

Don't forget your unit test!!!

## Let's Try it out Part 3

There are multiple ways of writing and reading a text file. This is required while dealing with many applications. There are several ways to read a plain text file in Java e.g. you can use FileReader, BufferedReader or Scanner to read a text file.

Given a text file, the task is to read the contents of a file present in a local directory and storing it in a string. Consider a file present on the system namely say it be ‘Sample1.txt’. Let the random content in the file be as inserted below in the pretag block. Now we will be discussing out various ways to achieve the same. The content inside file ‘Sample1.txt’.

#### Methods:

There are several ways to achieve the goal and with the advancement of the version in java, specific methods are there laid out which are discussed sequentially.

#### Methods:

* Using File.readString() method
* Using readLine() method of BufferReader class
* Using File.readAllBytes() method
* Using File.lines() method
* Using Scanner class (DON'T do this)

Let us discuss each of them by implementing clean java programs in order to understand them.

#### Method 1: Using File.readString() method

The readString() method of File Class in Java is used to read contents to the specified file.

##### Syntax:

```
Files.readString(filePath) ;
```

Parameters: File path with data type as Path

Return Value: This method returns the content of the file in String format.

#### Example 

`ReadingInDataMethod01`

```
public static String readDataIn(String pathToFile) throws IOException{
    Path fileName = Path.of(pathToFile);
    String str = Files.readString(fileName);
    return str;
}
```

`ReadingInDataDriver`


```
public static void main(String[] args)  {
    try {
        String pathToFile = "./files/Sample1.txt";
        String str = ReadingInDataMethod01.readDataIn(pathToFile);
        System.out.println(str);
    }catch (IOException ex){
        System.out.println("Error: no file "+ex.getMessage());
    }
}
```

Running the following code will output the following :

```
Code Differently
Our Students always forget to write there unit test.
```

Now even though its cool that we read in that data, that data is **offensive**! 

It should read "Our Students NEVER forget to write their unit test."

In the `ReadingInDataMethod01` class, let's create a new method called: 

```
public static String readDataInAndReplace(String pathToFile, 
String regex, 
String replace)

```

This method should read in the data , and use regex to replace any words before the string is returned.


#### Method 2: Using BufferedReader class

Just so you can see another method here is an example :

```
public static String readDataIn(String filePath){
    try (BufferedReader buffer = new BufferedReader(
             new FileReader(filePath))) {
        String str;
        while ((str = buffer.readLine()) != null) {
 
            builder.append(str).append("\n");
        }
    } catch (IOException e) {
       System.out.println("Error: no file "+ex.getMessage());
    }
    return builder.toString();
}
```

## Let's Try it out Part 4

In the package `practice.part02.playrewriter` complete the class `PlayReWriter`.

In the `files` folder there is a a file called `Hamlet.txt` inside of it is the complete play Hamlet. Your class will remix Hamlet using the following functions.

* characterNameChanger

```
public String characterNameChanger(String regex, 
String characterName, 
String input){
	// Given a block of text, and given a charcters name, 
	// will alter every occurance of that name.
	// Example: "HORATIO: Friends to this ground."
	// would be changed to "FlavaFlav: Friends to this ground."
}

```

* locationNameChanger

```
public String characterNameChanger(String regex, 
String locationName, 
String input){
	// Given a block of text, and given a charcters name, 
	// will alter every occurance of that name.
	// Example: "In which the majesty of buried Denmark"
	// would be changed to "In which the majesty of buried Wilmington"
}
```

Don't even think about forgetting your unit test!!!