//This was created by Pat Buoniconti for unit4 for CIS2571.  It is a GUI for a restaurant bill.

//imports all of the required classes
import java.util.ArrayList;
import java.util.List;
import javafx.application.Application;
import javafx.beans.value.ChangeListener;
import javafx.beans.value.ObservableValue;
import javafx.collections.FXCollections;
import javafx.collections.ObservableList;
import javafx.event.ActionEvent;
import javafx.event.EventHandler;
import javafx.geometry.Insets;
import javafx.scene.Scene;
import javafx.scene.control.Button;
import javafx.scene.control.ComboBox;
import javafx.scene.control.Label;
import javafx.scene.control.ListView;
import javafx.scene.control.TextField;
import javafx.scene.control.TitledPane;
import javafx.scene.image.Image;
import javafx.scene.image.ImageView;
import javafx.scene.input.MouseEvent;
import javafx.scene.layout.GridPane;
import javafx.scene.layout.HBox;
import javafx.scene.layout.VBox;
import javafx.scene.text.Font;
import javafx.scene.text.FontWeight;
import javafx.scene.text.Text;
import javafx.stage.Stage;

public class Restaurant extends Application {
	// Override the start method in the Application class
	public void start(Stage primaryStage) {

		//creates the panes
		//guiPane will be the main hbox that is set on the stage
		HBox guiPane = new HBox(20);
		
		//this will be the whole left side including top
		VBox includesTop = new VBox(10);
		
		//this will be just the picture and store name
		HBox top = new HBox(10);
		
		//this will be used for the right side 
		GridPane primaryPane = new GridPane();
		
		//creates the scene and readies the stage
		Scene billCalculator = new Scene(guiPane, 780, 600);
		primaryStage.setScene(billCalculator);
		primaryStage.setTitle("Restaurant Bill Calculator");
		primaryStage.centerOnScreen();

		//the clear button
		Button btclear = new Button("Clear Bill");
		btclear.setPrefWidth(100);

		//all the labels
		Label tableNumber = new Label("Table Number:");
		Label waiterName = new Label("Waiter's Name:");
		Label beverage = new Label("Beverage:");
		Label appetizers = new Label("Appetizers:");
		Label mainCourse = new Label("Main courses:");
		Label dessert = new Label("Dessert:");
		Label subtotal = new Label("Subtotal: $");
		Label tax = new Label("Tax: $");
		Label total = new Label("Total: $");
		Label waiterFinal = new Label("Waiter:");
		Label tableNumberFinal = new Label("Table No:");
		Label beverageOrdered = new Label("Beverage ordered:");
		Label appetizersOrdered = new Label("Appetizer ordered:");
		Label mainCoursesOrdered = new Label("Main course ordered:");
		Label dessertOrdered = new Label("Dessert ordered:");

		//all the TextFields
		final TextField waiterNameText = new TextField();
		final TextField waiterNameTextBottom = new TextField();
		final TextField tableNoTextBottom = new TextField();
		final TextField tableNumberText = new TextField();
		final TextField subtotalText = new TextField("0.00");
		final TextField taxText = new TextField("0.00");
		final TextField totalText = new TextField("0.00");
		final Text storeName = new Text("Pat's Restaurant");

		//gets the image from online and sizes it
		Image image = new Image(
				"http://www.i2clipart.com/cliparts/5/2/7/8/clipart-fast-food-lunch-dinner-hamburger-5278.png",
				50, 50, false, false);
		ImageView iv1 = new ImageView();
		iv1.setImage(image);
		iv1.maxWidth(10);

		//sets sizing to match the given image on Blackboard
		tableNumberFinal.setMinWidth(100);
		tax.setMinWidth(60);
		waiterFinal.setMinWidth(60);
		subtotal.setMinWidth(100);
		total.setMinWidth(60);
		btclear.setMinWidth(80);
		beverageOrdered.setMinWidth(110);
		appetizersOrdered.setMinWidth(110);
		mainCoursesOrdered.setMinWidth(130);
		dessertOrdered.setMinWidth(110);
		tableNumberText.setMaxWidth(50);
		waiterNameTextBottom.setMaxWidth(60);
		tableNoTextBottom.setMaxWidth(70);
		
		//sets Fonts to match Blackboard
		tableNumberFinal.setFont(Font.font("Verdana", FontWeight.BOLD, 11));
		waiterFinal.setFont(Font.font("Verdana", FontWeight.BOLD, 11));
		total.setFont(Font.font("Verdana", FontWeight.BOLD, 11));
		tax.setFont(Font.font("Verdana", FontWeight.BOLD, 11));
		subtotal.setFont(Font.font("Verdana", FontWeight.BOLD, 11));
		storeName.setFont(Font.font("Verdana", FontWeight.BOLD, 20));

		//sets fill colors
		tableNoTextBottom.setStyle("-fx-background-color: yellow;");
		waiterNameTextBottom.setStyle("-fx-background-color: yellow;");

		//adds image and store name to top
		top.getChildren().add(iv1);
		top.getChildren().add(storeName);

		//places all the waiter and table elements into grid
		GridPane waiterInformationGridPane = new GridPane();
		waiterInformationGridPane.setVgap(10);
		waiterInformationGridPane.setHgap(10);
		waiterInformationGridPane.add(waiterNameText, 1, 1);
		waiterInformationGridPane.add(tableNumberText, 1, 0);
		waiterInformationGridPane.add(tableNumber, 0, 0);
		waiterInformationGridPane.add(waiterName, 0, 1);

		//creates the title pane which allows the title
		TitledPane waiterInformationPane = new TitledPane("Waiter information",
				waiterInformationGridPane);

		primaryPane.add(waiterInformationPane, 0, 0);

		// creates the list of beverages and places it onto combobox
		ObservableList<String> beverageList = FXCollections
				.observableArrayList("Soda", "Tea", "Coffee", "Mineral Water",
						"Juice", "Milk");
		ComboBox beverageBox = new ComboBox(beverageList);

		// creates the list of apps and places it onto combobox
		ObservableList<String> appetizerList = FXCollections
				.observableArrayList("Buffalo Wings", "Buffalo Fingers",
						"Potato Skins", "Nachos", "Mushroom Caps",
						"Shrimp Cocktail", "Chips and Salsa");
		ComboBox appetizerBox = new ComboBox(appetizerList);

		// creates the list of main courses and places it onto combobox
		ObservableList<String> mainCourseList = FXCollections
				.observableArrayList("Seafood Alfredo", "Chicken Alfredo",
						"Chicken Picatta", "Turkey Club", "Lobster Pie",
						"Prime Rib", "Shrimp Scampi", "Turkey Dinner",
						"Stuffed Chicken");
		ComboBox mainCourseBox = new ComboBox(mainCourseList);

		// creates the list of desserts and places it onto combobox
		ObservableList<String> dessertList = FXCollections.observableArrayList(
				"Apple Pie", "Sundae", "Carrot Cake", "Mud Pie", "Apple Crisp");
		ComboBox dessertBox = new ComboBox(dessertList);

		//this section creates the observable lists from wrapping lists which will store the clicked on options from combo box
		List<String> dessertListSelected = new ArrayList<String>();
		ObservableList<String> dessertListSelected1 = FXCollections
				.observableList(dessertListSelected);
		List<String> beverageListSelected = new ArrayList<String>();
		ObservableList<String> beverageListSelected1 = FXCollections
				.observableList(beverageListSelected);
		List<String> appetizerListSelected = new ArrayList<String>();
		ObservableList<String> appetizerListSelected1 = FXCollections
				.observableList(appetizerListSelected);
		List<String> mainCourseListSelected = new ArrayList<String>();
		ObservableList<String> mainCourseListSelected1 = FXCollections
				.observableList(mainCourseListSelected);

		//grid for menu items
		GridPane menuItemsGridPane = new GridPane();
		menuItemsGridPane.setVgap(10);
		menuItemsGridPane.setHgap(10);
		menuItemsGridPane.add(beverage, 0, 0);
		menuItemsGridPane.add(appetizers, 0, 1);
		menuItemsGridPane.add(mainCourse, 0, 2);
		menuItemsGridPane.add(dessert, 0, 3);
		menuItemsGridPane.add(beverageBox, 1, 0);
		menuItemsGridPane.add(appetizerBox, 1, 1);
		menuItemsGridPane.add(mainCourseBox, 1, 2);
		menuItemsGridPane.add(dessertBox, 1, 3);

		//allows the title to be placed above the grid
		TitledPane menuItemTitledPane = new TitledPane("Menu Items",
				menuItemsGridPane);

		primaryPane.add(menuItemTitledPane, 0, 1);

		//creates Listviews that will use the observable lists
		ListView beverageListView = new ListView();
		ListView mainCourseListView = new ListView();
		ListView appetizerListView = new ListView();
		ListView dessertListView = new ListView();

		//sets up the right side of the primary stage
		GridPane itemsOrderedGridPane = new GridPane();
		itemsOrderedGridPane.setVgap(10);
		itemsOrderedGridPane.setHgap(10);
		itemsOrderedGridPane.add(beverageOrdered, 0, 0);
		itemsOrderedGridPane.add(appetizersOrdered, 0, 1);
		itemsOrderedGridPane.add(mainCoursesOrdered, 0, 2);
		itemsOrderedGridPane.add(dessertOrdered, 0, 3);
		itemsOrderedGridPane.add(beverageListView, 1, 0);
		itemsOrderedGridPane.add(mainCourseListView, 1, 2);
		itemsOrderedGridPane.add(appetizerListView, 1, 1);
		itemsOrderedGridPane.add(dessertListView, 1, 3);

		//allows for the title to be added 
		TitledPane itemsOrderedPane = new TitledPane("Items Ordered",
				itemsOrderedGridPane);

		//creates the bill layout
		GridPane billGridPane = new GridPane();
		billGridPane.setVgap(10);
		billGridPane.setHgap(10);
		billGridPane.add(subtotal, 0, 0);
		billGridPane.add(tax, 0, 1);
		billGridPane.add(total, 0, 2);
		billGridPane.add(waiterFinal, 0, 3);
		billGridPane.add(tableNumberFinal, 2, 3);
		billGridPane.add(subtotalText, 1, 0);
		billGridPane.add(taxText, 1, 1);
		billGridPane.add(totalText, 1, 2);
		billGridPane.add(tableNoTextBottom, 3, 3);
		billGridPane.add(waiterNameTextBottom, 1, 3);
		billGridPane.add(btclear, 1, 4);

		//allows for the title 
		TitledPane billPane = new TitledPane("Bill", billGridPane);

		//spacing
		guiPane.setPadding(new Insets(10, 10, 10, 10));
		primaryPane.setHgap(10);
		primaryPane.setVgap(5);

		//adds nodes
		primaryPane.add(billPane, 0, 3);
		includesTop.getChildren().add(top);
		includesTop.getChildren().add(primaryPane);
		guiPane.getChildren().add(includesTop);
		guiPane.getChildren().add(itemsOrderedPane);

		//displays the stage
		primaryStage.show();

		//listens to see if waiter name changes
		waiterNameText.textProperty().addListener(new ChangeListener<String>() {
			@Override
			public void changed(ObservableValue<? extends String> observable,
					String oldValue, String newValue) {

				// checks to see if input is not empty and sets the backgrounds green
				if (!waiterNameText.getText().isEmpty()
						&& waiterNameText.getText() != null) {
					// have to call the credit method
					waiterNameText.setStyle("-fx-background-color: green;");
					waiterNameTextBottom
							.setStyle("-fx-background-color: green;");
					waiterNameTextBottom.setText(waiterNameText.getText());

				}

				// if input is blank sets red background
				else {
					waiterNameText.setStyle("-fx-background-color: red;");
					waiterNameTextBottom.setStyle("-fx-background-color: red;");
				}

			}
		});

		//listens for input and if between 1 and 10 makes it green background
		tableNumberText.textProperty().addListener(
				new ChangeListener<String>() {
					@Override
					public void changed(
							ObservableValue<? extends String> observable,
							String oldValue, String newValue) {

						// checks to see if input is not empty and is of right
					
						try {
							int x = Integer.parseInt(tableNumberText.getText());

							// checks if in range
							if (x > 0 && x < 11) {
								// have to call the credit method
								tableNoTextBottom
										.setStyle("-fx-background-color: green;");
								tableNumberText
										.setStyle("-fx-background-color: green;");
								tableNoTextBottom.setText(tableNumberText
										.getText());

							}

							// if input is is wrong range set background to red
							else {
								tableNoTextBottom
										.setStyle("-fx-background-color: red;");
								tableNoTextBottom.setText("");
								tableNumberText
										.setStyle("-fx-background-color: red;");
							}

							// if number formatting was of wrong type input make red
						} catch (NumberFormatException a) {
							tableNoTextBottom
									.setStyle("-fx-background-color: red;");
							tableNumberText
									.setStyle("-fx-background-color: red;");
						}
					}
				});

		//listens to combo box and adds selection to the list, this is repeated four times, once for each combobox
		appetizerBox.getSelectionModel().selectedItemProperty()
				.addListener(new ChangeListener<String>() {
					@Override
					public void changed(
							ObservableValue<? extends String> observable,
							String oldValue, String newValue) {
						
						//adds to the observable list indirectly
						appetizerListSelected1.add(newValue);
						appetizerListView.setItems(appetizerListSelected1);
						
						//adds the new selection to the bill
						addBill(newValue,
								Double.parseDouble(subtotalText.getText()),
								subtotalText, taxText, totalText);
					}
				});

		beverageBox.getSelectionModel().selectedItemProperty()
				.addListener(new ChangeListener<String>() {
					@Override
					public void changed(
							ObservableValue<? extends String> observable,
							String oldValue, String newValue) {
						beverageListSelected1.add(newValue);
						beverageListView.setItems(beverageListSelected1);
						addBill(newValue,
								Double.parseDouble(subtotalText.getText()),
								subtotalText, taxText, totalText);
					}
				});

		mainCourseBox.getSelectionModel().selectedItemProperty()
				.addListener(new ChangeListener<String>() {
					@Override
					public void changed(
							ObservableValue<? extends String> observable,
							String oldValue, String newValue) {
						mainCourseListSelected1.add(newValue);
						mainCourseListView.setItems(mainCourseListSelected1);
						addBill(newValue,
								Double.parseDouble(subtotalText.getText()),
								subtotalText, taxText, totalText);

					}
				});

		dessertBox.getSelectionModel().selectedItemProperty()
				.addListener(new ChangeListener<String>() {
					@Override
					public void changed(
							ObservableValue<? extends String> observable,
							String oldValue, String newValue) {
						dessertListSelected1.add(newValue);
						dessertListView.setItems(dessertListSelected1);
						addBill(newValue,
								Double.parseDouble(subtotalText.getText()),
								subtotalText, taxText, totalText);
					}
				});

		//listens for a double click and if found removes the item at that index on list, repeats four times, for each list
		mainCourseListView.setOnMouseClicked(new EventHandler<MouseEvent>() {

			@Override
			public void handle(MouseEvent click) {

				if (click.getClickCount() == 2) {
					// makes a string of the thing clicked on
					String removed = ""
							+ mainCourseListView.getSelectionModel()
									.getSelectedItem();
					
					//removes that from the observable list
					mainCourseListSelected1.remove(mainCourseListView
							.getSelectionModel().getSelectedIndex());
					
					//removes the item from the price
					removeBill(removed,
							Double.parseDouble(subtotalText.getText()),
							subtotalText, taxText, totalText);
				}
			}
		});

		beverageListView.setOnMouseClicked(new EventHandler<MouseEvent>() {

			@Override
			public void handle(MouseEvent click) {

				if (click.getClickCount() == 2) {
					// Use ListView's getSelected Item
					String removed = ""
							+ beverageListView.getSelectionModel()
									.getSelectedItem();
					beverageListSelected1.remove(beverageListView
							.getSelectionModel().getSelectedIndex());
					removeBill(removed,
							Double.parseDouble(subtotalText.getText()),
							subtotalText, taxText, totalText);
				}
			}
		});

		appetizerListView.setOnMouseClicked(new EventHandler<MouseEvent>() {

			@Override
			public void handle(MouseEvent click) {

				if (click.getClickCount() == 2) {
					// Use ListView's getSelected Item
					String removed = ""
							+ appetizerListView.getSelectionModel()
									.getSelectedItem();
					appetizerListSelected1.remove(appetizerListView
							.getSelectionModel().getSelectedIndex());
					removeBill(removed,
							Double.parseDouble(subtotalText.getText()),
							subtotalText, taxText, totalText);
				}
			}
		});

		dessertListView.setOnMouseClicked(new EventHandler<MouseEvent>() {

			@Override
			public void handle(MouseEvent click) {

				if (click.getClickCount() == 2) {
					// Use ListView's getSelected Item
					String removed = ""
							+ dessertListView.getSelectionModel()
									.getSelectedItem();
					dessertListSelected1.remove(dessertListView
							.getSelectionModel().getSelectedIndex());
					removeBill(removed,
							Double.parseDouble(subtotalText.getText()),
							subtotalText, taxText, totalText);
				}
			}
		});

		// event handler for the clear button
		btclear.setOnAction(new EventHandler<ActionEvent>() {
			@Override
			public void handle(ActionEvent e) {
				
				//clears all the texts back to zeros and removes all elements from the list
				subtotalText.setText("0.00");

				taxText.setText("0.00");

				totalText.setText("0.00");

				appetizerListSelected1.clear();
				mainCourseListSelected1.clear();
				beverageListSelected1.clear();
				dessertListSelected1.clear();

			}
		});

	}

