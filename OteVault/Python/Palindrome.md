def palindrome(string):
	string = string.lower().replace(' ','')
	return string == string[::-1]

This code takes a string, removes its spaces, and checks if our string equals the reverse of the string

TO MAKE A PALINDROME "FIXER":

Use two pointers, one at the start, one at the end.
As long as they are matching, then we are good.
At the mid section: I thought of it as the middle character being "special", hence count should return 1 but thats wrong. It could be an occurring letter elsewhere in the string. 


We begin here: 
def possiblePalinByRemovingOneChar(string: str) -> int:

    low = 0

    high = len(string) -1

  

    while  low < high:

        if string[low] == string[high]:

            low+=1

            high-=1

        else:

            if isPalindrome(string, low + 1, high):

                return low

            if isPalindrome(string, low, high - 1):

                return high

            return -1
      return -2

we begin with low = 0, and , supposing our string is "salalams" , we got len(string) - 1 = 7 which is final position at our string
if 0 is smaller than 7, which it is:
	if string[0] which equals letter "s", is the same as string[7], which also equals the letter "s":
	 low goes up by one.
	 high goes down by one.
	 hence, low =1 , high = 6 . here we have "a" compared to "m"
	 So, they do not equal each other.
	 We call the isPalindrome function:
	 if isPalindrome (string, low+1, high):
		
	 
	 def isPalindrome(string: str, low: int, high:int) -> bool:

		    while low < high:
		
		        if string[low] != string[high]:
		
		            return False
		
		        low += 1
		
		        high -=1
		
		    return True

The function takes our string, our low, and our high, and returns bool
Low at this time = 2 since we called for low+1. High at this time = 6
string[low]. salalams. s is 0, a is 1, l is 2. so, [low] = "l", and [high] = "m".
they dont equal each other. we get "false".

We move in to the second execution of isPalindrome.
isPalindrome(string, low, high-1)
We have: low = 1, high is this time = 5
salalams. s is 0, a =1. so [low] = "a".
l is 2, a is 3 , l is 4, a is 5. 
so, [high] equals a as well
Its a match, so loop proceeds

low+=1 makes low a 2
high-=1 makes high a 4
[low] = l
[high] = l
its a match. loop continues
low is now a 3
high is also a 3
loop stops. we return True

we go back to our program

            if isPalindrome(string, low + 1, high):

                return low

            if isPalindrome(string, low, high - 1):

                return high

            return -1


so, the second of these two isPalindrome's with high -1, has returned True. This means, we return the variable high, but of possiblePalinByRemovingOneChar, NOT the one inside isPalindrome.
in this case, high = 6, which means : salalams.  starting from the end, s is 7, and m is 6. that means [high ] = m, which, indeed, is the character that we need to remove if we want to make our word palindromic. 
Now we move on to our main():

if __name__=="__main__":

    string = "salalams"

    idx = possiblePalinByRemovingOneChar(string)

    if idx == -1:

        print("Heck, hell na")

    elif idx==-2:

        print("Cream gravy, no removals even needed!")

    else:

        print("Wooo wee, makin bacon. Succesful with removal at index", idx)



The print we get here is "Woo wee, makin bacon, Succesful with removal at index 6",
since we didn't get -1, and neither did we get -2.





## IF OUR STRING IS A PALINDROME ALREADY


   low = 0

    high = len(string) -1

  

    while  low < high:

        if string[low] == string[high]:

            low+=1

            high-=1

        else:

            if isPalindrome(string, low + 1, high):

                return low

            if isPalindrome(string, low, high - 1):

                return high
          return -1
    return -2

See, here we will never go into the elses, since in every case, the strings will equal each other. low will go through its entire section, and high will do the same. at some point, low < high will stop being true, so the loop will break. return -1 happens only if neither isPalindrome equals True, so that means we can't fix the string by removing a single character. It's just not a Palindrome at that point.
However, if string [low] equals string[high] all the way till the while low < high loop goes, then we return -2. Which means, no fixing is required.



