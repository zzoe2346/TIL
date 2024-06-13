# JVM내의 스레드가 I/O로 blocking일때 JVM이 같이 블로킹 안되는 이유

## 왜 이런
명품운영체제라는 교재를 읽는데 프로세스내의 한 스레드에서 블로킹 입출력이 발생하면 프로세스 전체가 블록된다고 되어 있었다. 여기서 든 생각이 JVM에서 는 어떻게 되지하는거였는데, 자바의 I/O operations은 모두 non-blockinig 이로 설계되어 있다고한다. 이러니 JVM전체가 block안되는 것!

이 문제는 JVM에서의 스레드를 운영체제에서의 프로세스개념으로 치환해서 이해하면 쉽게 이해가간다. 

항상 느끼는데 용어들이 너무 중복사용되서 혼란한 상황이 많은거 같다.
## chatGPT한테서 받은 답변
When input/output (I/O) occurs in one thread within the Java Virtual Machine (JVM), it typically doesn't block the entire JVM. However, the particular behavior depends on how the I/O operation is handled and the concurrency model used in the application.

In general, Java I/O operations are designed to be non-blocking, especially when using classes from the `java.nio` package, which provides support for non-blocking I/O operations. For example, when reading from a file using `java.nio.file.Files`, the operation can be non-blocking if you use asynchronous methods such as `Files.readAllBytes(Path path, OpenOption... options)`.

If you're using traditional blocking I/O operations, such as those provided by classes in the `java.io` package (e.g., `FileInputStream` or `FileOutputStream`), the thread performing the I/O operation might be blocked until the operation completes. However, other threads within the JVM can continue their execution unaffected.

It's essential to understand that a JVM can handle multiple threads concurrently. Therefore, while one thread may be blocked waiting for I/O, other threads can continue executing their tasks.

Regarding the comparison with operating system processes, the concept is somewhat similar. In an operating system, when a process performs I/O, it may be blocked, meaning it's waiting for the I/O operation to complete. However, other processes can continue executing independently. Similarly, in a JVM, when a thread performs I/O, it may be blocked, but other threads within the same JVM can continue execution.

So, to answer your question directly: No, the entire JVM is not necessarily blocked when input/output occurs in one thread within the JVM. The impact of I/O operations depends on the concurrency model and the specific I/O operations being performed.