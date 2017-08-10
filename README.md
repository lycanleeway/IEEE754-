# IEEE754
HEX 8 Bytes to Double


/// 2017 .08 .10
// IEEE754.cpp : Defines the entry point for the console application.
//

#include "stdafx.h"
#include <stdio.h>
#include <iostream>
#include <math.h>
using namespace std;

double IEEE754(int a, int b, int c,int d,int e,int f,int g,int h)
{
	int sum[64];
	//////   abcdefgh → hgfedcba    h:0-7
	for (int i = 0; i <8 ; i++)
	{
		sum[7-i] = h % 2;
		h/= 2;
	}
	//////   abcdefgh → hgfedcba    g:8-15
	for (int i = 0; i <8; i++)
	{
		sum[15 - i] = g % 2;
		g /= 2;
	}

	//////   abcdefgh → hgfedcba    f:16-23
	for (int i = 0; i <8; i++)
	{
		sum[23 - i] = f % 2;
		f /= 2;
	}

	//////   abcdefgh → hgfedcba    e:24-31
	for (int i = 0; i <8; i++)
	{
		sum[31 - i] = e % 2;
		e /= 2;
	}

	//////   abcdefgh → hgfedcba    d:32-39
	for (int i = 0; i <8; i++)
	{
		sum[39 - i] = d% 2;
		d /= 2;
	}

	//////   abcdefgh → hgfedcba    c:40-47
	for (int i = 0; i <8; i++)
	{
		sum[47 - i] = c % 2;
		c /= 2;
	}

	//////   abcdefgh → hgfedcba    b:48-55
	for (int i = 0; i <8; i++)
	{
		sum[55 - i] = b % 2;
		b /= 2;
	}

	//////   abcdefgh → hgfedcba    a:56-63
	for (int i = 0; i <8; i++)
	{
		sum[63 - i] = a % 2;
		a /= 2;
	}

	////// IEEE754 64位双精度转换
	int S = sum[0];  //  指符号位S
	int E = sum[1] * 1024 + sum[2] * 512 + sum[3] * 256 + sum[4] * 128 + sum[5] * 64 + sum[6] * 32 + sum[7] * 16 + sum[8] * 8 + sum[9] * 4 + sum[10] * 2 + sum[11] * 1;  // 指含阶符的阶码E
	///////52位 代指尾数M  (1.Ｍ)
	double M = 1 * pow(2, 52);
		for (int k = 0; k < 52; k++)
		{
			M = M + sum[12 + k] * pow(2, 51 - k);
		}
		M = M / (pow(2, 52));

		double X;
		X = pow(-1, S) * M * pow(2, (E - 1023));

		return X;

}





int main()
{
	int a, b, c, d, e, f, g, h;
	double X;
	printf("input 8 bytes\n");
	scanf("%x,%x,%x,%x,%x,%x,%x,%x",&a, &b, &c, &d, &e, &f, &g, &h);
	X = IEEE754(a, b, c, d, e, f, g, h);
	printf("%.11f",X);

    return 0;
}

