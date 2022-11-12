# Content Providers

A content provider component supplies data from one application to others on request. Such requests are handled by the methods of the *ContentResolver* class. The data may be stored in the file system, the database or somewhere else entirely.

A content provider is implemented as a subclass of ContentProvider class and must implement a standard set of APIs that enable other applications to perform transactions.

```java
public class MyContentProvider extends  ContentProvider {
   public void onCreate(){}
}
```

We will go through these tags in detail while covering application components in individual chapters.
