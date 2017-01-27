/*
 * CS:APP Data Lab
 *
 * <Yulin Zhang 804483463>
 *
 * bits.c - Source file with your solutions to the Lab.
 *          This is the file you will hand in to your instructor.
 *
 * WARNING: Do not include the <stdio.h> header; it confuses the dlc
 * compiler. You can still use printf for debugging without including
 * <stdio.h>, although you might get a compiler warning. In general,
 * it's not good practice to ignore compiler warnings, but in this
 * case it's OK.
 */

#if 0
/*
 * Instructions to Students:
 *
 * STEP 1: Read the following instructions carefully.
 */

You will provide your solution to the Data Lab by
editing the collection of functions in this source file.

INTEGER CODING RULES:

  Replace the "return" statement in each function with one
  or more lines of C code that implements the function. Your code
  must conform to the following style:

  int Funct(arg1, arg2, ...) {
      /* brief description of how your implementation works */
      int var1 = Expr1;
      ...
      int varM = ExprM;

      varJ = ExprJ;
      ...
      varN = ExprN;
      return ExprR;
  }

  Each "Expr" is an expression using ONLY the following:
  1. Integer constants 0 through 255 (0xFF), inclusive. You are
      not allowed to use big constants such as 0xffffffff.
  2. Function arguments and local variables (no global variables).
  3. Unary integer operations ! ~
  4. Binary integer operations & ^ | + << >>

  Some of the problems restrict the set of allowed operators even further.
  Each "Expr" may consist of multiple operators. You are not restricted to
  one operator per line.

  You are expressly forbidden to:
  1. Use any control constructs such as if, do, while, for, switch, etc.
  2. Define or use any macros.
  3. Define any additional functions in this file.
  4. Call any functions.
  5. Use any other operations, such as &&, ||, -, or ?:
  6. Use any form of casting.
  7. Use any data type other than int.  This implies that you
     cannot use arrays, structs, or unions.


  You may assume that your machine:
  1. Uses 2s complement, 32-bit representations of integers.
  2. Performs right shifts arithmetically.
  3. Has unpredictable behavior when shifting an integer by more
     than the word size.

EXAMPLES OF ACCEPTABLE CODING STYLE:
  /*
   * pow2plus1 - returns 2^x + 1, where 0 <= x <= 31
   */
  int pow2plus1(int x) {
     /* exploit ability of shifts to compute powers of 2 */
     return (1 << x) + 1;
  }

  /*
   * pow2plus4 - returns 2^x + 4, where 0 <= x <= 31
   */
  int pow2plus4(int x) {
     /* exploit ability of shifts to compute powers of 2 */
     int result = (1 << x);
     result += 4;
     return result;
  }

FLOATING POINT CODING RULES

For the problems that require you to implent floating-point operations,
the coding rules are less strict.  You are allowed to use looping and
conditional control.  You are allowed to use both ints and unsigneds.
You can use arbitrary integer and unsigned constants.

You are expressly forbidden to:
  1. Define or use any macros.
  2. Define any additional functions in this file.
  3. Call any functions.
  4. Use any form of casting.
  5. Use any data type other than int or unsigned.  This means that you
     cannot use arrays, structs, or unions.
  6. Use any floating point data types, operations, or constants.


NOTES:
  1. Use the dlc (data lab checker) compiler (described in the handout) to
     check the legality of your solutions.
  2. Each function has a maximum number of operators (! ~ & ^ | + << >>)
     that you are allowed to use for your implementation of the function.
     The max operator count is checked by dlc. Note that '=' is not
     counted; you may use as many of these as you want without penalty.
  3. Use the btest test harness to check your functions for correctness.
  4. Use the BDD checker to formally verify your functions
  5. The maximum number of ops for each function is given in the
     header comment for each function. If there are any inconsistencies
     between the maximum ops in the writeup and in this file, consider
     this file the authoritative source.

/*
 * STEP 2: Modify the following functions according the coding rules.
 *
 *   IMPORTANT. TO AVOID GRADING SURPRISES:
 *   1. Use the dlc compiler to check that your solutions conform
 *      to the coding rules.
 *   2. Use the BDD checker to formally verify that your solutions produce
 *      the correct answers.
 */


#endif
/* howManyBits - return the minimum number of bits required to represent x in
 *             two's complement
 *  Examples: howManyBits(12) = 5
 *            howManyBits(298) = 10
 *            howManyBits(-5) = 4
 *            howManyBits(0)  = 1
 *            howManyBits(-1) = 1
 *            howManyBits(0x80000000) = 32
 *  Legal ops: ! ~ & ^ | + << >>
 *  Max ops: 90
 *  Rating: 4
 */
