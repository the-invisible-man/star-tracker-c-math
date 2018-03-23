# Star Tracker C Math Libraries

This repository has some early versions/proof concepts of the math functions for a past nanostallite project. The repo comes with trig functions, as well as a quaternion calculator. The quaternion calc returns a quaternion given an axis (x, y, z) and degree of rotation, in practice this is used to prevent [gimbal lock](https://en.wikipedia.org/wiki/Gimbal_lock). It contains a Quaternion object with (w, x, y, z). The project includes a star catalog in a csv file, as well as a sql to create the table that holds the csv data.

The database engine planned for this is mysqlite.

The implementations in this repository are based on the following theses:

*  Kenneth Daniel Diaz (2006), [Performance Analysis of a Fixed Point Star Tracker Algorithm for Use Onboard a Picosatellite](http://www.crn2.inpe.br/conasat1/projetos_cubesat/projetos/CP1%20-%20California%20Polytechnic%20Institute%20-%20USA/CP1%20-%20ADCS%20-%20Analisys%20of%20a%20Fixed%20Point%20Star%20Tracker%20Algorithm.pdf),

* Kara M. Huffman (2006), Designing Star Trackers to Meet Micro-satellite Requirements

## Algorithm

The algorithm aims to receive combinations of 3 stars from a specific reference frame in two-dimensional space and transform into 3-dimmensinal space, determine its properties, and use these results to find a match in our star catalog (Separate Module, not part of this module). The properties of each triangle is extracted through 3 different strategies.

* Area and Polar Moment
* Planar Angle
* Vector Angle

Our database needs to be prepared beforehand, this requires calculating all properties of our dataset. The main function demonstrates the mathematical function for using all three strategies.

The stars that we choose to calculate are exclusive to their magnitude. The naive appraoch to this problem would be to assume that any object in the sky is a star. This is not the case as you can have space dust touching the lens. For this we pick stars with a magnitude of at least 3.0. The magnitude of a star is its brightness, the lower the magnitude is the brighter the star is. For instance -5.0 would be brighter than 3.0. The brighter the star, the better chance of a match that we'll find in our dataset.

## Star Extractor

The star extractor project will put together the combinations of stars from an image file. The C++ project uses the OpenCV library and is available [here](https://github.com/the-invisible-man/star-extractor).
