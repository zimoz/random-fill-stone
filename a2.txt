//Author : zimo zhu



#include <iostream>
#include <string>
#include <fstream>
#include <iomanip>
#include <cmath>
#include <cstdlib>

using namespace std;

const int MAX_SIZEGRID = 50;        // size of largest board allowed    
const int MAX_INTERIOR_NEIGH = 8;   // number of neighbor bins for each interior bin
const int MAX_EDGE_NEIGH = 5;       // number of neighbor bins for each edge bin
const int MAX_CORNER_NEIGH = 3;     // number of neighbor bins for each corner bin
const int MAX_TYPES_NEIGH = 3;
//const int RAND_MAX =10000;
const int MAX_REPEATS = 100;

//This program consider a square board with N rows of N bins.  S stones ( 0 < S < N*N ) are placed randomly into the bins on the board
//Calculate the probability that a bin will contain a stone after all the stones have been placed on the board
//Randomly fill a 2d array with 0 and 1 
//then calculate the probability of the neighbour of one bin 
//put the calculated probability into to another 2d array

int MyFactorial( int numb );
double Permutation( int totNumObj, int numObjChosen );
void ArrayP1Fill( int sizeGrid, int** randGrid);
int ArrayRandFill( int sizeGrid, int numStones, int** randGrid, unsigned int seed);
void PrintSqArray( int sizeGrid, int elementWidth, int** myGrid);
void PrintArray(double myDist[][MAX_INTERIOR_NEIGH + 1]);
void CalcDistribution( int sizeGrid, int numStones, double distCalc[][MAX_INTERIOR_NEIGH + 1] );
void CountDistribution( int sizeGrid, int** randGrid, double distMeas[][MAX_INTERIOR_NEIGH + 1] );
void FillRandomArray ( int** randArray, int nrows,int ncols, unsigned int seed );
int main()
{
//initialize the variables
int size, numStones, seed,repeats,totNumObj,numObjChosen;
double Dist1 [3][9];
double Dist2 [3][9];
double Dist3 [3][9];
double Dist4 [3][9];
double Dist5 [3][9];

int numb;
int numReTries1;
int MAX_TRIES=3;
int numReTries2;
int numReTries3;
int numReTries4;


//checking the input value is vaild or not


numReTries1 = 0;
    do
    {		
        if( numReTries1 >  MAX_TRIES )
        {
            cout << "ERROR: Too many tries reading the number of bins"; 
            cout << endl;
            return 3;
        }
        if (numReTries1 > 0)
        {
            
            
            if(!cin)
                {
                    
                 cout << endl << "ERROR: the number of bins along the edge of the square board was not an integer" << endl; 
                 cin.clear();
                 cin.ignore(999,'\n');
               
                }
              else  if(size <=0 || size > MAX_SIZEGRID)
                 {
                        cout << endl << "ERROR: illegal number of bins along the edge of the square board." << endl;
                        
                 }
        }
        numReTries1++;		
        cout << "Enter the number of bins along the edge of the square board:  ";
        cin >> size;
    }	while ( size <= 0 || size > MAX_SIZEGRID||!cin);








numReTries2 = 0;
    do
    {		
       	 if( numReTries2 >  MAX_TRIES )
       	 {
            cout << "ERROR: Too many tries reading the number of stones"; 
            cout << endl;
            return 3;
      	  }
       	 if (numReTries2 > 0)
       	 {


        	if(!cin)
                {
                    
                 cout << endl << "ERROR: the number of stones was not an integer" << endl; 
                 cin.clear();
                 cin.ignore(999,'\n');  
                }
          else  if(numStones <=0 || numStones > (pow(size,2)))
                 {
                        cout << endl << "ERROR: illegal number of stones." << endl;
                 }
      

        }
       
            
            
            
        numReTries2++;		
        cout << "Enter the number of stones: ";
        cin >> numStones;
   }	while  (numStones <=0 || numStones > (pow(size,2))||(!cin));













numReTries3= 0;
    do
    {		
        if( numReTries3 >  MAX_TRIES )
        {
            cout << "ERROR: Too many tries reading the seed."; 
            cout << endl;
            return 3;
        }
        if (numReTries3 > 0)
        {
            
            if(!cin)
                {
                    
                 cout << endl << "ERROR: seed was not an integer" << endl;  
                 cin.clear();
                 cin.ignore(999,'\n'); 
                }
             else   if(seed <=1 || seed >RAND_MAX)
                 {
                        cout << endl << "ERROR:illegal seed." << endl;
                 }
            
        }
        numReTries3++;		
        cout << "Enter the seed for the random number generator: ";
        cin >> seed;
    }	while ((seed <=1 || seed >RAND_MAX)||(!cin));




numReTries4 = 0;
    do
    {		
        if( numReTries4 >  MAX_TRIES )
        {
            cout << "ERROR: Too many tries reading the number of test repeats."; 
            cout << endl;
            return 3;
        }
        if (numReTries4 > 0)
        {
            
            if(!cin)
                {
                    
                 cout << endl << "ERROR: number of test repeats was not an integer." << endl;  
                 cin.clear();
                 cin.ignore(999,'\n'); 
                }
              else  if(repeats <=0 || repeats >MAX_REPEATS)
                 {
                        cout << endl << "ERROR: illegal number of test repeats." << endl;
                 }
            
        }
        numReTries4++;		
        cout << "Eenter the number of repeats for test: ";
        cin >> repeats;
    }	while ((repeats <=0 || repeats >MAX_REPEATS)||(!cin));






// dynamic allocate the 2d array




int **myarray1 = new int*[size];
		for(int i=0; i<size; i++)
    	{
	   	 myarray1[i]=new int[size];
    	}


int **myarray2 = new int*[size];
		for(int i=0; i<size; i++)
    	{
	   	 myarray2[i]=new int[size];
    	}
int **myarray3 = new int*[size];
		for(int i=0; i<size; i++)
    	{
	   	 myarray3[i]=new int[size];
    	}






//try the following function and catch the throwed exceptions

try{    CalcDistribution(size, numStones, Dist1);
	
    	PrintArray(Dist1);
    	int z = ArrayRandFill(size, numStones, myarray1, seed);

    	PrintSqArray(size, 3, myarray1);
    	CountDistribution(size, myarray1, Dist2);
    
    	PrintArray(Dist2);
    	ArrayP1Fill(size,myarray2);
    	PrintSqArray(size,3,myarray2);
    	CountDistribution(size, myarray2, Dist4);
    	
    	PrintArray(Dist4);

    	
    	for(int i=0; i<3; i++){
    			for (int j=0; j<9; j++){
    				Dist3[i][j]=0;
    				Dist5[i][j]=0;
    			}
    		}
    	for (int k=0;k<repeats;k++){
    
    		ArrayRandFill(size,numStones, myarray3, z);

    		CountDistribution(size, myarray3, Dist5);

    		for(int i=0; i<3; i++){
    			for(int j=0; j<9; j++){
    				Dist3[i][j]+=Dist5[i][j];
    			}
    		}
    		for(int i=0; i<size; i++){
    			for (int j=0; j<size; j++){
    				myarray3[i][j] = 0;
    			}
    		}
    		for(int i=0; i<3; i++){
    			for (int j=0; j<9; j++){
    				Dist5[i][j]=0;
    			}
    		}

    		
    	}
    

    	for(int i=0; i<3; i++){
    		for(int j=0; j<9; j++){
    			Dist3[i][j] = (Dist3[i][j])/repeats;
    		}
    	}
    
    	PrintArray(Dist3);
   // delete the dynamic allocated array

    	for(int i=0;i<size;i++){
    		
    			delete[]myarray1[i];
    			delete[]myarray2[i];
    			delete[]myarray3[i];
    		
    	}
    	delete[]myarray1;
    	delete[]myarray2;
    	delete[]myarray3;
    	myarray1=NULL;
    	myarray2=NULL;
    	myarray3=NULL;
    }

	   

	catch(const char* msg){
    cerr << msg <<endl;
    exit(1);
	}

    	



    return 0;
}

