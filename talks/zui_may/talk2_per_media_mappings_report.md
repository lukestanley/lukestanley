# Feeling of Computing ZUI per-media mapping report

## Database check

- Tables found: `embedding, existing_topic_embedding, manifest, model_info, segment, source`.
- Segment count: `712`.
- Segment types: `chapter`=15, `key_point`=70, `tidy_paragraph`=73, `tidy_section`=14, `topic`=50, `vtt_cue`=297, `vtt_ngram_2`=49, `vtt_ngram_3`=48, `vtt_ngram_5`=46, `vtt_sentence`=50.
- Embedding models: `all-minilm:latest`, `embeddinggemma:latest`, `paraphrase-multilingual:latest`, `qwen3-embedding:0.6b`, `qwen3-embedding:4b`, `qwen3-embedding:8b`.
- Existing topic embeddings match the topic catalogue IDs exactly: `50/50` topic IDs overlap.
- Existing topic embedding self-match cosine is high, e.g. Qwen3 8B mean `0.967185`; this suggests the imported map-topic embeddings and current topic text embeddings are compatible.

## Timebase note

The JSON uses **local cut-video/VTT seconds** as the primary timeline. The SQLite manifest says subtitle zero is `00:31:55`, but the later re-encode command starts from the best original with `-ss 00:31:55` plus a second `-ss 00:00:04`, which makes the final accurate cut start around `00:31:59`. For original YouTube timestamps, the JSON includes corrected values computed as local time plus `00:31:59`.

## Media layers mapped

| Media layer | Mapping available | Notes |
|---|---|---|
| Video MP4 | chapters, VTT cues, speaker turns, visual anchors | local seconds are primary |
| Corrected VTT | cues, sentences, n-gram windows | used as timed alignment spine |
| Tidied transcript | sections and paragraphs to timed windows | semantic alignment via embeddings |
| Topic catalogue / map nodes | topics to timed VTT windows, short windows, sentences, and chapters | includes `icon_path`, cluster, rank, centrality |
| Key points | outline/table/takeaway rows to timed windows and chapters | useful for UI side navigation |
| PiP | speaker turn anchors | manual audit derived |
| Main screen visual | map-state anchors | manual audit derived |

## Best tidy-section to video chapter mappings

| Section | Video time | Chapter | Score |
|---|---:|---|---:|
| 👋 Introduction | `00:00:00.838`-`00:00:52.468` | Intro: good mental models, high-bandwidth visual cognition | 0.776 |
| 🧩 Why the first map looks messy | `00:00:52.468`-`00:01:35.655` | Why the first map looks messy (high-D to 2D, overlap, force-directed kludge) | 0.920 |
| 🧭 Finding non-overlapping positions without losing meaning | `00:01:35.655`-`00:03:57.121` | No-overlap layout that keeps semantic integrity | 0.782 |
| 🎨 Adding visual language with generated icons | `00:05:24.413`-`00:06:14.406` | Adding visual language: generated icons | 0.864 |
| ❓ Question: can the interface be used to express things? | `00:07:54.548`-`00:08:12.087` | Q (Ivy): can the interface express, not just reveal? | 0.836 |
| 🔁 Projecting back and arranging meaning | `00:08:12.087`-`00:10:12.774` | Projecting back with UMAP: where would a new thing land? | 0.906 |
| 🧮 Question from Marek “maf” Rogalski: can nodes occupy regions instead of points? | `00:11:35.105`-`00:12:55.193` | Q (maf): nodes as regions not points, Voronoi | 0.776 |
| 🗺️ Regions, Voronoi maps, and hidden structure | `00:11:35.105`-`00:12:55.193` | Q (maf): nodes as regions not points, Voronoi | 0.794 |
| 🌐 Question from Ivan Lugo: do meanings have shared shapes across languages? | `00:14:05.193`-`00:15:26.504` | Q (Ivan Lugo): shared shapes across languages | 0.695 |
| 📐 MiniLM, salience, and Manifold Steering | `00:15:26.504`-`00:16:57.935` | MiniLM salience, then the Manifold Steering paper | 0.854 |
| 🧱 Visual language and Robert Horn | `00:16:57.935`-`00:19:55.657` | Robert Horn and visual language; pandemic mess-maps | 0.915 |
| 👏 Closing | `00:19:55.657`-`00:20:17.599` | Closing | 0.868 |
| 💬 Relevant chat notes | `00:16:57.935`-`00:19:55.657` | Robert Horn and visual language; pandemic mess-maps | 0.646 |

## Example topic to video mappings

