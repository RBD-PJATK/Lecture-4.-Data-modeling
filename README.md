# Lecture 4. Data modeling

<h2 align="center">Lecture 4</h2>

<h2 align="center"><i>Data modeling</i></h2>

<hr><h3>Abstract</h3>

<p>Lecture 4 consists of four parts.</p>

<p>In the first we present two alternative notations for entity-relationship diagrams.
In practice many different notations are used  and one best standard does not exist.
We also describe an addendum with symbols to model views and subcategories.</p>

<p>In the second part we consider two problems that often occur in day-to-day
engineering. They concern hierarchical data and the temporal aspect of data.</p>

<p>The third part describes two object-relational extensions to the data model. One of them
comes with MS Visio, while the other is ODL (Object Definition Language) defined by
ODMG (Object Database Management Group).</p>

<p>The fourth part is devoted to <i>semistructured data</i> and the representation of
data in XML.</p>

<p>As in the previous lecture all the example diagrams are created by MS Visio.</p>


<hr><h3><a name="Alternatywna">Data modeling notation IDEF1X</a></h3>

<p>We are going to present two alternative notations for entity-relationship diagrams.
In practice many different notations are used  and one best standard does not exist.
All these notations are based on the notions <i>entity</i>-<i>attribute</i>-<i>relationship</i>.
The choice of the notation is really a secondary (or even tertiary) issue.  It is usually
determined by the CASE tool used by the project team.</p>

<p>We will start from IDEF1X. It is available in Visio.  Simply choose:
"Database -&gt; Options -&gt; Document :: Symbol set = IDEF1X" (instead of default
"Relational").</p>

<p align="center"><img border="0" src="images/4_3.png"></p>

<ul>
<li>Solid line = identifying relationship
<li>Dashed line = non-identifying relationship
<li>Black circle = detail entity
<li>Hollow diamond = optional relationship
<li>IE = index (Inversed Entry)
</ul>

<p>IDEF1X is the notation used by Erwin - a tool used earlier in PJWSTK. IDEF1X allows to
model many-many relationships directly, but this feature is not available directly
in MS Visio.  You can simulate such a relationship by the item "Dynamic connector".</p>

<p align="center"><img border="0" src="images/4_10.png"></p>

<table><tr><td class="przyk">
A <i>person</i> can work on many <i>projects</i>.  A <i>project</i> is conducted
by many <i>persons</i>.</td></tr></table>


<hr><h3><a name="Notacja">Chen's data modeling notation</a></h3>

<p>Peter Chen invented the modeling method based on entities and relationships in 1976.
Here we present this very first notation for entity-relationship diagramming. It is more
general than the two methods described previously, because it allows defining multi-argument and many-many
relationships. In this notation:

<ul>
<li>Entity = rectangle
<li>Attribute = circle
<li>Relationship = diamond
</ul>

If you want to use Chen's notation in Visio, use option
&quot;File -&gt; New -&gt; Database -&gt; Chen ERD&quot; instead of
&quot;File -&gt; New-&gt; Database -&gt; Database Model Diagram&quot;.</p>

<p align="center"><img border="0" src="images/4_9.png"></p>

<table><tr><td class="przyk">A person participates in a projects in a role.</td></tr></table>

<p>Here is a simple exercise on data modeling.</p>

<table><tr><td class="notec">Using Chen's notation draw an entity-relationship diagram for the zoo. Include
animals, their keepers and feed.  The model should contain the following relationship:
an <i>animal</i> eats <i>feed</i> served by a <i>keeper</i>.
</td></tr></table>

<p>As an "exploratory" task examine MS Visio:</p>

<table><tr><td class="notec">Find more notations for entity-relationship diagrams offered
by MS Visio. Perhaps some other notation is more suitable for you?
</td></tr></table>

<hr><h3><a name="Definiowanie">Views</a></h3>

<p>A view is a user-oriented presentation of the data from a database.  It is created
to cater for the needs of a user of the database. The first example shows a view with
names of persons (it is an attribute of the entity <i>Person</i>) and the locations of their
departments (it is an attribute of the entity <i>Department</i>). When you define a view,
you have to specify the join condition for tables participating in the view.</p>


