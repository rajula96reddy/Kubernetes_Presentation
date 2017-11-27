

@title[Introduction]
The Kitchen Sink
A GitPitch Feature Tour

@title[Theme Switcher]
Slideshow Theme Switcher

Available inside burger-menu. | Start switching themes right now!

@title[Go Fullscreen]
Tip!

For the best viewing experience
press F key to go fullscreen.
Markdown Slides

Press Down key for details. | See GitPitch Wiki for details.

Press Down Key

+++ @title[GFM]
Use GitHub Flavored Markdown
For Slide Content Creation

The same syntax you use to create project
READMEs and Wikis for your Git repos.
Code Presenting
Repo Source Files

Press Down key for examples. | See GitPitch Wiki for details.

Press Down Key

+++ @title[Present From Source]
Present Source Directly From Your Repo

Step through source code directly within your presentations. No more switching back and forth between your slideshow and your IDE!

+++?code=src/elixir/monitor.ex&lang=elixir&title=Source: Elixir Snippets

@[11-14](Elixir module-attributes as constants) @[22-28](Elixir with-statement for conciseness) @[171-177](Elixir case-statement pattern matching) @[179-185](Elixir pipe-mechanism for composing functions)=

@title[Present Static Block]
Code Presenting
Static Source Blocks

Press Down key for examples. | See GitPitch Wiki for details.

Press Down Key

+++ @title[Syntax Highlighting]
Present Source Embedded In Your Presentation Markdown

Enjoy code syntax highlighting for dozens of languages powered by highlight.js.

+++ @title[Block: Python Snippets]

Static Code Block: Python Snippets

from time import localtime

activities = {8: 'Sleeping', 9: 'Commuting', 17: 'Working',
              18: 'Commuting', 20: 'Eating', 22: 'Resting' }

time_now = localtime()
hour = time_now.tm_hour

for activity_time in sorted(activities.keys()):
    if hour < activity_time:
        print activities[activity_time]
        break
else:
    print 'Unknown, AFK or sleeping!'

@[1](Python from..import statement) @[3-4](Python dictionary initialization block) @[6-7](Python working with time) @[9-14](Python for..else statement)

@title[Present GIST]
Code Presenting
GitHub GIST

Press Down key for examples. | See GitPitch Wiki for details.

Press Down Key

+++ @title[Directly from GitHub]
Present Source Directly From GitHub GIST

Step through GIST source code within
online and offline presentations.

+++?gist=onetapbeyond/494e0fecaf0d6a2aa2acadfb8eb9d6e8&lang=Scala&title=GIST: Scala Snippets @title[Sample GIST]

@[23](Initialize Apache Spark cluster execution context) @[47-53](Transform RDD into set of AWS Lambda tasks) @[62](Delegate execution off Spark cluster to AWS Lambda) @[72-75](Handle AWS Lambda task execution results)

@title[Embed Images]
Image Slides
[ Inline ]

Press Down key for examples. | See GitPitch Wiki for details.

Press Down Key

+++
Make A Visual Statement

Use inline images to lend
a visual punch to your slideshow presentations.

+++ @title[Private Investocat]

Inline Image at Absolute URL

Image-Absolute

the Private Investocat by jeejkang

+++ @title[Octocat De Los Muertos]

Inline Image at GitHub Repo Relative URL

Image-Absolute

the Octocat-De-Los-Muertos by cameronmcefee

+++ @title[Daftpunktocat]

Animated GIFs Work Too!

Image-Relative

the Daftpunktocat-Guy by jeejkang

@title[Background Images]
Image Slides
[ Background ]

Press Down key for examples. | See GitPitch Wiki for details.

Press Down Key

+++ @title[Bold Statements]
Make A Bold Visual Statement

Use high-resolution background images
for maximum impact.

+++?image=https://d1z75bzl1vljy2.cloudfront.net/kitchen-sink/victory.jpg @title[V For Victory]

+++?image=https://d1z75bzl1vljy2.cloudfront.net/kitchen-sink/127.jpg @title[127.0.0.1]

@title[Embed Video]
Video Slides
[ Inline ]

