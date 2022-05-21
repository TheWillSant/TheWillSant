/*
 * Exercício 2 de "Exercícios com Funções - Parte II" (variante)
 * 
 * https://www.ime.usp.br/~macmulti/exercicios/funcoes2/index.html
 * 
 * (a) Escreva uma função que recebe como parâmetro um inteiro positivo
 * ano e devolve 1 se ano for bissexto, 0 em caso contrário.  (Um ano é
 * bissexto se ano % 4 == 0 && (ano % 100 != 0 || ano % 400 == 0).)  
 * 
 * (b) Escreva uma função que tem como parâmetros de entrada e saída três
 * números inteiros, dia, mes e ano, representando uma data, e modifica
 * esses inteiros de forma que eles representem o dia seguinte. 
 * 
 * (c) Escreva um programa que, dadas duas datas, determina o número de
 * dias entre essas datas.  Você pode supor que a primeira data é
 * anterior à segunda data.
 * 
 * Exercícios adicionais: (i) Quantos dias você já viveu?  (ii) Em que
 * dia da semana você nasceu?  Resolva (ii) sabendo que 1/1/1900 foi uma
 * segunda-feira.
 * 
 * $ calendario 28 8 2004 19 5 2022
 * Elapsed days: 6473
 * $ calendario 19 5 2022 31 12 2026
 * Elapsed days: 1687
 * $
 */ 

#include <stdio.h>
#include <stdlib.h>

/* leap_year(): devolve TRUE se e só se y é bissexto */
int leap_year(int y);

/* next_day(): atualiza a data dada para a data do dia seginte */
void next_day(int *d, int *m, int *y);

/* equal(): devolve TRUE se e só se são a mesma data */
int equal(int d0, int m0, int y0, int d1, int m1, int y1);

int main(int argc, char *argv[])
{
  int d0 = atoi(argv[1]), m0 = atoi(argv[2]), y0 = atoi(argv[3]),
      d1 = atoi(argv[4]), m1 = atoi(argv[5]), y1 = atoi(argv[6]);
      
  int N = 0;

  while (!equal(d0, m0, y0, d1, m1, y1)) {
    next_day(&d0, &m0, &y0);
    N++;
  }

  printf("Elapsed days: %d\n", N);
  
  return 0;
}

/* leap_year(): devolve TRUE se e só se y é bissexto */
int leap_year(int y) {
  return y % 4 == 0 && (y % 100 != 0 || y % 400 == 0);
}

/* equal(): devolve TRUE se e só se são a mesma data */
int equal(int d0, int m0, int y0, int d1, int m1, int y1) {
  return d0 == d1 && m0 == m1 && y0 == y1;
}

/* next_day(): atualiza a data dada para a data do dia seginte */
void next_day(int *d, int *m, int *y) {
  int last_day;
  if (*m == 1 || *m == 3 || *m == 5 || *m == 7
      || *m == 8 || *m == 10 || *m == 12)
    last_day = 31;
  if (*m == 4 || *m == 6 || *m == 9 || *m == 11)
    last_day = 30;
  if (*m == 2 && leap_year(*y))
    last_day = 29;
  if (*m == 2 && !leap_year(*y))
    last_day = 28;

  if (*d < last_day) { (*d)++; return; }

  *d = 1;
  if (*m < 12) { (*m)++; return; }

  *m = 1; (*y)++;
}