<p align="center"><img border="0" src="images/4_1.png"></p>

<p>The second example shows view <i>ProductOrder</i> with products ordered by customers.
It contains two attributes: <i>Customer name</i> (an attribute of entity <i>Customer</i>)
and <i>Product name</i> (an attribute of entity <i>Product</i>). Note that entities
<i>Customer</i> and <i>Product</i> that provide attributes for this view
are not connected directly. When you define the join condition (tab "Join Criteria"),
specify a sequence of join conditions that starts from entity <i>Customer</i>, goes
through entities <i>Order</i> and <i>Line item</i>, and stops at entity <i>Product</i>.
This example shows that the definition of a view can include other entities than those
that provide attributes for the view.</p>

<p align="center"><img border="0" src="images/4_2.png"></p>

<p>When you generate this model in MS Access, 
you will get a select query for each view.

<hr><h3><a name="Hierarchia">Subcategories</a></h3>

<p>There is one more relationship that frequently appears in entity-relationship models.
This relationship can connect any number of relationships.  In such cases one entity is
distinguished as the <i>super-entity</i> (or <i>general entity</i>),
while all the other related entities are the
<i>sub-entities</i> (or <i>specific entity</i>).  Such relationships are called
<i>category relationships</i>.
They allow specifying the inheritance of properties of the general entity by the
specific entities.  For example <i>Person</i> is the super-entity for sub-entities
<i>Designer</i>, <i>Analyst</i> and <i>Secretary</i>.</p>


<table><tr><td class="przyk">A person may be a designer, an analyst or a secretary.
Common properties are grouped in the entity <i>Person</i>. Specific attributes of
sub-entities fall into one of entities <i>Designer</i>, <i>Analyst</i>
and <i>Secretary</i>.
</td></tr></table>

<p align="center"><img border="0" src="images/4_5.png"></p>

<p>The attribute <i>Job</i> is called <i>the discriminator</i> because it indicates to which
sub-entity belongs an instance of the entity <i>Person</i>.  This categorization has been designated to
be <i>complete</i>, i.e. every person belongs to one subcategory.</p>

<p>Here is the full tool for the option "Entity Relationship" in MS Visio:

<p align="center"><img border="0" src="images/4_4.png"></p>

<p>A category relationship can be replaced by a set of one-to-one relationships between
the super-entity and each of the the sub-entities. During lecture 3 we presented three
ways to implement a one-to-one relationship in a relational database.  They can be used
to implement a category relationship:

<ol>
<li>separate tables for the super-entity and all the sub-entities,
<li>separate tables for all the sub-entities,
<li>one common table.
</ol>

MS Visio generates an Access database with the first method, i.e. separate tables are
created for the super-entity and all the sub-entities:

<p align="center"><img border="0" src="images/4_6.png"></p>

<p><table><tr><td class="notec">As an exercise build a categorization of flying
objects.  What properties are common? What properties are specific?
</td></tr></table>


<hr><h3><a name="Modelowanie danych hierarchicznych">Hierarchical data</a></h3>

<p>One of the most frequent patterns of data models are <i>hierarchies</i>.
For example let us consider the structure of a company:</p>

<p align="center"><img border="0" src="images/4_15.png"></p>

<p>There is an alternative way to model it.  All units of the company can be instances of one
entity.  The link to the master unit becomes the recursive relationship around this only
entity.</p>

<p align="center"><img border="0" src="images/4_14.png"></p>

<p>This model is simpler and more flexible. When the structure of the company changes, there
will be no need to change the schema of the database. Note that the recursive relationship
that represents the hierarchy must be optional. Otherwise there  will be no end of the
hierarchy.  If the relationship is optional, we can walk up this tree and we will eventually
reach the <i>root of the hierarchy</i>.</p>

<p>The entity <i>Unit</i> has an attribute <i>Type</i> that indicates the type of the unit, e.g.
"Department" or "Branch". The set of these type is small and rarely changed. To facilitate
the integrity checks for this attribute we can introduce a so called <i>dictionary entity</i>.
On the diagram below <i>UnitType</i> is a dictionary entity.</p>

