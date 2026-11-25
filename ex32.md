#include <stdio.h>

int main()
{
    int p[20],f[5],n,m,i,j,k,fault=0,pos,min,hit;

    scanf("%d%d",&n,&m);
    for(i=0;i<m;i++) f[i]=-1;

    for(i=0;i<n;i++) {
        scanf("%d",&p[i]);
        hit=0;

        for(j=0;j<m;j++)
            if(f[j]==p[i]) hit=1;

        if(!hit) {
            pos=0;
            for(j=1;j<m;j++)
                if(f[j]<f[pos]) pos=j;

            f[pos]=p[i];
            fault++;
        }

        for(k=0;k<m;k++)
            if(f[k]==p[i]) f[k]=i;
    }

    printf("Page Faults = %d",fault);
    return 0;
}
