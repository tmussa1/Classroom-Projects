// This project deals with abstract concepts in pointers,
// classes, inheritance relationships, and garbage collection

//Tofik Mussa
//Submitted to : Dr. Belcher

#include <iostream>
#include <string>
using namespace std;

class Enemy{
    
public:
  string enName;
  int health;
  
  Enemy() {
      enName = " ";
      health = 0;
    }
};
 
class EnemySquad
{
    
public:
 Enemy *enemies;
 int enemyCount;
 void removeWeak();
 void listThem();

EnemySquad() {
    enemies = NULL;
    enemyCount = 0;
}

EnemySquad(const EnemySquad& copied) {
    
    enemyCount = copied.enemyCount;
    
    if(enemyCount > 0) {
    
    enemies = new Enemy[enemyCount]; 
    
    for(int i=0; i < enemyCount; i++) {
        enemies[i] = copied.enemies[i];
    }
    }
}

~EnemySquad() {
    if(enemies != NULL) {
     delete enemies; 
     enemies = 0;
     enemyCount -= 1;
    }
}

};

void EnemySquad::listThem() {
    for(int i=0; i< enemyCount; i++) {
    cout <<"\n" << enemies[i].enName << "\n";
    cout << enemies[i].health << "\n";
    }
}

void EnemySquad::removeWeak() {
    
    int lowIndex = 0;
    
    if(enemyCount > 0) {
        
    for(int k=0; k<enemyCount; k++) { 
    if(enemies[k].health < enemies[lowIndex].health) {
    lowIndex = k;}
    } 
     
    Enemy* newEnemies = new Enemy[enemyCount-1];
    
    for(int j=0; j< enemyCount; j++) {
        if(j < lowIndex){
            newEnemies[j] = enemies[j];}
        else if(j > lowIndex){
            newEnemies[j-1] = enemies[j];}
    }
    
Enemy *temp = enemies;
delete [] temp;
enemies = newEnemies;
enemyCount -= 1;

}
}
EnemySquad* getASquad();
    
int main()
{

   EnemySquad *squad_one = getASquad();
   EnemySquad *squad_two = new EnemySquad(*squad_one);
   if(squad_two->enemies == NULL || squad_one->enemies == squad_two->enemies)
   {
 cout << "Did not do copy constructor correctly\n" << squad_one->enemies;
 return 1;
   }

   cout << "Squad one's warriors:";

   squad_one->listThem();

   //Remove two of squad two's weakest enemies
   squad_two->removeWeak();
   squad_two->removeWeak(); 
   cout << "Squad two's warriors after removing weakest 2 enemies:";  //This list must be different from squadOne's
   squad_two->listThem();


   delete  squad_two;   
//If flow crashes before here, you've made a logical error
   if(squad_one->enemies == NULL)
   {
 cout << "Did not remove enemies correctly\n";
 return 1;
   }

   squad_one->removeWeak(); //Must run without causing a runtime error

   cout << "Removed just one from squad one:";

   squad_one->listThem();

   delete  squad_one; 

   cout << "Game over.\n";
   system("PAUSE");

   return 0;
  
}

EnemySquad* getASquad(){

                EnemySquad * s = new EnemySquad;

 

                s->enemies=new Enemy[11];

                s->enemies[0].enName="Jack the Ripper";

                s->enemies[1].enName="Bad Guy";

                s->enemies[2].enName="Demoness";

                s->enemies[3].enName="Megatron";

                s->enemies[4].enName="Shocker";

                s->enemies[5].enName="Bad Leroy Brown";

                s->enemies[6].enName="Satan";

                s->enemies[7].enName="Gloom and Despair";

                s->enemies[8].enName="Lex Luthor";

                s->enemies[9].enName="Alien";

                s->enemies[10].enName="Predator";

                s->enemyCount=11;

                s->enemies[0].health=2;

                s->enemies[1].health=92;

                s->enemies[2].health=64;

                s->enemies[3].health=238;

                s->enemies[4].health=1;

                s->enemies[5].health=17;

                s->enemies[6].health=119;

                s->enemies[7].health=5;

                s->enemies[8].health=9;

                s->enemies[9].health=25;

                s->enemies[10].health=57;

 

 return s; //new EnemySquad;

}
