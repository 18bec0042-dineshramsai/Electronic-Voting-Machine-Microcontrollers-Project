/*18BEC0042 - ELECTRONIC VOTING MACHINE USING 8051 - MICROCONTROLLERS PROJECT - RAW CODE */
#include<reg51.h> /*Importing Libraries for all 51 microcontroller Families*/
#define msec 50
#define lcd_data_str_pin P2
/*Declaring the Pins for Control Lines of LCD*/
sbit rs = P3^0; //Register select (RS) pin with 3.0
sbit rw = P3^1; //Read write(RW) pin with 3.1
sbit en = P3^6; //Enable(EN) pin with 3.6
sbit ini_pin = P1^0; // Start voting pin
sbit stop_pin = P1^5; // Stop voting pin

/*Declaring Pins for Candidate Buttons*/
sbit candidate_1=P1^1; //Candidate1 is assigned to Pin 1.1
sbit candidate_2=P1^2; //Candidate2 is assigned to Pin 1.2
sbit candidate_3=P1^3; //Candidate3 is assigned to Pin 1.3
sbit candidate_4=P1^4; //Candidate4 is assigned to Pin 1.4

/*Declaring the necessary variables*/
int max = 0;
int carry = 0;
int arr[4];

int vote_amt[3],j;
unsigned int vote_1,vote_2,vote_3,vote_4; /*Using Unsigned as votes are always positive*/

void delay(int delay_time) /*User Defined Time delay function. We have to maintain some delay for passing each value to screen between logic high and low*/
{

int j,k;
for(j=0;j<=delay_time;j++)
for(k=0;k<=1000;k++);
}

void lcd_cmd(unsigned char cmd_addr) //User Defined Function to send command to LCD
{
lcd_data_str_pin = cmd_addr;
en = 1;
rs = 0;
rw = 0;
delay(1);
en = 0;
return;
}

void lcd_data_str(char str[50]) //Function to send string
{
int p;
for (p=0;str[p]!='\0';p++)
{
lcd_data_str_pin = str[p];
rw = 0;
rs = 1;
en = 1;

delay(1);
en = 0;
}
return;
}

void lcd_data_int(unsigned int vote) //Function to send 0-9 character values
{
char dig_ctrl_var;
int p;
for (j=2;j>=0;j--)
{
vote_amt[j]=vote%10;
vote=vote/10;
}

for (p=0;p<=2;p++)
{
dig_ctrl_var = vote_amt[p]+48;
lcd_data_str_pin = dig_ctrl_var;
rw = 0;
rs = 1;
en = 1;
delay(1);
en = 0;

}
return;
}

void vote_count() // Function to count votes
{
while (candidate_1==0 && candidate_2==0 && candidate_3==0 && candidate_4==0);
if (candidate_1==1)
{
while (candidate_1 == 1);
{
vote_1 = vote_1 + 1;
}
}

if (candidate_2==1)
{
while (candidate_2 == 1);
{
vote_2 = vote_2 + 1;
}
}

if (candidate_3==1)
{

while (candidate_3 == 1);
{
vote_3 = vote_3 + 1;
}
}

if (candidate_4==1)
{
while (candidate_4 == 1);
{
vote_4 = vote_4 + 1;
}
}
}

void lcd_ini()
{
lcd_cmd(0x38); /*Command for 8bit 2 row configuration or 5x7 Matrix Crystal Activation*/
delay(msec); /*Delay between each command so that the machine/lcd can execute*/
lcd_cmd(0x0E);/*Command for turning on Display with Cursor Blinking*/
delay(msec);
lcd_cmd(0x01); /*Command for Clearing the Screen*/
delay(msec);
lcd_cmd(0x81);/*Command for Force Cursor to Begin in 1st Line*/
delay(msec);

lcd_data_str("Welcome!!!"); /*Displays Welcome Message*/
delay(100);
lcd_cmd(0x01); /*Command for clearing the Screen*/
delay(msec);
lcd_cmd(0x80); /*Command for forcing the cursor to begin in 1st Line*/
delay(msec);
lcd_data_str( "Press" );/*Displays "Press" */
delay(msec);
lcd_cmd(0x14);/*Command for shifting cursor position to right*/
delay(msec);
lcd_data_str("button");/*Displays "BUTTON" */
delay(msec);

delay(msec);
lcd_cmd(0xC0);/* Command for forcing cursor to begin in 2nd Line*/
delay(msec);
lcd_data_str("to");/*Displays TO */
delay(msec);
lcd_cmd(0x14);/*Command for shifting cursor position to right*/
delay(msec);
lcd_data_str("vote");/*Displays "VOTE" */
delay(100);
lcd_cmd(0x01);/*Command for clearing the Screen*/
delay(msec);
lcd_cmd(0x80);/*Command for forcing the cursor to begin in 1st Line*/

delay(msec);
lcd_data_str("P1");/*Displays "P1" */
delay(msec);
lcd_cmd(0x84); /*Force cursor to jump to next bit giving one bit gap*/
delay(msec);
lcd_data_str("P2");/*Displays "P2" */
delay(msec);
lcd_cmd(0x88);/*Force cursor to jump to next bit giving one bit gap*/
delay(msec);
lcd_data_str("P3");/*Displays "P3" */
delay(msec);
lcd_cmd(0x8C);/*Force cursor to jump to next bit giving one bit gap*/
delay(msec);
lcd_data_str("P4");/*Displays "P4" */
delay(msec);

vote_count();
lcd_cmd(0x01);/*Command for clearing the Screen*/
delay(msec);
lcd_cmd(0x85);/*Command for forcing the cursor to begin in 1st Line*/
delay(msec);
lcd_data_str("Thank");/*Displays 'THANK' */
delay(msec);
lcd_cmd(0x14);/*Command for shifting cursor position to right */
delay(msec);

lcd_data_str("You!!");/*Displays You */
delay(100);
}

