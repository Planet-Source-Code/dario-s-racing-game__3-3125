<div align="center">

## Racing Game


</div>

### Description

It's a racing game. Use 4-left and 6-right. It covers all the basic syntax of C++. Please comment on the game.
 
### More Info
 
No side effects.


<span>             |<span>
---                |---
**Submitted On**   |
**By**             |[Dario S\.](https://github.com/Planet-Source-Code/PSCIndex/blob/master/ByAuthor/dario-s.md)
**Level**          |Intermediate
**User Rating**    |4.3 (13 globes from 3 users)
**Compatibility**  |C, C\+\+ \(general\), Borland C\+\+
**Category**       |[Games](https://github.com/Planet-Source-Code/PSCIndex/blob/master/ByCategory/games__3-13.md)
**World**          |[C / C\+\+](https://github.com/Planet-Source-Code/PSCIndex/blob/master/ByWorld/c-c.md)
**Archive File**   |[](https://github.com/Planet-Source-Code/dario-s-racing-game__3-3125/archive/master.zip)

### API Declarations

```
//i did not check which ones you actually need
#include <vcl.h>
#include <condefs.h>
#include <time.h>
#include <stdio.h>
#include <iostream.h>
#include <conio.h>
#include <dos.h>
#include <stdlib.h>
#include <fstream.h>
```


### Source Code

```
//------------------------------------------------------------------------------
#include <vcl.h>
#include <condefs.h>
#include <time.h>
#include <stdio.h>
#include <iostream.h>
#include <conio.h>
#include <dos.h>
#include <stdlib.h>
#include <fstream.h>
#pragma hdrstop
#pragma argsused
//------------------------------------------------------------------------------
void print_car(int x, int y, int car_num);
void move(int coordinates[10][2], char option, int erase[2], int car_num);
void erase_car(int x, int y);
void draw_road(void);
void move_right(int coordinates[10][2], int erase[2], int car_num);
void move_left(int coordinates[10][2], int erase[2], int car_num);
void move_down(int coordinates[10][2], int erase[2], int car_num);
void computer_move(int coordinates[10][2], int erase[2], int car_num);
bool check_over(int coordinates[10][2]);
int main(void)
 {
 time_t timer = 0;
 int time2 = 0;
 int time_left;
 int car_num;
 int coordinates[10][2];
 int erase[2];
 char option;
 bool over = false;
 int counter;
 textmode(C4350);
 for(counter = 0; counter < 10; counter++)
   {coordinates[counter][0] = -1;}
 car_num = 0;
 coordinates[0][0] = 23;
 coordinates[0][1] = 38;
 draw_road();
 print_car(coordinates[0][0], coordinates[0][1], -5);
 getch();
 timer = time(NULL);
 time_left = (180 - (timer - time2));
 time2 = timer;
 while(time_left != 0 && over == false)
  {
  textcolor(WHITE);
  textbackground(BLACK);
  if(time_left != (180 - (time(NULL) - time2)))
   {
   timer = time(NULL);
   time_left = (180 - (timer - time2));
   gotoxy(70, 1);
   cprintf("%d ", time_left);
   computer_move(coordinates, erase, car_num);
   over = check_over(coordinates);
   }
  if(kbhit() == true)
   {
   option = getch();
   move(coordinates, option, erase, 0);
   erase_car(erase[0], erase[1]);
   print_car(coordinates[0][0], coordinates[0][1], -5);
   over = check_over(coordinates);
   }
  }
 getch();
 clrscr();
 gotoxy(30, 20);
 cprintf("GAME OVER");
 getch();
 return 0;
 }
//------------------------------------------------------------------------------
void print_car(int x, int y, int car_num)
 {
 int color;
 textbackground(WHITE);
 if(car_num != -5)
  {
  switch(car_num%4)
   {
   case 0:
     {
     textcolor(BLACK);
     break;
     }
   case 1:
     {
     textcolor(LIGHTRED);
     break;
     }
   case 2:
     {
     textcolor(YELLOW);
     break;
     }
   case 3:
     {
     textcolor(LIGHTGREEN);
     break;
     }
   }
  }
 else
  {
  textcolor(LIGHTBLUE);
  }
 gotoxy(x, y);
 cprintf("%c%c%c%c%c", 0xDB, 0xC4, 0x1E, 0xC4, 0xDB);
 gotoxy(x, y+1);
 cprintf(" %c ", 0xDB);
 gotoxy(x, y+2);
 cprintf(" /%c\\ ", 0xDB, 0xC1, 0xDB);
 gotoxy(x, y+3);
 cprintf("%c%c%c%c%c", 0xDB, 0xC4, 0xDB, 0xC4, 0xDB);
 textcolor(BLACK);
 gotoxy(x, y);
 cprintf("%c", 0xDB);
 gotoxy(x+4, y);
 cprintf("%c", 0xDB);
 gotoxy(x, y+3);
 cprintf("%c", 0xDB);
 gotoxy(x+4, y+3);
 cprintf("%c", 0xDB);
 }
//------------------------------------------------------------------------------
void move(int coordinates[10][2], char option, int erase[2], int car_num)
 {
 if(option == '4')
  {move_left(coordinates, erase, car_num);}
 if(option == '6')
  {move_right(coordinates, erase, car_num);}
 }
//------------------------------------------------------------------------------
void erase_car(int x, int y)
 {
 int counter_x;
 int counter_y;
 int color;
 for(counter_x = x; counter_x < x+5; counter_x++)
   {
   for(counter_y = y; counter_y < y+4; counter_y++)
    {
    textbackground(WHITE);
    gotoxy(counter_x, counter_y);
    cprintf(" ");
    }
   }
 }
//------------------------------------------------------------------------------
void draw_road(void)
 {
 int counter;
 textbackground(GREEN);
 clrscr();
 window(11, 1, 49, 43);
 textbackground(7);
 clrscr();
 window(1, 1, 80, 43);
 textcolor(BLACK);
 }
//------------------------------------------------------------------------------
void move_right(int coordinates[10][2], int erase[2], int car_num)
 {
 if(coordinates[car_num][0] < 40)
   {
   erase[0] = coordinates[car_num][0];
   erase[1] = coordinates[car_num][1];
   coordinates[car_num][0] += 10;
   }
 }
//------------------------------------------------------------------------------
void move_down(int coordinates[10][2], int erase[2], int car_num)
 {
 erase[0] = coordinates[car_num][0];
 erase[1] = coordinates[car_num][1];
 if(coordinates[car_num][1] < 36)
  {
  coordinates[car_num][1] += 7;
  erase_car(erase[0], erase[1]);
  print_car(coordinates[car_num][0], coordinates[car_num][1], car_num);
  }
 else
  {
  erase_car(erase[0], erase[1]);
  coordinates[car_num][0] = -1;
  }
 }
//------------------------------------------------------------------------------
void move_left(int coordinates[10][2], int erase[2], int car_num)
 {
 if(coordinates[car_num][0] > 20)
   {
   erase[0] = coordinates[car_num][0];
   erase[1] = coordinates[car_num][1];
   coordinates[car_num][0] -= 10;
   }
 }
//------------------------------------------------------------------------------
void computer_move(int coordinates[10][2], int erase[2], int car_num)
 {
 int new_cars;
 int next_car;
 int x, y;
 new_cars = 0;
 for(next_car = 9; next_car > 0; next_car--)
   {
   if(coordinates[next_car][0] == -1 && new_cars == 0)
    {
    coordinates[next_car][0] = random(4);
    switch(coordinates[next_car][0])
     {
     case 0:
       {coordinates[next_car][0] = 13;
       break;}
     case 1:
       {coordinates[next_car][0] = 23;
       break;}
     case 2:
       {coordinates[next_car][0] = 33;
       break;}
     case 3:
       {coordinates[next_car][0] = 43;
       break;}
     }
    coordinates[next_car][1] = 3;
    x = coordinates[next_car][0];
    y = coordinates[next_car][1];
    print_car(coordinates[next_car][0], coordinates[next_car][1], next_car);
    new_cars++;
    }
   else
    {
    if(coordinates[next_car][0] != -1)
     {move_down(coordinates, erase, next_car);}
    }
   }
 }
//------------------------------------------------------------------------------
bool check_over(int coordinates[10][2])
 {
 int counter;
 for(counter = 1; counter < 10; counter++)
   {
   if((coordinates[counter][1] == coordinates[0][1]) &&
    (coordinates[counter][0] == coordinates[0][0]))
    {return true;}
   }
 return false;
 }
```

