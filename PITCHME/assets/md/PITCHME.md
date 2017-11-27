<span class="menu-title" style="display: none">Introduction</span>
## Kubernetes 101
##### <span style="font-family:Helvetica Neue; font-weight:bold">An Introduction to <span style="color:#e49436">Kubernetes</span></span>
---
<span class="menu-title" style="display: none">Recap</span>

## Container, Docker, Kubernetes!
A breif recap

---
<span class="menu-title" style="display: none">App</span>

### A basic Rails App!
![Image](./assets/md/assets/kubernetes-illustrated-guide-illustration-3.png)

---
<span class="menu-title" style="display: none">Container</span>

## Containerizing the App!
![Image](./assets/md/assets/kubernetes-illustrated-guide-illustration-4.png)

---

<span class="menu-title" style="display: none">Kubernetes</span>

## A basic Rails App!
![Image](./assets/md/assets/kubernetes-illustrated-guide-illustration-5.png)

---
<span class="menu-title" style="display: none">What is Kubernetes</span>

## Kubernetes!! Kubernetes!! What is this?
<!-- <span style="font-size:0.6em; color:gray">Available inside burger-menu.</span> |
<span style="font-size:0.6em; color:gray">Start switching themes right now!</span> -->
- Kubernetes is a **OPEN SOURCE** container orchestration software lead by **Google**
- The word **Kubernetes** is a Greek work which stands for a **Ship's Captain**
- The project focuses on building a robust platform for running thousands of containers in production.

---
<span class="menu-title" style="display: none">Stats1</span>
## Few Stats
<img align="left" src="./assets/md/assets/MostViewedProjects.png" width="300" height="400">
<img align="right" src="./assets/md/assets/MostDiscussedRepos.png" width="300" height="400">
<!-- <span style="font-size:0.6em; color:white">Github Octoverse Statistics from Sep '16 to Oct '17.</span> -->
---
<span class="menu-title" style="display: none">Stats2</span>
## Few Stats
![Image](./assets/md/assets/MostDiscussedRepos.png)
<span style="font-size:0.6em; color:gray">Github Octoverse Statistics since Sep '16 to Oct '17.</span>
---
<span class="menu-title" style="display: none">Present Static Block</span>

