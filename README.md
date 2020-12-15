# predictive_text_generator
program that has ability to analyze text for training, then make logical predictive and/or random text generation

## Generating Random Text (Markov)

<b>MarkovZero</b> -  a class which generates each letter by randomly choosing a letter from the training text. Has two private variables, a String myText, for the training text, and myRandom, a random number generator. It also has a constructor to initialize myRandom and three methods:
* *setRandom* - has one integer parameter named seed. This method allows generation of the same random text each time, helpful for testing purposes.
* *setTraining* - has one String parameter named s. The String s is used to initialize the training text.
* *getRandomText* - has one integer parameter named numChars. This method generates and returns random text that is numChars long. 

<b>MarkovOne</b> - a class which generates text randomly by predicting the next character based on one character that follows somewhere in the training text. Has the following methods:
* *getFollow* - has one String parameter named key. This method finds all the characters from the private variable myText in <b>MarkovOne</b> that follow key and puts all these characters into an ArrayList, then return the ArrayList. Here is an example of how the algorith works: if myText were “this is a test yes this is a test.”, then the call getFollows(“t”) should return an ArrayList with the Strings “h”, “e”, “ “, “h”, “e”, “.” as “t” appears 6 times. The call getFollows(“e”) should return an ArrayList with the Strings “s”, “s”, “s”. This method will work even if key is a word. Thus, getFollows(“es”) should return an ArrayList with the Strings “t”, “ “, “t”.
* *setTraining* - has one String parameter named s. The String s is used to initialize the training text.
* *getRandomText* - predicts the next character, by finding all the characters that follow the current character in the training text, and then randomly picking one of them as the next character.

<b>MarkovFour</b> - a class using modified methods from MarkovOne. Generates text randomly by predicting the next character based on four characters that follows somewhere in the training text. 

<b>MarkovModel</b> - a class using modified methods from MarkovOne. Uses N characters to predict the next character. An integer is passed in with the constructor to specify the number of characters used to predict the next character.

<b>MarkovRunner</b> - a class used to run the Markov classes, has the following methods:
* *runMarkovZero* - has no parameters. This method reads in a file the user chooses, creates a MarkovZero object, and then generates three sets of randomly generated text using the file read in to choose the random characters from.
* *runMarkovOne* - same as runMarkovZero except it creates a MarkovOne object and thus generates the result using the MarkovOne logic. E.g. if run with random seed set to 42, and the file confucius.txt. The first line of MarkovOne random text generated starts with:    nd are, Prevedowalvism n thastsour tr ndsang heag ti. the ffinthe
* *runMarkovFour* - generates random text using the MarkovFour class. If you set the random seed with 25 and run this method on confucius.txt, the first line of text should start with: ouses the people Minister said the that a many Project of it
* *runMarkovModel* - generates random text using the MarkovModel class. If you set the random seed with 38 and run this method with N = 6 on confucius.txt, the first line of text should start with: sters I could thrice before downloading, and his lord, might
* *printOut* - a helper method, called to print out the random text that was generated with around 60 characters per line.

<b>Tester</b> - used for testing, has the following methods:
* *testGetFollows* - has no parameters. This method creates a MarkovOne object, sets the training text as “this is a test yes this is a test.”. Then it calls getFollows and prints out the resulting ArrayList and also its size.
* *testGetFollowsWithFile* - has no parameters. This method creates a MarkovOne object, sets the training text to a file the user selects (similar to the methods in MarkovRunner), and then call getFollows. Example: if run on confucius.txt and looking for the characters that follow “t”, it will return 11548. 

## Interface and Abstract Class (InterfaceAbstract)

Restructuring the program to use an Interface an Abstract Class

<b>MarkovRunnerWithInterface</b> - a class for running the program to generate random text. This class has several methods:
* *runModel* - has three parameters: an IMarkovModel variable named markov, a String named text and an int named size. This method will work with any markov object that implements IMarkovModel.
* *runMarkov* - creates one of the types of Markov models, and calls runModel with it to generate random text.
* *printOut* - formats and prints the randomly generated text
* <b>MarkovZero</b>, <b>MarkovOne</b>, <b>MarkovFour</b>, and <b>MarkovModel</b> classes modified to implement the iMarkovModel interface
* *testHashMap* - creates an order-2 EfficientMarkovModel for testing purposes
* *compareMethods* - runs a MarkovModel and an EfficientMarkovModel for comparison purposes

