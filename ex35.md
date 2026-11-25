#include <stdio.h>

int main()
{
    int index[20],n,i;

    printf("Enter number of blocks: ");
    scanf("%d",&n);

    printf("Enter block numbers:\n");
    for(i=0;i<n;i++)
        scanf("%d",&index[i]);

    printf("Index block:\n");
    for(i=0;i<n;i++)
        printf("%d -> %d\n",i,index[i]);

    return 0;
}
