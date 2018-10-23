#include <iostream>
#include <cmath>
#include <vector>
using namespace std;
typedef unsigned long long int ullint;
const int MAX_N = 32;
ullint Edg[MAX_N][MAX_N]= {{0}};
static ullint ACTr = 0, ATr = 0;
int sz[MAX_N]= {1};
ullint CTr[MAX_N]= {0}, Lb[MAX_N][MAX_N]= {0};
int m = 1, n = 1;
ullint pwmx=1;

void ShowBits(ullint pt, int n)
{
    m = n*(n-1)/2;
    while (m--)
    {
        if(pt&pwmx)
            cout<<"1 ";
        else
            cout<<"0 ";
        pt<<=1;
    }
    cout<<endl;
}

void Show(ullint *L, int b, int n)
{
    for(int i=b; i<=n; i++)
    {
        cout<<L[i]<<",";
    }
    cout<<endl;
}

ullint Tr = 0;

bool DECOMPRESSION(int k)
{
    if(k==0)
    {
        //cout<<Tr<<endl;
        //ShowBits(Tr,n);
        ATr++;
    }
    else
    {
        for(int i=0; i<sz[k]; i++)
        {
            Tr|=Lb[k][i];
            DECOMPRESSION(k-1);
            Tr^=Lb[k][i];
        }
    }
    return true;
}

ullint tEdg=0;

bool COMPRESSION(int k)
{
    if(k==0)
    {
        ACTr++;
       // Show(CTr,0,n);
        DECOMPRESSION(n-1);
    }
    else
    {
        for(int i=0; i<k; i++)
        {
            if(!Edg[k][i]) continue;
            CTr[k]=Edg[k][i];
            sz[k]=0;
            tEdg=Edg[k][i];
            while (tEdg)
            {
                Lb[k][sz[k]]=tEdg&~(tEdg-1);
                tEdg^=Lb[k][sz[k]];
                sz[k]++;
            }
            for(int j=0; j<i; j++)
               Edg[i][j]|=Edg[k][j];
            COMPRESSION(k-1);
            CTr[k]=0;
            for(int j=0; j<i; j++)
              Edg[i][j]^=Edg[k][j];
        }
    }
    return true;
}

int main()
{
    ullint tp = 0;
    //All spanning trees for Complete graph
    n = 4;
    pwmx=pow(2,-1+n*(n-1)/2);
    int k=0;
    for(int j=1; j<n; j++)
    {
        for(int i=0; i<j; i++)
        {
            tp = pow(2,k);
            Edg[j][i]|=tp;
            k++;
        }
    }


    COMPRESSION(n-1);
    cout<<"The number of all compressed trees is "<<ACTr<<endl;
    cout<<"The number of all spanning trees is "<<ATr<<endl;
    return 0;
}
