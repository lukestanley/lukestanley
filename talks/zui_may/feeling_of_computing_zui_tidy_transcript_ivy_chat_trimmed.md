# 🗺️ Feeling of Computing demo transcript: 2D visual language topic map ZUI

**Recording section:** starts just after `31:57`.

**Hosted by Ivy Reese (previously known as Ivan Reese).**

**Tidying note:** filler words have been removed, automatic subtitle errors have been corrected, and the wording has been kept close to the spoken demo.

## 👋 Introduction

**Ivy Reese:** Ivan, thank you for presenting. That was super, super cool. Luke, whenever you’re ready, you’re up.

**Luke Stanley:** Hello. I’m interested in the problem of how we, as human beings, can get a good mental model of what is going on. I want to understand things and make use of our high-bandwidth visual centres, which are very good at interpreting information efficiently.

I’m interested in how things like embeddings, generated categories, different kinds of relationships, and graph structures can be used to make useful visualisations that do not look like a mess.

## 🧩 Why the first map looks messy

Speaking of which, this looks like a mess.

This is what happens when a data set of topics is projected down from high-dimensional space into 2D space. We should expect it to be a mess. We should expect overlap. By default, there is not a clean reduction down to two-dimensional space. That should not be surprising, but it is really annoying.

The reason this happens is that each item is mathematically just a point. It does not have any dimension in the two-dimensional representation unless that dimension is deliberately added.

When we add that dimension, we then have to decide what to do about overlap. One common thing people do is use a force-directed effect: if one node is too close to another node, the nodes push themselves apart. But then we have to tweak all kinds of fiddly variables to keep the semantic integrity authentic.

It is also a bit of a kludge to switch to a different kind of algorithm at presentation time, without any consideration of the semantic embeddings themselves.

## 🧭 Finding non-overlapping positions without losing meaning

I have settled on an approach where the process happens in multiple stages, but those stages are aware of the semantic relationships between the nodes. They use those relationships to find a good non-overlapping position for the nodes.

That gets us something a bit like this. It has no overlap, which is good.

These topics are from Samuel Pepys’s life and the things in it. I took them from a manually made list.

This is a lot better. The semantic integrity is actually quite good.

For example, there is the bladder-stone surgery he had. The stone was a personal concern of his. He had frequent pains, especially when he got cold, and it became one of his anxious preoccupations.

Another one is gold. Gold fits into a psychological kind of cluster for him. Likewise, his main occupational duties are in a place, and there is a Navy cluster. There is also the Great Fire of London, with a fittingly emptier area around it.

So the semantic integrity is good, but it is still not very intuitive.

## 🎨 Adding visual language with generated icons

These days we have image generators, so I semi-manually and semi-automatically generated icons for the topics. That probably helps a little bit.

What would be more useful is a zoomable user interface, where we can look at different things at different levels and see different zoom states, very much like what Ivan Lugo was talking about earlier.

I have not done much with that yet. There is a lot that could be done.

I do have large-language-model-generated salience scores for some of the topics. I use those to adjust the scale and opacity of some nodes.

For instance, there is a woman who was loosely related to some people in this area through gossip. She is not as central to Pepys’s life. Her centrality is low, but she is still an interesting figure. She is not at full opacity, because she is not worth foregrounding from the broad overview perspective of his life.

When I am zoomed out, the map shows things that are high-rank and high-salience, or some combination of those. When I zoom in, it shows more nodes without fading them out.

That is basically as far as I have got with that.

## ❓ Question: can the interface be used to express things?

**Ivy Reese:** I’m going to do the thing and jump in with a question in the middle. That’s the format.

I have this weird personal belief: any interface that presents information, or presents a visualisation of something, is also potentially a good interface through which we can express something.

There are two sides to every interface. So far, you have talked about what this interface is revealing, what it is showing, and how it relates to higher-dimensional spaces. I’m curious what you have thought about with respect to doing expressive work through this interface.

## 🔁 Projecting back and arranging meaning

**Luke:** Yes. We can actually project back. There is a popular library called `UMAP Learn` that lets us do that.

UMAP is a common solution for dimensionality reduction of high-dimensional data. It does not have a global objective. It is mostly local, which means it might mess up how things fit together in aggregate. That is not ideal.

But one cool thing it can do is project back. It can let us predict what high-dimensional representation, or high-dimensional embedding, would make sense if, for example, I put something new here. What might it mean, based on everything else the system knows about the space? How might it relate to these personal things, these social things, and these work things?

That can absolutely be done.

It is also sometimes useful to do drag-and-drop image-collage work. People often prefer paper for this kind of reason. It is a real pain, when working digitally, to lose the ability to arrange things freely.

So yes, I think that would be powerful.

Another common problem is that the orientation can flip around whenever one of these maps is regenerated. There are different ways of doing dimensionality reduction, and they are often based on a random seed, or on other stochastic things, that make it hard to keep the same orientation.

I perform a rotation that anchors two points. When I regenerate the map, the entire map coheres, which is really nice, especially for adding or removing points.

## 🧮 Question from Marek “maf” Rogalski: can nodes occupy regions instead of points?

**Ivy Reese:** We have time for maybe two more questions. If anybody in the audience has something they would like to ask, just unmute and go right ahead.

**Marek “maf” Rogalski:** I have one question. I really liked what you mentioned about reverse-projecting into high-dimensional spaces.

Mathematicians like to simplify things into spherical cows. When modelling things in 2D, we model everything as points. But in an actual 2D space, things also have dimensions. They have shapes.

