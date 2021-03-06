Tesco type provider
===================

This sample shows how to write a type provider that gives a type-safe access to 
categories that are currently provided by the Tesco web service. The categories
are obtained on the fly - this means that when Tesco changes the structure, the
type provider will automatically see the changes!

Important files:

 * `TescoProvider.sln` - Visual Studio solution with the type provider. The
    `ProvidedTypes*` files are standard template. The actual implementation is
	is in `TescoProvider.fs` and is commented :-)
	
 * `samples/Sample.fsx` - shows how to query port vines using the type provider
    (to run the sample, you first need to compile the type provider).
	When you open the file in Visual Studio, it will lock the type provider `dll`
	so you won't be able to rebuild - the best way to work is to use two instances
	of Visual Studio.

Tesco provider in action 
------------------------

The following sample shows how type providers work when used from an editor such as 
Visual Studio - we can navigate through categories using IntelliSense and pick, for example,
the category "Shery Port & Montilla" under "Drinks" and "Spirits". Then we can use
other F# features to query the data.


![Type provider in action!](https://raw.github.com/tpetricek/Documents/master/Samples/TescoProvider/screenshot.png)

Known issues
------------

 * When you try to get products in a category containing larger number of products,
   you get an error message complaining about `MaxReceivedMessageSize` from WCF - we should
   increaste this parameter (somehow?)

 * The type provider lets you enumerate products in categories that are not at the leaf
   of the category tree (e.g. `tesco.Drinks`) but the service does not return any data
   for those - we should either lazily iterate over all children or do not allow this.
