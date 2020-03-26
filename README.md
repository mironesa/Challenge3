# Challenge3
// Created on Thu March 26 2020
int l_motor = 0;
int r_motor = 2;
int speed = 50; 
int slow = 20;
int target = 200;
int pause = 300;	
int right_range = 2;
int left_range = 0;
int black_target = 800;
int tophat = 5;
	
int main(){	
	
wallrun();
turn_right();
turn_left();
findline();
followline();
}

void forwards(){
   motor(l_motor,speed); // go forward 
   motor(r_motor,speed);
}

void turn_right(){
   motor(l_motor,speed); //turn right
   motor(r_motor,-speed);
}

void turn_left(){ // turn left   
 motor(l_motor,-speed);
 motor(r_motor,speed);
 msleep(600);
 forwards();
 msleep(1500);
 ao();   
}


void veer_left() {
	motor(r_motor,speed);
	motor(l_motor,slow);
}

void veer_right() {
	motor(r_motor,slow);
	motor(l_motor,speed);
}

void findline(){
	
while(analog (tophat) >target){ // go foward until the sensor sees black line 
   forwards();
   }
   ao(); 
   printf("found line!\n"); 
}

void followline() {

while (analog(right_range) >target) { // follow the line untill it finds the wall
     printf("starting line follow!\n");

   if (analog(tophat) >black_target) { // stay close to the line
     veer_left();
     printf("vearing left!\n");
     }
  
   if (analog(tophat) >black_target) { // stay close to the line
     veer_right();
     printf("vearing right!\n");
     }
     ao();
}
    

 if (analog(right_range) >=target) { 
        veer_left(); //veer left 
        printf("veer away!/n"); // veer away 
         }

  if (analog(right_range) >=target) {
        veer_right(); //veer right
        printf("veer toward wall!/n"); //veer towards the wall
  }
 
}
