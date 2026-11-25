#include <stdio.h>

int main()
{
    int start,len,i;

    printf("Enter starting block and length: ");
    scanf("%d%d",&start,&len);

    printf("Allocated blocks: ");
    for(i=0;i<len;i++)
        printf("%d ",start+i);

    return 0;
}
