# Sample Content Model

This example is derived from a Drupal configuration export. Field machine names
are normalized to semantic names: implementation prefixes from the source
configuration are omitted. Drupal base fields such as node title, publication
status, ownership, and revision metadata are not repeated below.

Cardinality is shown as `1` for a single value and `unlimited` for a repeatable
field. A target lists the bundles allowed by an entity reference.

## Content types

### Article (`article`)

Time-sensitive content such as news, press releases, and blog posts.

| Machine name | Label | Type | Cardinality | Required | Target | Notes |
| --- | --- | --- | --- | --- | --- | --- |
| `lead` | Lead | Long text | 1 | Yes | | |
| `visibility` | Paywall setting | List (text) | 1 | Yes | | See [Controlled values](#controlled-values). |
| `hero` | Hero | Media reference | 1 | No | Image | |
| `media` | Media focus | Media reference | 1 | No | Image, Youtube | Changes the article layout when the article is about the selected media. |
| `author` | Author | Content reference | 1 | No | Author | |
| `components` | Components | Paragraph reference | unlimited | No | HTML, Photo, Video, Breakout, Cards, CTA, List, Stepper | |
| `publication_channel` | Magazine section | Taxonomy reference | unlimited | Yes | Magazine sections | Controls which magazine section displays the article. |

### Author (`author`)

An author used mainly for magazine articles.

| Machine name | Label | Type | Cardinality | Required | Target | Notes |
| --- | --- | --- | --- | --- | --- | --- |
| `lead` | Short bio | Long text | 1 | Yes | | |
| `visibility` | Paywall setting | List (text) | 1 | Yes | | See [Controlled values](#controlled-values). |
| `portrait` | Photo | Media reference | 1 | Yes | Image | |

### Course (`course`)

A course containing modules and lessons.

| Machine name | Label | Type | Cardinality | Required | Target | Notes |
| --- | --- | --- | --- | --- | --- | --- |
| `visibility` | Paywall setting | List (text) | 1 | Yes | | See [Controlled values](#controlled-values). |
| `components` | Components | Paragraph reference | unlimited | No | Module, Photo, Video, Cards, CTA, Other blocks, List, HTML, Stepper | |
| `introduction` | Introduction | Paragraph reference | unlimited | No | HTML | |
| `modules` | Modules | Paragraph reference | unlimited | No | Module | |

### Event (`event`)

An online or in-person event, usually in the past.

| Machine name | Label | Type | Cardinality | Required | Target | Notes |
| --- | --- | --- | --- | --- | --- | --- |
| `lead` | Lead | Long text | 1 | Yes | | |
| `visibility` | Paywall setting | List (text) | 1 | Yes | | See [Controlled values](#controlled-values). |
| `hero` | Hero | Media reference | 1 | No | Image | |
| `media` | Media focus | Media reference | 1 | No | Image, Youtube | Used for an event recording such as a webinar or talk. |
| `components` | Components | Paragraph reference | unlimited | No | HTML, Breakout, Cards, CTA, List, Stepper, Photo, Video | |

### Lesson (`lesson`)

A lesson belonging to a course.

| Machine name | Label | Type | Cardinality | Required | Target | Notes |
| --- | --- | --- | --- | --- | --- | --- |
| `lead` | Summary | Long text | 1 | No | | |
| `module` | Module | List (text) | 1 | Yes | | Administrative grouping; see [Controlled values](#controlled-values). |
| `visibility` | Paywall setting | List (text) | 1 | Yes | | See [Controlled values](#controlled-values). |
| `hero` | Hero | Media reference | 1 | No | Image | |
| `course` | Course | Content reference | 1 | Yes | Course | |
| `components` | Components | Paragraph reference | unlimited | No | HTML, Photo, Video, Breakout, CTA, Cards, List, Stepper, Other blocks | |
| `freetags` | Free tags | Taxonomy reference | unlimited | No | Free Tags | |

### Page (`page`)

Static content such as an About page.

| Machine name | Label | Type | Cardinality | Required | Target | Notes |
| --- | --- | --- | --- | --- | --- | --- |
| `lead` | Lead / Summary | Long text | 1 | Yes | | |
| `visibility` | Paywall setting | List (text) | 1 | Yes | | See [Controlled values](#controlled-values). |
| `layout` | Layout | Layout section | 1 | No | | Managed by Layout Builder. |
| `hero` | Hero | Media reference | 1 | No | Image | |
| `components` | Components | Paragraph reference | unlimited | No | HTML, Breakout, CTA, Cards, Feature, Photo, Video, Shopify blocks, Other blocks | |

### Magazine (`publication`)

A magazine or other publication.

| Machine name | Label | Type | Cardinality | Required | Target | Notes |
| --- | --- | --- | --- | --- | --- | --- |
| `published` | Date published | Date and time | 1 | Yes | | Official publication date. |
| `buylink` | Purchase link | Link | 1 | No | | Link to purchase a hard copy. |
| `code` | Issue code | Text | 1 | Yes | | For example, `RNLX25`. |
| `issue` | Issue No. | Text | 1 | No | | |
| `lead` | Issue summary | Long text | 1 | Yes | | |
| `visibility` | Paywall setting | List (text) | 1 | Yes | | See [Controlled values](#controlled-values). |
| `layout` | Layout | Layout section | 1 | No | | Managed by Layout Builder. |
| `canvas` | Canvas | Media reference | 1 | Yes | Image | Background for a magazine header or similar treatment. |
| `hero` | Cover art | Media reference | 1 | Yes | Image | |
| `content` | Articles & pages | Content reference | unlimited | No | Article, Page | Content belonging to the magazine. |
| `components` | Components | Paragraph reference | unlimited | No | Cards, CTA, List, HTML, Stepper | |
| `highlights` | In this issue | Paragraph reference | unlimited | No | Links | |

## Paragraph types

### Other blocks (`blockplugin`)

Selects a dynamic Drupal block.

| Machine name | Label | Type | Cardinality | Required | Target |
| --- | --- | --- | --- | --- | --- |
| `subtitle` | Subtitle | Paragraph reference | 1 | No | Subtitle |
| `blockplugin` | Block | Block field | 1 | No | |

### Breakout (`breakout`)

A tip or other breakout box.

| Machine name | Label | Type | Cardinality | Required |
| --- | --- | --- | --- | --- |
| `href` | Target link | Link | 1 | No |
| `markup` | Content | Long text | 1 | No |
| `view_mode` | Design | Paragraph view mode | 1 | No |

### Cards (`cards`)

A grid-like display of linked items.

| Machine name | Label | Type | Cardinality | Required | Target |
| --- | --- | --- | --- | --- | --- |
| `children` | Item | Repeatable structured item | unlimited | Yes | |
| `markup` | Content | Long text | 1 | No | |
| `subtitle` | Subtitle | Paragraph reference | 1 | No | Subtitle |

### CTA (`cta`)

A standalone call to action.

| Machine name | Label | Type | Cardinality | Required | Target |
| --- | --- | --- | --- | --- | --- |
| `href` | Target link | Link | 1 | No | |
| `label` | Label | Text | 1 | No | |
| `markup` | Content | Long text | 1 | No | |
| `image` | Image | Media reference | 1 | No | Image |

### Feature (`feature`)

A large styled feature.

| Machine name | Label | Type | Cardinality | Required | Target |
| --- | --- | --- | --- | --- | --- |
| `eyebrow` | Eyebrow | Text | 1 | No | |
| `href` | Target link | Link | 1 | No | |
| `label` | Label | Text | 1 | No | |
| `markup` | Content | Long text | 1 | No | |
| `title` | Title | Text | 1 | No | |
| `image` | Image | Media reference | 1 | No | Image |
| `view_mode` | Design | Paragraph view mode | 1 | No | |

### From library (`from_library`)

A component selected from the Paragraphs library.

| Machine name | Label | Type | Cardinality | Required | Target |
| --- | --- | --- | --- | --- | --- |
| `reusable_paragraph` | Reusable paragraph | Entity reference | 1 | Yes | Paragraphs library item |

### Links (`links`)

A simple list of links.

| Machine name | Label | Type | Cardinality | Required | Target |
| --- | --- | --- | --- | --- | --- |
| `children` | Links | Repeatable structured item | unlimited | No | |
| `image` | Background image | Media reference | 1 | No | Image |
| `subtitle` | Subtitle | Paragraph reference | 1 | No | Subtitle |

The Links editor exposes `linktext` and `linkurl` for each repeated item. The
underlying repeatable item also supports `eyebrow`, `heading`, `subheading`,
`body`, and `image` values.

### List (`list`)

Accordions, FAQs, and other repeatable information whose order is not central.

| Machine name | Label | Type | Cardinality | Required | Target |
| --- | --- | --- | --- | --- | --- |
| `children` | Item | Repeatable structured item | unlimited | Yes | |
| `markup` | Content | Long text | 1 | No | |
| `subtitle` | Subtitle | Paragraph reference | 1 | No | Subtitle |

### HTML (`markup`)

Flexible HTML content.

| Machine name | Label | Type | Cardinality | Required | Target |
| --- | --- | --- | --- | --- | --- |
| `markup` | Content | Long text | 1 | No | |
| `subtitle` | Subtitle | Paragraph reference | 1 | No | Subtitle |
| `view_mode` | Design | Paragraph view mode | 1 | No | |

### Module (`module`)

Groups lessons within a course.

| Machine name | Label | Type | Cardinality | Required | Target |
| --- | --- | --- | --- | --- | --- |
| `markup` | Summary | Long text | 1 | No | |
| `status` | Module status | List (text) | 1 | Yes | See [Controlled values](#controlled-values). |
| `image` | Image | Media reference | 1 | No | Image |
| `lessons` | Lessons | Content reference | unlimited | No | Lesson |
| `subtitle` | Module title | Paragraph reference | 1 | No | Subtitle |

### Photo (`photo`)

A photo with a caption.

| Machine name | Label | Type | Cardinality | Required | Target |
| --- | --- | --- | --- | --- | --- |
| `label` | Caption | Text | 1 | No | |
| `image` | Image | Media reference | 1 | No | Image, Library Photo |

### Stepper (`sequence`)

A timeline, stepper, or other ordered set of information.

| Machine name | Label | Type | Cardinality | Required | Target |
| --- | --- | --- | --- | --- | --- |
| `children` | Item | Repeatable structured item | unlimited | Yes | |
| `markup` | Content | Long text | 1 | No | |
| `subtitle` | Subtitle | Paragraph reference | 1 | No | Subtitle |

### Shopify blocks (`shopify`)

Selects a Shopify-related Drupal block.

| Machine name | Label | Type | Cardinality | Required |
| --- | --- | --- | --- | --- |
| `blockplugin` | Block | Block field | 1 | No |

### Subtitle (`subtitle`)

A section subtitle with an optional URL anchor.

| Machine name | Label | Type | Cardinality | Required | Notes |
| --- | --- | --- | --- | --- | --- |
| `anchor` | Anchor | Text | 1 | No | Supports fragment links such as `#section-name`. |
| `subtitle` | Subtitle | Text | 1 | Yes | |

### Video (`video`)

A Youtube video component.

| Machine name | Label | Type | Cardinality | Required | Target |
| --- | --- | --- | --- | --- | --- |
| `video` | Video | Media reference | 1 | No | Youtube |
| `subtitle` | Subtitle | Paragraph reference | 1 | No | Subtitle |

## Reusable block type

### Reusable block (`basic`)

| Machine name | Label | Type | Cardinality | Required | Target |
| --- | --- | --- | --- | --- | --- |
| `components` | Components | Paragraph reference | unlimited | No | HTML, Feature, CTA, Cards |

## Media types

### Image (`image`)

Locally managed images, ideally between 1000 and 2000 pixels wide or high.

| Machine name | Label | Type | Cardinality | Required | Target |
| --- | --- | --- | --- | --- | --- |
| `image` | Image | Image | 1 | Yes | |
| `collection` | Admin tag | Taxonomy reference | unlimited | Yes | Admin collections |

### Library Photo (`photolib`)

An image sourced from the Diggers OneDrive photo library.

| Machine name | Label | Type | Cardinality | Required |
| --- | --- | --- | --- | --- |
| `onedrive_image_fileid` | OneDrive file ID | Text | 1 | Yes |
| `onedrive_local_image` | Cached image | Image | 1 | No |
| `onedrive_metadata` | OneDrive Metadata | Long text | 1 | No |

### Youtube (`stream`)

An oEmbed video used for channel embeds.

| Machine name | Label | Type | Cardinality | Required |
| --- | --- | --- | --- | --- |
| `transcript` | Transcript | Text with summary | 1 | No |
| `oembed_video` | Remote video URL | Text | 1 | Yes |

## Taxonomy vocabularies

| Machine name | Label | Purpose |
| --- | --- | --- |
| `collections` | Admin collections | Administrative organization. |
| `publication_channel` | Magazine sections | High-level magazine sections; additions require approval. |
| `tags` | Free Tags | Groups articles on similar topics. |

## Controlled values

### Paywall setting (`visibility`)

| Stored value | Label |
| --- | --- |
| `public` | Free |
| `partial` | Members |
| `internal` | Staff |

### Lesson module (`module`)

| Stored value | Label |
| --- | --- |
| `tba` | TBA |
| `m01` through `m10` | Module 1 through Module 10 |
| `recap` | Recap |

### Module status (`status`)

| Stored value | Label |
| --- | --- |
| `released` | Released |
| `tease` | Coming soon (show summary) |
| `hide` | In progress (hide) |
