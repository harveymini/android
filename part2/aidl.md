# Android Interface Definition Language (AIDL)

The [Android Interface Definition Language (AIDL)](https://developer.android.com/guide/components/aidl) is similar to other [IDLs](https://en.wikipedia.org/wiki/Interface_description_language) you might have worked with. It allows you to define the programming interface that both the client and service agree upon in order to communicate with each other using interprocess communication (IPC). On Android, one process cannot normally access the memory of another process. So to talk, they need to decompose their objects into primitives that the operating system can understand, and marshall the objects across that boundary for you. The code to do that marshalling is tedious to write, so Android handles it for you with AIDL.



