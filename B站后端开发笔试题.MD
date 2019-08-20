##第一题
<font size=5 color=green>
英文句子单词翻转</br>
题目描述：原地翻转句子中单词的顺序，但单词内字符的顺序不变。</br>
要求：空间复杂度O(1) 时间复杂度O(n)</br>
输入：I am a student.</br>
输出：student. a am I
</font>

    #include <algorithm>
    #include <iostream>
    #include <string>
    
    using namespace std;
    
    string func(string &str)
    {
    	reverse(str.begin(), str.end());
    	int start = 0;
    	int size = str.size();
    	for (int i = 0; i < size; i++)
    	{
    		if (str[i] == ' ')
    		{
    			reverse(str.begin()+ start, str.begin() + i);
    			start = i + 1;
    		}
    	}
    
    reverse(str.begin() + start, str.end());
    
    	return str;
    }
    
    
    int main()
    {
    	string str;
    	getline(cin, str);
    	cout << func(str) << endl;
    	return 0;
    }


##第二题
<font size=5 color=green>
数组排成最小的数</br>
题目描述：输入一个正整数数组，将它们连接起来排成一个数，输出能排出的所有数字中最小的一个。</br>
输入：32,231 （表示数组{32,231}）</br>
输出：23123 （分别最小的数字）
</font>

    #include <algorithm>
    #include <iostream>
    #include <string>
    
    using namespace std;
    
    string func(string &str)
    {
    	reverse(str.begin(), str.end());
    	int start = 0;
    	int size = str.size();
    	for (int i = 0; i < size; i++)
    	{
    		if (str[i] == ' ')
    		{
    			reverse(str.begin()+ start, str.begin() + i);
    			start = i + 1;
    		}
    	}
    
    reverse(str.begin() + start, str.end());
    
    	return str;
    }
    
    
    int main()
    {
    	string str;
    	getline(cin, str);
    	cout << func(str) << endl;
    	return 0;
    }

##第三题
<font size=5 color=green>
01背包问题</br>
题目描述：现有N件物品，它们的重量w分别为w1,w2,...,wn,它们的价值v分别为v1,v2,...,vn,每件物品数量有且仅有一个，现在给你个承重为M的背包，求背包里装入的物品具有的价值最大总和？</br>
输入：</br>
5                 物品数量N=5件</br>
10                背包承重为M=10</br>
2 2 6 5 4         重量W分别为2 2 6 5 4</br>
6 3 5 4 6         价值V分别为6 3 5 4 6</br>
输出：</br>
15                背包内物品最大总和为15
</font>

    #include <numeric>
    #include <iostream>
    #include <vector>
    #include <algorithm>
    
    using namespace std;
    
    inline int MAX(int a, int b)
    {
    	return a > b ? a : b;
    }
    int getMaxVal(vector<int> &w, vector<int> &v, int C)
    {
    	int m = 0;
    
    	int N = w.size();
    	vector<vector<int> > dp;
    	dp.resize(N+1);
    	for (int i = 0; i < N+1; i++)
    	{
    		dp[i].resize(C + 1);
    		accumulate(dp[i].begin(), dp[i].end(), 0);
    	}
    
    	for(int i = 1; i <= N; i++)
    	{
    		for(int j = 0; j <= C; j++)
    		{
    			if(j < w[i-1])
    			{
    				dp[i][j] = dp[i-1][j];
    			}
    			else
    			{
    				dp[i][j] = MAX(dp[i-1][j],dp[i-1][j-w[i-1]]+v[i-1]);
    				if(m < dp[i][j])
    				{
    					m = dp[i][j];
    				}
    			}
    		}
    	}
    	return dp[N][C];
    }
    
    
    int main()
    {
    	int N, M;
    	cin >> N >> M;
    	vector<int> w(N), v(N);
    	for (int i = 0; i < N; i++)
    	{
    		cin >> w[i];
    	}
    	for (int i = 0; i < N; i++)
    	{
    		cin >> v[i];
    	}
    	cout << getMaxVal(w, v, M) << endl;
    	system("pause");
    	return 0;
    }