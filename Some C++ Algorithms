/* This project deals with the use 
of the standard template library specifically map
and reading from a file
Name: Tofik Mussa
Submitted to: Dr. Belcher
Date: 11/15/2017 */

#include <iostream>
#include <string>
#include <ctime>
#include <utility>
#include <map>
#include <algorithm>
#include <vector>
#include <fstream>
#include <iomanip>
#include "stdlib.h"
using namespace std;

class userKey {

public:
	string lastName;
	string firstInitial;

	bool operator<(const userKey &b) const {
		if (lastName == b.lastName) 
				return firstInitial < b.firstInitial;
		return lastName < b.lastName;
	}
};

struct func { //Function that prints each user with login time

public:

	void operator()(pair<userKey, long int> myPair) {

		struct tm * ptm;
		time_t timeInSecs = myPair.second;
		ptm = localtime(&timeInSecs);

		string weekday_name[] = { "Sunday", "Monday", "Tuesday", "Wednesday", "Thursday",
			"Friday", "Saturday" };
		string month_name[] = { "January", "February", "March", "April", "May", "June", "July", "August",
			"September", "October", "November", "December" };

		cout << myPair.first.firstInitial << " " << myPair.first.lastName << " logged in on " <<
			weekday_name[ptm->tm_wday] << " " << month_name[ptm->tm_mon + 1] << " " << ptm->tm_mday << "," << ptm->tm_year + 1900 << " at "
			<< ptm->tm_hour << ":" << ptm->tm_min << ":" << ptm->tm_sec << "\n";
	}
} myObj;

bool beforeTen(pair<userKey, long int> myPair2) {//Returns the number of users who logged in before 10

	struct tm * ptm;
	time_t timeInSecs = myPair2.second;
	ptm = localtime(&timeInSecs);

	return ptm->tm_hour < 10; 
}
int main()
{
	ifstream myFile;

	userKey name;
	long int userTime;
	char *stringTime;

	map<userKey, long int> myMap;
	map<userKey, long int>::iterator myIt;

	myFile.open("usrlogs.txt");

	while (!myFile.eof()) {

		pair<userKey, long int> myPair;

		stringTime = new char[25];

		getline(myFile, name.lastName, ',');
		getline(myFile, name.firstInitial, ','); //reads data from file
		myFile.getline(stringTime, 25, '\n');

		userTime = atol(stringTime);

		myPair.first = name;
		myPair.second = userTime;

		myIt = myMap.find(myPair.first);

		if (myIt == myMap.end()) { //inserts the pair if key doesn't exist
			myMap.insert(myPair);
		}
		else if (myIt != myMap.end() && (myPair.second > myIt->second)) { //inserts the pair if key exists but has time value smaller
			myMap.insert(myPair);
		}

	}
	delete[] stringTime;
	myFile.close();

	cout << "The number of unique IDs is " << myMap.size() << "\n" << "\n"; //the ID's are unique since duplicates were not added
																	
	for_each(myMap.begin(), myMap.end(), myObj);

	cout << "\n";

	cout << count_if(myMap.begin(), myMap.end(), beforeTen) <<  " people logged in before 10:00 AM\n" << "\n";

	system("PAUSE");
	return 0;
}