int howManyBits(int x) {
       /* first converts int into positive, then counts the bits using bit smear and bit count
	* adds 1 unless it is negative and is power of 2
	*/
       int a;
       int b;
       int L;
       int R;
       int S;
       int increment;
       int posneg = (x>>31) &1;
       int posnegc = ~posneg+1;
       int newx = (x^(x>>31)) + !!(x>>31);
       int pwrtwocheck = newx;
       
       int T = 0xFF << 8 | 0xFF;
       T = ~(T << 15 | T >> 1);
       
       newx |= newx >> 16;
       newx |= newx >> 8;
       newx |= newx >> 4;
       newx |= newx >> 2;
       newx |= newx >> 1;
      
       a = (0x55 << 8)|0x55;
       a = (a << 16)|a;
       b = ~a;
       L = ((newx&b) >> 1) & ~T;
       R = newx & a;
       S = L + R;
      
       a = (0x33 << 8) | 0x33;
       a = (a << 16)|a;
       b = ~a;
       L = ((S&b) >>2)& ~(T>>1);
       R = S&a;
       S = L+R;
       
       
       a = (0x0F << 8) | 0x0F;
       a = (a << 16) | a;
       b = ~a;
       L = ((S&b) >> 4)& ~(T>>3);
       R = (S&a);
       S = L+R;
       
       
       a = (0xFF << 16) | 0xFF;
       b = ~a;
       L = ((S&b) >> 8) & ~(T>>7);
       R = (S&a);
       S = L+R;
       
       
       a = (0xFF << 8) | 0xFF;
       b = ~a;
       L = ((S&b) >> 16) & ~(T>>15);
       R = (S&a);
       S = L+R;

       pwrtwocheck = pwrtwocheck & (pwrtwocheck+~0);
       increment = (~(!pwrtwocheck)+1);
       S += increment & posnegc;
       return S + 1;
       
}
/*
 * sm2tc - Convert from sign-magnitude to two's complement
 *   where the MSB is the sign bit
 *   Example: sm2tc(0x80000005) = -5.
 *   Legal ops: ! ~ & ^ | + << >>
 *   Max ops: 15
 *   Rating: 4
 */
int sm2tc(int x) {
  /* if negative, flip the magnitude and add one
   * if positive, return x
   */
  int a = x>>31;
  int b = 0xFF << 8| 0xFF;
  int y = x & (b << 15 | b >> 1);
  return (a^y)+ !!a;
}
/*
 * isNonNegative - return 1 if x >= 0, return 0 otherwise
 *   Example: isNonNegative(-1) = 0.  isNonNegative(0) = 1.
 *   Legal ops: ! ~ & ^ | + << >>
 *   Max ops: 6
 *   Rating: 3
 */
int isNonNegative(int x) {
  /*right shift all the way to get bitchain of 1s or 0s
   *return the not
   */
  return !(x>>31);
}

/*
 * rotateRight - Rotate x to the right by n
 *   Can assume that 0 <= n <= 31
 *   Examples: rotateRight(0x87654321,4) = 0x76543218
 *   Legal ops: ~ & ^ | + << >>
 *   Max ops: 25
 *   Rating: 3
 */
 int rotateRight(int x, int n) {
   /* bitmask the right side, bitmask the left side
    * shift the left to the right and vice versa
    *append 1 to the non significant bitspots
    *& the left and right together
    */
   int c;
   int d;
   int z = 0xFF << 8 | 0xFF;
   int T = ~(z<<15|z>>1);
   int negn = ~n+1;
   int negn1 = 31+negn;
   int b = x & (~(T >> (negn1)));
   b = b << (32 + negn);
   b = b|~((T>>n)<<1);
   c = x&(T>>(negn1));
   c = c>>n;
   d = (T>>n)<<1;
   c = c|d;
   return b&c;
}
/*
 * divpwr2 - Compute x/(2^n), for 0 <= n <= 30
 *  Round toward zero
 *   Examples: divpwr2(15,1) = 7, divpwr2(-33,4) = -2
 *   Legal ops: ! ~ & ^ | + << >>
 *   Max ops: 15
 *   Rating: 2
 */
int divpwr2(int x, int n) {
  /* calculate (2^n -1)
   * add it to x if x is negative
   * shift right to dive by power of 2
   */
  int posneg = x>>31;
  int z = (1<<n) + ~0;
  int add = z & posneg;
  return (x + add) >> n;
}
/*
 * allOddBits - return 1 if all odd-numbered bits in word set to 1
 *   Examples allOddBits(0xFFFFFFFD) = 0, allOddBits(0xAAAAAAAA) = 1
 *   Legal ops: ! ~ & ^ | + << >>
 *   Max ops: 12
 *   Rating: 2
 */
int allOddBits(int x) {
  /* create mask
   * or it with x then retun 1 if odds were 1, else 0
   */
  int a = (0x55<<8)|0x55;
  int b = (a << 16)|a;
  return !(~(b|x));
}
/*
 * bitXor - x^y using only ~ and &
 *   Example: bitXor(4, 5) = 1
 *   Legal ops: ~ &
 *   Max ops: 14
 *   Rating: 1
 */
int bitXor(int x, int y) {
  /*invert x and & with y
   *invert y and & with x
   *invert both and then & together
   *invert again to get answer
   */
  return ~(~(~x&y)&~(~y&x));
}
/*
 * isTmin - returns 1 if x is the minimum, two's complement number,
 *     and 0 otherwise
 *   Legal ops: ! ~ & ^ | +
 *   Max ops: 10
 *   Rating: 1
 */
int isTmin(int x) {
  /*add by itself to create overflow and truncation
   *this will create bitchain of 0, invert to return 1
   *if x was zero, return 0;
   */
  return !(x+x)^!x;
}