| Topic | Best chapter | Short window | Score | Short window text snippet |
|---|---|---:|---:|---|
| Mental Model Building | Intro: good mental models, high-bandwidth visual cognition | `00:00:00.838`-`00:01:18.256` | 0.472 | Hello I’m interested in the problem of how we as human beings, can get a good mental model of what is going on I want to understand things a |
| Raw Projection Messiness | Why the first map looks messy (high-D to 2D, overlap, force-directed kludge) | `00:00:25.679`-`00:01:42.276` | 0.626 | information efficiently I’m interested in how things like embeddings, generated categories, different kinds of relationships and graph struc |
| Semantic-Aware Multi-Stage Layout | No-overlap layout that keeps semantic integrity | `00:02:06.681`-`00:03:49.380` | 0.633 | But then we have to tweak all kinds of fiddly variables to keep the semantic integrity authentic It is also a bit of a kludge to switch to a |
| Regions Not Points | Q (maf): nodes as regions not points, Voronoi | `00:11:30.422`-`00:12:23.639` | 0.521 | But in an actual 2D space, things also have dimensions They have shapes We also think in categories On the screen, in a user interface many |
| Generated Topic Icons | Adding visual language: generated icons | `00:04:59.694`-`00:06:25.169` | 0.592 | with a fittingly emptier area around it So the semantic integrity is good, but it is still not very intuitive These days we have image gener |
| Zoomable User Interface | Adding visual language: generated icons | `00:05:28.937`-`00:06:53.046` | 0.611 | That probably helps a little bit What would be more useful is a zoomable user interface where we can look at different things at different l |
| Reverse Projection | Projecting back with UMAP: where would a new thing land? | `00:07:59.337`-`00:09:08.985` | 0.548 | higher-dimensional spaces I’m curious what you have thought about with respect to doing expressive work through this interface Yes We can ac |
| Manifold Steering | MiniLM salience, then the Manifold Steering paper | `00:15:17.357`-`00:16:32.003` | 0.635 | really efficient way Then the Manifold Steering paper came out It basically showed things like different dates mapping to a particular shape |
| Robert Horn Visual Language | Robert Horn and visual language; pandemic mess-maps | `00:16:44.705`-`00:17:48.207` | 0.729 | This is really cool to see It shows how it works on the data side Thank you Very cool I also love to point to Bob Horn Robert Horn, who coin |
| Collective Sensemaking Tools | Intro: good mental models, high-bandwidth visual cognition | `00:19:06.267`-`00:20:11.681` | 0.469 | risk areas How do we get them to collaborate and share their findings in a useful way We might make a mess map, or an information mural or s |

## Visual and PiP anchors added

| Time | Anchor | Meaning |
|---:|---|---|
| `00:00:00.000` | Opening webcam/start transition | The cut begins with the speaker webcam/call view before the screen-share map becomes the main visual. |
| `00:00:52.468` | Raw/prototype map with white circular nodes | Black canvas with white circular topic nodes and short labels; visually supports the point that the initial projection is messy and not intuitive. |
| `00:01:35.655` | Non-overlapping semantic-aware map layout | A cleaner map layout is shown after discussing overlap removal and preserving semantic integrity. |
| `00:05:24.413` | Generated icons added to the topic map | The map shifts from abstract nodes toward generated icon landmarks with labels, making topics more visually recognisable. |
| `00:06:14.406` | Salience, scale, opacity, and zoom states | Bottom controls such as Overview, Landmarks, Detail, a zoom slider, zoom readout, and visible-count readout are visually relevant but only partly spoken. |
| `00:08:12.087` | Reverse projection and expressive arrangement | Discussion of using a chosen map position to infer a high-dimensional embedding; screen remains on the map rather than showing a separate UMAP diagram. |
| `00:10:12.774` | Rotation anchor for stable map orientation | The discussion turns to keeping regenerated maps aligned across layout runs. |
| `00:11:30.422` | Regions, boxes, and Voronoi territories discussed verbally | The sampled video still shows the icon topic map rather than an actual Voronoi overlay or region-boundary feature. |
| `00:15:26.504` | Manifold Steering discussed verbally | The screen remains on the Pepys topic map; no paper screenshot or geometry diagram is shown in sampled frames. |
| `00:16:57.935` | Robert Horn and visual language discussed verbally | No Robert Horn source image or book page appears in sampled frames; external links or sidecards would enrich this segment. |

| Time | Speaker | Meaning |
|---:|---|---|
| `00:00:00.838` | Luke Stanley | Luke begins the demo after the opening handoff. |
| `00:07:49.000` | Ivy Reese | PiP switches to Ivy Reese for the question about expression through the interface. |
| `00:08:09.000` | Luke Stanley | PiP returns to Luke for the reverse-projection answer. |
| `00:11:31.000` | Marek “maf” Rogalski | PiP switches to Marek/maf for the regions, shapes, boxes, and Voronoi question. |
| `00:14:01.000` | Ivan Lugo | PiP switches to Ivan Lugo for the shared shapes across languages question. |
| `00:15:21.000` | Luke Stanley | PiP returns to Luke for the MiniLM and Manifold Steering answer. |
| `00:19:55.000` | Ivy Reese | PiP switches to Ivy Reese for the closing thanks. |

## Output files

- `talk2_per_media_mappings.json`: full nested mapping.
- `talk2_per_media_mappings_flat.tsv`: flattened mappings for spreadsheet inspection.
- `talk2_topic_to_video_mappings.tsv`: compact topic-to-video mapping.
- `talk2_section_to_video_mappings.tsv`: compact section-to-video mapping.

## Late Interaction note

A Late Interaction model is not needed for this first-pass mapping because the database already contains multi-model dense embeddings and the timed VTT spine. It would be useful for a second pass over exact phrase-to-cue linking, especially for visually prominent topic labels and short key points where normal dense embeddings can be too broad.