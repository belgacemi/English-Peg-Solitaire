# English-Peg-Solitaire
In this project we want to find solutions for solvable peg solitaire games.

The english version contains 33 cells. The goal is to find if there is a series of legal jumps that allows us to get from an initial configuration to a final configuration. </br>
</br>
                          ![Texte alternatif…](http://www.home.hs-karlsruhe.de/~pach0003/informatik_1/aufgaben/solitaer.jpg)
                         
As explained in the scientific article written by Masashi KIYOMI, Tomomi MATSUI from the university of Tokyo ( http://www.kurims.kyoto-u.ac.jp/~kyodo/kokyuroku/contents/pdf/1185-11.pdf) , the peg solitaire can be modeled by the following Mixed Integer Program : 
</br>
                            ![alt text](https://github.com/belgacemi/English-Peg-Solitaire/blob/master/images/IP1.jpg)

</br>
However solving this problem can take a lot of time, so we chose to implement the second method proposed by Kiomi and Matsui, which is based on a back-tracking search Algorithm. (see the solvprog function) </br>
In order to prune the search space we used two different methods: 
1.    First of all, it's proven that there is an upper bound for how many times each jump j is used in the path to get from the intial to the final configuration. 
This upper band is the solution for the following MIP: 
</br>

   ![alt text](https://github.com/belgacemi/English-Peg-Solitaire/blob/master/images/IP2.jpg)
</br>
We have used the solutions for this MIP (saved in an array) to prune the search space. 
If RUBj is unfeasible, the peg solitaire problem with the given intial and final configuration doesn't have any solution
2.  We have also used  a hash table where we have stored every configuartion of the cells that have shown to lead to no solution in order to speed up the backtracking algorithm .(see sansissue and solvprog functions).

</br>
We have chosen two ways to represent every configuration of the cells : the first one using a pandas dataframe (which is more pleasent visually) and the second one is an array. The cells are represented in this array in a logical order starting from the upper left of the game. Empty cells are represented by 0, the other ones are represented by the value one. </br>
We have used to solve the MIP RUBj the OR-tools developped by Google. (see the solving function)
