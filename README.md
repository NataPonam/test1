# src/s21_string.h
#ifndef S21_STRING_H
#define S21_STRING_H
#include <stdio.h>

size_t s21_strlen(const char *str);
int s21_strcmp(const char *str1, const char *str2);
char *s21_strcpy(char *dest, const char *src);
char *s21_strcat(char *dest, const char *src);
char *s21_strchr(const char *str, char symb);
char *s21_strstr(const char *str, const char *substr);

#endif
# src/s21_string.c
#include "s21_string.h"
size_t s21_strlen(const char *str)
{
  size_t len = 0;
  while (*str)
  {
    str++;
    len++;
  }
  return len;
}
int s21_strcmp(const char *str1, const char *str2)
{
  while (*str1 && (*str1 == str2))
  {
    str1++;
    str2++;
  }
  return *str1 - *str2;
}
char *s21_strcpy(char *dest, const char *src)
{
  char *start = dest;
  while (*src)
  {
    *dest = *src;
    dest++;
    src++;
  }

  *dest = '\0';
  return start;
}
char *s21_strcat(char *dest, const char *src)
{
  char *start = dest;
  while (*dest)
  {
    dest++;
  }

  for (; *src; src++, dest++)
  {
    *dest = *src;
  }
  *dest = '\0';
  return start;
}
char *s21_strchr(const char *str, char symb)
{
  if (str == NULL)
    return NULL;
  for (; *str; str++)
  {
    if (*str == symb)
      return (char *)str;
  }
  if (symb == '\0')
    return (char *)str;

  return NULL;
}
char *s21_strstr(const char *str, const char *substr)
{
  if (substr == NULL || *substr == '\0')
    return (char *)str;
  while (*str)
  {
    const char *init_str = str;
    const char *find = substr;

    while (*find && *init_str && *init_str == *find)
    {
      init_str++;
      find++;
    }
    if (!*find)
    {
      return (char *)str;
    }
    str++;
  }
  return NULL;
}
# src/s21_string_test.c
#include <stdio.h>
#include "s21_string.h"
(1)
void s21_strlen_test(){
 // Тест 1: Нормальные значения - обычная строка
    printf("Input: \"Hello\"\n");
    printf("Expected: 5\n");
    size_t result1 = s21_strlen("Hello");
    printf("Actual: %zu\n", result1);
    printf("Result: %s\n\n", (result1 == 5) ? "SUCCESS" : "FAIL");

 // Тест 2: Краевое значение - пустая строка
    printf("Input: \"\"\n");
    printf("Expected: 0\n");
    size_t result2 = s21_strlen("");
    printf("Actual: %zu\n", result2);
    printf("Result: %s\n\n", (result2 == 0) ? "SUCCESS" : "FAIL");
    
    // Тест 3: Краевое значение - один символ
    printf("Input: \"A\"\n");
    printf("Expected: 1\n");
    size_t result3 = s21_strlen("A");
    printf("Actual: %zu\n", result3);
    printf("Result: %s\n\n", (result3 == 1) ? "SUCCESS" : "FAIL");
}
(2)
void s21_strcmp_test() { 
    // Тест 1: Нормальные значения - одинаковые строки
    printf("Input: \"hello\", \"hello\"\n");
    printf("Expected: 0\n");
    int result1 = s21_strcmp("hello", "hello");
    printf("Actual: %d\n", result1);
    printf("Result: %s\n\n", (result1 == 0) ? "SUCCESS" : "FAIL");
    // Тест 2: Нормальные значения - разные строки
    printf("Input: \"apple\", \"banana\"\n");
    printf("Expected: negative value\n");
    int result2 = s21_strcmp("apple", "banana");
    printf("Actual: %d\n", result2);
    printf("Result: %s\n\n", (result2 < 0) ? "SUCCESS" : "FAIL");
    // Тест 3: Краевое значение - пустые строки
    printf("Input: \"\", \"\"\n");
    printf("Expected: 0\n");
    int result3 = s21_strcmp("", "");
    printf("Actual: %d\n", result3);
    printf("Result: %s\n\n", (result3 == 0) ? "SUCCESS" : "FAIL");
}
(3)
void s21_strcpy_test() {
    printf("\n=== Testing s21_strcpy ===\n\n");
    
    // Тест 1: Нормальные значения - копирование строки
    char dest1[20];
    printf("Input: dest[20], \"hello\"\n");
    printf("Expected: \"hello\"\n");
    char *result1 = s21_strcpy(dest1, "hello");
    printf("Actual: \"%s\"\n", dest1);
    printf("Return: %p\n", result1);
    printf("Result: %s\n\n", (s21_strcmp(dest1, "hello") == 0) ? "SUCCESS" : "FAIL");
    
    // Тест 2: Краевое значение - пустая строка
    char dest2[20] = "original";
    printf("Input: dest[20], \"\"\n");
    printf("Expected: \"\"\n");
    char *result2 = s21_strcpy(dest2, "");
    printf("Actual: \"%s\"\n", dest2);
    printf("Return: %p\n", result2);
    printf("Result: %s\n\n", (s21_strcmp(dest2, "") == 0) ? "SUCCESS" : "FAIL");
    
    // Тест 3: Краевое значение - один символ
    char dest3[20];
    printf("Input: dest[20], \"A\"\n");
    printf("Expected: \"A\"\n");
    char *result3 = s21_strcpy(dest3, "A");
    printf("Actual: \"%s\"\n", dest3);
    printf("Return: %p\n", result3);
    printf("Result: %s\n\n", (s21_strcmp(dest3, "A") == 0) ? "SUCCESS" : "FAIL");
    }
