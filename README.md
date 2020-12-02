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
