#luxsoft
#include<iostream>

struct Cell
{
   int x;
   int y;
   bool good;
};

class Ship
{
public:
   void init(Cell startCell, int size, bool isVertical);
   bool hit(Cell cell);
   void print();
   bool isDead();

private:
   int mSize; //1 - 4
   int mHeath;
   Cell mCoords[4];
};

class Map
{
public:
   void init(/*ghjghjgh*/);

   bool hit(Cell cell);

private:
   Ship ships[10];
   Cell field[100];
   int count;
};

bool Map::hit(Cell cell)
{
   bool result = false;
   for (int i = 0; i < 10; i++)
   {
      if (ships[i].hit(cell))
      {
         result = true;
      }
      else
      {
         field[count] = cell;
         field[count].good = false;
         count = count + 1;
      }
   }
   return result;
}





bool Ship::hit(Cell cell)
{
   bool result = false;

   for (int i = 0; i < mSize; i++)
   {
      if (mCoords[i].x == cell.x && mCoords[i].y == cell.y)
      {
         mCoords[i].good = false;
         result = true;
         mHeath = mHeath - 1;
         break;
      }
   }
   return result;
}

void Ship::init(Cell startCell, int size, bool isVertical)
{
   mSize = size;
   mHeath = size;
   for (int i = 0; i < size; i++)
   {
      mCoords[i].good = true;

      if (isVertical)
      {
         mCoords[i].x = startCell.x;
         mCoords[i].y = startCell.y + i;
      }
      else
      {
         mCoords[i].x = startCell.x + i;
         mCoords[i].y = startCell.y;
      }
   }
}

bool Ship::isDead()
{
   return (mHeath == 0);
}

void main()
{
   int value;
   Ship ship;

   Cell startCell;
   startCell.x = 1;
   startCell.y = 1;

   ship.init(startCell, 3, false);

   Cell hitCell;
   hitCell.x = 5;
   hitCell.y = 5;

   bool result = ship.hit(hitCell);

   bool dead = ship.isDead();
}
