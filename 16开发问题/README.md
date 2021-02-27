## 1 解释什么是流 (Streaming) 和如何实现一个流？

流代表了一序列的对象（通常为字节 byte），它们可以被有序的访问。典型的流操作有
- Read / Write (可以操作一个或者多个字节)
- Seek (可以移动当前的位置，以便下次操作的时候在移动后的位置)

流通常分别两种，一种是输入流（Input Streaming)；另一种是输出流 （Ouput Streaming)。输入流通常是需要处理一些数据，而不管这个数据是以何种产生；而输出流则是有一些数据会产生，而不管这些数据是被调用者如何处理。
流提供了一种很好的抽象，在计算机领域中内存，文件甚至是网络都可以被抽象成流，大大简化了编程模型。

接下来实现一个 `C#` 为流
```C#
class MyStream ： Stream
{
    private int cap = 10;
    private int index = 0;
    private byte[] arr = new byte[this.cap];

    public override int Read(byte[] buffer, int offset, int count)
    {
        int i = 0;
        for(; i < count && offset + i <  buffer.Length && index + i < cap; i++)
        {
            buffer[i+offset] = arr[i + index]
            index++;
        }
        return i;
    }

    public override void Write(byte[] buffer, int offset, int count)
    {
        for(int i = 0; i < count && offset + i < buffer.Length; i++)
        {
            Console.WriteLine(buffer[i+offset]);
        }
    }
} 
```