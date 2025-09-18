# door_struct.h
#ifndef DOOR_STRUCT.H
#define DOOR_STRUCT.H

struct door
{
  int id;
  int status;
};
#endif
# dmanager_module.c
#include "door_struct.h"
#include <stdio.h>
#include <stdlib.h>
#include <time.h>
#define DOORS_COUNT 15
#define MAX_ID_SEED 10000


void initialize_doors(struct door *doors);
void sort_doors(struct door *doors, int ar_size);
void close_doors(struct door *doors, int ar_size);
void output_doors(struct door *doors, int ar_size);

int main()
{
  struct door doors[DOORS_COUNT];

  initialize_doors(doors);
  sort_doors(doors, DOORS_COUNT);
  close_doors(doors, DOORS_COUNT);
  output_doors(doors, DOORS_COUNT);
}

// Doors initialization function
// ATTENTION!!!
// DO NOT CHANGE!
void initialize_doors(struct door *doors)
{
  srand(time(0));

  int seed = rand() % MAX_ID_SEED;
  for (int i = 0; i < DOORS_COUNT; i++)
  {
    doors[i].id = (i + seed) % DOORS_COUNT;
    doors[i].status = rand() % 2;
  }
}
void sort_doors(struct door *doors, int ar_size)
{
  for (int i = 0; i < ar_size - 1; i++)
  {
    int min = i;
    for (int j = i + 1; j < ar_size; j++)
    {
      if (doors[j].id < doors[min].id)
      {
        min = j;
      }
        }
    if (min != i)
    {
      struct door temp = doors[i];
      doors[i] = doors[min];
      doors[min] = temp;
    }
  }
}
void close_doors(struct door *doors, int ar_size)
{
  for (int i = 0; i < ar_size; i++)
  {
    doors[i].status = 0;
  }
}
void output_doors(struct door *doors, int ar_size)
{
  for (int i = 0; i < ar_size; i++)
  {
    printf("%d, %d\n", doors[i].id, doors[i].status);
  }
}
# Makefile
# Цель по умолчанию - собираем Quest 1
all: door_struct

# Стадия door_struct для Quest 1
door_struct:
	gcc -Wall -Wextra -Werror -std=c11 -c src/dmanager_module.c -o src/dmanager_module.o
	mkdir -p build
	gcc src/dmanager_module.o -o build/Quest_1

# Очистка
clean:
	rm -f src/*.o build/Quest_1

# Пересборка
rebuild: clean all
