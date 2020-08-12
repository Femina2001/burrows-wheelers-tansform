
#include <string.h> 
#include <iostream.h>
struct rotation { 
	int index; 
	char* suffix; 
};
int cmpfunc(const void* x, const void* y) 
{ 
	struct rotation* rx = (struct rotation*)x; 

	 
	for (int i = 0; i < len_text; i++) { 
		suff[i].index = i; 
		suff[i].suffix = (input_text + i); 
	} 	
	qsort(suff, len_text, sizeof(struct rotation), 
		cmpfunc); 	
	int* suffix_arr 
		= (int*)malloc(len_text * sizeof(int)); 
	for (int i = 0; i < len_text; i++) 
		suffix_arr[i] = suff[i].index; 
	return suffix;
char* findLastChar(int* input_text, 
				int* suffix_arr, int n) 
{ 
	char* bwt_arr = (char*)malloc(n * sizeof(char)); 
	int i; 
	for (i = 0; i < n; i++) { 
		// Computes the last char which is given by 
		// input_text[(suffix_arr[i] + n - 1) % n] 
		int j = suffix_arr[i] - 1; 
		if (j < 0) 
			j = j + n; 

		bwt_arr[i] = input_text[j]; 
	} 
	bwt_arr[i] = '\0';
	return bwt_arr; 
} 

// Driver program to test functions above 
int main() 
{ 
	char input_text[] = "Curneu MedTech Innovation is a health care technology firm 
	 at Heidelberg, Germany. We work on a motive of building affordable and 
	 innovative healthcare solutions that address the clinical needs thereby bringing
     better lives for the needy $";

	int len_text = strlen(input_text);
	int* suffix_arr 
		= computeSuffixArray(input_text, len_text); 


	char* bwt_arr 
		= findLastChar(input_text, suffix_arr, len_text); 

	printf("Input text : %s\n", input_text); 
	printf("Burrows - Wheeler Transform : %s\n", 
		bwt_arr); 
	return 0; 
} 