	//for whatever string is passed, the switch statement properly updates the total by adding the proper cost
	public static void addBill(String added, double oldSubtotal,
			TextField subtotalText, TextField taxText, TextField totalText) {
		switch (added) {
		case "Buffalo Wings": {
			oldSubtotal = oldSubtotal + 5.95;
			printBill(oldSubtotal, subtotalText, taxText, totalText);
			break;
		}
		case "Buffalo Fingers": {
			oldSubtotal = oldSubtotal + 6.95;
			printBill(oldSubtotal, subtotalText, taxText, totalText);
			break;
		}
		case "Potato Skins": {
			oldSubtotal = oldSubtotal + 8.95;
			printBill(oldSubtotal, subtotalText, taxText, totalText);
			break;
		}
		case "Nachos": {
			oldSubtotal = oldSubtotal + 8.95;
			printBill(oldSubtotal, subtotalText, taxText, totalText);
			break;
		}
		case "Mushroom Caps": {
			oldSubtotal = oldSubtotal + 10.95;
			printBill(oldSubtotal, subtotalText, taxText, totalText);
			break;
		}
		case "Shrimp Cocktail": {
			oldSubtotal = oldSubtotal + 12.95;
			printBill(oldSubtotal, subtotalText, taxText, totalText);
			break;
		}
		case "Chips and Salsa": {
			oldSubtotal = oldSubtotal + 6.95;
			printBill(oldSubtotal, subtotalText, taxText, totalText);
			break;
		}
		case "Soda": {
			oldSubtotal = oldSubtotal + 1.95;
			printBill(oldSubtotal, subtotalText, taxText, totalText);
			break;
		}
		case "Tea": {
			oldSubtotal = oldSubtotal + 1.50;
			printBill(oldSubtotal, subtotalText, taxText, totalText);
			break;
		}
		case "Coffee": {
			oldSubtotal = oldSubtotal + 1.25;
			printBill(oldSubtotal, subtotalText, taxText, totalText);
			break;
		}
		case "Mineral Water": {
			oldSubtotal = oldSubtotal + 2.95;
			printBill(oldSubtotal, subtotalText, taxText, totalText);
			break;
		}
		case "Juice": {
			oldSubtotal = oldSubtotal + 2.50;
			printBill(oldSubtotal, subtotalText, taxText, totalText);
			break;
		}
		case "Milk": {
			oldSubtotal = oldSubtotal + 1.50;
			printBill(oldSubtotal, subtotalText, taxText, totalText);
			break;
		}
		case "Apple Pie": {
			oldSubtotal = oldSubtotal + 5.95;
			printBill(oldSubtotal, subtotalText, taxText, totalText);
			break;
		}
		case "Sundae": {
			oldSubtotal = oldSubtotal + 3.95;
			printBill(oldSubtotal, subtotalText, taxText, totalText);
			break;
		}
		case "Carrot Cake": {
			oldSubtotal = oldSubtotal + 5.95;
			printBill(oldSubtotal, subtotalText, taxText, totalText);
			break;
		}
		case "Mud Pie": {
			oldSubtotal = oldSubtotal + 4.95;
			printBill(oldSubtotal, subtotalText, taxText, totalText);
			break;
		}
		case "Apple Crisp": {
			oldSubtotal = oldSubtotal + 5.95;
			printBill(oldSubtotal, subtotalText, taxText, totalText);
			break;
		}
		case "Seafood Alfredo": {
			oldSubtotal = oldSubtotal + 15.95;
			printBill(oldSubtotal, subtotalText, taxText, totalText);
			break;
		}
		case "Chicken Alfredo": {
			oldSubtotal = oldSubtotal + 13.95;
			printBill(oldSubtotal, subtotalText, taxText, totalText);
			break;
		}
		case "Chicken Picatta": {
			oldSubtotal = oldSubtotal + 13.95;
			printBill(oldSubtotal, subtotalText, taxText, totalText);
			break;
		}
		case "Turkey Club": {
			oldSubtotal = oldSubtotal + 11.95;
			printBill(oldSubtotal, subtotalText, taxText, totalText);
			break;
		}
		case "Lobster Pie": {
			oldSubtotal = oldSubtotal + 19.95;
			printBill(oldSubtotal, subtotalText, taxText, totalText);
			break;
		}
		case "Prime Rib": {
			oldSubtotal = oldSubtotal + 20.95;
			printBill(oldSubtotal, subtotalText, taxText, totalText);
			break;
		}
		case "Shrimp Scampi": {
			oldSubtotal = oldSubtotal + 18.95;
			printBill(oldSubtotal, subtotalText, taxText, totalText);
			break;
		}
		case "Turkey Dinner": {
			oldSubtotal = oldSubtotal + 13.95;
			printBill(oldSubtotal, subtotalText, taxText, totalText);
			break;
		}
		case "Stuffed Chicken": {
			oldSubtotal = oldSubtotal + 14.95;
			printBill(oldSubtotal, subtotalText, taxText, totalText);
			break;
		}
		}
	}

