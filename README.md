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
* <b>MarkovZero</b>, <b>MarkovOne</b>, <b>MarkovFour</b>, and <b>MarkovModel</b> classes modified to extend the iMarkovModel interface

<b>EfficientMarkovModel</b> - a class which extends AbstractMarkovModel and that builds a HashMap to calculate the follows ArrayList for each possible substring only once, and then uses the HashMap to look at the list of characters following when it is needed. This class includes:
* *toString* - method to print that this is the <b>EfficientMarkovModel</b> class of a specific number
* *buildMap* - method to build the HashMap
* *getFollows* - method that can look up the ArrayList of Strings, instead of computing it each time


Links to exercises:
* https://www.coursera.org/learn/java-programming-design-principles/supplement/xToQx/programming-exercise-generating-random-text
* https://www.coursera.org/learn/java-programming-design-principles/supplement/n1DIm/programming-exercise-interface-and-abstract-class