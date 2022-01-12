#include <iostream>
#include <string>
#include "Menu.cpp"
using namespace std;

int main(int argc, char** argv)
{
	Menu menu;
	while (true) {
		menu.printMenu();
		cout << "\nWelcome! What kind of drink do you prefer to have ? (Coffee or Tea): ";
		string input;
		cin >> input;
		if (input == "Coffee" || input == "coffee" || input == "c" || input == "C") {
			menu.prepareCoffee();
			break;
		}
		else if (input == "Tea" || input == "tea" || input == "t" || input == "T") {
			menu.prepareTea();
			break;
		}
		else if (input == "Quit" || input == "quit" || input == "q" || input == "Q") {
			cout << "\nThanks, Hope you will visit us again.\n";
			break;
		}
		else {
			cout << "\n Kindly enter Coffee, Tea or Quit to exit the program\n";
		}
	}
	return 0;
}

  
  #include <iostream>
#include <iomanip>
#include "MenuItem.cpp"
using namespace std;

class Menu {
private:
	MenuItem* coffees;
	MenuItem* teas;

	void addSugar() {
	sugar:
		cout << endl << " Would you like to have some sugar (Y/N): ";
		string input;
		cin >> input;
		if (input.length() > 1) {
			cout << endl << "Kindly enter Y or N" << endl;
			goto sugar;
		}
		switch (input[0]) {
		case 'y':
		case 'Y':
			break;
		case 'n':
		case 'N':
			break;
		default:
			cout << endl << "Kindly enter Y or N" << endl;
			goto sugar;
		}
	}

	void collectAmount(MenuItem item) {
	price:
		cout << endl << "Kindly pay " << item.getPrice() << " AED: ";
		string input;
		cin >> input;
		int itemPrice = -1;
		try {
			itemPrice = stoi(input);
		}
		catch (...) {
		}
		if (itemPrice == -1) {
			cout << endl << "Kindly enter digits only!" << endl;
			goto price;
		}
		else if (itemPrice < item.getPrice()) {
			cout << "\nYou have enter amount less than " << item.getPrice() << endl;
			goto price;
		}
		else if (itemPrice - item.getPrice() > 0) {
			cout << "\nYour change is " << itemPrice - item.getPrice() << " AED" << endl;
		}
	}

public:
	Menu() {
		coffees = new MenuItem[3];
		coffees[0] = MenuItem("Ice Coffee", 3);
		coffees[1] = MenuItem("Milk Coffee", 2);
		coffees[2] = MenuItem("Black Coffee", 1);
		teas = new MenuItem[3];
		teas[0] = MenuItem("Ice Tea", 3);
		teas[1] = MenuItem("Milk Tea", 2);
		teas[2] = MenuItem("Black Tea", 1);
	}

	void printMenu() {
		cout << endl << left << setw(20) << "Coffee" << left << setw(20) << "Price (AED)";
		cout << left << setw(20) << "Tea" << left << setw(10) << "Price (AED)" << endl;
		for (int i = 0; i < 3; i++) {
			cout << left << setw(20) << coffees[i].getName() << left << setw(20) << coffees[i].getPrice();
			cout << left << setw(20) << teas[i].getName() << left << setw(10) << teas[i].getPrice() << endl;
		}
	}

	void prepareCoffee() {
	prepare:
		cout << endl << "Which Coffee flavor do you wish to try?(Ice, Milk or Black): ";
		string input;
		cin >> input;
		if (input == "Ice" || input == "ice" || input == "I" || input == "i") {
			addSugar();
			collectAmount(coffees[0]);
		}
		else if (input == "Milk" || input == "milk" || input == "M" || input == "m") {
			addSugar();
			collectAmount(coffees[1]);
		}
		else if (input == "Black" || input == "black" || input == "B" || input == "b") {
			addSugar();
			collectAmount(coffees[2]);
		}
		else {
			cout << endl << "Kindly enter Ice, Milk or Black" << endl;
			goto prepare;
		}
	}

	void prepareTea() {
	prepare:
		cout << endl << "Which Tea flavor do you wish to try? (Ice, Milk or Black): ";
		string input;
		cin >> input;
		if (input == "Ice" || input == "ice" || input == "I" || input == "i") {
			addSugar();
			collectAmount(teas[0]);
		}
		else if (input == "Milk" || input == "milk" || input == "M" || input == "m") {
			addSugar();
			collectAmount(teas[1]);
		}
		else if (input == "Black" || input == "black" || input == "B" || input == "b") {
			addSugar();
			collectAmount(teas[2]);
		}
		else {
			cout << endl << "Kindly enter Ice, Milk or Black" << endl;
			goto prepare;
		}
	}

	~Menu() {
		delete[] coffees;
		delete[] teas;
	}
};



#include <string>
using namespace std;

class MenuItem {
private:
	string name;
	int price;

public:
	MenuItem() {

	}

	MenuItem(string name, int price) {
		this->name = name;
		if (price >= 0) { 
			this->price = price;
		} else{
			this->price = 0;
		}
	}

	int getPrice() {
		return price;
	}

	string getName() {
		return name;
	}
};

  
  
