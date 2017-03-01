# PrataC-

#pragma once
#include <iostream>
	
class Complex
{
private:
	double real;
	double imag;

public:
	Complex();
	Complex(double r, double i);
	~Complex();
	Complex operator+(const Complex &s)const;
	Complex operator-(const Complex &s)const;
	Complex operator*(const Complex &s)const;	
	friend Complex operator*(double s, const Complex &a);
	friend std::ostream & operator<<(std::ostream &os, const Complex &c);
	friend std::istream & operator>>(std::istream &is, Complex &s);
};

#include "Complex.h"



Complex::Complex()
{
	real = imag = 0;
}

Complex::Complex(double r, double i)
{
	real = r;
	imag = i;
}

Complex::~Complex()
{
}

Complex Complex::operator+(const Complex &s)const {
	return Complex(real + s.real, imag + s.imag);
}

Complex Complex::operator-(const Complex &s)const {
	return Complex(real - s.real, imag - s.imag);
}

Complex Complex::operator*(const Complex &s)const {
	return Complex(real*s.real - imag*s.imag, real*s.imag + imag*s.real);
}

Complex operator*(double s, const Complex &a) {
	Complex sec(s,0);
	return sec*a;
}

std::istream & operator>>(std::istream &is, Complex &s) {
	
	is >> s.real >> s.imag;
		return is;

}

std::ostream & operator<<(std::ostream &os, const Complex &c) {
	os << "Reel kisim: " << c.real << "Sanal kisim: " << c.imag << std::endl;
	return os;
}

#include "Complex.h"

int main() {

	Complex a(3.0, 4.0);

	Complex c;

	std::cout << "Enter a complex number (q to quit): ";
	
	while (std::cin >> c)
	{
		std::cout << "c is " << c << '\n';
		std::cout << "Complex conjugate is " << ~c << '\n';
		std::cout << "a is " << a << '\n';
		std::cout << "a + c is " << a + c << '\n';
		std::cout << "a * c is " << a * c << '\n';
		std::cout << "2 * c is " << 2 * c << '\n';
		std::cout << "Enter new complex number: ";
	}

	std::cout << "Bye" << std::endl;

	return 0;
}

#include <cstring> // string.h for some
#include "String.h"

using std::cin;
using std::cout;
// initializing static class member
int String::num_strings = 0;
// static method
int String::HowMany()
{
	return num_strings;
}
// class methods
String::String(const char * s) // construct String from C string
{
	len = std::strlen(s); // set size
	str = new char[len + 1]; // allot storage
	std::strcpy(str, s); // initialize pointer
	num_strings++; // set object count
}
String::String() // default constructor
{
	len = 4;
	str = new char[1];
	str[0] = '\0'; // default string
	num_strings++;
}
String::String(const String & st)
{
	num_strings++; // handle static member update
	len = st.len; // same length
	str = new char[len + 1]; // allot space
	std::strcpy(str, st.str); // copy string to new location
}
String::~String() // necessary destructor
{
	--num_strings; // required
	delete[] str; // required
}
// overloaded operator methods
// assign a String to a String

String & String::operator=(const String & st)
{
	if (this == &st)
		return *this;
	delete[] str;
	len = st.len;
	str = new char[len + 1];
	std::strcpy(str, st.str);
	return *this;
}
// assign a C string to a String
String & String::operator=(const char * s)
{
	delete[] str;
	len = std::strlen(s);
	str = new char[len + 1];
	std::strcpy(str, s);
	return *this;
}
// read-write char access for non-const String
char & String::operator[](int i)
{
	return str[i];
}
// read-only char access for const String
const char & String::operator[](int i) const
{
	return str[i];
}
// overloaded operator friends
bool operator<(const String &st1, const String &st2)
{
	return (std::strcmp(st1.str, st2.str) < 0);
}
bool operator>(const String &st1, const String &st2)
{
	return st2 < st1;
}
bool operator==(const String &st1, const String &st2)
{
	return (std::strcmp(st1.str, st2.str) == 0);
}
char * operator+(const String &st1, const String &st2){
	int len = st1.len + st2.len;
	char * newstr = new char[len + 1];
	std::strcpy(newstr,st1.str);
	std::strcat(newstr, st2.str);
	return newstr;
}
char * operator+(const char *st1, const String &st2) {
	return String(st1) + st2;
}

// simple String output
ostream & operator<<(ostream & os, const String & st)
{
	os << st.str;
	return os;
}
// quick and dirty String input
istream & operator >> (istream & is, String & st)
{
	char temp[String::CINLIM];
	is.get(temp, String::CINLIM);
	if (is)
		st = temp;
	while (is && is.get() != '\n')
		continue;
	return is;
}
////////////////////////////////////////////////////////////////////////////////
#pragma once

#include <iostream>
#include <valarray>
#include <string>

typedef std::valarray<int> ArrayInt;
typedef Pair<ArrayInt, ArrayInt> PairArray;

template <class T1, class T2>
class Pair
{
private:
	T1 a;
	T2 b;
public:
	T1 & first();
	T2 & second();
	T1 first() const { return a; }
	T2 second() const { return b; }
	Pair(const T1 & aval, const T2 & bval) : a(aval), b(bval) { }
	Pair() {}
};
template <PairArray V, PairArray N>
class Wine
{
private:
	std::string label;
	ArrayInt vint_year;
	ArrayInt num_bottles;
public:
	PairArray(vint_year, num_bottles);
	Wine();
	~Wine();
	Wine(const char * l, int y, const int yr[], const int bot[]);
	Wine(const char * l, int y);
};
