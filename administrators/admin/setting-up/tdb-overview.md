---
layout: page
title: '"Title Database" (TDB) Files: Use and Syntax'
---

As mentioned in the [introduction](../introduction), a **LOCKSS Title Database** file describes lists of archival units (AUs) that can be preserved in the network, including information linking AUs to plugins and parameters needed by the plugins, and essential identifying or bibliographic data.

The name title database is historic and implies an interactive database of some kind, but it is only a descriptive file -- there is no database system at this level.

"Title Database” (TDB) files are  human readable text files that define archival units for processing by the LOCKSS daemon.  One or more TDB files are processed by a script-controlled java program that converts the TDB1.0 syntax file in to  XML format for a LOCKSS daemon to load.  

The use of human readable TDB files to store information about the network AUs is a useful abstraction because;
- it allows the data to be stored in a repository with all the benefits of historic logging, and concurrent local editing.
- it allows for quick insight in to what content is available to the network.
- it allows for logical organization of large amounts of available content in to multiple discrete files.
- it puts a validation buffer in between human editors and the running daemon configuration
- it allows the update of daemon content configuration to occur on a regular, programmatically controlled, schedule

**Archival Units**
“Archival Unit” is the LOCKSS term for an “Archival Information Package” (AIP).  An Archival Unit represents a defined set of content with an identifer that is unique within the system and whose defined contents will be consistent across all nodes in the network.  The AU should become stable after a time (no more content will be added).  
The abstract concept of an AU could be:
- Volume 5 of the Journal of Something published by Publisher X
- All the books published in 2014 by Publisher Y
- All the items transferred in to the system by Publisher Q in Q1 of 2019 

An AU definition must identify how the LOCKSS network will be able to ingest the content, specifying the plugin and values for all the parameters the plugin requires. This AU definition is turned in to an immutable “auid” which is unique within a network. The auid is an encoded string representation of the plugin, its parameters and their values. While the auid contains all the information necessary for the daemon to ingest the content, the TDB file also maintains essential identifying or bibliographic data and the status of the AU within the system - is it ready to be preserved, already in process or no longer available for collection from the source?

For example:
The abstract AU: Publisher X, Journal of Something, Volume 5, ingested by the plugin `org.lockss.plugin.SampleJournalPlugin`, from the start url of: `https://www.pubx.com/something/`
might looks something like this. `org|lockss|plugin|SampleJournalPlugin&base_url~https%3A%2F%2Fpubx%2Ecom%2F&journal_id~something&volume_name~5`

**Defining AUs in TDB files**
TDB files are hierarchical and must ultimately resolve at a minimum hierarhcy of a 
-Publisher
 -Title
  -AU
The hierarchy is maintained through `{}` (curly bracket) definition blocks which can be nested arbitrarily deep for inheritence of common vaues.
Publisher, Title and AU definitions exist as semi-colon separated definitions within `<>` (angle bracket) pairs. 
The values required for an AU definition are defined by an “implicit” statement.

In it’s simplest form, for a journal, a valid TDB file could look like this:
```text
{
  publisher <…publisher definition goes here>
  {
    title <…title1 definition goes here>
      <au1 of title1 definition goes here>
      <au2 of title1 definition goes here>
  }
}
```
To show a more complete definition from our example above:
```text
{
  publisher <
    name = Publisher x
  >

  plugin = org.lockss.plugin.SampleJournalPlugin  
  implicit < status ; year ; name ; param[volume_name] >
  param[base_url] = https://www.pubx.com/

  {
    title <
      name = Journal of Something ;
      issn = 1111-1111 ;
      eissn = 2222-2222
    >
    param[journal_id] = something
  
    au < down ; 2006 ; Journal of Something Volume 5 ; 5 >
  }
}
```
The hierarchy for this TDB file means that the "Publisher X” is the publisher for all nested {} blocks and the “Journal of Something” is the journal title for all the AUs in its nested {} block.
Definitional Parameters - which are items required by a plugin, and which are indicated using the format `param[key_name]` are also inherited so the AU shown would inherit the 
`plugin` and `param[base_url]` from the publisher block
`param[journal_id]` from the title block

The implicit definition line: `implicit < status ; year ; name ; param[volume_name] >`
indicates what each field in the semi-colon separated AU definition means.
The last undefined parameter required by this particular plugin is one of the items in the AU definition line.
`param[volume_name]`

This makes sense because for a given publisher journal that is being harvested by the same plugin mechanism from the same origin, the only item that will change from one AU to the next is the scope of the content to be collected - in this case the volume. 

In this example, because the AU represents a scholarly publication, the TDB file also contains bibliographic metadata (issn, eissn) but this information is optional.  It does provide metadata to the system that can be used to resolve queries and also provides a human-readable source of information about what is being preserved. 

