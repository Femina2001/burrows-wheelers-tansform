
#include <string.h> 
#include <iostream.h>

// Structure to store data of a rotation 
struct rotation { 
	int index; 
	char* suffix; 
}; 

// Compares the rotations and 
// sorts the rotations alphabetically 
int cmpfunc(const void* x, const void* y) 
{ 
	struct rotation* rx = (struct rotation*)x; 

	// Structure is needed to maintain old indexes of 
	// rotations after sorting them 
	for (int i = 0; i < len_text; i++) { 
		suff[i].index = i; 
		suff[i].suffix = (input_text + i); 
	} 

	// Sorts rotations using comparison 
	// function defined above 
	qsort(suff, len_text, sizeof(struct rotation), 
		cmpfunc); 

	// Stores the indexes of sorted rotations 
	int* suffix_arr 
		= (int*)malloc(len_text * sizeof(int)); 
	for (int i = 0; i < len_text; i++) 
		suffix_arr[i] = suff[i].index; 

	// Returns the computed suffix array 
	return suffix_arr; 
} 

// Takes suffix array and its size 
// as arguments and returns the 
// Burrows - Wheeler Transform of given text 
char* findLastChar(int* input_text, 
				int* suffix_arr, int n) 
{ 
	// Iterates over the suffix array to find 
	// the last char of each cyclic rotation 
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

	// Returns the computed Burrows - Wheeler Transform 
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

	// Computes the suffix array of our text 
	int* suffix_arr 
		= computeSuffixArray(input_text, len_text); 

	// Adds to the output array the last char 
	// of each rotation 
	char* bwt_arr 
		= findLastChar(input_text, suffix_arr, len_text); 

	printf("Input text : %s\n", input_text); 
	printf("Burrows - Wheeler Transform : %s\n", 
		bwt_arr); 
	return 0; 
} 