void results() // Function to show results
{
int i;
carry = 0;
lcd_cmd(0x01); /*Command for clearing the screen */
delay(msec);
lcd_cmd(0x80);/*Command for forcing the cursor to begin in 1st Line*/
delay(msec);
lcd_data_str("Results");/*Displays 'RESULTS' */
delay(msec);
lcd_cmd(0x14);/*Command for shifting cursor position to right */
delay(msec);
lcd_data_str("Are");/*Displays 'ARE' */
delay(msec);
lcd_cmd(0x14);/*Command for shifting cursor position to right */
delay(msec);
lcd_data_str("Out");/* Displays 'OUT' */
delay(msec);

lcd_cmd(0x01); /*Command for clearing the screen */
delay(msec);

lcd_cmd(0x80);/*Command for forcing the cursor to begin in 1st Line*/
delay(msec);
lcd_data_str("P1");/*Displays P1*/
delay(msec);
lcd_cmd(0x84);/*Force cursor to jump to next bit giving one bit gap*/
delay(msec);
lcd_data_str("P2");/*Displays P2*/
delay(msec);
lcd_cmd(0x88);/*Force cursor to jump to next bit giving one bit gap*/
delay(msec);
lcd_data_str("P3");/*Displays P3*/
delay(msec);
lcd_cmd(0x8C);/*Force cursor to jump to next bit giving one bit gap*/
delay(msec);
lcd_data_str("P4");/*Displays P4 */
delay(msec);

lcd_cmd(0xC0);/* Command for forcing cursor to begin in 2nd Line*/
delay(100);
lcd_data_int(vote_1);/*Displays how many votes are casted for P1 */
delay(msec);

lcd_cmd(0xC4);/*Force cursor to jump to next bit giving one bit gap in 2nd Line*/
delay(msec);
lcd_data_int(vote_2);/*Displays how many votes are casted for P2 */

delay(msec);

lcd_cmd(0xC8);/*Force cursor to jump to next bit giving one bit gap in 2nd Line*/
delay(msec);
lcd_data_int(vote_3);/*Displays how many votes are casted for P3 */
delay(msec);

lcd_cmd(0xCC);/*Force cursor to jump to next bit giving one bit gap in 2nd Line*/
delay(msec);
lcd_data_int(vote_4);/*Displays how many votes are casted for P4 */
delay(300);

 /*Creating Numerical Arrays for storing no:of votes */ 
arr[0] = vote_1;
arr[1] = vote_2;
arr[2] = vote_3;
arr[3] = vote_4;

for( i=0; i<4; i++)
{
if(arr[i]>=max)
max = arr[i];
}

if ( (vote_1 == max) && ( vote_2 != max) && (vote_3 != max)&& (vote_4 != max) )
{

carry = 1;
lcd_cmd(0x01); /*Command for clearing the screen */
delay(msec);
lcd_cmd(0x82);/*Command for forcing the cursor to begin in 1st Line*/
delay(msec);
lcd_data_str("Hurray!!!");/* Displays 'HURRAY' */
delay(50);
lcd_cmd(0xC4);/*Command for forcing the cursor to begin in 2nd Line*/
delay(msec);
lcd_data_str("P1");/* Displays 'P1' */
delay(msec);
lcd_cmd(0x14);/* Command for shifting cursor position to right */
delay(msec);
lcd_data_str("wins");/*Displays 'WINS' */
delay(msec);
}

if ( (vote_2 == max) && ( vote_1 != max) && (vote_3 != max)&& (vote_4 != max) )
{
carry = 1;
lcd_cmd(0x01);/*Command for clearing the screen */
delay(msec);
lcd_cmd(0x82);/*Command for forcing the cursor to begin in 1st Line*/
delay(msec);
lcd_data_str("Hurray!!!");/* Displays 'HURRAY' */
delay(50);
lcd_cmd(0xC4);/*Command for forcing the cursor to begin in 2nd Line*/
delay(msec);
lcd_data_str("P2");/* Displays 'P2' */
delay(msec);
lcd_cmd(0x14);/* Command for shifting cursor position to right */
delay(msec);
lcd_data_str("wins");/*Displays 'WINS' */
delay(msec);
}

if ( (vote_3 == max) && ( vote_2 != max) && (vote_1 != max)&& (vote_4 != max) )
{
carry = 1;
lcd_cmd(0x01); /*Command for clearing the screen */
delay(msec);
lcd_cmd(0x82); /*Command for forcing the cursor to begin in 1st Line*/
delay(msec);
lcd_data_str("Hurray!!!"); /* Displays 'HURRAY' */
delay(50);
lcd_cmd(0xC4); /*Command for forcing the cursor to begin in 2nd Line*/
delay(msec);
lcd_data_str("P3"); /* Displays 'P3' */
delay(msec);
lcd_cmd(0x14); /* Command for shifting cursor position to right */
delay(msec);
lcd_data_str("wins"); /*Displays 'WINS' */
delay(msec);
}

if ( (vote_4 == max) && ( vote_2 != max) && (vote_3 != max)&& (vote_1 != max) )
{
carry = 1; 
lcd_cmd(0x01); /*Command for clearing the screen */
delay(msec);
lcd_cmd(0x82); /*Command for forcing the cursor to begin in 1st Line*/
delay(msec);
lcd_data_str("Hurray!!!"); /* Displays 'HURRAY' */
delay(50);
lcd_cmd(0xC4); /*Command for forcing the cursor to begin in 2nd Line*/
delay(msec);
lcd_data_str("P4"); /* Displays 'P4' */
delay(msec);
lcd_cmd(0x14); /* Command for shifting cursor position to right */
delay(msec);
lcd_data_str("wins"); /*Displays 'WINS' */
delay(msec);
}

/* LCD Code for displaying message when tie occurs between two or more particiants */ 
if (carry==0)
{
 /* Code for Displaying String 'CLASH BETWEEN' */
lcd_cmd(0x01); /*Command for clearing the screen */
delay(msec);
lcd_cmd(0x82); /*Command for forcing the cursor to begin in 1st Line*/
delay(msec);
lcd_data_str("clash");/* Displays CLASH*/
delay(50);
lcd_cmd(0x14); /* Command for shifting cursor position to right */
delay(msec);
lcd_data_str("between!!!"); /*Displays 'BETWEEN' */
delay(50);
if(vote_2 == max)
{
lcd_cmd(0xC5); /*Command for forcing the cursor to begin in 2nd Line with a gap of a bit*/
lcd_data_str("P2"); /*Displays 'P2' */
delay(50);
}
if(vote_3 == max)
{
lcd_cmd(0xC9); /*Command for forcing the cursor to begin in 2nd Line with a gap of a bit*/
lcd_data_str("P3"); /*Displays 'P3' */
delay(50);
}
if(vote_4 == max)
{

lcd_cmd(0xCD); /*Command for forcing the cursor to begin in 2nd Line with a gap of a bit*/
lcd_data_str("P4"); /*Displays 'P4' */
delay(50);
}
}
}

