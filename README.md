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
