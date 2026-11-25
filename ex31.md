#include <stdio.h>

int main()
{
    int p[20],f[5],n,m,i,j,k=0,fault=0,hit;

    printf("Enter pages and frames: ");
    scanf("%d%d",&n,&m);

    for(i=0;i<m;i++) f[i]=-1;

    for(i=0;i<n;i++) {
        scanf("%d",&p[i]);
        hit=0;

        for(j=0;j<m;j++)
            if(f[j]==p[i]) hit=1;

        if(!hit) {
            f[k]=p[i];
            k=(k+1)%m;
            fault++;
        }
    }

    printf("Page Faults = %d",fault);
    return 0;
}
