# WILD-CARD-REPLACEMENT

import sys

sys.setrecursionlimit(10**8)

t=int(input())

for i in range(t):

    s=input()
    
    list1={}
    
    def wildcardreplace(L,s):
    
        ind,longg,shor,symb=L+1,0,0,True
        
        while s[ind]!=')':
        
            C=s[ind]
            
            if C=='?':
            
                if symb:
                
                    longg+=1 
                    
                else:
                
                    shor+=1 
                    
            elif C=='+' : 
            
                symb=True
                
            elif C=='-' : 
            
                symb=False
                
            elif C=='(':
            
                a=wildcardreplace(ind,s)
                
                if symb:
                
                    longg+=a[0]
                    
                    shor+=a[1]
                    
                else:
                
                    longg+=a[1]
                    
                    shor+=a[0]
                    
                ind=a[2]
                
            ind+=1
            
        list1[L]=longg
        
        return [longg,shor,ind]
        
    wildcardreplace(0,s)
    
    Q=int(input())
    
    li=[]
    
    for i in range(Q):
    
        L,R=map(int,input().split())
        
        if L==R:
        
            li.append(1)
            
        else:
        
            li.append(list1[L-1])
            
    print(*li)