// function MyFactorial calculate the factorial of an integer in certain range
//if not , throw an exception

int MyFactorial(int numb)
{
		if ( numb<0 ) 
		{
        	throw  "Factorial of a negative Value not allowed in MyFactorial" ;
   		}
 		else if(numb >12)
 		{
 			throw "Factorial too large to represent in MyFactorial" ;
		}
 		else
 		{
	     if(numb>1)
	        return numb * MyFactorial(numb-1);
	        else
	        {
		    return 1;
	        } 
     	}
}
// calculate the permutation of total number and number to be choosen

double Permutation( int totNumObj, int numObjChosen )
{	
	try
	{
		MyFactorial(totNumObj);
	}
	catch (const char* msg)
	{
		cerr << "in this function Permutation"
		<< "MyFactorial was called"<<endl;
  		throw msg;
	}

	try
	{
		MyFactorial(numObjChosen);
	}
	catch (const char* msg)
	{
		cerr << "in this function Permutation"
		<< "MyFactorial was called"<<endl;
  		throw msg;
	}
	try
	{
		MyFactorial(totNumObj-numObjChosen);
	}
	catch (const char* msg)
	{
		cerr << "in this function Permutation"
		<< "MyFactorial was called"<<endl;
  		throw msg;
	}


	if (numObjChosen > totNumObj)
	{
		throw "ERROR: tried to select more objects than the total number of objects in Permutation";
	}
	if (totNumObj <=0)
	{
		throw "ERROR: tried to select from a group of objects with 0 or a negative number of members in Permutation";
	}
	if (numObjChosen < 0 )
	{
		throw "ERROR: tried to select a negative number of objects in Permutation";
	}


return MyFactorial(totNumObj)/(MyFactorial(numObjChosen)*MyFactorial(totNumObj-numObjChosen));
}

