#### 最短路
```c++
#include<iostream>
#include<cstring>
#include<algorithm>
const int N = 505, INF = 0x3f3f3f3f;
int n, m;
int g[N][N];
int dist[N];
bool st[N];

int dijkstra()
{
    memset(dist, -1, sizeof dist);
    dist[1] = 0;
    for(int i = 0; i < n; i ++)
    {
        int t = -1;
        for(int j = 1; j <= n; j++)
        {
            if(!st[j] && (t == -1 || dist[j] < dist[t]))
            {
                t = j;
            }
        }
        st[t] = true;
        for(int j = 1; j <= n; j++)
        {
            dist[j] = min(dist[j], dist[t] + g[t][j]);
        }
    }
    return dist[n];
}

int main()
{
    memset(g, 0x3f, sizeof g);
    scanf("%d%d",&n, &m);
    while(m--)
    {
        int a, b, c;
        scanf("%d%d%d",&a,&b,&c);
        g[a][b] = min(g[a][b], c);
    }
    int t = dijkstra();
    if(t == -1) puts("impossible");
    else printf("%d\n", t);
    return 0;
}
```