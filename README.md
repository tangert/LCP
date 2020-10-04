# LCP: Link Collection Protocol

LCP is an open standard for curating, editing, and sharing collections of URIs.

It can be used to build standard data interchange methods between  bookmarking services, curation services, file transfer tools, file systems, collaboration tools, news aggregators, and more.

The base is supposed to be very simple. Any kind of metadata can be attached on top of this and extra operations can be made, but the core is simply about 

# Core concepts
## Data structures
### Link
```typescript
Link {
  URI: string;
  id: string;
  data?: Dictionary<(string | number): (string | number | boolean)>
}
```
Links are the **core primitive.**

IDs are created through a URI hash.

Data is optional can be stored in them as key/value pairs. This includes metadata like name, description, time accessed, etc. Data is flat and cannot include nested dictionaries or lists.

### Collection
```typescript
Collection {
  id: string;
  items: Set<(Link.id | Collection.id)>;
  data: Dictionary<(string | number): (string | number | boolean)>
}
```
Collections are the core abstraction

Collections are unordered collections of unique Link IDs or Collection IDs.

Collection IDs are a hash of its items’ IDs and its data. This means that two people can create collections with the same items.

Collections are flat. If you want to implement nested collections, simply add other collection IDs to the set.

Data is required and can be stored in them as key/value pairs. This includes metadata like name, description, time accessed, ordering of items, etc. Data is flat and cannot include nested dictionaries or lists. 

## Operations
There are several key operations that can be performed on collections:

**Add**: you can add link IDs, collection IDs, and/or metadata into a collection.  

**Remove**: you can remove link IDs, collection IDs, and/or metadata into a collection.

**Branch**: Branching creates a copy of the collection with a reference back to the original collection. 

**Merge**: Merging takes two collections and turns them into one.

All actions operate are immutable, so you can run back each operation to go back to any previous actions.

## Open questions
???????