// fill a 2d array with 1 and 0 excatly like the problem given

void ArrayP1Fill(int sizeGrid, int** randGrid)
{

	if (randGrid ==NULL)
	{
		throw "ERROR: grid array argument in ArrayP1Fill was null ";
	}


	if (sizeGrid >MAX_SIZEGRID)
	{
		throw "ERROR: grid size in ArrayP1Fill is too large";
	}


	int i=0, j=0;

	for (i=0; i<sizeGrid; i++)
	{
		for(j=0; j<sizeGrid; j++)
		{
			if(i%2 == 0)
			{
				if(j%2 == 0)
				{
					randGrid[i][j] = 0;
				}
				else
				{
					randGrid[i][j] = 1;
				}
			}
			else if(i%2 != 0)
			{
				if(j%2 == 0)
				{
					randGrid[i][j] = 1;
				}
				else
				{
					randGrid[i][j] = 0;
				}
			}
		}
	}
}
//randomly fill a 2d array with 1 and 0

int ArrayRandFill(int sizeGrid, int numStones, int** randGrid, unsigned int seed)
{
	
	srand(seed);
	if (sizeGrid > MAX_SIZEGRID)
	{
		throw "ERROR: grid size in ArrayRandFill is too large";
	}

	
	if(randGrid == NULL)
	{
		throw "ERROR: grid array argument in ArrayRandFill was null ";
	}

	if(numStones>pow(sizeGrid,2)){
		throw "ERROR: number of stones in ArrayRandFill is greater than number of grid cells";
	}

	for(int i=0; i<numStones;)
	{
		int rand1 = rand();
		//cout << "rand1 is "<< rand1<<endl;
		int rand2 = rand();
		//cout <<"rand2 is " <<rand2 << endl;
		if ((rand1%sizeGrid>=0)&&((rand1%sizeGrid)<sizeGrid)&&(rand2%sizeGrid>=0)&&((rand2%sizeGrid)<sizeGrid))
		{
			if(randGrid[rand2%sizeGrid][rand1%sizeGrid] == 0)
			{
				randGrid[rand2%sizeGrid][rand1%sizeGrid] = 1;
				i++;
			}
			else{

			}

		}
	}
	return rand();
}

//print the square array

void PrintSqArray( int sizeGrid, int elementWidth, int** myGrid)
{
    if(elementWidth<2 || elementWidth>12){
    	throw "ERROR: width for each element printed in PrintSqArray is out of range";
    }

	if (sizeGrid > MAX_SIZEGRID)
	{
		throw "ERROR: grid size in ArrayRandFill is too large";
	}


	if(myGrid==NULL)
	{
		throw "ERROR: grid array argument in ArrayRandFill was null ";
	}
	for (int i=0; i < sizeGrid;i++)
	{
		for(int j=0 ;j<sizeGrid; j++)
		{
			cout << fixed<<setw(elementWidth)<<myGrid[i][j];
		}
		cout <<endl;
	}
	cout << endl <<endl ;
}

//print the array with certain size and precision

