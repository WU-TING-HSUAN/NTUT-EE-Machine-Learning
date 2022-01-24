import numpy as np
import pandas as pd
import matplotlib.pyplot as plt
import csv
from sklearn.metrics import mean_squared_error
from sklearn.datasets import load_boston
name=["Apple","Bread","Butter","Cheese","Corn","Dill","Eggs","Ice cream","Kidney Beans","Milk","Nutmeg","Onion","Sugar","Unicorn","Yogurt","chocolate"]
dataset = pd.read_csv('apriori_train.csv',encoding=' big5')
rows = dataset.iloc[:].values
column, row =len(rows),len(rows[0])-1
array2D = [[0 for _ in range(row)] for _ in range(column)]
array2D=np.array(array2D)

for i in range(0,len(rows)):
    for j in range(1,len(rows[0]-1)):
        if(rows[i,j] == True):
            array2D[i,j-1]=1
#資料預處理

support_count = 0.03*1000
confidence = 0.7

#k=1
count_1=[]
first_del=[]
for i in range(0,len(rows[0])-1):
    c=0
    for j in range(0,len(rows)):
        if(array2D[j][i]==1):
            c+=1
    count_1.append(c)

for i in range(0,len(count_1)):
    print(name[i],"count:",count_1[i])
    
for i in range(0,len(count_1)):
    if(count_1[i]<=support_count):
        first_del.append(name[i])
name_count_1={}
for i in range(0,len(name)):
    name_count_1[name[i]]=count_1[i]
    
from itertools import combinations
ans=[]
flag=0
for i in range(2,len(rows[0])):
    com = list(combinations(name,i))
    for j in com:
        flag = 1
        for x in first_del:
            
            if(x in j):
                flag = 0
                break
            else:
                flag = 1
        if(flag==1):
            ans.append(j)
for i in ans:
    print(i)
    
count = 0 
name_label=[0,1,2,3,4,5,6,7,8,9,10,11,12,13,14,15]
name_count = np.zeros(len(ans), dtype=int)
max_count = 0
name_dic={}
for i in ans:
    step=[]
    for j in i:
        if(j in name):
            step.append(name.index(j))
    for num,j in enumerate(array2D):
        flag=0
        for k in step:
            if(j[k]!=1):
                flag=1
        if(flag!=1):
#             print(num)
            name_count[count]+=1
#             print(name_label)
    count+=1
finial_ans=[]
finial_count=[]
for i in range(0,len(ans)):
    if(name_count[i]>=support_count):
        finial_ans.append(ans[i])
        finial_count.append(name_count[i])
for i in range(0,len(finial_ans)):
    name_dic[finial_ans[i]] = finial_count[i]
    print(finial_ans[i],"count",":",finial_count[i])
    if(len(finial_ans[i])>max_count):
        max_count=len(finial_ans[i])
 item_set=[]
subset=[]
cofidence=[]

for i in range(0,len(finial_ans)):
    for j in finial_ans[i]:
        a=finial_count[i]/name_count_1[j]
        if(a>=confidence):
            print(finial_ans[i],"子集 : ",j,"confidence : ",a)
            item_set.append(finial_ans[i])
            subset.append(j)
            cofidence.append(a)
#         else:
#             print(finial_ans[i],"子集 : ",j,"的cofidence : ",a)
for i in range(0,len(finial_ans)):
    for j in range(2,max_count):
        finial_com = list(combinations(finial_ans[i],j))
        if(len(finial_com)>=2):
            for j in finial_com:
                a=int(name_dic[j])
                if(finial_count[i]/a>=confidence):
                    print(finial_ans[i],"子集 : ",j,"confidence : ",finial_count[i]/a)
                    item_set.append(finial_ans[i])
                    subset.append(j)
                    cofidence.append(finial_count[i]/a)
#                 else:
#                     print("項目 : ",finial_ans[i],"子集 : ",j,"cofidence : ",finial_count[i]/a)
