+++
Description = ""
date = "2015-09-20T14:45:54-07:00"
draft = false
menu = "main"
title = "Network graph of people's names"
type = "page"

+++

## Intro
DBpedia has a dataset of ~1,000,000 famous people which contains such information as givenName, surname, birthDate, deathDate etc.
I have been playing with this dataset in various ways.

I've also been playing with making network graphs using the igraph R package.

The logical thing to do is to combine the two, and make network graphs of people's names.

Feed igraph an edge list consisting of < givenName>,< surname>, and it gives you a graph where the first and last names are nodes, connected by lines each representing one person.

The two highly detailed images are using the first 20,000 names, from A. A. Englander to Hugh Latimer. This means that first names starting with I-Z are ignored.

igraph includes many algorithms for laying out network graphs nicely.
I am using both the Kamada-Kawai algorithm and the Fruchterman-Reingold algorithm.


## Node connections
The Alice node will be connected to the Smith node if there exists a person named Alice Smith.
Likewise, the Bob node will be connected to the Smith node if there exists a person names Bob Smith.
If there exist both a person named Alice Smith and a person named Bob Smith, then the Alice
node will be indirectly connected to the Bob node in two hops.

As more names are added, groups of connected names form and grow larger.
Eventually all the large groups are connected together in a single group,
and the small groups that failed to connect are left to be pushed to the edges.
When using 20,000 names, the largest I have observed a group becoming while staying separate from the main group, is just 26 names.

### Star and crescent

1. Take lots of points.
1. Connect some of those points.
1. There are now some points and some groups of points.
1. Connect some more points.
1. Now, some more points and groups of points are connected.
1. The probability that two points in *n* points will be connected by a random connection is (1/n) * (1/n).
1. The probability that two groups of *x* connected points will be connected by a random connection is x/n * x/n.
1. Therefore, larger groups will tend to connect together, and there will emerge one large group to which many are connected, and lots of small groups and individual points that do not connect to other.


The Kamada-Kawai algorithm and particularly the Fruchterman-Reingold
algorithm, try to keep large groups separate from each other.
The larger the group, the more important it is, and the more it should be separated from other groups.

Any time that there is a circle inside a larger circle with lots of little
things filling in the edges, the little things form into a crescent shape.

![Star and crescent formed by Kamada-Kawai on 20,000 names](/images/names-kk-20000-small.png "Star and crescent formed by Kamada-Kawai on 20,000 names.")

The `names` dataset contains one extremely large group, and lots of small <= 26 groups.

Kamada-Kawai algorithm using 500 names.
The Kamada-Kawai has no compunction about allowing lines to cross, but cares quite strongly that important groups stay separate from other non-connected groups.
![Kamada-Kawai render with 500 names](/images/person-names-kk-12-500.png "Kamada-Kawai")

Larger number of names shwoing a more pronounced cresent.
![Kamada-Kawai 5000 x 5000](https://s3-us-west-2.amazonaws.com/content-isaacleonard.com/person-names-kk.png)

Fruchterman-Reingold algorithm using 500 names.
The Fruchterman-Reingold tries to keep lines from crossing when possible, but lets non-connected groups be closer.
![Fruchterman-Reingold render with 500 names](/images/person-names-fr-12-500.png "Fruchterman-Reingold")

Larger number of names showing a more pronounced shape.
![Fruchterman-Reingold algorithm at 5000 x 5000](https://s3-us-west-2.amazonaws.com/content-isaacleonard.com/person-names-fr.png)

The original dataset: http://wiki.dbpedia.org/Downloads2015-04

## Download

You can download the full resolution renders below. **Warning!** The 2^14 renders are 50-60 MB each. They may use 3+ GB of RAM and/or crash your image viewer when you try to display them. They do have the advantage that you can zoom in far enough to read the names.


#### Kamada-Kawai algorithm using 500 names
- [5000 x 5000 8.9 MB](https://s3-us-west-2.amazonaws.com/content-isaacleonard.com/person-names-kk.png)

#### Fruchterman-Reingold algorithm using 500 names
- [5000 x 5000. 7.4 MB](https://s3-us-west-2.amazonaws.com/content-isaacleonard.com/person-names-fr.png)

#### Kamada-Kawai algorithm using 20,000 names
- [large (2^14 x 2^14 64MB)](https://s3-us-west-2.amazonaws.com/content-isaacleonard.com/person-names-kk-14-20000.png)
- [small (1683 x 1683 1.6 MB)](https://s3-us-west-2.amazonaws.com/content-isaacleonard.com/names-kk-20000-small.png)

#### Fruchterman-Reingold algorithm using 20,000 names

- [large (2^14 x 2^14 64MB)](https://s3-us-west-2.amazonaws.com/content-isaacleonard.com/person-names-fr-14-20000.png)
- [small (1683 x 1683 1.6 MB)](https://s3-us-west-2.amazonaws.com/content-isaacleonard.com/names-fr-20000-small.png)


As a derivative work of creative commons data, these images are likewise released under Creative Commons.
https://creativecommons.org/licenses/by-sa/3.0/