void PrintArray(double myDist[][MAX_INTERIOR_NEIGH + 1])
{	



	for (int i=0; i < 3;i++)
	{
		for(int j=0 ;j<(MAX_INTERIOR_NEIGH + 1); j++)
		{
			cout << setw(12)<<fixed<<setprecision(3)<<myDist[i][j];

		}
		cout <<endl;
	}
	cout << endl <<endl ;
}


//calculate the distribution
 
void CalcDistribution( int sizeGrid, int numStones, double distCalc[][MAX_INTERIOR_NEIGH + 1] )
{	
	try
	{	for (int i = 0; i < 8; i++)
		{
		Permutation(8,i);
		}
		for (int j = 0; j < 5; j++)
		{
		Permutation(5,j);
		}
		for (int k = 0; k < 3; k++)
		{
			Permutation(3,k);
		}
		
	}
	catch (const char* msg)
	{
		cout << "in this function CalcDistribution"
		<< "Permutation was called"<<endl;
  		throw msg;
	}









	if (sizeGrid>MAX_SIZEGRID)
	{
		throw "ERROR: length of one side of the grid in CalcDistribution is larger than MAX_SIZEGRID";
	}
	if (numStones>pow(sizeGrid,2))
	{
		throw "ERROR: number of stones in CalcDistribution is greater than number of grid cells";
	}

	for(int i=0;i<=8;i++)
	{
		distCalc[0][i]= Permutation(8,i)*pow(numStones/pow(sizeGrid,2),i)*pow(1-(numStones/pow(sizeGrid,2)),8-i);
	}
	for(int j =0 ;j<=8;j++)
	{
		if(j>5){
			distCalc[1][j]=0;
		} 
		else{
			distCalc[1][j]=Permutation(5,j)*pow(numStones/pow(sizeGrid,2),j)*pow(1-(numStones/pow(sizeGrid,2)),5-j);
		}
		
	}
	for(int k = 0 ;k<=8; k++)
	{ 	
		if(k>3){
			distCalc[2][k]=0;
		}

		else{
			distCalc[2][k]=Permutation(3,k)*pow(numStones/pow(sizeGrid,2),k)*pow(1-(numStones/pow(sizeGrid,2)),3-k);
		}
	}
}

//count the number of neighbour which contained 1 in 3 different cases: corner edge and interior.

