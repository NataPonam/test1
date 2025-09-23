
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
void enter_new_text(const char *file_path)
{
  char str[1000];

  FILE *fp = fopen(file_path, "a");
  if (fp == NULL)
  {
    printf("n/a\n");
    return;
  }
  int c;
  while ((c = getchar()) != '\n' && c != EOF)
    ;
  if (fgets(str, sizeof(str), stdin) != NULL)
  {
    fseek(fp, 0, SEEK_END);
    long pos = ftell(fp);
    if (pos > 0)
    {
      fputc('\n', fp);
    }
    fputs(str, fp);
  }

  fclose(fp);
  print_file(file_path);
}

int main(void)
{

  int input_n;
  char file_path[256];
  while (1)
  {
    printf("Enter:\n\"1\" to enter file_path;\n\"2\" to enter a new text;\n\"-1\" for exit;\n");
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
      printf("Enter file_path:\n");
      if (scanf("%255s", file_path) != 1)
      {
        printf("n/a\n");
        while (getchar() != '\n')
          ;
        break;
      }
      print_file(file_path);
      break;
    case 2:
      printf("Enter new text:\n");
      enter_new_text(file_path);
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