Press Down key for examples. | See GitPitch Wiki for details.

Press Down Key

+++ @title[YouTube, etc]
Bring Your Presentations Alive

Embed YouTube, Vimeo, MP4 and WebM
inline on any slide.

+++ @title[Fresh Guacamole]

YouTube Video

+++ @title[Gravity]

Vimeo Video

+++ @title[Big Buck Bunny]

MP4 Video

@title[Background Videos]
Video Slides
[ Background ]

Press Down key for examples. | See GitPitch Wiki for details.

Press Down Key

+++ @title[Viewer Experience]
Maximize The Viewer Experience

Go fullscreen with MP4 and WebM videos.

+++?video=http://clips.vorwaerts-gmbh.de/big_buck_bunny.mp4 @title[Big Buck Bunny]
Math Notation Slides

Press Down key for examples. | See GitPitch Wiki for details.

Press Down Key

+++ @title[Beautiful Math]
Beautiful Math Rendered Beautifully

Use TeX, LaTeX and MathML markup
powered by MathJax.

+++ @title[Sample]

$$\sum_{i=0}^n i^2 = \frac{(n^2+n)(2n+1)}{6}$$

+++ @title[Sample]

\begin{align} \dot{x} & = \sigma(y-x) \\ \dot{y} & = \rho x - y - xz \\ \dot{z} & = -\beta z + xy \end{align}

+++ @title[Sample]
The Cauchy-Schwarz Inequality

\[ \left( \sum_{k=1}^n a_k b_k \right)^{\!\!2} \leq \left( \sum_{k=1}^n a_k^2 \right) \left( \sum_{k=1}^n b_k^2 \right) \]

+++ @title[Inline Sample]
In-line Mathematics

This expression \(\sqrt{3x-1}+(1+x)^2\) is an example of an inline equation.
Chart Slides

Press Down key for examples. | See GitPitch Wiki for details.

Press Down Key

+++ @title[Chart Types]
Chart Data Rendered Beautifully

Use Bar, Line, Area, and Scatter charts among many other chart types directly within your markdown, all powered by Chart.js.

+++ @title[Sample Line Chart]

+++ @title[Sample Bar Chart]
Slide Fragments

Press Down key for examples. | See GitPitch Wiki for details.

Press Down Key

+++
Reveal Slide Concepts Piecemeal

@title[Piecemeal Concepts]

Step through slide content in sequence
to slowly reveal the bigger picture.

+++ @title[Piecemeal Lists]

    Java
    Groovy |
    Kotlin |
    Scala |
    The JVM rocks! |

+++ @title[Piecemeal Tables]
Firstname 	Lastname 	Age
Jill 	Smith 	25
Eve 	Jackson 	94
John 	Doe 	43
PITCHME.yaml Settings

Press Down key for examples. | See GitPitch Wiki for details.

Press Down Key

+++ @title[Custom Look and Feel]
Stamp Your Own Look and Feel

Set a default theme, custom logo, custom css, background image, and preferred code syntax highlighting style.

+++ @title[Custom Behavior]
Customize Slideshow Behavior

Enable auto-slide with custom slide intervals, presentation looping, and RTL flow.

@title[Keyboard Controls]
Slideshow Keyboard Controls

Press Down key for examples. | See GitPitch Wiki for details.

Press Down Key

+++ @title[Try Out Now!]
Try Out These Great Features Now!

Mode 	On Key 	Off Key
Fullscreen 	F 	Esc
Overview 	O 	O
Blackout 	B 	B
Help 	? 	Esc
GitPitch Social

Press Down key for examples. | See GitPitch Wiki for details.

Press Down Key

+++ @title[Designed For Sharing]
Slideshows Designed For Sharing

    View any slideshow at its public URL
    Promote any slideshow using a GitHub badge
    Embed any slideshow within a blog or website
    Share any slideshow on Twitter, LinkedIn, etc
    Print any slideshow as a PDF document
    Download and present any slideshow offline

@title[Get The Word Out!]
GO FOR IT.
JUST ADD PITCHME.md ;)
PITCHPIT
