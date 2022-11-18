---
published: false
---
Algorithms. Something you'd learn during your CS degree, which I don't currently have. Which was a good reason to register for a Top Coder challenge creating a dual-pivot quick sort using Ruby. Since I'm also studying Ruby (on Rails), it was a good way to kill two birds with one stone. Learn an algorithm and also practice with a new language.

Learning the algorithm was the hard part. 

The Challenge Overview was:

- The idea of dual pivot quick sort is to take two pivots, one in the left end of the array and the second, in the right end of the array.
- The left pivot must be less than or equal to the right pivot, so we swap them if necessary.
- Then, we begin partitioning the array into three parts: in the first part, all elements will be less than the left pivot, in the second part all elements will be greater or equal to the left pivot and also will be less than or equal to the right pivot, and in the third part all elements will be greater than the right pivot. 
- Then, we shift the two pivots to their appropriate positions as we see in the below bar, and after that we begin quicksorting these three parts recursively, using this method.
    
Which sounds easy enough. If you understand Ruby already. My first couple of tries resulted in a final array of arrays. Luckily they were all sorted arrays within the array but it still wouldn't work properly. I caved and googled dual-pivot quicksort and came across [this article](https://www.geeksforgeeks.org/dual-pivot-quicksort/) which outlined the algorithm but using C.

After studying that for a bit and learning how variables/parameters were passed in Ruby (reference vs. value), I was able to write a functioning sorrting method.

I won the challenge and had some good feedback from it. I used my code comments as a document of my own understanding of what was going on
            which resulted in a whole lot of unnecessary comments. Cleaned them up but it'll be good to go back and reference at a later time when I go
            to study other algorithms. I also got in touch with one of the other entrants via a common Slack channel. After exchanging notes, his implementation was
            sooooo much cleaner and more "Ruby" than mine. It'll be another thing I reference when I look to write some quality Ruby code in the future.
        </p>