For a file-transfer plugin which might be used to preserve an opaque set of arbitrary content without bibliographic information, a simple TDB file might look like this:
```text
{

  publisher <
    name = Publisher FT, Inc ;
    info[network_id] = 1234
  >
  
  {
    title <
       name = Publisher FT, Inc Source Content
    >
    
    plugin = org.lockss.plugin.SampleSourcePlugin
    param[base_url] = http://www.ingest-site.com/sourcefiles/pubft-released/
    
    implicit < status ; year ; name ; param[dir] >

    au < crawling ; 2019 ; Publisher FT, Inc Source Content 2019_1 ; 2019_1 >
    au < crawling ; 2019 ; Publisher FT, Inc Source Content 2019_2 ; 2019_2 >

  }

}
```
Again, the AU is inheriting a specific publisher definition and title definition, but in this case, the title is just a designation of what the opaque collection of content represents.
The plugin in this case requires ony two parameters - a start_url and a “dir” which designates the unique batch of content -  in this case is a  subdirectory below the start_url to narrow the ingest.

Another new item in this example is the use of any arbitrary information key value protected with the `info[]` syntax.  In the example it represents a unique identifier that the people managing the network might find useful to keep track of publishers programmatically. 

**Implicit statements**
In addition to any parameters required by the plugin each AU implicit statement should contain at least three other items:

 - status. - this is an indication of the state of this AU in the preservation process. See the section below for possible values.  This status informs the LOCKSS daemon’s behavior with regards to this AU.
 - name - this is a human readable name that is used to identify this content in the LOCKSS user interface. It should be unique in the system (for clarity) but is any arbitrary string.
 - year - this is the “publication year” of the content. It is useful for queries, bibliographic information and in the case of file-transfer content which might span many years, it should represent the year of delivery to the system.

Additionally, it might also contain optional further key-values that, while not used by the plugin, might be helpful to catalog the specifics of the content.  
<TODO: information here about whether these are used in any way by the daemon, (bibliographic info?) or whether they’re just for use by the TDB tools>
 - author
 - doi
 - volume
 - isbn

The ordering of the keys in the implicit statement are arbitrary. By custom, the status value comes first.   The string values given in an AU definition <> must match the ordering of the implicit statement.

**Status Values**
```text
expected+---->|exists+---->|manifest+---->|testing+---->|ready+---->|released+---->|down+---->|superseded+
```
expected, exists, manifest, testing and ready indicate content that has not yet been added to any node in the network.
released, down, and superseded indicate content that exists on at least one node in the network.

an AU that is in a released state (released or higher) should never be moved “back” to a pre-release state

 - expected  - AU definition is written, and the content is expected to be availalbe at the origin site but has not yet shown up
 - exists - AU definition is written and the content does exists at the origin site
 - manifest - AU definition is written and the content does exist at the origin site and it is available for preservation (proper permission,  plugin is available, etc)
 - testing - optional state to indicate someone is testing the collection of this AU
 - ready - optional state to indicate that someone has already tested the collection of this AU and it is ready to be released

 - released - this AU has been released for preservation by the network and is available to add to any node in the network
 - down - this AU is no longer preservable at the origin site
 - superseded - this AU exists on nodes in the network but there is now a different version of the abstract definition of this content that is considered more complete (perhaps using a different plugin or from a different site)


**Nested Inheritence** (and why it might be useful)
For practical reasons to manage a large number of publishers, we create a separate TDB file for each publisher and often for each plugin that publisher uses. They might require multiple plugins either because they provide content from a variety of origins (books vs journals or a combination of harvest and file-transfer) or because the content has changed platform over time.  Our convention is to name the files by publisher name:
publisher_x.tdb with variants to help identify the contents,
publisher_x.books.tdb
publisher_x.filetran.tdb

It doesn’t matter how many different TDB files there are as they are combined in to a single XML file for use by the daemon (although there is an optional subdirectory feature - see section below)
Hierarchical inheritence only applies within one TDB file.

This might be a useful feature for the following reasons:
1) You might choose to have multiple plugins in one file:
```text
{
<publisher>
{
 plugin.for.journals.by.harvest
   <title1>
     {
      <au>….<au>
     }
   <title2>
   {
     <au>….<au>
   }
}
plugin.for.filetransfer.of.special.content
<title>
{
  <au1>
  <au2>
 }    
}
```
2. You might choose to change a parameter within a title block to adapt for a change
```text
{
<publisher>
  plugin = x.y.z
  param[base_url] = https://foo.com/
  {
       <title>
       {
         param[journal_id] = old_form_id
 <au>
        }

       {
         param[journal_id] = new_id
            <au>
        }
   }
  
}
```

**Common issues**
<> definitions are semi-colon separated, not terminated


**TDB tools and getting information out of TDB files**


**TDB1.0 Syntax Cheat Sheet**

 - `attr[key]` - Attributes - used by some plugins to handle…. more here.
 - `comment[comment-string]` - deprecated, use #
 - `hidden[key]` 
 - `info[key]` - arbitrary information that can be parsed out by TDB processing tools
 - `param[key]` - Definitional Parameters defined by the plugin used by the AU. They must be inherited or defined in the AU definition as per the implicit statement.

```text
{
publisher <>
title <>
au <>
}
```
