akka-kryo-serialization - kryo-based serializers for Scala and Akka
=====================================================================

This library provides custom Kryo-based serializers for Scala. It can be used for a general purpose and very efficient Kryo-based serialization of such Scala types like Option, Tuple, Enumeration and most of Scala's collection types.   

Features
--------

*   It is more efficient than JDK-based default serialization mechanisms - both in size and speed 
*   Almost any Scala and Java class can be serialized using it without any additional configuration or code changes
*   Efficient serialization of such Scala types like Option, Tuple, Enumeration, most of Scala's collection types
*   Apache 2.0 license


How to use this library in your project
----------------------------------------

To use this library, you need to do include a dependency on this library into your project:

	`libraryDependencies += "com.romix.akka" % "scala-kryo-serialization" % "0.2-SNAPSHOT"`
    
Which Maven repository contains this library?
---------------------------------------------

Currently, this library is not available on the Maven Central or the like, but it is planned.
For the time being, if you intend to use it in your project, you need to check out the project from Github and do
    `sbt compile publish-local`

If you wish to use it within an OSGi environment, you can add OSGi headers to the build by executing:
    `sbt osgi-bundle publish-local`

Note that the OSGi build uses the sbt-osgi plugin, which may not be available from Maven Central or the
Typesafe repo, so it may require a local build as well. sbt-osgi can be found at 
https://github.com/sbt/sbt-osgi.

Using this library  
-------------------

Simply add this library to your classpath. It does not have any external dependencies besides Kryo.
All serializers for Scala classes can be found in the package `com.romix.scala.serialization.kryo`

If you want to use any of those serializers in your code, add some of the following lines to your code as required:

			// Serialization of Scala enumerations
			kryo.addDefaultSerializer(classOf[scala.Enumeration#Value], classOf[EnumerationSerializer])
			kryo.register(Class.forName("scala.Enumeration$Val"))
			kryo.register(classOf[scala.Enumeration#Value])

			// Serialization of Scala maps like Trees, etc
			kryo.addDefaultSerializer(classOf[scala.collection.Map[_,_]], classOf[ScalaMapSerializer])
			kryo.addDefaultSerializer(classOf[scala.collection.generic.MapFactory[scala.collection.Map]], classOf[ScalaMapSerializer])

			// Serialization of Scala sets
			kryo.addDefaultSerializer(classOf[scala.collection.Set[_]], classOf[ScalaSetSerializer])
			kryo.addDefaultSerializer(classOf[scala.collection.generic.SetFactory[scala.collection.Set]], classOf[ScalaSetSerializer])

			// Serialization of all Traversable Scala collections like Lists, Vectors, etc
			kryo.addDefaultSerializer(classOf[scala.collection.Traversable[_]], classOf[ScalaCollectionSerializer])
      
 