<b>AbstractMarkovModel</b> - abstract class that implements IMarkovModel. This class has several items:
* Two protected fields myText, a String, and myRandom, of type Random
* A constructor that creates myRandom
* A *setTraining* method that is public. This method sets the the private String variable myText to the parameter text.
* A signature for the abstract method getRandomText that has one integer parameter named numChars indicating the length of the randomly generated text. 
* *getFollows* - method modified to be protected instead of public, and removed from the Markov classes below
* <b>MarkovZero</b>, <b>MarkovOne</b>, <b>MarkovFour</b>, and <b>MarkovModel</b> classes modified to extend the IMarkovModel interface

<b>EfficientMarkovModel</b> - a class which extends AbstractMarkovModel and that builds a HashMap to calculate the follows ArrayList for each possible substring only once, and then uses the HashMap to look at the list of characters following when it is needed. This class includes:
* *toString* - method to print that this is the <b>EfficientMarkovModel</b> class of a specific number
* *buildMap* - method to build the HashMap
* *getFollows* - method that can look up the ArrayList of Strings, instead of computing it each time

## Word N-Grams (WordNGramStarterProgram)

<b>IMarkovModel</b> - an interface that has three signatures: 
* *setTraining* - has one String parameter named text
* *setRandom* - has one int parameter named seed
* *getRandomText* - has one int parameter named numChars and returns a String

<b>MarkovWordOne</b> - a class which has two private variables, a String array myText, to hold the words from the training text, and myRandom, a random number generator. It also has a constructor to initialize *myRandom* and the following methods:
* *setRandom* - has one integer parameter named seed. Using this method will allow you to generate the same random text each time, which helps in testing the program.
* *setTraining* - has one String parameter named text. The String text is split into words and stored in myText. The words are used to initialize the training text.
* *getRandomText* - has one integer parameter named numWords. This method generates and returns random text that has numWords words. This class generates each word by randomly choosing a word from the training text that follows the current word in the training text. 
* *getFollows* - has one String parameter named key. This method returns an ArrayList of all the single words that immediately follow an instance of key somewhere in the training text. 
* *indexOf* - helper method that has three parameters, a String array named words, a String named target, and an integer named start. This method starts looking at the start position and returns the first index location in words that matches target. If no word is found, then this method returns -1. 
* *testIndexOf* - has no parameters. This method is only for testing the indexOf method. This method creates a simple String array with the words “this is just a test yes this is a simple test” then look for the words: “this” starting at 0, “this” starting at 3, “frog” starting at 0, “frog” starting at 5, “simple” starting at 2 and “test” starting at 5. 

<b>MarkovWordTwo</b> - a class, copied from MarkovWordOne. Modified to work for two consectuive words. Has two keys: key1 and key2 that are consecutive words in the text, and then *getFollows* returns the list of single words that follow these two words. 
* For example: if the text was “this is just a test yes this is a simple test”, then getFollows of “this” “is” would return an ArrayList with “just” and “a”, and getFollows of “just” “a” returns an ArrayList with “test”. Specifically, we will do it slightly differently than in the videos:
* *getFollows* - modified to have two String parameters, key1 and key2
* *indexOf* - modified to have four parameters: a String array words, a String target1, a String target2, and an integer start. Returns the first location of target1 such that target2 immediately follows it, and the search starts looking at index start.

<b>MarkovRunner</b> - a class which has four methods:
* *runModel* - has three parameters, an IMarkovModel named markov, a String text that represents the training text, and an integer named size that represents the number of random words to generate. 
* *runModel* - overloaded method which also includes a fourth parameter, an int named seed.
* *runMarkov*  - has no parameters. This method reads in a file the user chooses, creates a MarkovWordOne object, and then calls runModel to generate and print three sets of randomly generated text using the file read in to choose the random words.
* *printOut* - is called by *runModel* to print out the random text that was generated with around 60 characters per line. 
>* If the random seed is set to 175 and generates 120 words, then run on the file confucius.txt. You should get the output (first five lines shown):
teacher. 12. He that his doings from the free distribution of
Ling, the people by learning; then those over with this or hate
daring and hates his muttering a belief in war. He refused all
likelihood, between men. Fan Ch'ih did not go with you? The Master
said, At his best pupil, who notifies you may ignore propriety;
* *runMarkovTwo* - generates random text with MarkovWordTwo. 
>* If run run confucius.txt with the random number seed 549. The first line of your output should be:
the minister know me? Because I was not so great; xix. 21, says

## WordGram

A class that makes it easier to extend Markov word prediction

