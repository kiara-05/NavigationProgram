# Project Part [2]

 In Part 2 of my FAMU Campus Map Navigator project, I am building upon the functionality from Part 1 by incorporating user interaction with a menu system using loops and switch statements. This phase allows the user to input their current location and destination, view a list of available buildings, and navigate through the program's options. The data for the buildings is loaded from a CSV file, and the program provides a user-friendly menu to interact with the campus map

## Table of Contents
1. [Statement of Independent Effort](#statement-of-independent-effort)
1. [Analysis of Specifications](#analysis-of-specifications)
    - [Main](#main)
1. [Pseudocode](#pseudocode)
1. [Flowchart](#flowchart)
1. [Test Cases](#test-cases)
1. [Code](#code)
1. [User Manual](#user-guide)
1. [References](#references)

## Statement of Independent Effort




I, Kiara Pee, hereby certify that this is my original work completed with the assistance of the resources listed in the reference. I used these resources in the following areas: Syntax and Error Handling.


## Analysis of Specifications

This section outlines the inputs, processes, and outputs of my project. The program uses a CSV file to store building names and coordinates (latitude and longitude), and allows the user to perform actions like entering their location and destination, viewing available buildings, and navigating through the program using a menu system.

### Main

_Fill in the values in the IPO Chart. See video in Canvas for example._

| Input    | Process  | Output   |
| -------- | -------- | -------- |
| CSV file with builidng data     | Load data into program memory using loadBuilidngData     | Building names and coordinates loaded     |
| User's location and desitination     | Get the user's location and destination from input     | Display confirmation of location and destination     |
| User's menu choice     | Execute action based on user's menu selection     | Perform corresponding action     |


## Pseudocode

```text=
BEGIN Main
    DECLARE String location, destination
    DECLARE Int choice
    
    // Load building data
    LOAD building data from CSV file into memory
    
    DO
        DISPLAY menu options (1. Enter your location and destination, 2. View all available buildings, 3. Exit)
        GET user choice
        
        SWITCH choice
            CASE 1:
                PROMPT user for location and destination
                DISPLAY "You are at [location] and your destination is [destination]."
            CASE 2:
                DISPLAY list of all available buildings
            CASE 3:
                EXIT program
        END SWITCH
    WHILE choice != 3
END

```

## Flowchart

_https://lucid.app/lucidchart/f6ded7ef-150e-4b9f-b179-e076d9374210/edit?viewport_loc=-622%2C-762%2C2758%2C2640%2C0_0&invitationId=inv_359261d1-f559-4925-9506-2f107f447ec4_

[//]: <> (The syntax to add an image can be found here - https://www.markdownguide.org/basic-syntax/#images-1)

## Test Cases

|Case #|Case Description|Input|Condition (e.g., invalid input) |Output|
|:---:|:---|:---|:---:|:---|
|1|User selects "View all available buildings"|Menu option 2|Valid input |Displays the list of building|
|2|User inputs a valid location and destination|Location: "Library", Destination: "Student Center" |Valid location and destination|Displays confirmation: "You are at Library and your destination is Student Center.|
|3|User selects invalid menu option|Menu option 5|Invalid menu option|Error message: "Invalid choice. Please try again."  |
|4|User selects "Exit" option|Menu option 3|Valid input|Exits the program with "Exiting the program..." message|
|5|User inputs location with leading/trailing spaces|Location: " Library |Location input with extra spaces|  Displays confirmation without spaces: "You are at Library..."|


## Code

_https://codio.com/home/projects?sharedToken=c1e5ad80-e8f1-4130-99dc-e1520b497f49_
```text=
/*For Part two  of my project I'm adding feautures for user interaction in the Menu System,
 using switch statements and loops*/

#include <iostream>
#include <fstream> //handles file input and output
#include <string> //for storing and manipulating building names and other textual data
#include <sstream> //Used to seperate the  in my csv file into seperate values 
#include <vector>// I chose vector over array incase I decide to expand on the project and add more builidings

//Define the struct to hold the buildings data
struct Building {
    std::string name;
    double latitude, longitude;

};


//Declare vector to store the buildings
std::vector<Building> buildings;


//Function to read from the csv file
void loadBuildingData(const std::string& filename) {
    std::ifstream file(filename);//Attempt to open file

    //Part 2- Check if file was opened
    if (!file.is_open()) {
        std::cerr << "Error: Could not open the file '" << filename << "'. Please check if it exists and is accessible.\n";
        return;
    }
   
   
    std::string line;


    std::getline(file, line);


    while (std::getline(file, line)) {
        std::stringstream ss(line);
        std::string name, latStr, lonStr;
        double lat, lon;

        // Read the building name, latitude, and longitude from each line
        std::getline(ss, name, ',');
        std::getline(ss, latStr, ',');
        std::getline(ss, lonStr, ',');
        
        lat = std::stod(latStr);
        lon = std::stod(lonStr);
        
        // This stores the information in the programs memory by creating a Building object and adding it to the vector
        buildings.push_back({name, lat, lon});
    }

    file.close();

}



//Function to display the building names
void displayBuildings() {
    std::cout << "Buildings on campus:\n";
    for (const auto& building : buildings) {
        std::cout << building.name << "\n";
    }
}

//Part 2- Iplementing the menu 
//Load and display the building data in the main function 
int main() {
    //load
    loadBuildingData("locations.csv");

    int choice = 0;

    do {
        std::cout << "\nMenu: \n";
        std::cout << "1. Enter your location and destination \n";
        std::cout << "2. View all available buildings\n"; 
        std::cout << "3. Exit\n";
        std::cout << "Enter your choice: ";
        
        
        std::cin >> choice;

    

        switch (choice) {
            case 1: {
                std::string location, destination;
                std::cout << "Enter your current location: ";
                std::cin.ignore(); // To ignore leftover newline
                std::getline(std::cin, location);
                std::cout << "Enter your destination: ";
                std::getline(std::cin, destination);
                std::cout << "You are at " << location << " and your destination is " << destination << ".\n";
                break;
            }
            case 2:
                displayBuildings();
                break;

            case 3:
                std::cout << "Exiting the program...\n";
                break;
            default:
                std::cout << "Invalid choice. Please try again :/ \n";

        }

    } while (choice != 3);
   

    return 0;

}
```

## User Manual

[User Manual](GUIDE.md) <br/>

## References

Deitel, H., & Deitel, P. (2024). C++ How to Program: An objects-neutral approach (11th ed.). Pearson.
Unit 8: Functions and an intro to function templates.

Malik, D. S. (2017). C++ Programming: From problem analysis to program design (8th ed.). Cengage Learning.
Unit 16, Section 16.2.

Programiz. (n.d.). Functions in C++. Programiz. Retrieved December 6, 2024, from https://www.programiz.com/cpp-programming/function

YouTube. (2020, March 3). Functions in C++ (C++ programming tutorial for beginners) [Video]. YouTube.
https://www.youtube.com/watch?v=V9zuox47zr0

YouTube. (2021, January 25). C++ Functions tutorial for beginners | Learn functions in C++ [Video]. YouTube.
https://www.youtube.com/watch?v=a10a11oxjrA

YouTube. (2020, April 17). Introduction to functions in C++ | C++ Tutorial | Learn C++ programming [Video]. YouTube.
https://www.youtube.com/watch?v=SGyutdso6_c&t=1s

Smith, J. (2021). Advanced C++ programming: Functions and templates. Tech Publications.

Brown, L. (2019). Mastering function implementation in C++. Code Press.