## Code Presenting
## Static Source Blocks
<span style="font-size:0.6em; color:gray">Press Down key for examples.</span> |
<span style="font-size:0.6em; color:gray">See [GitPitch Wiki](https://github.com/gitpitch/gitpitch/wiki/Code-Presenting) for details.</span>

![Image](./assets/md/assets/down-arrow.png)

+++
<span class="menu-title" style="display: none">Syntax Highlighting</span>
#### Present Source Embedded In Your Presentation Markdown

<br>

Enjoy code syntax highlighting for dozens of languages powered by [highlight.js](tlhttps://highlightjs.org).

+++
<span class="menu-title" style="display: none">Block: Python Snippets</span>

Static Code Block: Python Snippets

```python
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
```

<span class="code-presenting-annotation fragment current-only" data-code-focus="1">Python from..import statement</span>
<span class="code-presenting-annotation fragment current-only" data-code-focus="3-4">Python dictionary initialization block</span>
<span class="code-presenting-annotation fragment current-only" data-code-focus="6-7">Python working with time</span>
<span class="code-presenting-annotation fragment current-only" data-code-focus="9-14">Python for..else statement</span>

---
<span class="menu-title" style="display: none">Present GIST</span>

## Code Presenting
## GitHub GIST
<span style="font-size:0.6em; color:gray">Press Down key for examples.</span> |
<span style="font-size:0.6em; color:gray">See [GitPitch Wiki](https://github.com/gitpitch/gitpitch/wiki/Code-Presenting) for details.</span>

![Image](./assets/md/assets/down-arrow.png)

+++
<span class="menu-title" style="display: none">Directly from GitHub</span>

#### Present Source Directly From GitHub GIST

<br>

Step through GIST source code within    
*online and offline* presentations.

+++

<span class='menu-title slide-title'>GIST: Scala Snippets</span>
```Scala
package io.onetapbeyond.lambda.spark.executor.examples

import io.onetapbeyond.lambda.spark.executor.Gateway._
import io.onetapbeyond.aws.gateway.executor._
import org.apache.spark._
import scala.collection.JavaConverters._

/*
 * TaskDelegation
 *
 * https://github.com/onetapbeyond/lambda-spark-executor
 *
 * A sample application that demonstrates the basic usage
 * of SAMBA to delegate selected Spark RDD tasks to execute
 * on AWS Lambda compute infrastructure in the cloud.
 */
object TaskDelegation {

  def main(args:Array[String]):Unit = {

    try {

      val sc = initSparkContext()

      /*
       * Initialize a basic batch data source for the
       * example by generating an RDD[Int].
       */
      val dataRDD = sc.parallelize(1 to BATCH_DATA_SIZE)

      /*
       * API_GATEWAY represents the API on the AWS API
       * Gateway implemented by an AWS Lambda function.
       * We register the gateway as a Spark broadcast
       * variable so it can be safely referenced later
       * within the Spark RDD.map operation that builds
       * our AWSTask.
       */
      val gateway = sc.broadcast(API_GATEWAY)

      /*
       * Map over dataRDD[Int] to produce an RDD[AWSTask].
       * Each AWSTask will execute an AWS Lambda function
       * exposed by the API_SCORE_ENDPOINT endpoint on the
       * AWS API Gateway.
       */
      val aTaskRDD = dataRDD.map(num => {

        AWS.Task(gateway.value)
           .resource(API_SCORE_ENDPOINT)
           .input(Map("num" -> num).asJava)
           .post()
      })

      aTaskRDD.foreach { aTask => println(aTask) }

      /*
       * Delegate aTaskRDD[AWSTask] execution to AWS Lambda
       * compute infrastructure to produce
       * aTaskResultRDD[AWSResult].
       */
      val aTaskResultRDD = aTaskRDD.delegate

      /*
       * As this is an example application we can simply use
       * the foreach() operation on the RDD to force the
       * computation and to output the results. And as we are
       * using a mock API on the AWS API Gateway there is no
       * response data, the result simply indicates success
       * or failure.
       */
      aTaskResultRDD.foreach { result => {
        println("TaskDelegation: compute score input=" +
          result.input + " result=" + result.success)
      }}

    } catch {
      case t:Throwable =>
        println("TaskDelegation: caught ex=" + t)
    }

  }

  def initSparkContext():SparkContext = {
    val conf = new SparkConf().setAppName(APP_NAME)
    new SparkContext(conf)
  }

  private val APP_NAME = "SAMBA Task Delegation Example"
  private val BATCH_DATA_SIZE = 10
  private val API_ID = "06ti6xmgg2"
  private val API_STAGE = "mock"
  private val API_SCORE_ENDPOINT = "/score"
  private val API_GATEWAY:AWSGateway =
    AWS.Gateway(API_ID).region(AWS.Region.OREGON)
                       .stage(API_STAGE)
                       .build()
}
```

<span class="menu-title" style="display: none">Sample GIST</span>

<span class="code-presenting-annotation fragment current-only" data-code-focus="23">Initialize Apache Spark cluster execution context</span>
<span class="code-presenting-annotation fragment current-only" data-code-focus="47-53">Transform RDD into set of AWS Lambda tasks</span>
<span class="code-presenting-annotation fragment current-only" data-code-focus="62">Delegate execution off Spark cluster to AWS Lambda</span>
<span class="code-presenting-annotation fragment current-only" data-code-focus="72-75">Handle AWS Lambda task execution results</span>

---
<span class="menu-title" style="display: none">Embed Images</span>

## Image Slides
## [ Inline ]
<span style="font-size:0.6em; color:gray">Press Down key for examples.</span> |
<span style="font-size:0.6em; color:gray">See [GitPitch Wiki](https://github.com/gitpitch/gitpitch/wiki/Image-Slides) for details.</span>

![Image](./assets/md/assets/down-arrow.png)

+++

#### Make A Visual Statement

<br>

Use inline images to lend   
a *visual punch* to your slideshow presentations.


+++
<span class="menu-title" style="display: none">Private Investocat</span>

<span style="color:gray; font-size:0.7em">Inline Image at <b>Absolute URL</b></span>

![Image](./assets/md/assets/octocat-privateinvestocat.jpg)


<span style="color:gray; font-size: 0.5em;">the <b>Private Investocat</b> by [jeejkang](https://github.com/jeejkang)</span>


+++
<span class="menu-title" style="display: none">Octocat De Los Muertos</span>

<span style="color:gray; font-size:0.7em">Inline Image at GitHub Repo <b>Relative URL</b></span>

![Image](./assets/md/assets/octocat-de-los-muertos.jpg)

<span style="color:gray; font-size:0.5em">the <b>Octocat-De-Los-Muertos</b> by [cameronmcefee](https://github.com/cameronmcefee)</span>


+++
<span class="menu-title" style="display: none">Daftpunktocat</span>

<span style="color:gray; font-size:0.7em"><b>Animated GIFs</b> Work Too!</span>

![Image](./assets/md/assets/octocat-daftpunkocat.gif)

<span style="color:gray; font-size:0.5em">the <b>Daftpunktocat-Guy</b> by [jeejkang](https://github.com/jeejkang)</span>

---
<span class="menu-title" style="display: none">Background Images</span>

## Image Slides
## [ Background ]
<span style="font-size:0.6em; color:gray">Press Down key for examples.</span> |
<span style="font-size:0.6em; color:gray">See [GitPitch Wiki](https://github.com/gitpitch/gitpitch/wiki/Image-Slides#background) for details.</span>

![Image](./assets/md/assets/down-arrow.png)

+++
<span class="menu-title" style="display: none">Bold Statements</span>

#### Make A Bold Visual Statement

<br>

Use high-resolution background images   
for *maximum impact*.

+++
<!-- .slide: data-background-image="./assets/md/assets/victory.jpg" data-background-size="100% 100%" -->

<span class="menu-title" style="display: none">V For Victory</span>

+++
<!-- .slide: data-background-image="./assets/md/assets/127.jpg" data-background-size="100% 100%" -->

<span class="menu-title" style="display: none">127.0.0.1</span>

---
<span class="menu-title" style="display: none">Embed Video</span>
## Video Slides
## [ Inline ]
<span style="font-size:0.6em; color:gray">Press Down key for examples.</span> |
<span style="font-size:0.6em; color:gray">See [GitPitch Wiki](https://github.com/gitpitch/gitpitch/wiki/Video-Slides) for details.</span>

![Image](./assets/md/assets/down-arrow.png)

+++
<span class="menu-title" style="display: none">YouTube, etc</span>

#### Bring Your Presentations Alive

<br>

Embed *YouTube*, *Vimeo*, *MP4* and *WebM*   
inline on any slide.

+++
<span class="menu-title" style="display: none">Fresh Guacamole</span>

#### Video Slide Disabled
#### [ GitPitch Offline ]

+++
<span class="menu-title" style="display: none">Gravity</span>

#### Video Slide Disabled
#### [ GitPitch Offline ]

+++
<span class="menu-title" style="display: none">Big Buck Bunny</span>

#### Video Slide Disabled
#### [ GitPitch Offline ]


---
<span class="menu-title" style="display: none">Background Videos</span>

## Video Slides
## [ Background ]
<span style="font-size:0.6em; color:gray">Press Down key for examples.</span> |
<span style="font-size:0.6em; color:gray">See [GitPitch Wiki](https://github.com/gitpitch/gitpitch/wiki/Video-Slides#background) for details.</span>

![Image](./assets/md/assets/down-arrow.png)

+++
<span class="menu-title" style="display: none">Viewer Experience</span>

#### Maximize The Viewer Experience

<br>

Go fullscreen with *MP4* and *WebM* videos.

+++

#### Video Slide Disabled
#### [ GitPitch Offline ]

<span class="menu-title" style="display: none">Big Buck Bunny</span>

---

## Math Notation Slides
<span style="font-size:0.6em; color:gray">Press Down key for examples.</span> |
<span style="font-size:0.6em; color:gray">See [GitPitch Wiki](https://github.com/gitpitch/gitpitch/wiki/Math-Notation-Slides) for details.</span>

![Image](./assets/md/assets/down-arrow.png)

+++
<span class="menu-title" style="display: none">Beautiful Math</span>

#### Beautiful Math Rendered Beautifully

<br>

Use *TeX*, *LaTeX* and *MathML* markup   
powered by [MathJax](https://www.mathjax.org).

+++
<span class="menu-title" style="display: none">Sample</span>

`$$\sum_{i=0}^n i^2 = \frac{(n^2+n)(2n+1)}{6}$$`

+++
<span class="menu-title" style="display: none">Sample</span>

`\begin{align}
\dot{x} & = \sigma(y-x) \\
\dot{y} & = \rho x - y - xz \\
\dot{z} & = -\beta z + xy
\end{align}`

+++
<span class="menu-title" style="display: none">Sample</span>

##### The Cauchy-Schwarz Inequality

`\[
\left( \sum_{k=1}^n a_k b_k \right)^{\!\!2} \leq
 \left( \sum_{k=1}^n a_k^2 \right) \left( \sum_{k=1}^n b_k^2 \right)
\]`

+++
<span class="menu-title" style="display: none">Inline Sample</span>

##### In-line Mathematics

This expression `\(\sqrt{3x-1}+(1+x)^2\)` is an example of an inline equation.

---

## Chart Slides
<span style="font-size:0.6em; color:gray">Press Down key for examples.</span> |
<span style="font-size:0.6em; color:gray">See [GitPitch Wiki](https://github.com/gitpitch/gitpitch/wiki/Chart-Slides) for details.</span>

![Image](./assets/md/assets/down-arrow.png)

+++
<span class="menu-title" style="display: none">Chart Types</span>

#### Chart Data Rendered Beautifully

<br>

Use *Bar*, *Line*, *Area*, and *Scatter* charts among many other chart types directly within your markdown, all powered by [Chart.js](http://www.chartjs.org).

+++
<span class="menu-title" style="display: none">Sample Line Chart</span>

<canvas data-chart="line">
<!--
{
 "data": {
  "labels": ["January"," February"," March"," April"," May"," June"," July"],
  "datasets": [
   {
    "data":[65,59,80,81,56,55,40],
    "label":"My first dataset","backgroundColor":"rgba(20,220,220,.8)"
   },
   {
    "data":[28,48,40,19,86,27,90],
    "label":"My second dataset","backgroundColor":"rgba(220,120,120,.8)"
   }
  ]
 },
 "options": { "responsive": "true" }
}
-->
</canvas>

+++
<span class="menu-title" style="display: none">Sample Bar Chart</span>

<canvas class="stretch" data-chart="horizontalBar">
<!--
{
 "data" : {
  "labels" : ["Grapefruit", "Orange", "Kiwi",
    "Blackberry", "Banana",
    "Blueberry"],
  "datasets" : [{
    "data": [48, 26, 59, 39, 21, 74],
    "backgroundColor": "#e49436",
    "borderColor": "#e49436"
  }]
  },
  "options": {
    "title": {
      "display": true,
      "text": "The most delicious fruit?",
      "fontColor": "gray",
      "fontSize": 20
    },
    "legend": {
      "display": false
    },
    "scales": {
      "xAxes": [{
        "ticks": {
            "beginAtZero": true,
            "max": 80,
            "stepSize": 10,
            "fontColor": "gray"
        },
        "scaleLabel": {
          "display": true,
          "labelString": "Respondents",
          "fontColor": "gray"
        }
      }],
      "yAxes": [{
        "ticks": {
            "fontColor": "gray"
        }
      }]
    }
  }
}
-->
</canvas>

---

## Slide Fragments
<span style="font-size:0.6em; color:gray">Press Down key for examples.</span> |
<span style="font-size:0.6em; color:gray">See [GitPitch Wiki](https://github.com/gitpitch/gitpitch/wiki/Fragment-Slides) for details.</span>

![Image](./assets/md/assets/down-arrow.png)

+++

#### Reveal Slide Concepts Piecemeal
<span class="menu-title" style="display: none">Piecemeal Concepts</span>

<br>

Step through slide content in sequence   
to *slowly reveal* the bigger picture.

+++
<span class="menu-title" style="display: none">Piecemeal Lists</span>

- Java
- Groovy  <!-- .element: class="fragment" -->
- Kotlin  <!-- .element: class="fragment" -->
- Scala   <!-- .element: class="fragment" -->
- The JVM rocks!  <!-- .element: class="fragment" -->

+++
<span class="menu-title" style="display: none">Piecemeal Tables</span>

<table>
  <tr>
    <th>Firstname</th>
    <th>Lastname</th>
    <th>Age</th>
  </tr>
  <tr>
    <td>Jill</td>
    <td>Smith</td>
    <td>25</td>
  </tr>
  <tr class="fragment">
    <td>Eve</td>
    <td>Jackson</td>
    <td>94</td>
  </tr>
  <tr class="fragment">
    <td>John</td>
    <td>Doe</td>
    <td>43</td>
  </tr>
</table>

---
## <span style="text-transform: none">PITCHME.yaml</span> Settings
<span style="font-size:0.6em; color:gray">Press Down key for examples.</span> |
<span style="font-size:0.6em; color:gray">See [GitPitch Wiki](https://github.com/gitpitch/gitpitch/wiki/Slideshow-Settings) for details.</span>

![Image](./assets/md/assets/down-arrow.png)

+++
<span class="menu-title" style="display: none">Custom Look and Feel</span>

#### Stamp Your Own Look and Feel

<br>

Set a default theme, custom logo, custom css, background image, and preferred code syntax highlighting style.

+++
<span class="menu-title" style="display: none">Custom Behavior</span>

#### Customize Slideshow Behavior

<br>

Enable auto-slide with custom slide intervals, presentation looping, and RTL flow.


---
<span class="menu-title" style="display: none">Keyboard Controls</span>
## Slideshow Keyboard Controls
<span style="font-size:0.6em; color:gray">Press Down key for examples.</span> |
<span style="font-size:0.6em; color:gray">See [GitPitch Wiki](https://github.com/gitpitch/gitpitch/wiki/Slideshow-Fullscreen-Mode) for details.</span>

![Image](./assets/md/assets/down-arrow.png)

+++
<span class="menu-title" style="display: none">Try Out Now!</span>

#### Try Out These Great Features Now!

<br>

| Mode | On Key | Off Key |
| ---- | :------: | :--------: |
| Fullscreen | F |  Esc |
| Overview | O |  O |
| Blackout | B |  B |
| Help | ? |  Esc |


---

## GitPitch Social
<span style="font-size:0.6em; color:gray">Press Down key for examples.</span> |
<span style="font-size:0.6em; color:gray">See [GitPitch Wiki](https://github.com/gitpitch/gitpitch/wiki/Slideshow-GitHub-Badge) for details.</span>

![Image](./assets/md/assets/down-arrow.png)

+++
<span class="menu-title" style="display: none">Designed For Sharing</span>

#### Slideshows Designed For Sharing

<br>

- View any slideshow at its public URL
- [Promote](https://github.com/gitpitch/gitpitch/wiki/Slideshow-GitHub-Badge) any slideshow using a GitHub badge
- [Embed](https://github.com/gitpitch/gitpitch/wiki/Slideshow-Embedding) any slideshow within a blog or website
- [Share](https://github.com/gitpitch/gitpitch/wiki/Slideshow-Sharing) any slideshow on Twitter, LinkedIn, etc
- [Print](https://github.com/gitpitch/gitpitch/wiki/Slideshow-Printing) any slideshow as a PDF document
- [Download and present](https://github.com/gitpitch/gitpitch/wiki/Slideshow-Offline) any slideshow offline

---
<span class="menu-title" style="display: none">Get The Word Out!</span>

## GO FOR IT.
## JUST ADD <span style="color:#e49436; text-transform: none">PITCHME.md</span> ;)