	//uses the subtotal passed from the removeBill/addBill methods to edit the final textfield values
	public static void printBill(double subtotal, TextField subtotalText,
			TextField taxText, TextField totalText) {
		String subtotals = String.format("%.2f", (subtotal));
		subtotalText.setText(subtotals);

		String taxes = String.format("%.2f", ((subtotal * .08)));
		taxText.setText(taxes);

		String totals = String.format("%.2f", (((.08 * subtotal) + subtotal)));
		totalText.setText(totals);
	}
	
	//for whatever string is passed, the switch statement properly updates the total by removing the proper cost
	public static void removeBill(String removed, double oldSubtotal,
			TextField subtotalText, TextField taxText, TextField totalText) {
		switch (removed) {
		case "Buffalo Wings": {
			oldSubtotal = oldSubtotal - 5.95;
			printBill(oldSubtotal, subtotalText, taxText, totalText);
			break;
		}
		case "Buffalo Fingers": {
			oldSubtotal = oldSubtotal - 6.95;
			printBill(oldSubtotal, subtotalText, taxText, totalText);
			break;
		}
		case "Potato Skins": {
			oldSubtotal = oldSubtotal - 8.95;
			printBill(oldSubtotal, subtotalText, taxText, totalText);
			break;
		}
		case "Nachos": {
			oldSubtotal = oldSubtotal - 8.95;
			printBill(oldSubtotal, subtotalText, taxText, totalText);
			break;
		}
		case "Mushroom Caps": {
			oldSubtotal = oldSubtotal - 10.95;
			printBill(oldSubtotal, subtotalText, taxText, totalText);
			break;
		}
		case "Shrimp Cocktail": {
			oldSubtotal = oldSubtotal - 12.95;
			printBill(oldSubtotal, subtotalText, taxText, totalText);
			break;
		}
		case "Chips and Salsa": {
			oldSubtotal = oldSubtotal - 6.95;
			printBill(oldSubtotal, subtotalText, taxText, totalText);
			break;
		}
		case "Soda": {
			oldSubtotal = oldSubtotal - 1.95;
			printBill(oldSubtotal, subtotalText, taxText, totalText);
			break;
		}
		case "Tea": {
			oldSubtotal = oldSubtotal - 1.50;
			printBill(oldSubtotal, subtotalText, taxText, totalText);
			break;
		}
		case "Coffee": {
			oldSubtotal = oldSubtotal - 1.25;
			printBill(oldSubtotal, subtotalText, taxText, totalText);
			break;
		}
		case "Mineral Water": {
			oldSubtotal = oldSubtotal - 2.95;
			printBill(oldSubtotal, subtotalText, taxText, totalText);
			break;
		}
		case "Juice": {
			oldSubtotal = oldSubtotal - 2.50;
			printBill(oldSubtotal, subtotalText, taxText, totalText);
			break;
		}
		case "Milk": {
			oldSubtotal = oldSubtotal - 1.50;
			printBill(oldSubtotal, subtotalText, taxText, totalText);
			break;
		}
		case "Apple Pie": {
			oldSubtotal = oldSubtotal - 5.95;
			printBill(oldSubtotal, subtotalText, taxText, totalText);
			break;
		}
		case "Sundae": {
			oldSubtotal = oldSubtotal - 3.95;
			printBill(oldSubtotal, subtotalText, taxText, totalText);
			break;
		}
		case "Carrot Cake": {
			oldSubtotal = oldSubtotal - 5.95;
			printBill(oldSubtotal, subtotalText, taxText, totalText);
			break;
		}
		case "Mud Pie": {
			oldSubtotal = oldSubtotal - 4.95;
			printBill(oldSubtotal, subtotalText, taxText, totalText);
			break;
		}
		case "Apple Crisp": {
			oldSubtotal = oldSubtotal - 5.95;
			printBill(oldSubtotal, subtotalText, taxText, totalText);
			break;
		}
		case "Seafood Alfredo": {
			oldSubtotal = oldSubtotal - 15.95;
			printBill(oldSubtotal, subtotalText, taxText, totalText);
			break;
		}
		case "Chicken Alfredo": {
			oldSubtotal = oldSubtotal - 13.95;
			printBill(oldSubtotal, subtotalText, taxText, totalText);
			break;
		}
		case "Chicken Picatta": {
			oldSubtotal = oldSubtotal - 13.95;
			printBill(oldSubtotal, subtotalText, taxText, totalText);
			break;
		}
		case "Turkey Club": {
			oldSubtotal = oldSubtotal - 11.95;
			printBill(oldSubtotal, subtotalText, taxText, totalText);
			break;
		}
		case "Lobster Pie": {
			oldSubtotal = oldSubtotal - 19.95;
			printBill(oldSubtotal, subtotalText, taxText, totalText);
			break;
		}
		case "Prime Rib": {
			oldSubtotal = oldSubtotal - 20.95;
			printBill(oldSubtotal, subtotalText, taxText, totalText);
			break;
		}
		case "Shrimp Scampi": {
			oldSubtotal = oldSubtotal - 18.95;
			printBill(oldSubtotal, subtotalText, taxText, totalText);
			break;
		}
		case "Turkey Dinner": {
			oldSubtotal = oldSubtotal - 13.95;
			printBill(oldSubtotal, subtotalText, taxText, totalText);
			break;
		}
		case "Stuffed Chicken": {
			oldSubtotal = oldSubtotal - 14.95;
			printBill(oldSubtotal, subtotalText, taxText, totalText);
			break;
		}
		}
	}

	/**
	 * The main method is only needed for the IDE with limited JavaFX support.
	 * Not needed for running from the command line.
	 */
	public static void main(String[] args) {
		launch(args);
	}
}
