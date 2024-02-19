// Online C++ compiler to run C++ program online
#include <iostream>
using namespace std;
int precedenceChecker(char opr){
    if(opr == '('||opr == '['||opr == '{'){return 1;}
    else if(opr =='/'){return 2;}
    else if(opr =='*'){return 3;}
    else if(opr =='+'){return 4;}
    else if(opr =='-'){return 5;}
    else{
        return 6;
    }
}

string inputExpression(){
    string expression;
    cout<<"Please  Enter your Expression"<<endl;
    cin>>expression;
    return expression;
}

// this function will return a pointer that will point out starting of the array
char* stringToCharacterArray(string expression){
    char* characterArray = new char[50];//Dynammically allocate memory address for array
    int iterations = expression.length();
    for (int i = 0;i<iterations;i++){
        characterArray[i]= expression[i];
    }
    return characterArray;
}

char** printCertainArray(char* address){
    int iteraations =0;
    while(address[iteraations] != '\0'){
        iteraations++;
    }
    cout << "You Entered"<<endl;
    char* operatorsArray = new char[100];
    int* indexArray = new int[100];
    int indexOfOpearor = 0;
    int index = 0;
    
    for (int i = 0;i<iteraations;i++){
        cout<<address[i]<<endl;
        if(address[i] == '(' || address[i] == '{' || address[i] == '['|| address[i] == ']'|| address[i] == '}'|| address[i] == ')'|| address[i] == '/' || address[i] == '*'|| address[i] == '+'|| address[i] == '-'){
            operatorsArray[indexOfOpearor] = address[i];
            indexArray[index] = i;
            indexOfOpearor++;
            index++;
        }
    }
    //for checking address of startinf index of aray not value we can use static_cast<void*>(address to first index)
    // here I have created pointer array to store pointers to two arrays  I have created.
    
    char** arraysAddresses = new char*[5];
    // Storing first address of eaach array in pointer array
    arraysAddresses[0] = reinterpret_cast<char*>(operatorsArray);
    arraysAddresses[1] = reinterpret_cast<char*>(indexArray);
    //Returning address of first index of pointers aarray
    return arraysAddresses;
    
}

void PrecedenceAndOperation(char* characterArray,char* operatorArray, int* indexOfOperatorArray){
    cout<<"some vallues are "<<characterArray[0]<<operatorArray[0]<<indexOfOperatorArray[0];
    // now Our arrays are setuped now we can perform operations here
    int iterations = 0;
    while(operatorArray[iterations]!='\0'){
        iterations++;
    }
    int higherPrecedence = 6;
    int higherPrecedenceIndex = 0;
    for(int i = 0;i<iterations;i++){
        int precedence = precedenceChecker(operatorArray[i]);
        if(higherPrecedence>=precedence){
            higherPrecedence = precedence;
            higherPrecedenceIndex = i;
        }
    }
    cout <<"Highest Precedence operator is "<<operatorArray[higherPrecedenceIndex]<<"and index is "<<higherPrecedenceIndex;
    
}














int main() {

    string userExpression = inputExpression();
    char* addressToCharArray = stringToCharacterArray(userExpression);
    char** arrayAddresses = printCertainArray(addressToCharArray);
    //declaring pointer to get address to  firsst index of my array and next line printing second value  of my array at that index.
    char* oprator1ArrayAddress =  arrayAddresses[0];
    //to  converts address of characteer type in to int I have used below lin eof reinterpret_cast<int*>(arrayAddresses[1]);
    int* indexArrayAddress = reinterpret_cast<int*>(arrayAddresses[1]);
    PrecedenceAndOperation(addressToCharArray,oprator1ArrayAddress,indexArrayAddress);

    return 0;
}



