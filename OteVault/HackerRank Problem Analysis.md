### ZIG ZAG SEQUENCE
 - - - - - - - - - - - -
The problem:
We got an array like so: {1, 2, 3, 4 , 5, 6 , 7}
We need it to be like this:  {1, 2, 3, 7, 6, 5, 4}

This is called a Zig Zag Sequence.
This has to be scalable with even hundreds and thousands of numbers in an array.

First, we use sort() to sort the array in ascending order.
Then, we take the middle element of the array using int((n-1)/2)
We do n-1 , because we start counting from zero.
So if I have 16 elements, it'll do 16-1 = 15. from 0 to 15 thats 16 elements.
Then we divide by 2. That would mean 15/2 = 7.5
Because 7.5 is not a valid array index, with int(), we ensure that only
the integer part of the result is taken. so, int(7.5) equals 7.
Meaning, from an array of 16 elements ,we get mid=7

{1, 2, 3, 4, 5, 6, 7, 8, 9,10,11,12,13,14,15,16} 

a[mid]=8

then, we perform a[mid], a[n-1] = a[n-1], a[mid]

n=16 is the max length of the array
mid is position 7 counting from 0, position 7's value is 8
n-1= position 15 counting from 0, position 15's value is 16

a[mid] which equals 8, and a[n-1] which equals 16, will now swap

our new array is 
{1, 2, 3, 4, 5 ,6 ,7, 16, 9 , 10, 11, 12, 13, 14, 15, 8 }

we then declare:
st = mid + 1  //meaning, position 7 + 1 , equals position 8. One after mid
ed= n -2        //meaning, position 16 - 2, equals position 14. Two below array length, and one before the last element.

Then we do:

(while st <= ed):
	a[st], a[ed] = a[ed], a[st] 
	st = st + 1
	ed = ed - 1

The "while":
As long as position 8 is smaller than position 14:
Swap position 8 with position 14
Position 8's value is 9
Position 14's value is 15
9 is indeed smaller than OR equal to 15
So our new array is:
{1, 2, 3, 4, 5 ,6 ,7, 16, 15 ,10, 11, 12, 13, 14, 9, 8 }
Then, st increments by 1.
This means st that indicated position 8, now indicates position 9
Then also, et decreases by 1.
This means et that indicated position 14, now indicates position 13

The "while" will now check again:
is st smaller or equal to ed?
st indicates position 9.
et indicates position 13.
position 9's value? is 10
position 13's value? is 14
10 is indeed smaller than or equal to 14
This means, they will swap
Our new array is :
{1, 2, 3, 4, 5 ,6 ,7, 16, 15 , 14, 11, 12, 13, 10, 9, 8 }

Now to speed things up, since we see the pattern.
st + 1 = 9 + 1 = position 10
ed -1 = 13-1 = position 12
position 10 = value 11
position 12 = value 13

value 11 is smaller than 13
SWAP
New array:
{1, 2, 3, 4, 5 ,6 ,7, 16, 15 ,14, 13, 12, 11, 10, 9, 8 }
st + 1 = 10 + 1 = position 11
ed -1 = 12 -1 = position 11


both are the same position
so we are comparing value 12 to value 12
//I have run the same exact code with the same exact array in visual studio...
  It does not seem to execute itself further after this point. Probably
  because it tries to swap itself with itself and it does not decide to run further.

So our final array is this:

{1, 2, 3, 4, 5 ,6 ,7, 16, 15 ,14, 13, 12, 11, 10, 9, 8 }
And so, the zig-zag is complete.

Key Takeaways:

st is a pivot that starts +1 position ahead of mid, and moves in ascending order, finding the immediately smallest character on the right side of mid
ed is a pivot that starts -1 position below the last value, and moves in descending order,
finding the immediately largest character on the right side of mid
the two are compared so that they may be swapped. swapping the largest found with the smallest found, after the mid, is the way to sort these characters in a descending order from the middle of the array and after. Hence, achieving the ZigZag








