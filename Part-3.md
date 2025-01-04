# Project Part [.3]
[//]: <> (Basic markdown syntax can be found here -https://www.markdownguide.org/basic-syntax/)
[//]: <> (Copy this file and rename it based on the submission number, i.e., PART1.md. Remove all the comments and italisized text before submitting.)
_In Part 3 of my FAMU Campus Map Navigator project, I am building upon the functionality from Part 2 by updating the directions and adding actual routes.. This phase allows the user to input their current location and destination, view a list of available buildings, and navigate through the program's options. The data for the buildings is loaded from a CSV file, and the program provides a user-friendly menu to interact with the campus map.
._
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
I, Kiara Pee, hereby certify that this is my original work completed with the assistance of ***[NAME]***/the resources listed in the reference. I used these resources in the following areas: ***[...]***.
## Analysis of Specifications
_This section outlines the inputs, processes, and outputs of my project. The program uses a CSV file to store building names and coordinates (latitude and longitude), and allows the user to perform actions like entering their location and destination, viewing available buildings, and navigating through the program using a menu system.
_
### Main
| Input                                                | Process                                                              | Output                                                    |
|------------------------------------------------------|----------------------------------------------------------------------|-----------------------------------------------------------|
| User inputs a location and destination               | Program checks if the location and destination are in the buildings list | Directions from the location to the destination, or "Invalid location or destination" |
| User selects the option to view all available buildings | Program reads the building names from the CSV file                     | List of all building names                                |
| User enters a location that is not in the buildings list | Program searches for the location and doesn't find it                | "Invalid location or destination"                         |
| User enters a destination that is not in the buildings list | Program searches for the destination and doesn't find it              | "Invalid location or destination"                         |
## Pseudocode
```text=
START
    DEFINE Building as a structure with:
        - name (string)
        - latitude (double)
        - longitude (double)
        - directions (string)
    DEFINE Route as a structure with:
        - startBuilding (string)
        - endBuilding (string)
        - startLatitude (double)
        - startLongitude (double)
        - endLatitude (double)
        - endLongitude (double)
        - directions (string)
    DECLARE vector buildings as a list of Building objects
    FUNCTION loadBuildingData(filename)
        OPEN file with the given filename
        IF file is not open
            PRINT "Error: Could not open the file"
            RETURN
        ENDIF
        READ the first line (header) and ignore
        WHILE there is another line in the file
            SPLIT the line into components using commas
            STORE each component in appropriate variables
            CREATE a Building object with the extracted data
            ADD the Building object to the buildings vector
        END WHILE
        CLOSE the file
    END FUNCTION
    FUNCTION displayBuildings()
        PRINT "Buildings on campus:"
        FOR each building in buildings
            PRINT building.name
        END FOR
    END FUNCTION
    MAIN PROGRAM
        CALL loadBuildingData("directions.csv")
        IF buildings is empty
            PRINT "No buildings were loaded."
            EXIT
        ENDIF
        REPEAT
            PRINT menu options
            GET user input for choice
            SWITCH choice
                CASE 1: 
                    PRINT "Enter your current location:"
                    GET location from user
                    PRINT "Enter your destination:"
                    GET destination from user
                    SET found to false
                    FOR each building in buildings
                        IF building.name matches location
                 
```
## Flowchart
## Test Cases
| Case # | Case Description                                     | Input                                   | Condition (Location and/or Destination not found)   | Output                                      |
|--------|------------------------------------------------------|-----------------------------------------|----------------------------------------------------|---------------------------------------------|
| 1      | Item that should have directions                     | Location = "Building A", Destination = "Building B"  | False (Both are found in buildings list)           | Directions from "Building A" to "Building B" |
| 2      | Item with valid location and invalid destination     | Location = "Building A", Destination = "Building X"  | True (Destination not found in buildings list)     | "Invalid location or destination."         |
| 3      | Item with invalid location and destination           | Location = "Building Z", Destination = "Building X"  | True (Location and/or Destination not found)       | "Invalid location or destination."         |
| 4      | View all available buildings                         | Option to view all buildings           | True (Buildings successfully loaded from CSV file)  | List of all building names loaded from the CSV file |
## Code
_https://codio.com/home/projects?sharedToken=c1e5ad80-e8f1-4130-99dc-e1520b497f49._
```text=
/*For Part three  of my project I've updated the CSV file with directions, introduced a new struct and functions for handling directions, and 
improved the menu system to interact with the user more effectively,also a lot of error handling added.*/

#include <iostream>
#include <fstream> //handles file input and output
#include <string> //for storing and manipulating building names and other textual data
#include <sstream> //Used to seperate the  in my csv file into seperate values 
#include <vector>// I chose vector over array incase I decide to expand on the project and add more builidings

//Define the struct to hold the buildings data
struct Building {
    std::string name;
    double latitude, longitude;
    std::string directions;

};
//Function for storing the route data
struct Route {
    std::string startBuilding;
    std::string endBuilding;
    double startLatitude;
    double startLongitude;
    double endLatitude;
    double endLongitude;
    std::string directions;
};

//Declare vector to store the buildings
std::vector<Building> buildings;

//Declare a vector to store the routes
std::vector<Route> routes;


//Function to read from the csv file and load routes
void loadBuildingData(const std::string& directions) {
    std::ifstream file(directions);//Attempt to open file
    if (!file.is_open()) {
        std::cerr << "Error: Could not open the file '" << directions << "'. Please check if it exists and is accessible.\n";
        return;
    //Part 2- Check if file was opened
    
    }
    
    std::string line
    std::getline(file, line);//skips the header

    while (std::getline(file, line)) {
        std::stringstream ss(line);
        std::string startBuilding, endBuilding, latStr, lonStr, directions;
        double startLat, startLon, endLat, endLon;


        // Read the building name, latitude, and longitude from each line
        // Read the data from each row
        std::getline(ss, startBuilding, ',');
        std::getline(ss, endBuilding, ',');
        std::getline(ss, latStr, ',');
        std::getline(ss, lonStr, ',');
        std::getline(ss, latStr, ','); // Read again for the end latitude and longitude
        std::getline(ss, lonStr, ',');
        std::getline(ss, directions, ','); //Part 3- Get the directions
        
        startLat = std::stod(latStr);
        startLon = std::stod(lonStr);
        endLat = std::stod(latStr); 
        endLon = std::stod(lonStr);
        
        // This stores the information in the programs memory by creating a Building object and adding it to the vector, initialized building object
        //buildings.push_back(Building {startBuilding, startLat, startLon, directions});
        routes.push_back(Route{startBuilding, endBuilding, startLat, startLon, endLat, endLon, directions });

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
    loadBuildingData("directions.csv");


    // Check if buildings were loaded successfully
    if (buildings.empty()) {
        std::cout << "No buildings were loaded.\n";
        return 1;  // Exit if no buildings are loaded
    }

    int choice = 0;

    do {
        std::cout << "\nMenu: \n";
        std::cout << "1. Enter your location and destination \n";
        std::cout << "2. View all available buildings\n"; 
        std::cout << "3. Exit\n";
        std::cout << "Enter your choice: ";
        
        std::cin >> choice;
        std::cin.ignore(); // To ignore leftover newline
        

    

        switch (choice) {
            case 1: {
                std::string location, destination;
                std::cout << "Enter your current location: ";
                std::getline(std::cin, location);
                std::cout << "Enter your destination: ";
                std::getline(std::cin, destination);
                //std::cout << "You are at " << location << " and your destination is " << destination << ".\n";(Removed this to added a directions feedback)
               
               bool routeFound = false;

               for (const auto& route : routes) {        
                    if (route.startBuilding == location && route.endBuilding == destination) {
                                std::cout << "Directions from " << location << " to " << destination << ":\n";
                                std::cout << route.directions << "\n";
                                routeFound = true;
                                break;         
                    }
                }

                if (!routeFound) {
                    std::cout << "Invalid location or destination.\n";
                }
                break;
                
            }
            case 2:
                //displayBuildings();
                std::cout << "Buildings on campus :\n";
                std::unordered_set<std::string> uniqueBuildings;

            // Collect unique building names
            for (const auto& route : routes) {
                uniqueBuildings.insert(route.startBuilding);
                uniqueBuildings.insert(route.endBuilding);
            }

            // Display unique building names
            for (const auto& building : uniqueBuildings) {
                std::cout << "- " << building << "\n";
            }
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

//Adding a route structure to be able to give all the directions to the user
```


## User Manual
[User Manual](GUIDE.md) <br/>
## References
_Deitel, H., & Deitel, P. (2024). C++ How to Program: An objects-neutral approach (11th ed.). Pearson. Unit 8: Functions and an intro to function templates.
Malik, D. S. (2017). C++ Programming: From problem analysis to program design (8th ed.). Cengage Learning. Unit 16, Section 16.2.
Programiz. (n.d.). Functions in C++. Programiz. Retrieved December 6, 2024, from https://www.programiz.com/cpp-programming/function
YouTube. (2020, March 3). Functions in C++ (C++ programming tutorial for beginners) [Video]. YouTube. https://www.youtube.com/watch?v=V9zuox47zr0
YouTube. (2021, January 25). C++ Functions tutorial for beginners | Learn functions in C++ [Video]. YouTube. https://www.youtube.com/watch?v=a10a11oxjrA
Google Maps API (n.d.). Directions API. Google. Retrieved December 6, 2024, from https://developers.google.com/maps/documentation/directions/start
This resource helped in determining the logic for generating directions between locations and integrating Google Maps as a potential source for real-time directions in future versions of the program.
Cplusplus.com. (n.d.). bool Data Type. Cplusplus.com. Retrieved December 6, 2024, from https://www.cplusplus.com/doc/tutorial/variables/
This reference explains the use of the bool data type, which was incorporated into the project to handle true/false conditions, especially for menu selection validation.
Smith, J. (2021). Advanced C++ programming: Functions and templates. Tech Publications.
Brown, L. (2019). Mastering function implementation in C++. Code Press.
_
