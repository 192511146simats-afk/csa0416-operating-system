#include <stdio.h>

int buffer[5], in=0,out=0;

void produce(int x)
{
    buffer[in]=x;
    in=(in+1)%5;
    printf("Produced: %d\n",x);
}

void consume()
{
    int x=buffer[out];
    out=(out+1)%5;
    printf("Consumed: %d\n",x);
}

int main()
{
    produce(10);
    produce(20);
    consume();
    consume();

    return 0;
}
