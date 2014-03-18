##HAT: Hypermedia Adventure Text

####Table of Contents
1. Inspiration
2. High Level Description
3. Entities

####Inspration
Hypermedia Adventure Text is a simple experiment in designing a basic
hypermedia type. With types out there for specifically designing mazes
I thought it would be cool to design a type for old school text adventure
games ala [Zork](http://en.wikipedia.org/wiki/Zork). The type itself is a
subset of [Siren](https://github.com/kevinswiber/siren). This is because
there is already tooling and a community present around that type. The
eventual goal of this type is to be able to represent a text game like
Zork through an HTTP API.


####High Level Description
The concept of linking and representing the state of entities in hypermedia makes it a great
candidate for creating old text based adventure games like Zork. By linking through the main kind of entity
in HAT called storypoints we can traverse back and forth through and adventure story. By giving each storypoint
a set of actions to perform we can let the user know what they can actually do in that specific area.

####Entities

Entities in HAT will be structured with the following top level properties.

1. `"class"` - Possible classes in a proper HAT implementation will be `"story"`, `"storypoint"`, `"character"`. These
classes are used to describe the context of the current entity returned from the API.

2. `"properties"` - Data on the entity you are retrieving. For storypoints you'll want to have two properties. One is the
current location in the game world, and the other is the message that will be printed out to the console.

3. `"actions"` - These are actions that can be taken by the player in the game world. Specific to different story points.

4. `"links"` - These are required for navigating through the games various story points.

Example
```
{
  "class": ["storypoint"],
  "properties":{
    "message": "You are standing in an open field west of a white house, with a boarded front door. There is a small mailbox here.",
    "location":"West of House"
  },
  "actions": [
    {
      "name":"open-mailbox",
      "title":"Open Mailbox",
      "method": "GET",
      "href":"http://zork.io/story/1/open-mailbox",
      "type":"application/x-www-form-urlencoded"
    }
  ],
  "links":[
    { "rel": ["self"], "href":"http://zork.io/story/1" },
    { "rel": ["next"], "href":"http://zork.io/story/2"}
  ]
}
```

#####A Note on contributions

I would love if others would like to contribute! Simply issue a pull request and we can talk out anything. This is
not a serious hypermedia project / type by any means. However, I think it's a neat way to explore the concepts
outside of a CRUD type API.
