# Transpose Matrix Problem
Lot of problem we have alreay solved in mathematics and matrix is the most common problem in provious classes and still now. 
In this post i try to solve matrix transpose problem programmaticaly.so let try to solve this problem use python
programming language.

Example:

 -----------                       ---------
| 2 | 4 | 7 |                      | 2 | 3 |
 -----------  ----- Transpose -- > ---------
| 3 | 5 | 8 |					   | 4 | 5 |
 -----------                       ---------
                                   | 7 | 8 |                            
                                   ---------


 if list of list lenght are equil then use this below this method

transpose_table = [[2,4,7],[3,5,8]]
x = [list(i) for i in zip(*transpose_table)]
print(x)


You need to install numpy in order to import it 
Numpy transpose returns similar result when  
applied on 1D matrix

import numpy
matrix=[[1,2,3],[4,5,6]] 
print(matrix) 
print("\n") 
print(numpy.transpose(matrix))


######################### Custom transpose if all list are not equal ####################

m = [[1,2,3],[3,4],[5,6],[1],[],['',2]]
def custom_transpose(m):
	column_max = max([len(i) for i in m])
	modify_list = []
	for i in m:
		x = column_max-len(i)
		if x > 0:
			for add_value in range(x):
				i.append("")
		modify_list.append(i)
	t_list = [list(i) for i in zip(*modify_list)]
	return t_list

t_list = custom_transpose(m)
print(t_list)