<b>WordGram</b> - a class which represents words that have an ordering. For example, a WordGram might be the four words “this” “is” “a” test”, in this order. The WordGram class has two private variables, a String array myWords to store the words in order, one word per slot, and a private integer myHash you will use to be able to use WordGrams as a key with a HashMap. This class has several methods:
* *WordGram* - a constructor that has three parameters, a String array named source, an integer named start, and an integer named size. The constructor copies the size number of words from source starting at the position start into a new WordGram.
* *wordAt* - has one integer argument name index. The method returns the word in the WordGram at position index.
* *length* - has no parameters. Returns the length of the WordGram.
* *toString* - has no parameters. It prints a WordGram out, showing all the words in the WordGram on one line separated by spaces.
* *equals* - has one parameter of type Object named o. This method returns true if two WordGrams are equal and false otherwise.
* *shiftAdd* - has one String parameter word. This method returns a new WordGram the same size as the original (without altering the original), consisting of each word shifted down one index.
>* for example the word in slot 1 would move to slot 0, the word in slot 2 would move to slot 1, etc.) and word added to the end of the new WordGram. 
>* For example, if a WordGram of size 4 is “this” “is” “a” “test”, and shiftAdd is called with the argument “yes”, then the method would return a new WordGram ”is” “a” “test” “yes”.
* *hashCode* - return an integer that is a hash code that represents the WordGram.


<b>WordGramTester</b> - a class with methods for testing the WordGram. Contains the following methods:
* *testWordGram* - builds and prints several WordGrams from a String.
* *testWordGramEquals* - tests if two WordGrams are equivalent.
* *testWordGramShift* - tests the shiftAdd method from the WordGram class.

<b>MarkovWord</b> - a Markov class that works for any number of words and uses the WordGram class to handle those words. This class implements IMarkovModel. This class has three private variables, a String array named myText, a Random variable named myRandom, and an integer variable named myOrder. This class has the following methods, similar to what the MarkovWordOne class had, but extended for handling a larger number of words:
* *MarkovWord* - A constructor with one integer parameter that is the order (how many words to use in prediction). This method initializes myOrder and myRandom.
* *setRandom* - has one integer parameter named seed. Using this method allows generation of the same random text each time, which helps in testing the program. (unchanged from MarkovWordOne)
* *setTraining* - has one String parameter named text. The String text is split into words and stored in myText. The words are used to initialize the training text. (uncharged from MarkovWordOne)
* *indexOf* - has three parameters, a String array of all the words in the training text named words, a WordGram named target, and an integer named start indicating where to start looking for a WordGram match in words. This method returns the first position from start that has words in the array words that match the WordGram target. If there is no such match then it will return -1.
* *getFollows* - has one WordGram parameter named kGram. This method returns an ArrayList of all the single words that immediately follow an instance of the WordGram parameter somewhere in the training text. This method calls indexOf to find these matches.
* *getRandomText* - has one integer parameter named numWords. This method generates and returns random text that has numWords words. This class generates each word by randomly choosing a word from the training text that follows the current word(s) in the training text. Updated so that it works for any Markov order (not just order one), and uses WordGram objects.

<b>EfficientMarkovWord</b> - modified MarkovWord class to be more efficient. This class also implements IMarkovModel and now builds a HashMap to calculate the follows ArrayList for each possible WordGram only once, and then uses the HashMap to look at the list of characters following when it is needed. This class includes the following methods:
* *buildMap* - used to build the HashMap.
* *getFollows* - this getFollows method is much shorter, as it can look up the WordGram, instead of computing it each time.
* *printHashMapInfo* -prints out the following information about the HashMap:
>* Print the HashMap (all the keys and their corresponding values). Only do this if the HashMap is small.
>* Print the number of keys in the HashMap
>* Print the size of the largest value in the HashMap—that is, the size of the largest ArrayList of characters
>* Print the keys that have the maximum size value.

<b>MarkovRunner</b> - modified to include the following methods:
* *testHashMap* - creates an order-2 EfficientMarkovWord with:
>* seed 42
>* the training text is “this is a test yes this is really a test”
>* the size of the text generated is 50
* *compareMethods* - runs a MarkovWord and an EfficientMarkovWord, to compare which is faster.

Links to exercises:
* https://www.coursera.org/learn/java-programming-design-principles/supplement/xToQx/programming-exercise-generating-random-text
* https://www.coursera.org/learn/java-programming-design-principles/supplement/n1DIm/programming-exercise-interface-and-abstract-class
* https://www.coursera.org/learn/java-programming-design-principles/supplement/wkafw/programming-exercise-word-n-grams
* https://www.coursera.org/learn/java-programming-design-principles/supplement/cajch/programming-exercise-wordgram-class