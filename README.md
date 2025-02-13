# CMPS 2200  Recitation 02

**Name (Team Member 1):**Zev Gaslin  
**Name (Team Member 2):**Josh Haddad

In this recitation, we will investigate recurrences. 
To complete this recitation, follow the instructions in this document. Some of your answers will go in this file, and others will require you to edit `main.py`.



## Running and testing your code
- To run tests, from the command-line shell, you can run
  + `pytest test_main.py` will run all tests
  + `pytest test_main.py::test_one` will just run `test_one`
  + We recommend running one test at a time as you are debugging.

## Turning in your work

- Once complete, click on the "Git" icon in the left pane on repl.it.
- Enter a commit message in the "what did you change?" text box
- Click "commit and push." This will push your code to your github repository.
- Although you are working as a team, please have each team member submit the same code to their repository. One person can copy the code to their repl.it and submit it from there.

## Recurrences

In class, we've started looking at recurrences and how to we can establish asymptotic bounds on their values as a function of $n$. In this lab, we'll write some code to generate recursion trees (via a recursive function) for certain kinds of recurrences. By summing up nodes in the recurrence tree (that represent contributions to the recurrence) we can compare their total cost against the corresponding asymptotic bounds. We'll focus on  recurrences of the form:

$$ W(n) = aW(n/b) + f(n) $$

where $W(1) = 1$.

- [ ] 1. (2 point) In `main.py`, you have stub code which includes a function `simple_work_calc`. Implement this function to return the value of $W(n)$ for arbitrary values of $a$ and $b$ with $f(n)=n$.

- [ ] 2. (2 point) Test that your function is correct by calling from the command-line `pytest test_main.py::test_simple_work` by completing the test cases and adding 3 additional ones.

- [ ] 3. (2 point) Now implement `work_calc`, which generalizes the above so that we can now input $a$, $b$ and a *function* $f(n)$ as arguments. Test this code by completing the test cases in `test_work` and adding 3 more cases.

- [ ] 4. (2 point) Now, derive the asymptotic behavior of $W(n)$ using $f(n) = 1$, $f(n) = \log n$ and $f(n) = n$. Then, generate actual values for $W(n)$ for your code and confirm that the trends match your derivations.

**TODO: your answer goes here**
f(n) = 1
We can derive asymptotic behavior by assuminging values of a=1 and b=2. Because f(n)=1 d=0 and logb(a)=0 and 0=0 we can determine the asymptoic behavior of this function to be T(n) = theta(n^dlog(n)). This agrees with our code which states work_calc(30000, 1, 2, lambda n: 1) == 19 for the very large value 300000. The value (300000^0)log(300000) is approximately equal to 19 which proves our result.

f(n) = log(n)
We can derive asymptotic behavior by assuminging values of a=1 and b=2. Because f(n)=log(n) d<0 and logb(a)=2 and (a number greater than 0)>=0 we can determine the asymptoic behavior of this function to be T(n) = n^d. d then has to be calculated by solving n^d=log_2(n) for d. doing this we get d= ln(log(n))/ln(n). This gives us a time complexity of 0(n) which roughly agrees with our function.

f(n) = n
accroding to the master theroem, a = 2, b = 2, f = n. T(n) = a*T(n/2) + n^d, where n^d = f(n). f(n) = n so d = 1. becase d >0, T(n) = n^d, or n^1 which = n. So the work function is n
depth = log_2(n); 
work = nlogn
this means that the output should be nlogn, so when the input is 1000 the output should be 9965.

- [ ] 5. (4 points) Now that you have a nice way to empirically generate valuess of $W(n)$, we can look at the relationship between $a$, $b$, and $f(n)$. Suppose that $f(n) = n^c$. What is the asypmptotic behavior of $W(n)$ if $c < \log_b a$? What about $c > \log_b a$? And if they are equal? Modify `test_compare_work` to compare empirical values for different work functions (at several different values of $n$) to justify your answer. 

**TODO: your answer goes here**
If c < \log_b a
    Root Dominated:  Asymptotic behavior is theta(n^(logb a))
if c > \log_b a
    Leaf Dominated: Asymptotic behavior is theta(n^c)
if c = \log_b a  
Balacnced: Asymptotic behavior is theta(n^(log b a) log(n))

- [ ] 6. (3 points) $W(n)$ is meant to represent the running time of some recursive algorithm. Suppose we always had $a$ processors available to us and we wanted to compute the span of the same algorithm. Implement the function `span_calc` to compute the empirical span, where the work of the algorithm is given by $W(n)$. Implement `test_compare_span` to create a new comparison function for comparing span functions. Derive the asymptotic expressions for the span of the recurrences you used in problem 4 above. Confirm that everything matches up as it should. 

**TODO: your answer goes here**
for f(n) = 1, span = s(n/2) +1 = a series which when evaluated becomes log(n) so the span is log(n)

for f(n) = log(n) the span s(n/2) + log(n). evaluating the s(n/2) series again becomes log(n), so the span is log(n)^2

for f(n) = n, the span s(n/2) + n becomes the series n + n/2 + n/3 + ... whihc when evaluated becomes an experesion witht he hihgest power bieng n, so the span is n