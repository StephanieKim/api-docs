## Scala Client

If you work in Scala, you will be able to use the Algorithmia Java Client. The Java client is available on GitHub, published to Maven Central, and is automatically available to any algorithm you create on the Algorithmia platform.

```
libraryDependencies ++= Seq(
  "com.algorithmia" % "algorithmia-client" % "1.0.+",
)
```

The Algorithmia Java Client is published to Maven central.

It can be added as a dependency to other projects that wish to use the Algorithmia API by adding it to `libraryDependecies`.

To instantiate, set your API key on the client.

`val client = Algorithmia.client("YOUR_API_KEY")`

### Calling Algorithms in Scala

> Algorithms called with the `.pipe()`:

```
val response = client.algo("demo/Hello").pipe("Liz")
val result = response.as(new TypeToken<String>(){})
val durationInSeconds = response.getMetadata.getDuration
```

There are two ways to call an algorithm: `.pipeJson` and `.pipe`.

`.pipeJson:`

* Use pipeJson when you are manually converting objects to JSON. This can be useful when working on edge cases or in testing.

* We recommend that you use .pipe whenever possible.

`.pipe:`

* Use .pipe whenever possible. .pipe will take an object and convert it into the JSON structure required.

* You can use .pipe with binary files. No JSON serialization is required with .pipe.

### Casting results in Scala

> For an algorithm that returns a string:

```
stringResult.as(new TypeToken<String>(){})
```

> For an algorithm that returns an array of strings:

```
stringArrayResult.as(new TypeToken<List<String>>(){})
```

> For an algorithm that returns a custom class, cast the result to that class:

```
class CustomClass {
  val maxCount: Int
  val items: List[String]
}
customClassResult.as(new TypeToken<CustomClass>(){})
```

> For debugging, it is often helpful to get the JSON String representation of the result:

```
anyResult.asJsonString
```

In order to cast the result to a specific type, call `.as()` with a TypeToken.

On the right pane, you'll find examples of how to do this to return a string, an array of strings, and a custom class.

<aside class="notice">
  To create a TypeToken, use the syntax <code>new TypeToken&lt;CustomClass&gt;(){}</code> ensuring that the trailing <code>{}</code> is present to create an anonymous subclass.
</aside>

### Working with Data in Scala

> Create a directory "foo"

```
val foo = client.dir("data://.my/foo")
foo.create()
```
> Upload files to "foo" directory

```
foo.file("sample.txt").put("sample text contents")
foo.file("binary_file").put(new byte[] { (byte)0xe0, 0x4f, (byte)0xd0, 0x20 })
foo.putFile(new File("/local/path/to/myfile"))
```

> List files in "foo"

```
for(file <- foo.getFileIter) {
  println(s"${file.toString} at URL: ${file.url}")
}
```

> Get contents of files

```
val sampleText = foo.file("sample.txt").getString
val binaryContent = foo.file("binary_file").getBytes
val tempFile = foo.file("myfile").getFile
```

> Delete files and directories

```
foo.file("sample.txt").delete()
foo.delete(true) // true implies force deleting the directory and its contents
```

The Algorithmia Java Client provides an easy way to manage data stored within Algorithmia. Basic usage samples are shown in the right pane. See the [DataAPI docs](../data.md) for more information.

#### Additional resources

* <a href="http://www.javadoc.io/doc/com.algorithmia/algorithmia-client/1.0.3">Algorithmia Client Java Docs <i class="fa fa-external-link"></i></a>
* <a href="https://github.com/algorithmiaio/algorithmia-java">Algorithmia Java Client Source Code<i class="fa fa-external-link"></i></a>
