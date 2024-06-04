---
layout:     post
title:      "CS106B Assignments1"
subtitle:   "Getting Your C++ Legs （2024.spring）"
date:       2024-06-03 11:08:51
author:     "GanZJ"
header-img: "img/post-bg-cs106b.jpeg"
catalog: true
tags:
  - cs106b
---

## Perfect numbers

```cpp
long smarterSum(long n) {
    /* TODO: Fill in this function. */
    long total = 0;
    for(long divisor = 1; divisor <= sqrt(n); divisor++){
        if(divisor == 1 || divisor == sqrt(n))
            total += divisor;
        else if ( n % divisor == 0)
            total = total + divisor + n/divisor;
    }
    return total;
}
```



```cpp
long findNthPerfectEuclid(long n) {
    if (n < 1 )
        return -1;

    long count = 1;
    long k = 1;
    do{
        long m = pow(2,k) - 1;
        if (smarterSum(m) == 1 && count == n)
            return pow(2,k-1) * (pow(2,k) - 1);
        if (smarterSum(m) == 1){
            count ++;
        }
        k++;
    }while(true);

    return -1;
}
```



```c++
STUDENT_TEST("Multiple time trials of findPerfects on increasing input sizes") {
   int smallest = 20000, largest = 160000;
   for (int size = smallest; size <= largest; size *= 2) {
       TIME_OPERATION(size, findPerfects(size));
   }
   EXPECT(!isPerfect(-6));
   EXPECT(!isPerfect(-5));
   EXPECT(!isPerfect(-4));
}

STUDENT_TEST("Multiple time trials of findPerfects on increasing input sizes") {
   int smallest = 20000, largest = 160000;
   for (int size = smallest; size <= largest; size *= 2) {
       TIME_OPERATION(size, findPerfectsSmarter(size));
   }
}

STUDENT_TEST("Confirm smarterSum is corrent"){
    EXPECT_EQUAL(smarterSum(25),6);
    EXPECT_EQUAL(smarterSum(100),divisorSum(100));
    EXPECT_EQUAL(smarterSum(-100),divisorSum(-100));
}

STUDENT_TEST("Confirm findNthPerfectEuclid is corrent"){
    EXPECT_EQUAL(findNthPerfectEuclid(1),1);
    EXPECT_EQUAL(findNthPerfectEuclid(3),28);
    EXPECT_EQUAL(findNthPerfectEuclid(5),8128);
    EXPECT_EQUAL(findNthPerfectEuclid(-1),-1);
    EXPECT_EQUAL(findNthPerfectEuclid(9),
                 2305843008139952128);
}

```



## soundex

```cpp
string lettersOnly(string s) {
    string result = "";
    for (int i = 0; i < s.length(); i++) {
        if (isalpha(s[i])) {
            result += s[i];
        }
    }
    return result;
}

/*保留第一个字母，后续用数字替换*/
string replaceToDigit(string s) {
    if(s == "")
        return "";
    string result = charToString(s[0]);
    for (int i = 1; i < s.length(); i++) {
        switch (tolower(s[i])){
        case 'a':case 'e':case 'i':case 'o':case 'u':case 'h':case 'w':case 'y':
            result += "0";
            break;
        case 'b':case 'f':case 'p':case 'v':
            result += "1";
            break;
        case 'c':case 'g': case 'j':case 'k':case 'q':case 's':case 'x':case 'z':
            result += "2";
            break;
        case 'd':case 't':
            result += "3";
            break;
        case 'l':
            result += "4";
            break;
        case 'm':case 'n':
            result += "5";
            break;
        case 'r':
            result += "6";
            break;
        default:
                break;
        }
    }
    return result;
}

/*去重*/
string coalesceDuplicateDigits(string s){
    if(s.empty())
        return "";
    string result = "";
    for (size_t i = 0 ;i < s.length(); ++i) {
        if (!isdigit(s[i]) || (isdigit(s[i]) && s[i] != s[i - 1])){ //第一个字母和重复队列的第一
            result.push_back(s[i]);
        }
    }
    return result;
}

/*
 * 此函数负责将第一个字母大写、去0，保持字符串大小为4
*/
string formatString(string s){
    if(s.empty())
        return "";
    string result = "";
    for (size_t i = 0 ;i < s.length(); ++i) {
        if (!isdigit(s[i]) ) {
            result.push_back(toupper(s[i]));
        }else if (s[i] != '0'){
            result.push_back(s[i]);
        }
    }
    if(result.length() > 4)
        result = result.substr(0,4);
    else {
        result = result + std::string(4 - result.length(), '0');
    }
    return result;
}

/* TODO: Replace this comment with a descriptive function
 * header comment.
 */
string soundex(string s) {
    /* TODO: Fill in this function. */
    return formatString(coalesceDuplicateDigits(replaceToDigit(lettersOnly(s)))) ;
}

/*
 * 构建姓名与soundex的哈希
   不能使用STL
*/
std::unordered_map<string, std::vector<std::string>> build_name_hash_map(Vector<std::string>& vec) {
    std::unordered_map<string, std::vector<std::string>> name_hash_map;
    for (const auto& s : vec) {
        // cout<<"this is s:"<< s<< endl;
        string Soundex = soundex(s);

        name_hash_map[Soundex].push_back(s);  // 向对应的向量中添加字符串
    }
    return name_hash_map;
}


/* TODO: Replace this comment with a descriptive function
 * header comment.
 */
void soundexSearch(string filepath) {
    // This provided code opens the specified file
    // and reads the lines into a vector of strings
    ifstream in;
    Vector<string> allNames;

    if (openFile(in, filepath)) {
        allNames = readLines(in);
    }
    cout << "Read file " << filepath << ", "
         << allNames.size() << " names found." << endl;

    // The names read from file are now stored in Vector allNames

    /* TODO: Fill in the remainder of this function. */
    std::unordered_map<string, std::vector<std::string>> name_hash = build_name_hash_map(allNames);
    while(true){
        cout << endl <<"Enter a surname (RETURN to quit): ";
        string s;
        cin >> s;
        if(s == "RETURN")
            break;
        string target = soundex(s);
        cout << endl <<"Soundex code is " << target << endl << "Matches from database :";
        for(int i =0; i< name_hash[target].size(); ++i){
            cout << "\""<< name_hash[target][i] << "\"" << " ";
        }


    }
}


```

