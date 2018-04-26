# Pantry Prequel
Helps the user keep track of any food, and that food's expiration dates, in their pantry.

## example code
'''java
	//check for upcoming exp dates
	public String[] checkExpDates(String[] stuff) {
	  String[] dates = new String[stuff.length];
		String[] food = new String[stuff.length];
		for(int i = 0; i < stuff.length; i++){
			dates[i] = getPantryItem(stuff[i])[2];
			food[i] = getPantryItem(stuff[i])[1];
		}
		List<String> expSoon = new ArrayList<String>();
		Calendar expCalendar = new GregorianCalendar();
		SimpleDateFormat dateFormat = new SimpleDateFormat("MM/dd/yyyy");
		Date dt = new Date();
		expCalendar.setTime(dt);
		expCalendar.add(Calendar.DATE, 7);
		Date beforeDate = expCalendar.getTime();
		for(int i = 0; i < dates.length; i++){
			Date given = new Date();
			try {
				given = dateFormat.parse(dates[i].trim());
			} catch (ParseException pe) {
				System.out.println("Could not parse");
			}
			if(given.before(beforeDate)){
				expSoon.add(food[i]);
			}
		}
		
		String[] expSoonArray = expSoon.toArray(new String[expSoon.size()]);
		return expSoonArray;
	}'''
This portion of the code searches for spaces in the morse code, marking individual letters, and converts them into germanic letters. I had a hard time working this portion out but I think it turned out nicely.

## Motivation
I created this project primarily for a school project. I chose to create a Morse code decoder because I knew it would be a challenge for me and would help me expand my knowledge with strings, arrays, and sequential text files.

# Installation
Download project with the link 'C++ final project.cpp', all additional files are created in the script.

# Tests
		cout << endl;
		cout << "1  English to Morse code" << endl;
		cout << "2  Morse code to English" << endl;
		cout << "3  Conversation mode" << endl;
		cout << "4  Recently encoded words" << endl;
		cout << "5  Recently decoded words" << endl;
		cout << "6  Clear memory" << endl;
		cout << "7  Exit program" << endl;
		cout << "Enter menu option: ";
		cin >> menuOption;
		cout << endl;
		
This is the first thing you will see as you run the program. Using the first option, "English to Morse code", will allow you to convert words and phrases using the germanic alphabet into the morse code alphabet. Here the user will first type a word or phrase in english and the program will convert it to morse code, displaying the newly encoded word below preceded by a "-->".

		1  English to Morse code
		2  Morse code to English
		3  Conversation mode
		4  Recently encoded words
		5  Recently decoded words
		6  Clear memory
		7  Exit program
		Enter menu option: 1

		Enter a word or a phrase (press [enter] to exit): Example
		--> . -..- .- -- .--. .-.. .
		
By selecting option two you can convert words and phrases from Morse code to the germanic alphabet. Here the user will first type a word or phrase in morse code and the program will convert it back into english, displaying the newly decoded word below preceded by a "-->"

		Enter a word or a phrase in morse code, seperate each word by a space,
		a forward slash and another space ' / '. Seperate each letter by a single
		space (press [enter] to exit): . -..- .- -- .--. .-.. .
		--> example

Option three allows you to have a conversation of sorts. You can convert words and phrases back and forth from english to morse code and then from morse code to english. This pattern will repeat until you prompt the program to stop. The display here will appear very simalar to options one and two but instead of returning immediatly back to the menu options you will be given the option to continue translating words, or continuing the conversation in a sense.

		Converstation mode allows you to encode and decode
		sentances repeatedly, starting with encoding.
		When prompted by "Continue..." press [enter] to continue
		the converstation or press [space] [enter] to leave converstation mode

		Continue...

		Enter a word or a phrase (press [enter] to exit): Hello how are you
		--> .... . .-.. .-.. --- / .... --- .-- / .- .-. . / -.-- --- ..- 

		Enter a word or a phrase in morse code, seperate each word by a space,
		a forward slash and another space ' / '. Seperate each letter by a single
		space (press [enter] to exit): --. --- --- -.. / .- -. -.. / -.-- --- ..-
		--> good and you

		Continue...

The program automatically stores recently decoded and encoded words and phrases in seperate text files. Options 4 and 5 allow you to see your recent words, while option 6 clears this memory.
		EXAMPLE --> . -..- .- -- .--. .-.. . 
		HELLO HOW ARE YOU --> .... . .-.. .-.. --- / .... --- .-- / .- .-. . / -.-- --- ..- 
		
		. -..- .- -- .--. .-.. . --> example
		--. --- --- -.. / .- -. -.. / -.-- --- ..- --> good and you
		
		5  Recently decoded words
		6  Clear memory
		7  Exit program
		Enter menu option: 6

		Memory cleared.
		
The final option will terminate the program.
