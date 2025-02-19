# Chapter 11 - OpenColorIO

OpenColorIO (OCIO) is a software library which provides cross application color consistency.

You can use OCIO in RV's display, look, viewing, linearize and color pipelines. In each case OCIO can be used to convert from an incoming and outgoing color space with a user defined OCIO context. OCIO requires some work to set up and should be considered an advanced feature. Large facilities may find OCIO particularly useful in RV when used in conjunction with Nuke, Mari, or other products which support it.

You can learn about OpenColorIO at the [OpenColorIO website](http://www.opencolorio.org) .

In order to use OCIO with RV a source setup package needs to be created along with OCIO configuration files, LUTs, and an appropriate user environment. RV comes with a package called ocio_source_setup which implements a default policy for using OCIO. We recommend the package be copied and modified to suit each facility that uses OCIO.

There are four OCIO node types available in RV: OCIOLook, OCIOFile, OCIODispay, and the generic OCIO node. The default ocio_source_setup will use these nodes to replace RV's existing color, look, and display pipelines.

RV uses the OCIO GPU path instead of the more common CPU path for color computation. There are slight differences between the two which you will need to be aware of. Specifically, the color allocation parameters in the config file can have a big effect on the quality of the OCIO LUTs generated by the library.

The reference manual contains more detailed information about how to configure RV's OCIO nodes.

### 11.1 The ocio_source_setup Package


OpenColorIO defines color spaces which are used to transform images for viewing or for storage in various file formats. It does not have any policy about when to apply these transforms.

The provided ocio_source_setup package uses the default Sony Picture Imageworks method of detecting color space names in the incoming file names. The package queries OCIO and if the file name matches, the package will use OCIO nodes in various places in RV's pipelines instead of the usual RV color processing. If the incoming file name does not match an OCIO color space, the package will allow the existing RV color management to be used.

One gotcha with this package is that once an OCIO managed file name has been detected, the package will use OCIO for the display correction as well. So mixed OCIO and RV managed imagery will always be viewed using OCIO's display color corrections.

The package provides a basic menu fashioned after the OCIO display example program which allows you to file, look, and display transforms as well as forcing unrecognized media to use OCIO.

In order to use the ocio_source_setup package you need to do the following:

*   Find the “OpenColorIO Basic Color Management” package in the Packages tab of the preferences. Make sure the “load” button next to the package name is activated and restart RV.
*   Set the OCIO environment variable to the path to your config file.
*   Start RV and load an image with the color space in the name.
*   Note the "OCIO" top-level menu that appears when you use RV this way. You can use this menu to chose a Linearizing transform, or Display transform, from those provided by your config.

The OpenColorIO mailing list and website is a good place to get help about config files, documentation, and general operation.