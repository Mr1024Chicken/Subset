# Subset
finding the sum of all subset in a given array and target value
/*

CSE 2320--Lab 2
Kha Vo

take input from keyboard or " < " shell input.

*/

#include <stdio.h>
#include <stdlib.h>

void readInput(int* n,int* m,int** S,int** C)
{
int i;

scanf("%d",n);
scanf("%d",m);

*S=(int*) malloc((*n+1)*sizeof(int));
*C=(int*) malloc(((*m)*(*n+1))*sizeof(int));
if (!(*S) || !(*C))
{
  printf("malloc failed %d\n",__LINE__);
  exit(0);
}

(*S)[0]=0;               
for (i=1;i<=*n;i++)
  scanf("%d",*S+i);
}

void subsetSum(int n,int m,int* S,int* C,int card)
{
int i,j,sum ,local;

  for (j=1;j<=n;j++)
  {
    sum = m -S[j];      
	if (card ==1){			// 1 card special case
		if(m == S[j]){
		break;
		}
		else {
			continue;
		}
	}                                      
  
	 local = (n * sum) + (card -1);
	if(sum >=0 && C[local] <j){
			break;
 }
  }

  local = (n*m) +card;
  C[local] = j;				// building up the cost table 

}

void writeOutput(int n,int m,int* S,int* C)
{
int i, j=0 , k=0, l=0;
printf("m = %d\n", m);
printf(" i    S\n");
printf("*************\n");

for(i =0; i <=n; i++){
printf("%3d %3d\n",i ,S[i]);
}

printf( "i___card___C\n");
printf("*************\n");
for(i = 1; i<= ((m+1)*(n)); i ++){
		if (j ==n){
		j =0;
		k++;
		
}
		j++;
		printf("%3d %3d %3d\n",k,j,C[i]);
		
		
}
int card;
int sum;
	for(i= 1; i<= n;i ++){
		sum=m;
		card=i;
		
		if(C[(sum * n)+card] <= n){
			printf("Solution for %d element\n",i);
			printf(" i    S\n");
		printf("*************\n");
		for(card = i; card >0; card --){
		
		printf(" %d  %d\n", C[(sum * n)+card],S[C[(sum * n)+card]]);
		sum -= S[C[(sum * n)+card]];
		}
		}
		else{
		printf("No solution for %d element\n",i);
		}
	}

}


int main()
{
int n=0;  
int m=0;    
int *S;   
int *C;   
int j=0,i=0;

readInput(&n,&m,&S,&C);

for (i =0; i <= m ; i++){
	for (j = 1; j <=n;j++){
		if (i==0){	
		C[j] = n+1;
		}
		
			subsetSum(n,i,S,C,j);
		
	}
}
writeOutput(n,m,S,C);


free(S);
free(C);
}
