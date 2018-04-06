/*
 * hillcipher.c

 *
 *  Created on: Jun 20, 2017
 *      Author: Tyler Glorie
 */
#include <stdio.h>
#include <string.h>
#include <stdlib.h>
#include <ctype.h>

int main(int argc, char **argv){

	//prepare files
	FILE * pkey;
	pkey = fopen(argv[1],"r");
	if(pkey == NULL) printf("Could not open %s\n",argv[1]);
	FILE * pinput;
	pinput = fopen(argv[2],"r");
	if(pinput == NULL) printf("Could not open %s\n",argv[2]);

	char * input;
	int * output;
	char c = 0;
	int ksize=0;
	int key[9][9];
	int temp;

	int i = 0;
	int j = 0;
	int k = 0;
	int length = 0;

	input = malloc(sizeof(char)*10000);
	output = malloc(sizeof(int)*10000);
	//read dimension of array to ksize
	fscanf(pkey,"%d",&ksize);
	printf("\nKey Matrix:\n\n"); //print "header"
	//place key into array and print key array
	for(i=0;i<ksize;i++){
		for(j=0;j<ksize;j++){
			fscanf(pkey,"%d",&key[i][j]);//read each int
			printf("%d ",key[i][j]); //print each int
		}
		printf("\n"); // new line after each row
	}
	printf("\nPlaintext:\n");
	i=0;
	while(fscanf(pinput,"%c",&c) != EOF){ //read values into array with range of 0-25
		if ((c >= 'a') && (c <= 'z')) //places lowercases into input array
		{
			input[i] = c - 'a';
			i++;
		}
		else if ((c >= 'A') && (c <= 'Z'))  //places uppercases into input array
		{
			input[i] = c - 'A';
			i++;
		}
		length = i;
	}
	while(length % ksize != 0){ //pad with Xs
		input[length++] = 'x' -'a';
	}
	//printing plaintext
	for(i=0;i<length;i++){
		printf("%c",input[i]+'a');
		if((i+1)%80 == 0) printf("\n");
	}
	printf("\n");
	//performing the matrix calculations
	for(i=0;i<length;i++){
		output[i] = 0;
	}

	for(i=0;i<length;0){
		for(j=0;j<ksize;j++){
			for(k=0;k<ksize;k++){
				output[i+j] = output[i+j] + key[j][k]*input[i+k];
			}
		}
		i+=ksize;
	}
	//taking the mod 25 of output file
	for(i=0;i<length;i++){
		 output[i] = output[i]%26;
	}
	printf("\nCypherText:\n\n");
	for(i=0;i<length;i++){
		printf("%c",output[i]+'a');
		if((i+1)%80 == 0) printf("\n");
	}
	printf("\n");



return 0;
}
