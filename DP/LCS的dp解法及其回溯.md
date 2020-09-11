```C++
#include<iostream>
#include<algorithm>
#include<string>
#include<stack>
#include<vector>
#include<cstdio>
#include<cstring>
using namespace std;

const int maxn = 2000;//兼容的最长字符串长度
char a[maxn],b[maxn];
int len1,len2;
string ans;
int dp[maxn][maxn];

int LCS(int x,int y){//dp核心函数
    if(x<0 || y<0)return 0;
    if(dp[x][y]!=-1)return dp[x][y];
    dp[x][y] = (a[x]==b[y])? (1+LCS(x-1,y-1)) : max(LCS(x-1,y),LCS(x,y-1));
    return dp[x][y];//从后向前依次对比并记忆相应结果-记忆化搜索
}

int BackTrace(){//回溯核心函数
    int x = len1 - 1;
    int y = len2 - 1;
    ans="";
    //再仿照dp思路第二次进行遍历
    while(x>=0 && y>=0){
        if(a[x]==b[y]){
            ans += a[x];
            x--;y--;
        }else{
            if(dp[x-1][y] > dp[x][y-1])x--;
            else y--;
        }
    }
    //回溯后对字符串反转才是答案
    reverse(ans.begin(),ans.end());
    return 0;
}

//上面两个核心函数其实思维角度是一致的

int main(){
    //初始化
    memset(a,0,sizeof(a));
    memset(b,0,sizeof(b));
    scanf("%s %s",a,b);
    len1 = strlen(a);
    len2 = strlen(b);
    memset(dp,-1,sizeof(dp));
    //LCS检测
    LCS(len1-1,len2-1);
    //回溯
    BackTrace();
    //输出答案
    cout<<ans<<endl;
    return 0;
}
```
