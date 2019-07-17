---
layout: post
title: PlantUML and Markdown Integration
---

[PlantUML](http://plantuml.com/) is a really awesome way to create diagrams by writing code instead of drawing and dragging visual elements. Markdown is a really nice documentation tool.

Here's how I combine the two, to create docs with embedded diagrams.

## Step 0: Setup

Get the command-line PlantUML from [the download page](http://plantuml.com/download) or your relevant package manager.

## Step 1: Create a Markdown file

Use your favorite markdown or text editor. Most (if not all) developer-oriented text editors have some kind of markdown support.

Remember that md files can contain html, and that html is passed-through to the generated html as-is.

When you want to embed a diagram, create a hidden div: `<div hidden>`.

Now start a code block by indenting or typing 3 backticks. The first line of the code block must be `@startuml` followed by a file name (with no extension). The following lines should be the actual diagram code, ending with `@enduml`. End the code block and close the div.

Finally, to actually show the diagram in the document, add an image in markdown:
```![](firstDiagram.svg)```. The name must be the same name as in the `@startuml` command, with a `.svg` extension.

### All together now
	
	Regular **Markdown** here.
	
	## Diagrams
	
	The following diagram shows the beginning of a conversation between *Alice* and *Bob*:
	
	<div hidden>
	```
	@startuml firstDiagram
	
	Alice -> Bob: Hello
	Bob -> Alice: Hi!
			
	@enduml
	```
	</div>
	
	![](firstDiagram.svg)
	
	Some more markdown.
	
## Step 2: Run PlantUML on the Markdown file

On the command line:

	plantuml -tsvg FILENAME

Where FILENAME is the name of the markdown file.

For every PlantUML block in the file, one svg diagram is generated. When the markdown to html converter is running, the html will contain image links to the generated images.

If for some reason you want to use PNG files for the diagrams and not SVG, use `![](firstDiagram.png)` in the image reference and remove the `-tsvg` in the command line. PNG files are compatible in more places, but they don't look good when zooming in and on high resolution displays.

## Step 3: Convert locally to HTML or upload to GitHub

If you host the files in GitHub (or other services that convert md to html on the fly), the last step is uploading or pushing the files. Make sure to include everything: the markdown and the generated diagrams.

Otherwise, use your favorite tool for converting markdown to html - a markdown editor or a command line tool.