void main() /*Main Function*/
{
ini_pin = stop_pin = 1;
vote_1 = vote_2 = vote_3 = vote_4 = 0;
candidate_1 = candidate_2 = candidate_3 = candidate_4 = 0;
lcd_cmd(0x38); /*Command for 8bit 2 row configuration or 5x7 Matrix Crystal Activation*/
delay(msec);
lcd_cmd(0x0E); /*Command for turning on Display with Cursor Blinking*/
delay(msec);
lcd_cmd(0x01);/*Command for clearing the screen */ 
delay(msec);
lcd_cmd(0x80);/* Command for forcing the cursor to begin in first line */
delay(msec);
lcd_data_str( "Press" );/* Displays 'PRESS' */
delay(msec);
lcd_cmd(0x14); /* Command for shifting Cursor position to Right */
delay(msec);
lcd_data_str("init"); /*Displays INIT */

delay(msec);

delay(msec);
lcd_cmd(0xC0); /* Command for forcing the cursor to begin in 2nd line */
delay(msec);
lcd_data_str("to");/* Displays 'TO' */
delay(msec);
lcd_cmd(0x14); /* Command for shifting Cursor position to Right */
delay(msec);
lcd_data_str("begin"); /* DISPLAYS 'BEGIN' */
delay(100);
while(1)
{
while(ini_pin != 0)
{
if (stop_pin == 0)
break;
}
if (stop_pin == 0)
{
break;
}
lcd_ini();
}

while(1)
{
results();
}
}


