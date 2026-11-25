#include <stdio.h>
#include <stdlib.h>

int main()
{
    int a[20],n,head,i,total=0;

    scanf("%d",&n);

    for(i=0;i<n;i++) scanf("%d",&a[i]);

    scanf("%d",&head);

    for(i=0;i<n;i++) {
        total+=abs(head-a[i]);
        head=a[i];
    }

    printf("Total Head Movement = %d",total);
    return 0;
}
