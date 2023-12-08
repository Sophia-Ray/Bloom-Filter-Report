Sophia Ray

CS 130A

November 17, 2023

Bloom Filter Report

	In this report, I will demonstrate how I set up two different types of hash functions that will be used to implement a bloom filter using the C++ language. I will run a series of tests to answer questions about the efficiency of each type of function, data sets they may perform better in, and their strengths and weaknesses when used to implement a bloom filter. For this project, I fixed the size of the universe, N,  to be 10<sup>10   </sup>and the number of items in the subset, n, to be 100,000. I also fixed a prime number p to be  2<sup>35</sup>-1 using a Mersenne prime algorithm.

	The first part of this project was to create two different types of hash functions. The first function I implemented, called hashFunc1, fixed k seeds at the start of the program, and then used a random number generated from that. The second hash function I created, called hashFunc2, used a uniform random a and b, as well as prime p and the size of the hash table m to generate a mapped value. 

	For testing these functions, I set the number of hash functions, k, to be 5, and let the hash table size be 100,000. I began by looping through 1000 values of x, and each function is ran k times per x value, so I received 5000 mapped values. For each function, I also ran two different types of data. On each function, I looped through values 0-1000, and also randomized values up to m. My goal was to determine if randomized 

values or consecutive values create different results.
[first screenshot](images/screenshot 1.png)
Both of these graphs look nearly identical to one another, so I concluded that data choice did not matter for either function 1 and 2, and each function produced values that hit uniformly all over the plot. I also ran another test to determine if one function produces more collisions than the other 


[first screenshot](images/screenshot 2.png)
 function. I added a counter to each loop that incremented whenever a mapped value already existed. I repeated this with both types of data for each function 10 times and concluded that they all have similar median values besides the randomized values for hash function 2. The randomized values for hash function 2 produced a median of 2177 (with k=5 and c=10), and the other 3 types had medians of 120, 111, and 121. I repeated this experiment with both smaller k values and larger k values, and learned that as the k value increases, so does the number of collisions, and that changing the c value did not affect the collision numbers. I also noted that the range of both types of data in function 2 varied significantly more than in hash function 1. The ranges for function 1 were 38 and 33, whereas function 2 had ranges of 945 and 592, indicating a much higher appearance of outliers.

	Overall, both hash functions behave efficiently and produce similar results to one another, however if using random data, it may be better to implement hash function 1 rather than hash function 2.

	Part 2 of this report is to implement the actual bloom filter. It was extremely simple to implement and very efficient. I used the bitset data structure as my container for the bloom filter because I am able to fix the size of the array at the beginning since I know m. I created one insert function and one query function for each type of hash function, and I just followed the lecture code for designing it.

	Once the bloom filter was implemented, I was able to begin part 3 of this project and analyze the false positive rates. I determined the false positive rate by inserting values from 0 to n into the bloom filter, then doing 10000 queries on random numbers that are outside of this range. Since I know that all 10000 values should not be in the bloom filter, I kept count of each true I received and divided by 10000 to find the rate. My first collection of data was done by fixing c=10 and changing the k value. I did this 10 times for each k value for function 1 and found the median, and I did this 30 times for each k value for function 2. I had to collect much more data for function 2 because of the wide range I described earlier in part 1 of this report. Only taking 10 values caused my data to be more random and unpredictable for function 2, so I had to increase that to see the larger trend.


[first screenshot](images/screenshot 3.png)
	

I was able to plot the theoretical values by plugging in each k and c into the theoretical function derived in lecture. I got the theoretical optimal k value from using k = cln2 as derived from lecture also. This data shows that function 1 follows the theoretical function pretty closely, whereas the second hash function has more optimal results. Hash function 2 has a similar shape to the theoretical function (maybe an outlier at/after k=10), yet its false positive rates are significantly lower. For both functions, the theoretical k value was close to what would be expected.

[first screenshot](images/screenshot 4.png)

	I also plotted each function when c=15 to see if anything changes.

The shape of function 1 is similar to the previous graph, being a similar type of curve and close to the expected false positive rate. Hash function 2 is a lot less curve-like in this graph because the variability of the values were much higher compared to the other function. If this experiment was done taking more values, like 1000, then this graph would become more curved and less steep. Although the shape is slightly different then before, we are still seeing the false positive rates be largely under the theoretical rates like shown before. Also, the optimal k value seems to be accurate to the functions as well.

	Overall, I conclude that both of these functions are suitable for implementing a bloom filter, yet they both have their strengths and weaknesses. Hash function 1 followed closely to the theoretical function and showed very little variability throughout the entire experiment, thus this function is extremely stable and consistent in its data. On the other hand, hash function 2 has been more unpredictable in its results and has many, many outliers, yet the false positive rates are consistently low in comparison to the first function, making its false positive ratio reliable.