void CountDistribution( int sizeGrid, int** randGrid, double distMeas[][MAX_INTERIOR_NEIGH + 1] )
{	
	if (randGrid ==NULL)
	{
		throw "ERROR: grid array argument in CountDistribution was null";
	}

	if (sizeGrid > MAX_SIZEGRID)
	{
		throw "ERROR: length of one side of the grid in CountDistribution is larger than MAX_SIZEGRID";
	}

	int T=0;
	double num_inter_bin = (sizeGrid-2)*(sizeGrid-2);
	double num_edge_bin = 4*(sizeGrid-2);
	double num_corner_bin = 4;

	for(int k=0; k<sizeGrid; k++)
	{
		for(int p=0; p<sizeGrid; p++)
		{
			if((k>=1)&&(k<=(sizeGrid-2))&&(p>=1)&&(p<=(sizeGrid-2)))
			{
				if(randGrid[k-1][p-1] == 1)
				{
					T+=1;
				}
				if(randGrid[k-1][p] == 1)
				{
					T+=1;
				}
				if(randGrid[k-1][p+1] == 1)
				{
					T+=1;
				}
				if(randGrid[k][p-1] == 1)
				{
					T+=1;
				}
				if(randGrid[k][p+1] == 1)
				{
					T+=1;
				}
				if(randGrid[k+1][p-1] == 1)
				{
					T+=1;
				}
				if(randGrid[k+1][p] == 1)
				{
					T+=1;
				}
				if(randGrid[k+1][p+1] == 1)
				{
					T+=1;
				}
				distMeas[0][T] += (1/num_inter_bin);
				// cout << "this is T " << T << endl;
				// cout << "this is distMeas "<< distMeas[0][T]<< endl;
				T = 0;
				
			}
			else if((k==0 && ((p>=1)&&(p<=(sizeGrid-2))))
				|| ((k==(sizeGrid-1))&&(p>=1)&&(p<=(sizeGrid-2)))
				|| ((k>=1)&&(k<=(sizeGrid-2))&&(p==0))
				|| ((k>=1)&&(k<=(sizeGrid-2))&&(p==(sizeGrid-1))))
			{
				if(k==0)
				{
					if(randGrid[k][p-1] == 1)
					{
						T+=1;
					}
					if(randGrid[k+1][p-1] == 1)
					{
						T+=1;
					}
					if(randGrid[k+1][p] == 1)
					{
						T+=1;
					}
					if(randGrid[k][p+1] == 1)
					{
						T+=1;
					}
					if(randGrid[k+1][p+1] == 1)
					{
						T+=1;
					}
					distMeas[1][T] += (1/num_edge_bin);
					T = 0;
				}
				else if (k==(sizeGrid-1))
				{
					if(randGrid[k-1][p-1] == 1)
					{
						T+=1;
					}
					if(randGrid[k-1][p] == 1)
					{
						T+=1;
					}
					if(randGrid[k-1][p+1] == 1)
					{
						T+=1;
					}
					if(randGrid[k][p-1] == 1)
					{
						T+=1;
					}
					if(randGrid[k][p+1] == 1)
					{
						T+=1;
					}
					distMeas[1][T] += (1/num_edge_bin);
					T = 0;
				}
				else if (p==0)
				{
					if(randGrid[k-1][p] == 1)
					{
						T+=1;
					}
					if(randGrid[k+1][p] == 1)
					{
						T+=1;
					}
					if(randGrid[k-1][p+1] == 1)
					{
						T+=1;
					}
					if(randGrid[k][p+1] == 1)
					{
						T+=1;
					}
					if(randGrid[k+1][p+1] == 1)
					{
						T+=1;
					}
					distMeas[1][T] += (1/num_edge_bin);
					T = 0;
				}
				else
				{
					if(randGrid[k-1][p-1] == 1)
					{
						T+=1;
					}
					if(randGrid[k][p-1] == 1)
					{
						T+=1;
					}
					if(randGrid[k+1][p-1] == 1)
					{
						T+=1;
					}
					if(randGrid[k-1][p] == 1)
					{
						T+=1;
					}
					if(randGrid[k+1][p] == 1)
					{
						T+=1;
					}
					distMeas[1][T] += (1/num_edge_bin);
					T = 0;
				}
			}
			else if (((k==0)&&(p==0))
					|| ((k==0)&&(p==(sizeGrid-1)))
					|| ((k==sizeGrid-1)&&(p==0))
					|| ((k==sizeGrid-1)&&(p==sizeGrid-1)))
			{
				if((k==0) && (p==0))
				{
					// cout << "loop checkec" << endl;
					if(randGrid[k][p+1] == 1)
					{
						T+=1;
						//cout << "this is t "<< T << endl;
					}
					if(randGrid[k+1][p] == 1)
					{
						T+=1;
					}
					if(randGrid[k+1][p+1] == 1)
					{
						T+=1;
					}
					distMeas[2][T] += (1/num_corner_bin);
					// cout << setprecision(2) << distMeas[2][T] << endl;
					// cout << "this is second t "<< T << endl;
					// cout <<setprecision(3)<< "distMeas "<< distMeas[2][T] << endl;
					T = 0;
				}
				else if((k==0) && (p==(sizeGrid-1)))
				{
					if(randGrid[k][p-1] == 1)
					{
						T+=1;
					}
					if(randGrid[k+1][p-1] == 1)
					{
						T+=1;
					}
					if(randGrid[k+1][p] == 1)
					{
						T+=1;
					}
					distMeas[2][T] += (1/num_corner_bin);
					T = 0;
				}
				else if((k==(sizeGrid-1)) && (p==0))
				{
					if(randGrid[k-1][p] == 1)
					{
						T+=1;
					}
					if(randGrid[k-1][p+1] == 1)
					{
						T+=1;
					}
					if(randGrid[k][p+1] == 1)
					{
						T+=1;
					}
					distMeas[2][T] += (1/num_corner_bin);
					T = 0;
				}
				else
				{
					if(randGrid[k-1][p] == 1)
					{
						T+=1;
					}
					if(randGrid[k-1][p-1] == 1)
					{
						T+=1;
					}
					if(randGrid[k][p-1] == 1)
					{
						T+=1;
					}
					distMeas[2][T] += (1/num_corner_bin);
					T = 0;
				}
			}
		}
	
	}
}