<p align="center"><img border="0" src="images/4_16.png"></p>

<table><tr><td class="notec">
The set of the components of a car constitutes a hierarchy based on the containment
relationship (a component aggregates other components). Draw a data-relationship diagram of this hierarchy.
</td></table>

<hr><h3><a name="Modelowanie czasu">Modeling changes in time</a></h3>

<p>Designers of databases often face the problem of data that changes in
time.  The question is how to include the aspect of time in the data model. 
We are not only interested in the current salary, job and department of an
employee but we want to know also his/her prevoius salaries, jobs and departments.</p>

<p align="center"><img border="0" src="../wyklad03/images/3_5.png"></p>

<p>In such cases we employ the same technique that was used to handle
many-many relationships.  We add a so called <i>temporal entity</i> that
will represent the changes in time.  It can store the log of values of the
attributes or instances of the relationships with other entities. First, we
solve the problem how to enrich the data model so that it contains the
history of salaries (attribute <i>Salary</i>) and jobs (attribute
<i>Job</i>).  We add new dependent entities <i>SalaryHist</i> (the history
of salaries) and <i>JobHist</i> (the history of jobs). We also add an attribute
(<i>From</i>) to mark the time the change occurred.  This attribute should
be an element of the primary key. Perhaps you will want to create another
attribute <i>To</i> which is to store the time when the value becomes
invalid.</p>

<p align="center"><img border="0" src="images/4_112.png"></p>

