// Skynet HK-Aerial
//Nicholas Buckley 10.21.2018

//including everything need for program to run
//cstdlib and ctime are used for random number generator
#include "pch.h"
#include <iostream>
#include <string>
#include <cstdlib>
#include <ctime>

using namespace std;
using std::cout;
using std::cin;
using std::endl;
using std::string;

//Creation of main function
int main()
{
	srand(static_cast<unsigned int>(time(0)));//seed random number generator
	int target, targetLocationPrediction, searchGridHighNumber, searchGridLowNumber, ping, Aiping, Humanping, Aiguess, Humanguess; //all ints need for program
	char again; //Used to see inf user wants to play again
	
	
	

	//Introduction text
	cout << "Welcome to Skynet HK-Aerial Target Locator\n\n";
	cout << "You will be in competition with two AIs to find the target location.\n";
	cout << "Onces you locate the target the amount of tries each user made will be displayed.\n";
	cout << "Generating random enemy location on 8x8 grid (1-64) ...\n";
	//Starting a do loop for the program
	do // do statement for user to play again
	{
		searchGridHighNumber = 64; // starting grid max at 64
		searchGridLowNumber = 1; //starting grid min at 1
		ping = 1; //this is the amount of tries that it will take
		Aiping = 1; //this is the amount of tries that it will take for the linear AI
		Humanping = 0; //This is the amount of tries for the user
		Aiguess = 1; //This is the guess for the linear search AI
		Humanguess = 1;
		targetLocationPrediction = ((searchGridHighNumber - searchGridLowNumber) / 2) + searchGridLowNumber; //the target location prediction that is used to predict between the min an max
		target = (rand() % 64) + 1; // random number between 1 and 64
		do // Bianery AI
		{

			++ping;//increasing number of tries by 1 each time
			targetLocationPrediction = ((searchGridHighNumber - searchGridLowNumber) / 2) + searchGridLowNumber; //changning the prediction each loop based off of max and min of grid

			if (targetLocationPrediction > target)//if the prediction is higher than the target location
			{
				searchGridHighNumber = (targetLocationPrediction - 1);//changing the grid max based off of target location

			}
			else if (targetLocationPrediction < target)//if the prediction is lower than the target location
			{
				searchGridLowNumber = (targetLocationPrediction + 1);//changing the grid man based off of target location

			}
			else //printed when the target location and prediction equal 
			{
		
			}
		} while (target != targetLocationPrediction);//Ending the loop once the target and prediction are equal

		do // Linear AI
		{

			++Aiping;//increasing number of tries by 1 each time

			if (Aiguess > target)//if the prediction is higher than the target location
			{
				Aiguess = (Aiguess - 1);//changing the grid max based off of target location

			}
			else if (Aiguess < target)//if the prediction is lower than the target location
			{
				Aiguess = (Aiguess + 1);//changing the grid man based off of target location

			}
			else //printed when the target location and prediction equal 
			{

			}
		} while (target != Aiguess );//Ending the loop once the target and prediction are equal

		do // User loop
		{
			cout << "====================================================================================================================\n";//spacing
			cout << "Enter your guess for the target location: ";
			cin >> Humanguess;
			++Humanping;//increasing number of tries by 1 each time
		

			if (Humanguess > target)//if the prediction is higher than the target location
			{
				cout << "Your guess was higher than the target location.\n"; // Telling the user that the guess is too high
				cout << "Try again.\n"; // Instructing user to attempt again

			}
			else if (Humanguess < target)//if the prediction is lower than the target location
			{
				cout << "Your guess was lower than the target location.\n"; // Telling the user that the guess is too low
				cout << "Try again.\n"; // Instructing user to attempt again

			}
			else //printed when the target location and prediction equal 
			{
				cout << "====================================================================================================================\n";
				cout << "\nAll drones have now found the enemy.\n";
				cout << "The enemy was hiding at grid location #" << target << ".\n\n"; // displaying target location

				cout << "The Human Player using a human search took " << Humanping << " guesses to find the enemy location, final target prediction was #" << target << ".\n"; // displaying user attempts
				cout << "The AI Player using linear search took " << Aiguess << " guesses to find the enemy location, final target prediction was #" << target << ".\n"; // displaying AI attempts
				cout << "The AI Player using a binary search took " << ping << " guesses to find the enemy location, final target prediction was #" << target << ".\n"; // displaying AI attmepts
				cout << "====================================================================================================================\n";
			

			}
		} while (target != Humanguess);//Ending the loop once the target and prediction are equal

	
			cout << "\nWould you like to play again? Y/N: "; // Ask user to play again
			cin >> again; // record user input

	} while (again == 'Y'); // if input is Y user will play again

	cout << "\nThanks for playing!\n"; // closing statement 



	return 0;//returning zero to assure no problems



}
