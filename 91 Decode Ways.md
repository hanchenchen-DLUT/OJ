# 91 Decode Ways

1. 从后往前遍历。

2. 如果s[n]=0，那么s[n]到s[end]的decode ways =0：

3. 如果s[n]能够和s[n+1]组成1～26之间的数字，那么s[n]到s[end]的decode ways =：

   s[n]、（s[n+1]]到s[end]的decode ways）

4. 如果s[n]能够和s[n+1]组成1～26之间的数字，那么s[n]到s[end]的decode ways =：

   s[n]s[n+1]、（s[n+2]到s[end]的decode ways ）//用b记录+

   s[n]、（s[n+1]]到s[end]的decode ways）//用a记录

   将s[n]到s[end]的decode ways数量赋值给a

5. 例	

   | s    | 2    | 6    | 3    | 2    | 2    | 0    | 3    | 1    | 4    |
   | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- |
   | a    |      |      |      |      |      |      |      | 2    |      |
   | b    |      |      |      |      |      |      |      |      | 1    |

   | s    | 2    | 6    | 3    | 2    | 2    | 0    | 3    | 1    | 4    |
   | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- |
   | a    |      |      |      |      |      |      | 2    |      |      |
   | b    |      |      |      |      |      |      |      | 2    |      |

   | s    | 2    | 6    | 3    | 2    | 2    | 0    | 3    | 1    | 4    |
   | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- |
   | a    |      |      |      |      |      | 0    |      |      |      |
   | b    |      |      |      |      |      |      | 2    |      |      |

   | s    | 2    | 6    | 3    | 2    | 2    | 0    | 3    | 1    | 4    |
   | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- |
   | a    |      |      |      |      | 2    |      |      |      |      |
   | b    |      |      |      |      |      | 0    |      |      |      |

   | s    | 2    | 6    | 3    | 2    | 2    | 0    | 3    | 1    | 4    |
   | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- |
   | a    |      |      |      | 2    |      |      |      |      |      |
   | b    |      |      |      |      | 2    |      |      |      |      |

   | s    | 2    | 6    | 3    | 2    | 2    | 0    | 3    | 1    | 4    |
   | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- |
   | a    |      |      | 2    |      |      |      |      |      |      |
   | b    |      |      |      | 2    |      |      |      |      |      |

   | s    | 2    | 6    | 3    | 2    | 2    | 0    | 3    | 1    | 4    |
   | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- |
   | a    |      | 2    |      |      |      |      |      |      |      |
   | b    |      |      | 2    |      |      |      |      |      |      |

   | s    | 2    | 6    | 3    | 2    | 2    | 0    | 3    | 1    | 4    |
   | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- |
   | a    | 4    |      |      |      |      |      |      |      |      |
   | b    |      | 2    |      |      |      |      |      |      |      |


6. 执行用时 :4 ms, 在所有 C++ 提交中击败了89.97%的用户

   内存消耗 :8.4 MB, 在所有 C++ 提交中击败了53.04%的用户

   ```c++
   class Solution {
   public:
       int numDecodings(string s) {
           int len=s.size();
           if(len==0||s[0]=='0')return 0;
           if(len==1)return 1;
           int a=0,b=0;
           if(s[len-1]!='0')b=1;
           if(s[len-2]=='1'||s[len-2]=='2'&&s[len-1]<='6')a=1+b;
           else if(s[len-2]=='0') a=0;
           else a=b;
           for(int i=len-3;i>=0;i--){
               //cout<<a<<endl;
               if(s[i]=='0'){
                   b=a;
                   a=0;
               }else if(s[i]=='1'||(s[i]=='2'&&s[i+1]<='6')){
                   a=a+b;
                   b=a-b;
               }else{
                   b=a;
               }
               if(a+b==0)return 0;
           }
           return a;
       }
   };
   ```

   

1. 超出时间限制*5
2. 解答错误*9