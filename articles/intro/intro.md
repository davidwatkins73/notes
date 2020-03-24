# Introduction to Waltz


## Background

Many organisations are frustrated with the quality and coverage of their enterprise 
architecture information. Data is often gathered in an ad-hoc fashion and stored in multiple 
disconnected systems with limited user bases.  The data contained within these systems is often 
stale and has limited coverage, when users attempt to answer business questions they must 
navigate through multiple systems and often need to initiate new ad-hoc data gathering exercises 
to pull together the information needed.

Waltz, which was started as an open source system in 2015, is designed to address these issues.  Its 
approach is to connect these data sets and open them up to all employees.  By allowing employees to 
view, manipulate and modify or crowd source data capture, we believe that we can greatly improve the 
current status quo of enterprise information management.


## Overview

### Core Entities 

Waltz's revolves around several basic entities:

- _Organisational Units_:  the hierarchy of departments and divisions within the enterprise
- _Applications_ and _Actors_:  applications are used when describing the technical landscape and are 
    typically owned by an organisational unit.   Actors are used to define internal and external 
    non-application entities. For example the _Bank of England_ may be an external actor and the _Chief Risk
    Officer_ may be an internal actor. 
- _Data flows_:  these are flows of data between applications and actors, the flows are enriched with
    data types and can be optionally documented down to the detailed specification level.
- _Taxonomies_:  Waltz allows clients to specify many types of taxonomies which are then used to define and
    rate how other entities fit within the organisation.   
- _Change Initiatives_:  Enterprises are not static and so change must be accounted for.  Amongst the 
    mechanisms Waltz offers are Change Initiatives which describe specific sets of scheduled changes.
- _People_:  Waltz is particularly interested in how people are related to the above entities. 

These core entities (and many other supporting entities) form the basis of the Waltz data model.  Flexibility
in the model is offered by specific, client definable, extension entities.  Having a strong, opinionated model 
allows Waltz to do a lot more 'out of the box' without requiring heavy customisation which often yields 
unsatisfactory results and increases delivery times.

Combining these entities allows us to describe an individual application, a simple example would be:
 
> '_Application_ `Scribbler` is owned by the _organisational unit_ `Operations` and performs 
> the `Confirmations` and `Settlements` functions from the `Business Function` _taxonomy_.  
> The application is managed by `Alex Bridgers` and has 3 developers.  It is connected to
> the application `Rolodex` for `Counterparty` data and has another, outgoing, _data flow_ 
> to the `DTC` _external actor_.
>  
> Technically the application comprises an Oracle database, MQ Series middleware and is 
> hosted on a cluster of Tomcat instances running on top of Solaris.  The total costs 
> for the application are `$300K` per year.
>
> The application is mentioned in an upcoming _Change Initiative_ to modernize database stacks 
> which is being led by `Ingrid Lipford`. 


### Grouping

A large part of the power of Waltz comes from its ability to dynamically aggregate entities to provide
custom views over the enterprise data set.  We can easily navigate to a grouping entity to see
breakdowns of all the other entities they reference.  For example we can view the _Organisational Unit_
`Operations` and see all applications with their costs, data flows, related taxonomy mappings and change
initiatives (and others).

There are many different kinds of grouping entities in Waltz. The common ones, some of which we have already 
mentioned, are:  

- Organisational Units
- People: e.g. all entities initiatives that a `Alex Bridgers` is related to.
- Taxonomy items: e.g. all entities relating to the business function: `Settlements`. 
- Data types: e.g. applications consuming/producing particular classes of data

These groupings also aggregate up hierarchies.  Looking at a senior manager shows all entities his employee
tree is responsible for.  An organisational unit aggregates all sub-units, a data type aggregates child types etc.

In addition to these in-built '_natural_' groups, Waltz allows users to define ad-hoc custom groups.  These
are frequently used to do custom analysis, often to support specific project based work.  These custom groups
can be kept private or published for the entire organization to view.  

By analysing the usage of custom groups we find that hidden taxonomies are often revealed.  In a recent example
we were looking through the custom groups and noticed a large number were capturing applications directly (or 
indirectly) involved with various banking regulations.  This suggested that a new taxonomy could be created and 
applications would be mapped explicitly to regulations rather than implicitly via a custom group.  


### Flexibility

Although Waltz provides a fixed, opinionated, data model there are several entities designed to allow flexible 
usage. These include:  

Waltz _Surveys_ are one of the main entities designed for flexibility. These allow users to define a template, 
consisting of a list of questions - each of which can have either simple answer types (text, numbers, enums etc) or 
relate to another entity in the Waltz model (e.g. applications or taxonomy items).  Once a template is prepared it can 
be issued to a set of users derived from the Waltz model. As an example we may wish to issue a survey to all 
`application managers` who have an application referenced by the `Operations` org-unit grouping entity.

Two examples of the use of surveys are to support programme governance:

- Programme Governance: Each _Change Initiative_ has a fixed survey which asks the programme owners how the work 
  relates to the overall bank strategies. Is it strategic or tactical, are we knowingly taking on technical debt etc.
- Electronic Communications: In a highly regulated industry it is important to know which applications support 
  person-person communications.  Surveys are used to help the compliance department understand the risk and formulate
  the appropriate actions to ensure all applications adhere to policy.  
  
Additionally Waltz supports custom _Assessments_ for applications.  These simply take the form of a drop-down 
value (with comment) but have been proven to be very useful for extending the Waltz model.  A recent example
is the `Sensitive data` assessment, which indicates if an application contains data of a highly confidential 
nature.  Another recent example is an ALM flag which indicates if an application is production ready. 

To support numeric data sets, Waltz uses _Indicators_ which capture metrics against core entities (typically 
applications). These can then be rolled up via the groups and their values can be charted over time.  These
have been employed to track various key performance/risk indicators and also to help track adoption of various
policies (e.g. on-boarding to internal cloud platforms).


### Future State

Enterprises change over time and Waltz helps to describe these changes.  A variety of mechanisms exist to support 
this.  _Change Initiatives_, which have already been mentioned formally describe projects and programmes which will
impact the enterprise.  Applications, their individual flows and taxonomy mappings can also have planned retirements,
commencements and replacements.   To help visualize these changes Waltz supports Roadmaps where a sequence of future
states can be documented.  

Note that this area of Waltz is undergoing active development and is evolving rapidly with new editing screens and 
visualisations being planned for the coming months.

### Much more

As this is only a brief introduction to Waltz there are many topics which have not been covered.  In particular 
Waltz is aiding with Data Lineage by providing a simple, constrained diagram editor which allows users to quickly
illustrate data flows throughout the bank.  These diagrams build upon the underlying model by suggesting only those
connections which already exist.  Once a diagram is completed, it, in turn, can be used as a grouping entity by 
analysing its bill of materials.


## Evolving Waltz

Waltz is being actively developed.  Focus areas for the coming months are around enhanced support for Surveys, 
data lineage, future state and cataloging opensource license and security vulnerabilities.

A key challenge we face is evolving Waltz to better support the transition from traditional application architectures
to more modern architectures such as micro-services and lambdas.  As applications are broken apart we need to 
consider how we can maintain a clear picture at the enterprise level and ensure that adequate governance, policies 
and procedures are in place.


## Next Steps

Waltz is a community driven project but we are always willing to assist teams in evaluating Waltz for their
organisations.  Please reach out to us via the FINOS mailing lists or directly on our issue tracking system for
help and assistance.