(4)
void s21_strcat_test() {
    printf("\n=== Testing s21_strcat ===\n\n");
    
    // Тест 1: Нормальные значения - конкатенация строк
    printf("Test 1: Normal concatenation\n");
    char dest1[20] = "hello";
    printf("Input: dest=\"hello\", src=\" world\"\n");
    printf("Expected: \"hello world\"\n");
    char *result1 = s21_strcat(dest1, " world");
    printf("Actual: \"%s\"\n", dest1);
    printf("Return: %p\n", result1);
    printf("Result: %s\n\n", (s21_strcmp(dest1, "hello world") == 0) ? "SUCCESS" : "FAIL");
    
    // Тест 2: Краевое значение - пустая source строка
    printf("Test 2: Empty source string\n");
    char dest2[20] = "hello";
    printf("Input: dest=\"hello\", src=\"\"\n");
    printf("Expected: \"hello\"\n");
    char *result2 = s21_strcat(dest2, "");
    printf("Actual: \"%s\"\n", dest2);
    printf("Return: %p\n", result2);
    printf("Result: %s\n\n", (s21_strcmp(dest2, "hello") == 0) ? "SUCCESS" : "FAIL");
    
    // Тест 3: Краевое значение - пустая dest строка
    printf("Test 3: Empty destination string\n");
    char dest3[20] = "";
    printf("Input: dest=\"\", src=\"hello\"\n");
    printf("Expected: \"hello\"\n");
    char *result3 = s21_strcat(dest3, "hello");
    printf("Actual: \"%s\"\n", dest3);
    printf("Return: %p\n", result3);
    printf("Result: %s\n\n", (s21_strcmp(dest3, "hello") == 0) ? "SUCCESS" : "FAIL");
    }
(5)
void s21_strchr_test() {    
    const char *test_str = "Hello, World!";
    
    // Тест 1: Нормальные значения - символ существует
    printf("Input: str=\"%s\", c='o'\n", test_str);
    printf("Expected: pointer to first 'o'\n");
    char *result1 = s21_strchr(test_str, 'o');
    printf("Actual: found at position %ld\n", result1 - test_str);
    printf("Character: '%c'\n", *result1);
    printf("Result: %s\n\n", (result1 != NULL && *result1 == 'o') ? "SUCCESS" : "FAIL");
    
    // Тест 2: Нормальные значения - символ не существует
    printf("Input: str=\"%s\", c='z'\n", test_str);
    printf("Expected: NULL\n");
    char *result2 = s21_strchr(test_str, 'z');
    printf("Actual: %p\n", result2);
    printf("Result: %s\n\n", (result2 == NULL) ? "SUCCESS" : "FAIL");

// Тест 3: Краевое значение - первый символ
    printf("Test 3: First character\n");
    printf("Input: str=\"%s\", c='H'\n", test_str);
    printf("Expected: pointer to beginning\n");
    char *result3 = s21_strchr(test_str, 'H');
    printf("Actual: found at position %ld\n", result3 - test_str);
    printf("Result: %s\n\n", (result3 == test_str) ? "SUCCESS" : "FAIL");
    }
