# Pantry Prequel
### Helps the user keep track of any food, and that food's expiration dates, in their pantry.

## Introduction
As a poor college student, trying to eat healthily, I’ve wasted a lot of food by letting it get old. Whether my bread gets moldy or my milk goes sour I can never seem to finish the things I buy before they go bad; this happens in part because I forget about what food I have in the cupboard and also in part because I’m just not creative enough with food to know what to make. “The Pantry Prequel” will help take care of this problem by keeping track of what food the user has and reminding you when that food will expire. It will also provide recipes with the ingredients that are going to expire soon. In the future I plan to make this program a fully functional app with a handful of other features. 

## Example Code
This section of code checks all the food in your inventory to make sure it is not expiring within the next week.

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
	}
	
This portion of code takes what ingredients a user as imputed searches the web for recipes including those ingredients. The user can also include ingredients they want to exclude.

		//search button
		HBox btnPane = new HBox(10);
		btnPane.setAlignment(Pos.CENTER_RIGHT);
		Button searchBtn = new Button("Search");
		searchBtn.setOnAction(e -> {
			String includeText = includeTF.getText().replace(", ", ",");
			includeText = includeText.replace(" ", "%20");
			String excludeText = excludeTf.getText().replace(", ", ",");
			excludeText = excludeText.replace(" ", "%20");
			String searchStr = "http://www.allrecipes.com/search/results/?ingIncl=" + includeText + "&ingExcl=" + excludeText + "&sort=re";
			getHostServices().showDocument(searchStr);
		});
		
		Button clearButton = new Button("Clear");
		clearButton.setOnAction(e -> {
			includeTF.setText("");
			excludeTf.setText("");
		});
		btnPane.getChildren().addAll(clearButton, searchBtn);
		
		//data for list view
		String[] foodNames = new String[foodList.length];
		for(int i = 0; i < foodList.length; i++){
			String[] pantryItem = getPantryItem(foodList[i]);
			foodNames[i] = pantryItem[1];
			foodNames[i] += " (Expires: ";
			foodNames[i] += pantryItem[2];
			foodNames[i] += ")";
		}
		
		//list view
		ListView<String> foodListView = new ListView<String>();
		ObservableList<String> items = FXCollections.observableArrayList(foodNames);
		foodListView.setItems(items);
		foodListView.setOnMouseClicked(e -> {
			int add = foodListView.getFocusModel().getFocusedIndex();
			String tempText = includeTF.getText();
			tempText = tempText.trim();
			if (tempText.length() > 0)
				if (tempText.charAt(tempText.length()-1) != ',')
					tempText += ", ";
			tempText += getPantryItem(foodList[add])[1];
			includeTF.setText(tempText);
		});

## Installation
For instalation, download the .zip file. All the files you need are in the src folder. Once you have opened the src folder open the "PantryPrequel.java" file. This is the file you will need to run any tests.

## Tests	
<img src = "https://github.com/14thansen/Pantry-Prequel/blob/master/Screen%20Shot%202018-04-26%20at%209.29.40%20AM.png"/>

This is the first thing you will see as you run the program. If you click the about button a window will appear that will give you some basic information app using the app.

To empty the inventory just erase the "pantry.txt" file in the src folder.

<img src = "https://github.com/14thansen/Pantry-Prequel/blob/master/Screen%20Shot%202018-04-26%20at%209.41.53%20AM.png"/>
		
You can access this window by clicking the add food button from the previous window. Here if you miss any imformation the program will tell you what you need to fix.

<img src = "https://github.com/14thansen/Pantry-Prequel/blob/master/Screen%20Shot%202018-04-26%20at%209.48.31%20AM.png"/>

This window is accessed by clicking on the search button from the first screen. By clicking on foods from the table you can add them to your "include" text box. Once you press search it will open a website in a browser window with a custom search based on the foods you put in your include and exclude text boxes.

<img src = "https://github.com/14thansen/Pantry-Prequel/blob/master/Screen%20Shot%202018-04-26%20at%209.51.26%20AM.png"/>

This window is accessed by clicking on any food. If you attempt to change the expiration date incorrectly it will automatically reset the expiration date back to what it was before.

## Motivation
I created this project for my final project at school. I was inspired however, by my brother-in-law. It was his idea, I'm just helping make it a reality.
