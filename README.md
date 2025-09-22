# MAIN
#include <stdio.h>
#include <string.h>
void print_file(const char *file_path)
{
  FILE *fp = fopen(file_path, "r");
  if (fp == NULL)
  {
    printf("n/a\n");
    return;
  }
  fseek(fp, 0, SEEK_END); // pointer  to the end
  long pos = ftell(fp);   // check position
  if (pos == 0)
  {
    printf("n/a\n");
    fclose(fp);
    return;
  };
  rewind(fp); // pointer to start

  char arr[256];
  int ch;
  int i = 0;
  while ((ch = fgetc(fp)) != EOF && i < 255)
    arr[i++] = ch;
  arr[i] = '\0';
  printf("%s\n", arr);
  fclose(fp);
}

int main(void)
{

  int input_n;
  char file_path[256];
  while (1)
  {
    printf("Enter \"1\" for file_path and \"-1\" for exit");
    if (scanf("%d", &input_n) != 1)
    {
      printf("n/a\n");
      while (getchar() != '\n')
        ;
      continue;
    }
    switch (input_n)
    {
    case 1:
      printf("Enter file_path");
      if (scanf("%255s", &file_path) != 1)
      {
        printf("n/a\n");
        while (getchar() != '\n')
          ;
        break;
      }
      print_file(file_path);
      break;

    case -1:
      return 0;

    default:
      printf("n/a\n");
      break;
    }
  };

  return 0;
}
# Makefile
makefile
# Простой Makefile для проекта cipher

# Компилятор
CC = gcc

# Флаги компиляции
CFLAGS = -Wall -Wextra -Werror -std=c11

# Имя исполняемого файла
TARGET = cipher

# Папка с исходным кодом
SRC_DIR = src

# Папка для сборки
BUILD_DIR = build

# Исходный файл
SRC_FILE = $(SRC_DIR)/cipher.c

# Полный путь к исполняемому файлу
OUTPUT = $(BUILD_DIR)/$(TARGET)

# Основная цель - сборка проекта
all: cipher

# Цель для сборки программы
cipher: $(BUILD_DIR) $(OUTPUT)

# Создание папки build если её нет
$(BUILD_DIR):
	mkdir -p $(BUILD_DIR)

# Компиляция программы
$(OUTPUT): $(SRC_FILE)
	$(CC) $(CFLAGS) -o $(OUTPUT) $(SRC_FILE)

# Очистка собранных файлов
clean:
	rm -rf $(BUILD_DIR)

# Пересборка проекта
rebuild: clean all

# Пересборка
rebuild: clean all
