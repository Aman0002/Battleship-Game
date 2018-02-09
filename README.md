# Battleship-Game
import java.util.ArrayList;
import java.util.Arrays;
import java.util.Random;
import java.util.Scanner;
public class battleship {

    public static Scanner input=new Scanner(System.in);
    public static char[][] UserOcean=new char[10][10];
    public static char[][] ComputerOcean=new char[10][10];
    public static Random rand=new Random();

    public static void main(String[] args)
    {   //Step-1
        System.out.println("**** Welcome to Battle Ships game ****");
        System.out.println("Right now, the sea is empty.\n");
        /*
        prints the  empty Ocean .
        here we can pass any array
        UserOcean or Computer Ocean
        as they have no effect in printing the empty Ocean
        */
        printMap(UserOcean);
        //Step-2
        System.out.println("Where would you like to place the ships ?");
        Deployplayersship();
        //Step-3
        Deploycomputersship();
        //Step-4
        Battle();
    }
    public static void printMap(char[][] Ocean)
    {
        System.out.println("   0123456789   ");
        for(int row=0;row<10;row++)
        {
            System.out.print(row+" |");
            for(int col=0;col<10;col++)
            {
                if(Ocean[row][col]==0)//here 0 represents that there is no element means null
                {
                   System.out.print(" ");
                }else
                {
                    System.out.print(Ocean[row][col]);
                }
            }
            System.out.println("| "+row);
        }
        System.out.println("   0123456789   ");
    }
    public static void Deployplayersship()
    {
        int x,y ;//these are the co-ordinates for the player's ship deploying
      for(int i=0;i<5;i++)
      {
          System.out.print("Enter X coordinate for your ship "+(i+1)+": ");
           x = input.nextInt();
          System.out.print("Enter Y coordinate for your ship "+(i+1)+": ");
           y = input.nextInt();
           //1st condition
          while(x<0||x>9)
          {
              System.out.println("Invalid location!");
              System.out.print("Enter X coordinate for your ship "+(i+1)+": ");
              x = input.nextInt();
          }
          while(y<0||y>9)
          {
              System.out.println("Invalid location!");
              System.out.print("Enter Y coordinate for your ship "+(i+1)+": ");
              y = input.nextInt();
          }
          //2nd condition
          while(UserOcean[x][y]=='@')
          {   System.out.println("you can NOT place two or more ships on the same location.");
              System.out.print("Enter X coordinate for your ship "+(i+1)+": ");
              x = input.nextInt();
              System.out.print("Enter Y coordinate for your ship "+(i+1)+": ");
              y = input.nextInt();

          }
          UserOcean[x][y]='@';

      }
      printMap(UserOcean);//to represent the current situation of ships
      }
    public static void Deploycomputersship()
    {

        int x,y ;//these are the co-ordinates for the computer's  ship
        System.out.println("Computer is deploying ships.");
        for(int i=0;i<5;i++)
        {

            x = rand.nextInt(10);//generates random number from 0-9
            y = rand.nextInt(10);
            //1st condition
            while(x<0||x>9)
            {
                x = rand.nextInt(10);
            }
            while(y<0||y>9)
            {
                y = rand.nextInt(10);
            }
            //2nd condition
            while(ComputerOcean[x][y]=='@')
            {   x = rand.nextInt(10);
                y = rand.nextInt(10);
            }
            ComputerOcean[x][y]='@';
            System.out.println((i+1)+". shipDEPLOYED");

        }
        System.out.println("-------------------------------");
    }
    public static void Battle() {
        int playership = 5, computerships = 5;
        //Player's turn
        while (playership >= 0 && computerships >= 0) {
            System.out.println("Your Turn");
            int x1, y1;//here they are the user's guess co-ordinates
            System.out.print("Enter X co-ordinate: ");
            x1 = input.nextInt();
            System.out.print("Enter Y co-ordinate: ");
            y1 = input.nextInt();
            //checking that x and y should be in the Ocean map
            while (x1 < 0 || x1 > 9) {
                System.out.println("Invalid location!");
                System.out.print("Enter X co-ordinate: ");
                x1 = input.nextInt();
            }
            while (y1 < 0 || y1 > 9) {
                System.out.println("Invalid location!");
                System.out.print("Enter Y co-ordinate: ");
                y1 = input.nextInt();
            }
            if (ComputerOcean[x1][y1] == '@')//computer's looses ship
            {
                System.out.println("Boom! You sunk the ship!");
                UserOcean[x1][y1] = 'x';
                  computerships--;
            } else if (UserOcean[x1][y1] == '@')//player's looses his ship
            {
                System.out.println("Oh No! You sunk your own ship:(");
                UserOcean[x1][y1] = '!';
                  playership--;
            } else {
                System.out.println("Sorry! You missed");
                UserOcean[x1][y1] = '-';
                }
            printMap(UserOcean);
            System.out.println("Your's ship :"+playership+"and computer's ship :"+computerships);
           //Computer's turn
            System.out.println("Computer's Turn");
            int x2,y2;//computer's guesses
            x2=rand.nextInt(10);
            y2=rand.nextInt(10);
            while(UserOcean[y2][x2]=='x' || UserOcean[y2][x2]=='!' || UserOcean[y2][x2]=='-'){
                x2=rand.nextInt(10);
                y2=rand.nextInt(10);
            }
            if(UserOcean[x2][y2]=='@')//computer sunk the user ship
            {
             System.out.println("The Computer sunk one of your ships!");
             UserOcean[x2][y2]='x';
             playership--;
            }
            else if(ComputerOcean[x2][y2]=='@')//computer sunk his own ship
            {
                System.out.println("The Computer sunk one of it's own ships!");
                UserOcean[x2][y2]='!';
                computerships--;
            }
            else {
                System.out.println("Computer  missed");
                UserOcean[x2][y2] = '-';
            }
            printMap(UserOcean);
            System.out.println("Your's ship:"+playership+"and computer's ship:"+computerships);
            }
            //Step-5
            //GAME OVER
        if(computerships == 0){
            System.out.println("Hooray! You win the battle :)");
        }else{
            System.out.println("Sorry! You lose :(");
        }
    }

}