(6)
void s21_strstr_test() {
const char *init_str = "Hello, World!";
    // Тест 1: Нормальные значения - подстрока существует
    printf("Input: init_str=\"%s\", find=\"World\"\n", init_str);
    printf("Expected: pointer to \"World!\"\n");
    char *result1 = s21_strstr(init_str, "World");
    printf("Actual: found at position %ld\n", result1 - init_str);
    printf("Substring: \"%s\"\n", result1);
    printf("Result: %s\n\n", (result1 != NULL && s21_strcmp(result1, "World!") == 0) ? "SUCCESS" : "FAIL");

      // Тест 2: Нормальные значения - подстрока не существует
    printf("Input: init_str=\"%s\", find=\"Python\"\n", init_str);
    printf("Expected: NULL\n");
    char *result2 = s21_strstr(init_str, "Python");
    printf("Actual: %p\n", result2);
    printf("Result: %s\n\n", (result2 == NULL) ? "SUCCESS" : "FAIL");
    
    // Тест 3: Краевое значение - пустая find
    printf("Input: init_str=\"%s\", needle=\"\"\n", init_str);
    printf("Expected: pointer to init_str\n");
    char *result3 = s21_strstr(init_str, "");
    printf("Actual: %p, init_str: %p\n", result3, init_str);
    printf("Result: %s\n\n", (result3 == init_str) ? "SUCCESS" : "FAIL");
}
int main() {
    s21_strlen_test();    
    s21_strcmp_test();    
    s21_strcpy_test();   
    s21_strcat_test();    
    s21_strchr_test();    
    s21_strstr_test();    
    return 0;
}
# Makefile
test test
CC = gcc
CFLAGS = -Wall -Wextra -std=c11
SRC_DIR = src
BUILD_DIR = build

SRCS = $(SRC_DIR)/s21_string.c $(SRC_DIR)/s21_string_test.c
OBJS = $(SRCS:$(SRC_DIR)/%.c=$(BUILD_DIR)/%.o)

.PHONY: all strlen_tests strcmp_tests strcpy_tests strcat_tests strchr_tests strstr_tests clean test

# Сборка всех тестов
all: strlen_tests strcmp_tests strcpy_tests strcat_tests strchr_tests strstr_tests

# Quest 1-5: существующие цели
strlen_tests: $(BUILD_DIR)/Quest_1
strcmp_tests: $(BUILD_DIR)/Quest_2
strcpy_tests: $(BUILD_DIR)/Quest_3
strcat_tests: $(BUILD_DIR)/Quest_4
strchr_tests: $(BUILD_DIR)/Quest_5

# Quest 6: Тесты для strstr
strstr_tests: $(BUILD_DIR)/Quest_6

$(BUILD_DIR)/Quest_1: $(OBJS)
	@mkdir -p $(BUILD_DIR)
	$(CC) $(CFLAGS) -o $@ $(OBJS)

$(BUILD_DIR)/Quest_2: $(OBJS)
	@mkdir -p $(BUILD_DIR)
	$(CC) $(CFLAGS) -o $@ $(OBJS)

$(BUILD_DIR)/Quest_3: $(OBJS)
	@mkdir -p $(BUILD_DIR)
	$(CC) $(CFLAGS) -o $@ $(OBJS)

$(BUILD_DIR)/Quest_4: $(OBJS)
	@mkdir -p $(BUILD_DIR)
	$(CC) $(CFLAGS) -o $@ $(OBJS)

$(BUILD_DIR)/Quest_5: $(OBJS)
	@mkdir -p $(BUILD_DIR)
	$(CC) $(CFLAGS) -o $@ $(OBJS)

$(BUILD_DIR)/Quest_6: $(OBJS)
	@mkdir -p $(BUILD_DIR)
	$(CC) $(CFLAGS) -o $@ $(OBJS)

# Компиляция объектных файлов
$(BUILD_DIR)/%.o: $(SRC_DIR)/%.c
	@mkdir -p $(@D)
	$(CC) $(CFLAGS) -c $< -o $@

# Очистка
clean:
	rm -rf $(BUILD_DIR)

# Запуск всех тестов
test: all
	@echo "=== Running Quest_1 tests ==="
	./$(BUILD_DIR)/Quest_1
	@echo "=== Running Quest_2 tests ==="  
	./$(BUILD_DIR)/Quest_2
	@echo "=== Running Quest_3 tests ==="
	./$(BUILD_DIR)/Quest_3
	@echo "=== Running Quest_4 tests ==="
	./$(BUILD_DIR)/Quest_4
	@echo "=== Running Quest_5 tests ==="
	./$(BUILD_DIR)/Quest_5
	@echo "=== Running Quest_6 tests ==="
	./$(BUILD_DIR)/Quest_6

# Запуск конкретных тестов
test_strstr: strstr_tests
	./$(BUILD_DIR)/Quest_6
