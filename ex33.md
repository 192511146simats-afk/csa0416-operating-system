#include <stdio.h>

int main()
{
    int p[20],f[5],n,m,i,j,k,pos,max,next,hit,fault=0;

    scanf("%d%d",&n,&m);
    for(i=0;i<m;i++) f[i]=-1;

    for(i=0;i<n;i++) {
        scanf("%d",&p[i]);
        hit=0;

        for(j=0;j<m;j++)
            if(f[j]==p[i]) hit=1;

        if(!hit) {
            pos=0; max=-1;

            for(j=0;j<m;j++) {
                next=0;
                for(k=i+1;k<n;k++)
                    if(f[j]==p[k]) { next=k; break; }

                if(next==0) { pos=j; break; }

                if(next>max) {
                    max=next;
                    pos=j;
                }
            }

            f[pos]=p[i];
            fault++;
        }
    }

    printf("Page Faults = %d",fault);
    return 0;
}