<p>Now we are going to solve the problem how to enrich
the data model so that it contains the history of employees' assignments to departments
(this is a relationship between entities <i>Person</i> and <i>Department</i>).
We add a new dependent entity <i>AssigmentHist</i>
(the history of employee's assignments to departments). We also add an attribute
(<i>From</i>) to mark the time the assignment occurred.  This attribute should be an
element of the primary key.  As before, you may want to create another attribute
<i>To</i> that is to store the time when the assignment becomes invalid.</p>

<p align="center"><img border="0" src="images/4_111.png"></p>

<p>This way we have described the changes to attributes and relationships that
happen in time. We can also ask whether it is reasonable to consider changes of an
entity itself. The changes of attributes of entities could be represented as before but
it does not concern the primary key, because a change of its value means the change of the
identity of the entity. This change can be represented as replacement of one instance by
another, i.e. deletion and insertion with probable movement of some attributes.</p>

<p>Sometimes it could be only the deletion with the history of values of the attributes.
In fact, databases of banks and companies usually store information on accounts and
employees although they are no longer customers or employees.  Here is one possible
solution that consists in adding attribute <i>Status</i>.  It indicates whether a person
is currently an employee of the company.</p>

<p align="center"><img border="0" src="images/4_110.png"></p>

<p>We could also move the data from deleted objects to separate entities that are
a kind of historical archive of the database.  It would be reasonable especially when
the number of instances of the entities is huge, because it speeds up database searches.
</p>

<table><tr><td class="notec">
Draw a "temporal" data model for the cadastral data.  We are interested in the
relationships between owners and real estates. Take into account that sometimes estates
are destroyed and owners die.
</td></tr></table>

<hr><h3><a name="Obiektowo">Object-relational model</a></h3>

<p>In an object database objects are instances of object types (classes) with methods
and inheritance. Objects are stored in object tables.</p>

<h4><a name="Tabela">Object table</a></h4>

<p><i>Object table</i> is a table where there are objects of a given object type (class). The transition
from a relational table to the object table is driven by the following rule:

<p align="center"><i>row</i> -&gt; <i> object</i></p>

<p>As a result of this transformation every row of a table gains the identity
and the methods and becomes an object.</p>

<p>The value of an attribute may be non-atomic (complex), e.g. a list of values,
a set of values, a record or a reference to another object.</p>

<h4><a name="Model">Object-relational model in MS Visio</a></h4>

<ul>
<li>We introduce two object types <i>AddressType</i> and <i>PersonType</i>.
<li>We introduce the table <i>Persons</i> which will store a set of objects of type
        <i>PersonType</i>.
<li>Every object of type <i>PersonType</i> has:
        <ul>
        <li>three atomic (non-complex) attributes:
                <i>firstName</i>, <i>secondName</i> and <i>birthDate</i>,
        <li>two attributes of a complex type:
                <ul>
                <li><i>address</i> of type <i>AddressType</i> and
                <li><i>mgr</i> that is a reference to an object of type <i>PersonType</i>.
                </ul>
        </ul>
</ul>

<p align="center"><img border="0" src="images/4_7.png"></p>

<p>In the current version of MS Access there are no object features.  They are
available for example in DBMS Oracle that will be used to teach the sequel
subject, i.e. "Database systems".</p>

<p><table><tr><td class="notec">
Create an object-relational definition of collection "Set of contacts". A contact
is a record that indicates both the kind and the data, e.g. &lt;kind = "private e-mail",
data = "ian@mailserver.edu"&gt;. Draw an object relational-model of a person with
an attribute that stores the contacts to this person.
</td></tr></table>

<hr><h3><a name="Model3">Collections</a></h3>

<p>A collection is the model of a bunch of values. We are interested not only in the
item's membership in the collection but also in other aspects like the order of the members
and multiple membership.  We classify collections as follows:</p>

<dl>
<dt><i>Set</i>
<dd>An unordered collection of values without repetitions, e.g. {4,8,9}.
<dt><i>List</i>
<dd>An ordered collection of values with possible repetitions, e.g. (1,2,1,5,6,7).
<dt><i>MultiSet</i>
<dd>An unordered collection of values with possible repetitions, e.g.
    {4,8,4,8,8,9}.
</dl>

<h4>Examples of collections of persons: Group, Line and Enrollment</h4>

<p align="center"><img border="0" src="images/4_01.png"></p>

<p>Using collections of the object-relational model we can easily capture
certain phenomena we met before.  These phenomena are non-atomic attributes,
attributes whose values change in time (see <a href="#exercise8">exercise 8</a>).
We can also model relationships that change in time, but we have to use object references
and integrity constraints that limit the range of references.  Appropriate methods
will be presented during the sequel lecture "Database systems".</p>

<p>In the relation model we can render collections in the following ways:</p>

<ol>
<li><i>A group</i>:

<p align="center"><img border="0" src="images/4_8.png"></p>

<p>In a single group persons are unordered and do not repeat.  This uniqueness
is enforced by the primary key that consists of <i>Empno</i> and <i>Group_id</i>.
</p>

<li><i>A line</i>

<p align="center"><img border="0" src="images/4_80.png"></p>

<p>Persons in the line are ordered by the attribute <i>Position</i>.
A person may occur many times in the same line.  If we want to forbid such
repetitions,
we can set a unique index on attributes <i>Line_id</i> and <i>Empno</i>.</p>

<li><i>Participations</i> (a multiset)</i>

<p align="center"><img border="0" src="images/4_81.png"></p>

<p>In a single collection <i>Project</i> (a multiset) a person can occur more that once
(e.g. in different roles).
We allowed this by adding the attribute <i>Occurrence</i> to the primary key of
the entity
<i>Participation</i>. The order of participations is irrelevant.</p>

<p>The entity <i>Participation</i> could include more information like
the role in the project.  If we do not need such information, we can move
the attribute
<i>Occurrence</i> out of the primary key and treat is as the number of occurrences
of the person identified by <i>Empno</i> in the <i>Project</i>.</p>

</ol>

<hr><h3><a name="ODL">ODL</a> (<i>Object Definition Language</i>)
- a language for object modeling</h3>

<p>ODL is a part of ODMG 3.0 that is a standard for object databases (<i>ODMG</i> =
<i>Object Database Management Group</i>).  The syntax of ODL is based on OMG IDL that
in turn is based on C++.  Therefore it is not surprising that ODL resembles C++.</p>

<p>The basic notion of ODL is <i>an object</i>. It has a unique identifier
(<i>OID</i> = <i>Object IDentifier</i>) that distinguishes it from other objects.
Objects with similar properties are grouped into classes modeled as interfaces.</p>

<p>The specification of the schema of an object class in ODL contains three kinds of properties:

<dl>
<dt><i>attributes</i>
<dd>They are assigned values of elementary (integers or strings) or complex types.
<dt><i>relationships</i>
<dd>They are references to objects of a given class or collections (e.g. sets)
        of such references.
<dt><i>methods</i>
<dd>They are functions that operate on objects of the class.
</dl>

<h4><a name="Deklaracja">The declaration of a class</a></h4>

<pre>interface Movie {
   attribute string title;
   attribute integer year;
   attribute integer duration;
   attribute enum Tape {color, black_white} tapeType;
}</pre>

<p>Attribute <i>tapeType</i> is assigned a value of the enumeration type that has two
values: {color,black_white).  Object <i>Movie</i> is a tuple of values, e.g.
("Gone with the Wind", 1939, 231, color).</p>

<h4><a name="Rekord">A class with an attribute of a complex type</a></h4>

<pre>interface Star {
   attribute string name;
   attribute Struct Addr {string street, string city } address;
}</pre>

<p>An attribute <i>address</i> is a record, i.e. a value of a complex type
<b>Struct</b> <i>Addr</i>.  This type consists of two fields:
<i>street</i> and <i>city</i>. In ODL a record is defined with the keyword <b>Struct</b>
and the list of fields and their types surrounded by curly brackets.</p>

<h4><a name="Pozadane">A relationship between objects of classes</a></h4>

<pre>interface Movie {
   attribute string title;
   attribute integer year;
   attribute integer duration;
   attribute enum Tape {color, black_white} tapeType;
   <font color="red">relationship Set&lt;Star&gt; cast inverse Stars::stars_in;</font>
}</pre>

<p>In each object of the class <i>Movie</i> there is an attribute
<i>cast</i> which stores the set of references to objects of class
<i>Stars</i>. If you have the object <i>Movie</i>, you can retrieve information
of the stars who played in this movie.  It is indicated by the keyword
<b>Set</b> that precedes the string <code>&lt;Star&gt</code>.</p>

<p>In ODL the definition of a type of sets of elemenets of type <i>T</i>
consists of the keyword <b>Set</b> followed by <i>T</i> in angle brackets.</p>

<p>Apart from <b>Set</b>&lt;T&gt; ODL provides also other kinds of collections:

<ol>
<li>multiset <b>Bag</b>&lt;T&gt;,
<li>list <b>List</b>&lt;T&gt;,
<li>vector (array) of length <i>n</i> <b>Array</b>&lt;T,<i>n</i>&gt;.
</ol>

<h4><a name="Odwrotny">The inverse relationship</a></h4>

<p>Together with the information on actors starring in a movie, we also
want (and in fact we have to) store the information on the movies of each star.
In the class <i>Star</i> we add:

<pre>interface Star {
   attribute string name;
   attribute Struct Addr {string street, string city } address;
   <font color="red">relationship Set&lt;Movie&gt; stars_in inverse Movie::cast;</font>
}</pre>

<p>This way we define an important coincidence between these two
relationships:</p>

<table><tr><td class="important">
If the star <i>S</i> <u>stars_in</u> in the movie <i>M</i>, then
the movie <i>M</i>'s <u>cast</u>
contains the star <i>S</i>.
</td></tr></table>

<p>This coincidence is specified in ODL with the keyword <b>inverse</b> and the name
of the related class and the name of the inverse relationship.  In fact it is obligatory to
define an inverse relationship for each relationship in ODL.</p>

<h4><a name="Licz">Cardinality</a></h4>

<p>The relationship between classes <i>Movie</i> and <i>Star</i> is many-many, because
we used keyword <b>Set</b> on both sides.  If this keyword (more precisely any collection type)
is used only at one side, the relationship is many-one.  If none of the sides is marked with a collection type,
the relationship is one-to-one.</p>

<h4><a name="Jedn">Many-one relationship</a></h4>

<table><tr><td class="przyk">
Let us assume that in every movie we distinguish one star as a <i>superstar</i>
of this movie. One actor can be a superstar of many movies.  It is an example of
many-one relationship between classes <i>Movie</i> and <i>Star</i>.
</td></tr></table>


<pre>interface Movie {
   attribute string title;
   attribute integer year;
   attribute integer duration;
   attribute enum Tape {color, black_white} tapeType;
   relationship Set&lt;Star&gt; cast inverse Stars::stars_in;
   <font color="red">relationship Star superstar inverse Star::outstanding;</font>
}

interface Star {
   attribute string name;
   attribute Struct Addr {string street, string city } address;
   relationship Set&lt;Movie&gt; stars_in inverse Movie::cast;
   <font color="red">relationship Set&lt;Movie&gt; outstanding inverse Movie::superstar;</font>
}</pre>

<table><tr><td class="notec"><a href="javascript:popUp('ok1.html',580,380)">
Give</a> the definition of classes <i>Employee</i> and <i>Department</i> in ODL.
Specify the following relationship: "An employee works in one department".
</td></tr></table>

<h4><a name="Specyfikacja">Methods</a></h4>

<p>You can specify methods among features of a class.  Here is an example with the method
to calculate employee's age from the date of birth.</p>

<pre>interface Employee {
   attribute string firstName;
   attribute string secondName;
   attribute genderType Enum {male, female} gender;
   attribute Date birthDate;
   <font color="red">short Age();</font>
};</pre>

<h4><a name="Dziedzicz">Inheritance</a></h4>

<p>A class may inherit all properties from another class.  For instance
class <i>Professor</i> inherits from class <i>Employee</i>. Every object
defined by interface <i>Professor</i> apart from its own attributes and methods
has also all attributes an methods of interface <i>Employee</i>:</p>

<pre>interface Professor <font color="red">: Employee</font> {
   attribute string degree;
};</pre>

<p>The whole domain of object modeling is the subject of another lecture
"Design of information system", where you will find more details.
</p>

<hr><h3><a name="Ds">Semistructured data</a></h3>

<p>The semistructured data model is very important in applications of databases.</p>

<ul>
<li>First, it serves as the model that supports the <font color="red">integration
        of databases</font>, because it allows describing data stored in two or even
        more databases.  Although the integrated databases contain similar data,
        usually every one of them has a different schema.  This way the integrated
        databases in disparate locations look and operate like a single database.
<li>Second, this model serves as <font color="red">the model of documents</font>
        that supports sharing data over the Internet.
</ul>

<p>The <i>structural models</i>, i.e. the models presented previously (relational and object-relational),
are based on the notion of <i>schema</i>.  The semistructured model has no schema.  The data is
self-describing, because it carries the information on its schema.  This is the fundamental
difference between the structural models and semistructured model.</p>

<h4>Semistructured data model</h4>

<p><i>A document</i> is a set of nodes. <i>A node</i> is either a leaf or an inner
node.  <i>Leaves</i> store data of a type (e.g. strings, numbers).
Each inner node is the starting point of at least one <i>edge</i>.
Each edge is labeled.  This label describes the nature of the link.
One of the nodes is distinguished as <i>the root</i>.  No edge points to the root.  The root represents the
whole document.  There must exist a path from to the root to each non-root node.  This
graph need not be a tree.</p>

<p align="center"><img border="0" src="images/4_200.png"></p>

<p>Nodes represent <i>objects</i>. Edge labels play two roles. Let us assume that
there is an edge from node <i>N</i> to node <i>K</i>:

<ul>
<li>first, the edge can represent <u>an attribute</u> of object <i>N</i>
<li>second, the edge can represent <u>a relationship</u> between objects <i>N</i>
        and <i>K</i>.
</ul>

<h4><a name="XML">XML</a></h4>

<p>The same data may be presented as text in the form of <i>an XML document</i>.
In such documents edge labels are stored as tags.  Between the opening and closing
tag there is the textual representation of the subgraph pointed by this edge.</p>

<pre>&lt;LIST&gt;
  &lt;PUBLICATION&gt;
    &lt;AUTHOR&gt;
      &lt;FIRSTNAME&gt;Lech&lt;/FIRSTNAME&gt;
      &lt;SECONDNAME&gt;Banachowski&lt;/SECONDNAME&gt;
    &lt;/AUTHOR&gt;
    &lt;TITLE&gt;Databases&lt;/TITLE&gt;
    &lt;YEAR&gt;1998&lt;/YEAR&gt;
  &lt;/PUBLICATION&gt;
  &lt;PUBLICATION&gt;
    &lt;AUTHOR&gt;
       &lt;FIRSTNAME&gt;Michał&lt;/FIRSTNAME&gt;
       &lt;SECONDNAME&gt;Lentner&lt;/SECONDNAME&gt;
    &lt;/AUTHOR&gt;
    &lt;TITLE&gt;Oracle9i&lt;/TITLE&gt;
    &lt;FORMAT&gt;Hardcover&lt;/FORMAT&gt;
  &lt;/PUBLICATION&gt;
&lt;/LIST&gt;</pre>

<p>The tags define the internal structure of an XML document.</p>

<h4>Associations between objects of the same XML document</h4>

<p>The XML data model allows linking objects. For instance a publication may
have many authors and one author may write many publications. We can introduce
object identifiers of data type <b>ID</b>.
<b>IDREF</b> and <b>IDREFS</b> are types of object references.
<b>IDREF</b> is a single pointer, while <b>IDREFS</b> is a list of pointers.
These types allow creating semistructured data in the form of an arbitrary graph.
As we told before, semistructured databases are not limited to trees.
Here is an example: a document with publications and authors.</p>

<pre>&lt;LIST&gt;
  &lt;AUTHOR Auth_id="LB" Publ_list ="BD1,BD2,BD3"&gt;
    &lt;FIRSTNAME&gt;Lech&lt;/FIRSTNAME&gt;
    &lt;SECONDNAME&gt;Banachowski&lt;/SECONDNAME&gt;
  &lt;/AUTHOR&gt;
  &lt;AUTHOR Auth_id="KS" Publ_list="BD1,BD2,SO"&gt;
    &lt;FIRSTNAME&gt;Krzysztof&lt;/FIRSTNAME&gt;
    &lt;SECONDNAME&gt; Stencel&lt;/SECONDNAME&gt;
  &lt;/AUTHOR&gt;
  &lt;PUBLICATION Publ_id="BD1" Auth_list="LB, KS"&gt;
    &lt;TITLE&gt;Databases. Server application design&lt;/TITLE&gt;
    &lt;YEAR&gt;2001&lt;/YEAR&gt;
  &lt;/PUBLICATION&gt;
  &lt;PUBLICATION Publ_id="BD2" Auth_list="LB,KS,AC,EM,KM"&gt;
   &lt;TITLE&gt;Databases. Lectures and tutorials&lt;/TITLE&gt;
   &lt;FORMAT&gt;Hardcover&lt;/FORMAT&gt;
  &lt;/PUBLICATION&gt;
  ...
&lt;/LIST&gt;</pre>

<p>Note that the associations described above are stored in the form
of attributes of the nodes.</p>

<p>The value of an <b>ID</b> attribute must be a name and must be
unique inside the document.
These values uniquely identify nodes of the document. A node may have at most
one attribute of type <b>ID</b>.</p>

<p>The value of an <b>IDREF</b> attribute must be the value of another attribute
of type <b>ID</b>. The value of an <b>IDREFS</b> attribute must be a list of
values of some attributes of type <b>ID</b>.</p>

<hr><h3><a name="Podsumowanie">Summary</a></h3>

<p>In lecture 4 we continued the course in the data modeling.  We presented
the following issues:</p>

<ol>
<li>two alternative notations for data modeling - IDEF1X and Chen's,
<li>extensions concerned with views and subcategories,
<li>patterns of model for hierarchical data and changes in time,
<li>object features in data modeling:
        <ul>
        <li>object-relational notation in MS Visio (object types and tables, records and collections),
        <li>textual notation ODL that resembles the syntax of object-oriented languages
                C++ and Java (classes-interfaces, relationships, collections,
                structural types, methods and inheritance),
        </ul>
<li>semistructured data model (graphs and XML documents).
</ol>

<hr><h3><a name="Slownik">Dictionary</a></h3>

<dl>

<dt><a href="#Notacja">Chen's notation</a>
<dd>The first notation for entity-relationship diagramming.  The entity is drawn
        as a rectangle, an attribute as a circle and a relationship as a diamond. It allows
        representing multi-argument and many-many relationships.

<dt><a href="#Model3">collection</a>
<dd>The model of a set of values. Apart from the item's membership it may
also store other aspects like the order of the members and multiple membership.

<dt><a href="#Modelowanie danych hierarchicznych">hierarchical data</a>
<dd>Data connected with hierarchical relationship, e.g. the structure of a company.

<dt><a href="#Odwrotny">inverse relationship</a>
<dd>A relationship that represents the inverse relation with respect
        to the given relationship.

<dt><a href="#Obiektowo">object-relational model</a>
<dd>Data model that apart from "flat" relations (tables) includes also
         complex data structures defined by objects types or classes
         known from object-oriented programming.

<dt><a href="#Tabela">object table</a>
<dd>A table that stores objects of a given object type (class).
      The transition from a relational table to the object table is driven
      by rule <i>row -&gt; object</i>.  As the result of this transformation
      every row of a table gains the identity and the methods and becomes an object.

<dt><a href="#Obiektowo">object type</a>
<dd>The definition of a class objects. A pattern of objects that includes
        concepts like attributes of complex types and methods.

<dt><a href="#ODL">ODL</a> (Object Definition Language)
<dd>An object modeling language.

<dt><a href="#Ds">semistructured data model</a>
<dd>A general data model where the structure of the data is defined
      as a graph with nodes and edges.

<dt><a href="#Hierarchia">subcategory</a>
<dd>A sub-entity.  An entity connected to the super-entity by a
      subcategory relationship.

<dt><a href="#Hierarchia">subcategory relationship</a>
<dd>A relationship that connects the super-entity with its sub-entities
      that extend its properties.  Such a relationship may be either complete
      (if the union of the sets of the instances of subentities is the
      set of the instances of the super-entity) or incomplete (otherwise).

<dt><a href="#Modelowanie czasu">time</a>
<dd>The aspect of changes of data in time.  It concerns
        the changes of values of attributes, instances of relationships and entities.

<dt><a href="#XML">XML document</a>
<dd>A textual document enriched with tags that describe the meaning of its
      data.  It is a textual representation of data in the semistructured model.
      It is used to integrate data from several databases, to separate
      the document from its visual representation and to transfer data
      over the Internet.

</dl>

<hr><h3><a name="Zadania">Exercises</a></h3>

<p>Some of them appeared also in the text of the lecture.</p>

<ol>
<li>Using Chen's notation draw an entity-relationship diagram for the zoo. Include
          animals, their keepers and feed.  The model should contain the following relationship:
          an <i>animal</i> eats <i>feed</i> served by a <i>keeper</i>.
<li>Build a categorization of flying objects.  What properties are common? What properties are specific?
<li>The set of the components of a car constitutes a hierarchy based on the containment
        relationship (a component aggregates other components). Draw a data-relationship diagram of this hierarchy.
<li>Draw a "temporal" data model for the cadastral data.  We are interested in the
         relationships between owners and real estates. Take into account that sometimes estates
         are destroyed and owners die.
<li>Propose a data model for the problem of changes of entities in time.
            Include the relationship between instances of entities and
            their versions that change in time.
<li>Create an object-relational definition of collection "Set of contacts". A contact
           is a record that indicates both the kind and the data, e.g. &lt;kind = "private e-mail",
           data = "ian@mailserver.edu"&gt;. Draw an object relational-model of a person with
           an attribute that stores the contacts to this person.
<li>Make the previous exercise in the  relational model. Draw appropriate
         entity-relationship diagram.
<li><a name="exercise8">Create an object-relationship diagram by replacing
       the relationships by collections on the following diagram:</a></p>
       
       <p align="center"><img border="0" src="images/4_112.png"> </p>

       <p>What a kind of collection should be used?</p>

<li>Write an ODL definition of classes <i>Employee</i> and <i>Project</i>
          and the many-many relationship between them:
          "An <i>employee</i> works for one or more <i>projects</i>.
          A <i>projects</i> is developed by one or more <i>employees</i>."
</ol>
