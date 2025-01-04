# Project Part [1]


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

_This section outlines the inputs, processes, and outputs of my project. The program loads building data from a CSV file, storing the building names and coordinates (latitude and longitude). Part 2 is about getting prepared to implement user interaction through a menu system, where users can input their location and destination and view available buildings. While the menu functionality is not yet implemented, this phase lays the groundwork for user interaction._

### Main

| Input    | Process  | Output   |
| -------- | -------- | -------- |
| CSV file with building data	|Load data into program memory using loadBuildingData |	Building names and coordinates loaded |
| User's location and destination (future implementation) | Prepare to capture user input for location and destination | Display confirmation of location and destination (future output) |
| Building data in memory | Prepare to display available buildings in menu | List of buildings (future output) |


## Pseudocode

```text=
BEGIN Main
    DECLARE String location, destination
    DECLARE Int choice
    
    // Load building data
    LOAD building data from CSV file into memory
    
    // Preparing for menu interaction
    DO
        DISPLAY (Placeholder for menu options)
        GET user choice
        
        // Menu options and user interaction will be implemented in future stages
        
    WHILE choice != 3  // Placeholder for menu exit condition
END

```

## Flowchart

_https://lucid.app/lucidchart/e170fb0b-b05c-4bd8-98b5-099db3167f3a/view_

[//]: <> (The syntax to add an image can be found here - https://www.markdownguide.org/basic-syntax/#images-1)

## Test Cases

|Case #|Case Description|Input|Condition |Output|
|:---:|:---|:---|:---:|:---|
|1|Building data is successfully loaded |	CSV file with building data |	Valid file | Displays the list of buildings after menu is implemented|
|2|User inputs valid location and destination (future) |	Location: "Library", Destination: "Student Center"	| Valid location and destination |	Displays confirmation message (to be implemented in later phases)|
|3|User inputs invalid location (future)| Location: "Invalid Building" | Invalid location	Error message: | "Invalid location. Please try again." (to be implemented)|
|4|User inputs destination (future)	| Destination: "Student Center" | Valid destination |	Displays confirmation message (to be implemented in later phases)|


## Code

_(https://codio.com/home/projects?sharedToken=c1e5ad80-e8f1-4130-99dc-e1520b497f49)_
```text=
/*For Part one of my project I'm focusing on loading the data from locations.csv and filing it, I will do this 
through vectors*/

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
    std::ifstream file(filename);
    std::string line;


    std:: getline(file,line);


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



//Function to display the buildijng names
void displayBuildings() {
    std::cout << "Buildings on campus:\n";
    for (const auto& building : buildings) {
        std::cout << building.name << "\n";
    }
}
//Load and display the building data in the main function 
int main() {
    //load
    loadBuildingData("locations.csv");


    //display
    displayBuildings();

    return 0;
}
```
## User Manual

[User Manual](GUIDE.md) <br/>

## References

Deitel, H., & Deitel, P. (2024). C++ How to program: An objects-neutral approach (11th ed.). Pearson.
Malik, D. S. (2017). C++ programming: From problem analysis to program design (8th ed.). Cengage Learning.
Programiz. (n.d.). Functions in C++. Retrieved December 6, 2024, from https://www.programiz.com/cpp-programming/function