We also think in categories. On the screen, in a user interface, many of those things could be grouped together by putting them in a box, or surrounding them with a line. That is how many mind maps are presented.

Are there any ways of quantifying the size of those embeddings on screen, so they are not just points and can be assigned a region of space?

## 🗺️ Regions, Voronoi maps, and hidden structure

**Luke:** Yes, that definitely could be done. I have not done that yet. I do not have it saying, for example, that this belongs to a work cluster. I do not have that kind of membership information at the moment, but it is doable.

**Marek “maf” Rogalski:** Just looking at the 2D screen, I guess something like a Voronoi map would be the easiest approach. But there is this underlying structure in the projection, where different sections of the embedding space occupy different parts of the screen.

**Luke:** Yes. In terms of what people are doing with pretrained models and embedding spaces, they are finding out some really cool things recently.

Particular geometric patterns are being shared among completely different models. We are starting to peer into that geometric representation space that they have learned in high dimensions.

People are interested in that from a machine-learning interpretability and safety perspective as well.

**Marek “maf” Rogalski:** Thanks.

## 🌐 Question from Ivan Lugo: do meanings have shared shapes across languages?

**Ivy Reese:** We have time for one more question.

**Ivan Lugo:** I have a quick one too.

That last point about high dimensionality and language reminds me of an article I saw on Hacker News, or somewhere around there. It was an arXiv paper, and it talked about that very thing. Researchers had found that across a number of languages, there was a very definite pattern to certain words, word groups, and semantics.

One thing that this project is showing is that this is a kind of language. I’m looking at Dining, Great Fire, and Prize Goods, and there is a certain visual theme and linguistic theme to it.

I’m curious because you have clearly operated on this from different texts and different spaces. Have you seen linguistic patterns in the way you have built this out? Have you tried to visualise that? For instance, in this case Dining means this, but for another person Dining means that. Have you been able to express that at all?

## 📐 MiniLM, salience, and Manifold Steering

**Luke:** One thing I was looking into was whether I could use off-the-shelf MiniLM embeddings to do salience prediction by extracting a few dimensions and maybe multiplying some of them together.

That worked pretty well.

I would have a data set of different kinds of life events at different scales. Then we could zoom in on ways to slice the normal embeddings we get for a piece of text, and use that to predict something like salience in a really efficient way.

Then the Manifold Steering paper came out. It basically showed things like different dates mapping to a particular shape inside large language models. They look at things like weekdays in different language models corresponding to certain shapes.

So I put aside my naive way of finding a few columns that had useful parameters, and tried to get my head around the whole higher-dimensional geometry they are using, because it seems more fundamental.

If that answers your question.

**Ivan Lugo:** It does exactly. That paper is perfect.

We are finding that things have a definitive shape. Whether I am speaking Italian, German, French, English, or some weird mixture, if I say a word like good, bad, evil, or positive, it is going to have some kind of shape.

When I am talking to you and I can see that shape, that is another dimension we can communicate across.

That is very much why I am trying to build my whole system. What you are describing is that we need a visual medium for it. This is really cool to see. It shows how it works on the data side. Thank you. Very cool.

## 🧱 Visual language and Robert Horn

**Luke:** I also love to point to Bob Horn, Robert Horn, who coined the term visual language, or at least popularised it. He wrote a book about it.

He is a wise elder gentleman who lives somewhere in San Francisco, as far as I know. I do not know how active he is at the moment. Maybe a decade ago, he published some really cool PDFs to `archive.org`, after they had already scanned his visual language book.

He has a very clear walkthrough of how this can make sense between us. How can somebody have an inkling of what this is about by looking at it, without actually knowing about Pepys and his life?

There are a whole load of language components that he talks about and explains: why it is important to have text, why it is important to have visuals, how they fit together, and what level of abstraction works.

His book is probably from the 1980s or 1990s. I do not know how well-known it is, but it is out there on `archive.org`, and he posted it as himself.

I encourage people who are wondering about the grammar of visual language to check that out, because he has thought about this stuff a lot.

People have been using this kind of thing actively for things like studying pandemics. How do we communicate with hundreds of different people who have different specialisms in different bio-risk areas? How do we get them to collaborate and share their findings in a useful way?

We might make a mess map, or an information mural, or something like that. There is a defined language that has been mapped out to some degree. That does not mean there are no new forms of language, or new ways of doing things, that we are discovering as we make new media. But it is a really useful body of work to check out.

## 👏 Closing

**Ivy Reese:** That is probably a good note to end on. Luke, thank you very much for sharing what seems to be promising first steps on a project. I will be excited to see this unfold in the coming months.

Thanks to Jasmine Otto, Ivan Lugo, and Luke for demoing today. Thanks everybody for coming out, and we will see you next time.

## 💬 Relevant chat notes

| Time | Shared by | Note | Relevance |
|---:|---|---|---|
| `07:50 PM` | Marek “maf” Rogalski | “I wish I had something like that when watching Dark :P” | Shows the map idea landing as a way to understand complex narratives. |
| `08:01 PM` | Ivan Lugo | [Robert Horn, *Visual Language*](https://www.amazon.com/Visual-Language-Global-Communication-Century/dp/189263709X) | Book link shared immediately after the Robert Horn / visual-language discussion. |
| `08:01 PM` | Ivan Lugo | [Robert E. Horn](https://en.wikipedia.org/wiki/Robert_E._Horn) | Background link for Robert Horn. |

