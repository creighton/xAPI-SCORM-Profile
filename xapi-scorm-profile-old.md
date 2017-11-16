# Experience API SCORM Profile

## Advanced Distributed Learning (ADL)

>"Copyright 2016 Advanced Distributed Learning (ADL) Initiative, U.S. Department of Defense

>Licensed under the Apache License, Version 2.0 (the "License"). You may not use this file except in compliance with the License. You may obtain a copy of the License at
>http://www.apache.org/licenses/LICENSE-2.0

>Unless required by applicable law or agreed to in writing, software distributed under the License
>is distributed on an "AS IS" BASIS, WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express
>or implied. See the License for the specific language governing permissions and limitations under the License."  


## Glossary
##### Activity:  
Generally synonymous with content, it is the entity with which the learner interacts - ie: video, lesson, slides, etc.   
##### Activity Provider:  
An application that delivers activities to the learner - ie: browser, e-reader, mobile app, etc.  
##### Experience:  
A notable interaction or event between the learner(s) and an activity - ie: took a test, completed the activity, answered a question, etc.  
##### Experience API (xAPI):  
A specification created to provide a way to represent and report experiences between a learner, or group of learners, and some activity.  
##### Internationalized Resource Identifier (IRI):  
A format of an identifier, related to URI, that supports the Universal Character Set (Unicode). See [RFC 3987](http://tools.ietf.org/html/rfc3987).  
##### Statement:  
The xAPI data format for representing learner experience data. See [xAPI Statement](https://github.com/adlnet/xAPI-Spec/blob/master/xAPI.md#statement).

## 1.0 Purpose
The Experience API (xAPI) was created in response to the eLearning community’s desire to modernize the Sharable Content Object Reference Model (SCORM) capabilities, which was initially developed to make courseware interoperable with learning management systems. Since its introduction in 2000, SCORM has played a critical role in the proliferation of online training and education courses. The Experience API introduces a new paradigm for tracking and recording learning-related data. Learners can be tracked as they perform work tasks, produce work outputs, communicate, collaborate, and engage in just about any other online activity. This API uses a flexible data format that supports many different use cases and needs. However with this flexibility arises the need for developers to formalize the data they track and what that data means. By formalizing the data reported by content and the format of that data, tools can be created that can make sense of that data.

The Sharable Content Object Reference Model (SCORM) community is one area that could benefit from providing a formalized method for compiling and formatting learner experiences. Using the xAPI and the guidance contained within this profile, developers can create xAPI statements that can be interpreted by any other system that understands the guidelines described in this document. This will support the integrity and consistency of the data across SCORM content and provide a base vocabulary needed for interpreting and reporting on that data.

SCORM is well established and accepted in many organizations around the world as the interoperable way to deliver and track web-based learning content. If the traditional LMS and content model is working for your organization, there is no need to change to use the xAPI.

However there are use cases that are difficult if not impossible to meet with SCORM. These cases prompted ADL to begin looking for alternative options. The initial effort resulted in the xAPI specification. It was intended to resolve issues such as:
- SCORM assumes content is managed and launched by an LMS (Advanced Distributed Learning Initiative, 2012, p. RTE-2-7).
  - Not all content can be contained and managed by an LMS, such as video games, virtual worlds, and simulators.
- SCORM embeds its API in a web page (Advanced Distributed Learning Initiative, 2012, p. RTE-3-28).
  - Not all content is web-based content. In cases where the content is not web-based, finding the SCORM API is not defined, like mobile apps and platform-based games.
- SCORM has a strictly defined data model (Advanced Distributed Learning Initiative, 2012, p. RTE-4-3).
  - Not every learning experience fits neatly into that model - things like tracking altitude in a flight simulator, or how many times a user paused a video does not translate into the SCORM data model.
- SCORM tracking only applies for an individual learner (Advanced Distributed Learning Initiative, 2012, p. RTE-2-5).
  - Group learning and interactions cannot be recorded with SCORM.
  - Data about instructors, tutors, mentors and peers cannot be stored with SCORM.
- SCORM does not provide guidance on how to get data back out of an LMS (Advanced Distributed Learning Initiative, 2012, p. RTE-2-5).
  - The interface described in SCORM only exists during the life of a sharable content object (SCO) communication session. There is no SCORM API that exists outside of that communication session.
  - Reporting and data access requirements are not standardized in SCORM resulting in proprietary, LMS-specific, reporting functionality that can differ between vendors.  

##2.0 When to Use this Profile
The Experience API by design is flexible enough to support many training scenarios. This flexibility enables it to support learning solutions that are currently difficult or impossible in the SCORM model. But flexibility without consensus on how to represent the data prevents interoperability.  

This profile should be used when the organization already has a SCORM learning environment but wants to utilize the xAPI to enable features that SCORM does not support, such as the examples listed in section 1.0. These can include:  
- Modifying SCORM content to post learning events (xAPI Statements) to an LRS to allow for other systems to access the data typically stored in an LMS.  
- Creating learning applications that are not SCORM content that can report data to an LRS in the same way as SCORM content, providing an interoperable data format for learning experiences produced both by SCORM content and other learning content.  

Use of this profile allows organizations to incrementally transition from a centralized SCORM LMS to diverse and flexible systems without the loss of interoperability. It also allows for systems, such as SCORM LMSs and third party reports, to treat experiences from SCORM content and non SCORM content the same way.  

## 3.0 How to Use this Profile
This document is intended to be used in addition to the [xAPI specification](https://github.com/adlnet/xAPI-Spec/blob/master/xAPI.md). All communication, data formats and experiences shall follow the requirements in the xAPI specification. The guidance provided in this document is to add information specifically to support SCORM communications in xAPI format.  

### 3.1 Supporting SCORM Features
SCORM is a mature and formal specification that allows for delivering content and tracking learner’s progress. By identifying the key features in SCORM, it is possible to provide guidance on how to implement the same features with the xAPI, such as:

- Launching and Initializing Content
- Supporting the SCORM Temporal Model
- Mapping the SCORM data model to xAPI Statements

### 3.2 General Guidance on Statements
In the xAPI, activity providers and activities issue statements about the learner’s experiences. These statements hold the data about the experience, such as, if the learner was successful, or did the learner complete the content. Additional information and guidance is provided below. All statements issued shall meet the requirements in the xAPI specification and the guidance described in the following sections.  

#### IRIs
[IRIs](https://github.com/adlnet/xAPI-Spec/blob/master/xAPI.md#def-iri) are used as identifiers in many parts of the xAPI specification. Their syntax consists of a hierarchical part, which is broken into an authority and a path. The authority part shall represent a domain of your organization - ie. adlnet.gov, army.mil. The path part shall identify the object - /courses/cs/CS101. If you are identifying something that cannot be represented by an fully qualified path, use a tag IRI - tag:adlnet.gov,2013:expapi:0.9:extensions - where the domain is a domain you control, the date is the date this tag was created, the next part is the type - scorm, xapi, the version - 2004, 1.2, 1.0.1, and the last part is the identifier. (see [http://www.ietf.org/rfc/rfc4151.txt](http://www.ietf.org/rfc/rfc4151.txt))  

__Good IRIs__  
Good IRIs uniquely identify an object  
  <pre>`http://adlnet.gov/activities/courses/CS/CS101`</pre>
  <pre>`http://mydomain.com/content/understanding-fire-safety`</pre>
__Bad IRIs__  
Bad IRIs are not unique and could conflict with others using the same identifier  
    <pre>`act:my-activity01`</pre>
    <pre>`http://example.com/activity/01`</pre>

#### Actor
The actor property refers to the learner that is interacting with the activity. The actor should be able to be mapped back to the learner in the LMS. Any of the [Actor formats described in the xAPI specification](https://github.com/adlnet/xAPI-Spec/blob/master/xAPI.md#actor) are allowed. However some formats can potentially expose personally identifiable information, it is recommended to use a format that protects the learner’s information.  
__Agent__
``` javascript
  "actor":{
    "account":{
       "homePage":"http://lms.adlnet.gov/",
       "name":"500-627-490"
    }
  }
```
__Group__
``` javascript
"actor":{
  "objectType":"Group",
  "name":"team a",
  "member":[
    {
       "account":{
          "homePage":"http://lms.adlnet.gov/",
          "name":"500-627-490"
       }
    },
    {
       "account":{
          "homePage":"http://lms.adlnet.gov/",
          "name":"500-344-153"
       }
    }
  ]
}
```  

#### Verb
Verbs in the xAPI spec represent the action that is being recorded for this experience, such as "read" a book and "answered" a question. The xAPI allows for any verb to be used within a statement assuming it follows the [rules defined in the xAPI specification](https://github.com/adlnet/xAPI-Spec/blob/master/xAPI.md#verb). However this flexibility causes issues when trying to report on the data. For consistency and interoperability, those implementing this profile shall use the verbs maintained by ADL at http://adlnet.gov/expapi/verbs/, and use the definition and usage on the ADL Verb pages as guidance.  
__Verb__  
``` javascript
"verb":{
    "id":"http://adlnet.gov/expapi/verbs/initialized",
    "display":{
       "en-US":"initialized"
    }
 }
```  
Some verbs have special meaning when related to SCORM. Implementers of this profile shall use these verbs only when reporting the events in the following table:  
<table>
  <tr><th>xAPI Verb</th><th>SCORM Equivalent</th><th>Description</th><th>Scope</th></tr>
  <tr>
    <td><a href="http://adlnet.gov/expapi/verbs/initialized">initialized</a></td>
    <td>Initialize()<br>LMSInitialize()</td>
    <td>Initialization of the SCO attempt</td>
    <td>SCO</td>
  </tr>
  <tr>
    <td><a href="http://adlnet.gov/expapi/verbs/terminated">terminated</a></td>
    <td>Terminate()<br>LMSFinish()</td>
    <td>Termination of the SCO attempt</td>
    <td>SCO</td>
  </tr>
  <tr>
    <td><a href="http://adlnet.gov/expapi/verbs/suspended">suspended</a></td>
    <td>cmi.exit=suspend<br>cmi.core.exit=suspend</td>
    <td>Suspension of the SCO attempt</td>
    <td>SCO</td>
  </tr>
  <tr>
    <td><a href="http://adlnet.gov/expapi/verbs/resumed">resumed</a></td>
    <td>cmi.entry=resume<br>cmi.core.entry=resume</td>
    <td>Resumption of the SCO attempt</td>
    <td>SCO</td>
  </tr>
  <tr>
    <td><a href="http://adlnet.gov/expapi/verbs/passed">passed</a></td>
    <td>cmi.success_status=passed<br>cmi.core.lesson_status=passed</td>
    <td>The leaner's performance on this attempt at least met the minimum threshold for the activity</td>
    <td>course<br>SCO<br>objective</td>
  </tr>
  <tr>
    <td><a href="http://adlnet.gov/expapi/verbs/failed">failed</a></td>
    <td>cmi.success_status=failed<br>cmi.core.lesson_status=failed</td>
    <td>The performance on this attempt did not meet the minimum threshold for the activity</td>
    <td>course<br>SCO<br>objective</td>
  </tr>
  <tr>
    <td><a href="http://adlnet.gov/expapi/verbs/scored">scored</a></td>
    <td>cmi.scored.scaled<br>cmi.core.score.raw</td>
    <td>Used when the activity wants to record a score without implying a level of satisfaction or completion of the activity, or wants to provide evidence toward satisfaction or completion</td>
    <td>course<br>SCO<br>objective</td>
  </tr>
  <tr>
    <td><a href="http://adlnet.gov/expapi/verbs/completed">completed</a></td>
    <td>cmi.completion_status=completed<br>cmi.core.lesson_status=completed</td>
    <td>The learner has experienced a sufficient amount of the activity</td>
    <td>course<br>SCO<br>objective</td>
  </tr>
  <tr>
    <td><a href="http://adlnet.gov/expapi/verbs/responded">responded</a></td>
    <td>cmi.interactions.n.learner_response<br>cmi.interactions.n.student_response</td>
    <td>The learner's response to some interaction</td>
    <td>interaction</td>
  </tr>
</table>

#### Object
The object property describes the item with which the learner is interacting. The type of object could be an Activity, an Actor or Group, or a Statement (as StatementRef or Sub-Statement). If it is an Actor or a Statement follow the rules defined in the [xAPI specification](https://github.com/adlnet/xAPI-Spec/blob/master/xAPI.md#414-object). However if it is an Activity, follow the rules in the xAPI specification and the rules outlined below.  

##### Activity
Things like courses, SCOs, and objectives are considered activities. Since these experiences are commonly what SCORM content wants to capture, the following sections detail the recommended usage to create interoperable statements.  

###### Activity IRI
Activity IDs are required to be [IRIs](http://en.wikipedia.org/wiki/Internationalized_resource_identifier) and follow the requirements within the [xAPI specification](https://github.com/adlnet/xAPI-Spec/blob/master/xAPI.md#4141-when-the-objecttype-is-activity). In addition it is recommended that the IRIs are IRLs and that the location contains the metadata ([Activity Definition](https://github.com/adlnet/xAPI-Spec/blob/master/xAPI.md#activity-definition)) of the activity. Additionally activity IRIs should be constructed in a predictable way to make interpreting those IRIs possible in a standard way.  

###### Course IRI
The course IRI may be decided by the organization as long as it follows the IRI rules described in the xAPI spec. The activity provider or activity must support the launch courseIRI property, described in the launch section of this document, and update the course IRI to that property value if the local and launch-provided values differ. This allows for content to use the most up-to-date identifier in the context of the current launch.  

__Guidelines for Activity IRI Construction__  
- Follow the guidance described in the Internationalized Resource Identifier (IRI) section in this document
- Course IRIs should be in the format: `<scheme>://<authority>/<course path>`
  - Course path is any IRI path to the course activity definition, ie `courses/CS/101`
- SCO IRIs should be in the format: `<courseIRI>/<sco path>`
  - SCO path is any IRI path to the SCO activity definition, ie `lesson/01`
- Interaction IRIs should be in the format: `<scoIRI>/interactions/<interaction path>`
  - Interaction path is any IRI path to the interaction activity definition, ie `multi-choice/07`
- Objectives IRIs vary depending on the scope of the objective
  - If the objective is local to the SCO: `<scoIRI>/objectives/<objective path>`
  - If the objective is available to the entire course: `<courseIRI>/objectives/<objective path>`
  - If the objective is available to any course (global): `<scheme>://<authority>/objectives/<objective path>`
  - Objective path is any IRI path to the objective activity definition, ie `recognize-shapes-obj/`

###### Activity Definition
The [activity definition](https://github.com/adlnet/xAPI-Spec/blob/master/xAPI.md#activity-definition) provides information about the activity. At a minimum all activities should include an activity definition with a name, description and type. If the activity is representing a SCORM interaction, follow the rules outlined in the xAPI specification for [interaction activities](https://github.com/adlnet/xAPI-Spec/blob/master/xAPI.md#interactionacts).  

###### Activity Types  
Activity types are used to identify what an activity represents, both to humans and machines. The type could be used to reporting systems to determine, for example, what Statements are about assessments. Including an activity type is recommended. The following table describes types to be used for common SCORM concepts such as SCOs and interactions.  

<table>
<tr><th>SCORM object</th><th>Activity Type IRI</th></tr>
<tr><td>course</td><td><a href="http://adlnet.gov/expapi/activities/course">http://adlnet.gov/expapi/activities/course</a></td></tr>
<tr><td>module</td><td><a href="http://adlnet.gov/expapi/activities/module">http://adlnet.gov/expapi/activities/module</a></td></tr>
<tr><td>SCO</td><td><a href="http://adlnet.gov/expapi/activities/lesson">http://adlnet.gov/expapi/activities/lesson</a></td></tr>
<tr><td>assessment</td><td><a href="http://adlnet.gov/expapi/activities/assessment">http://adlnet.gov/expapi/activities/assessment</a></td></tr>
<tr><td>interaction</td><td><a href="http://adlnet.gov/expapi/activities/interaction">http://adlnet.gov/expapi/activities/interaction</a></td></tr>
<tr><td>objective</td><td><a href="http://adlnet.gov/expapi/activities/objective">http://adlnet.gov/expapi/activities/objective</a></td></tr>
<tr><td>attempt</td><td><a href="http://adlnet.gov/expapi/activities/attempt">http://adlnet.gov/expapi/activities/attempt</a></td></tr>
</table>

#### Result
The [result property of a statement](https://github.com/adlnet/xAPI-Spec/blob/master/xAPI.md#415-result) represents the outcome of a learner experience. Statements issued using a result shall follow the requirements listed in the xAPI specification and the additional guidance described in this document.

#### Context
The context property adds additional contextual information about the learner experience. Information like who is the instructor of this content, with what registration this experience is associated, or to what activities this experience is related. Statements shall meet all the [requirements in the xAPI specification](https://github.com/adlnet/xAPI-Spec/blob/master/xAPI.md#416-context) and the additional guidelines described in this document.  

##### Context Registration
[Context registration](https://github.com/adlnet/xAPI-Spec/blob/master/xAPI.md#4161-registration-property) is used to store an LMS registration value. This is value is up to the organization, LMS or developer and provides a way to easily query the LRS for Statements related to the registration value. [See the xAPI spec for query options](https://github.com/adlnet/xAPI-Spec/blob/master/xAPI.md#723-getstatements).  

##### Context Activities
[Context activities](https://github.com/adlnet/xAPI-Spec/blob/master/xAPI.md#4162-contextactivities-property) allow statements to be related to other activities. Regarding this profile, the context activities are used to relate Statements by SCO, course, assessment, or other groupings. The following rules are defined to support those groupings.  

<table>
<tr><th>Type</th><th>Use</th></tr>
<tr><td>parent</td><td>Used to identify the activity which contains the current activity, such as the activity of the SCO that contains an assessment, interaction, or objective.</td></tr>
<tr><td>grouping</td><td>Used to identify the course activity and any other activities that should be grouped together.</td></tr>
<tr><td>category</td><td>All Statements based on this profile shall include the xAPI SCORM Profile activity.<br> {"id":"https://w3id.org/xapi/scorm"}</td></tr>
<tr><td>other</td><td>Up to the organization or developer.</td></tr>
</table>

#### Timestamp
The [timestamp property](https://github.com/adlnet/xAPI-Spec/blob/master/xAPI.md#417-timestamp) gives the activity provider or activity the ability to set the date and time when the experience occurred. This is different from the [stored timestamp](https://github.com/adlnet/xAPI-Spec/blob/master/xAPI.md#418-stored) property, which indicates when the LRS saved the statement about the experience. All statements shall set the timestamp property. By doing this, it makes it possible to order statements in the same order as they were submitted by the activity provider or activity.

#### Authority
The [authority property](https://github.com/adlnet/xAPI-Spec/blob/master/xAPI.md#419-authority) for each statement is set by the LRS to the agent who submitted the statement. This property can be used to filter statements based on the activity provider or activity. By using this property as a GET statements filter, it is possible to narrow down the returned statements to the ones submitted by agents whom your organization trusts.

#### Attachments
Attachments give the ability to include supporting documents or information that do not directly map to a section of an xAPI statement. Examples of attachments include PDF certificates, essays, videos, and the JSON web signature. Attachments are not returned by the LRS by default, but can be included by adding the attachments filter to GET statements requests. [See the xAPI specification for more details](https://github.com/adlnet/xAPI-Spec/blob/master/xAPI.md#signature).

## 4.0 Launching and Initializing Activities
In a SCORM environment, an activity is launched by the LMS. The LMS can provide activities with launch parameters and initial data model values. This helps a SCO to work correctly in the current environment. In comparison, xAPI activities can exist outside of an LMS - information such as learner name and identifier, or the location of the xAPI LRS may be unknown at the launch of the activity.

Solutions such as ADL xAPI Launch, Rustici Software Launch, AICC CMI5 and IMS LTI all provide ways for systems, such as an LMS, to launch and initialize activities that are not managed by the LMS. Any of those solutions may be leveraged to solve specific, individual issues that are not addressed in this document. At a minimum the following properties are recommended for launching and initializing activities:  
- entry: ab-initio or resume
- endpoint: LRS endpoint
- actor: Agent Account
  - Account Homepage: location of the LMS that holds the user account information
  - Account Name: an identifier for the learner that is at least unique to the scope of the LMS
    - It is recommended that the name is does not contain personally identifiable information such as the learner’s name
- courseiri: IRI that identifies the entire course within at least the context of the LMS
  - It is recommended that this identifier is unique and defined by a domain which your organization controls. ex: `http://adlnet.gov/courses/compsci/xxx`  

Since xAPI activites do not need to be web-based, the means of initializing the activities will vary. Following are three strategies:  

### 4.1 Web-Based Activities
The activity is hosted on some web server and is launched in a web browser. This strategy is similar to SCORM content but is not required to be hosted by the LMS. In this scenario, the LMS, or some system responsible for knowing about the learner and this activity, launches the activity with the launch parameters.  
__Example:__
__Decoded for readability:__  
```
http://adlnet.gov/mycontent?entry=ab-initio&endpoint=https://lrs.adlnet.gov/xapi/&actor={"account":{"homePage":"http://lms.adlnet.gov/scorm/","name":"149893"}}&courseiri=http://adlnet.gov/courses/compsci/xxx
```  
__URL-encoded:__  
```
http://adlnet.gov/mycontent?entry=ab-initio&endpoint=https%3A%2F%2Flrs.adlnet.gov%2Fxapi%2F&actor=%7B%22account%22%3A%7B%22homePage%22%3A%22http%3A%2F%2Flms.adlnet.gov%2Fscorm%2F%22%2C%22name%22%3A%22149893%22%7D%7D&courseiri=http%3A%2F%2Fadlnet.gov%2Fcourses%2Fcompsci%2Fxxx
```  

### 4.2 LMS-Provided Endpoint
The LMS provides an endpoint that activity providers can query to retrieve the launch parameters. Web-based applications can still access this information via an AJAX GET request to the LMS provided endpoint. All other content would access this information in a similar way by issuing an HTTP GET request for the launch parameters.  
__Request:__  
``` HTTP GET launch/?agentid=<learner id>&courseiri=<course iri> ```  
> NOTE: How the activity provider gets the learner id, course IRI and location of the endpoint is up to the content developer and the LMS.  

__Response:__  
``` javascript
Content-Type: application/json
{
   "entry":"ab-initio",
   "endpoint":"https://lrs.adlnet.gov/xapi/",
   "actor":
   {
      "account":
      {
          "homePage":"http://lms.adlnet.gov/scorm/",
          "name":"149893"
      }
   },
   "courseiri":"http://adlnet.gov/courses/compsci/xxx"
}
```  
> NOTE: The course IRI in this response shall be used in all statements issued for this activity. This requirement allows for the LMS to change the IRI from the one originally configured in the activity. This may be necessary to accommodate for changes due to various sessions, or other changes that occurred since the initial creation of the course IRI.  

### 4.3 Out-of-Band Configuration
If the above launch options are not possible developers can preconfigure the activity provider or allow for user input to configure the launch parameters. Work with the LMS and LRS providers for configuration details.  

## 5.0 Supporting the SCORM Temporal Model
SCORM has a temporal model which describes interaction states such as an attempt and a session. The xAPI uses an Activity Stream style model where experiences are all reported to the stream without a sense of session or attempt. This does not mean, however, that xAPI statements cannot be related to one another. By properly using the context attribute of a Statement it is possible to group Statements using the registration ID or broader activity IDs.  

### Initializing an attempt
*  Generate the activity attempt IRI. The way this is done is up to the developer. The only requirement is that the attempt IRI is unique.  
*  Add the attempt IRI to the `attempts` array in the Activity State document either by creating the `attempts` array or appending to the existing array. See the [Appendix](#scorm-activity-state) for the Activity State format.  
*  Create a Statement  
    *  Set `actor` to the learner's agent object  
    *  Set `verb` to the ADL Verb [initialized](http://adlnet.gov/expapi/verbs/initialized)  
    *  Set `object` to the activity object for the SCO, using the SCO IRI as the activity's ID  
    *  Set `object.definition.type` to `http://adlnet.gov/expapi/activities/lesson`
    *  Set `context.contextActivities.grouping` array to include the attempt activity and the course activity  
    *  Set `context.contextActivities.category` array to include the xAPI SCORM Profile activity ([See context for profile activity](#context))  
    *  Set `timestamp` to the time the attempt was initialized, see [timestamp](https://github.com/adlnet/xAPI-Spec/blob/master/xAPI.md#417-timestamp) for details  

([See an example in the Appendix](#initialize-a-sco-attempt))  

### Reporting learner activity during an attempt  
During the session, Statements are collected and sent to the LRS much like SCORM SCOs reporting to the LMS. Statements can be sent to the LRS either immediately or collected and sent as a bundle. A few rules need to be followed to connect attempt relevant statements.
*  Set `actor` to the learner's agent object
*  If the statement is about the SCO, such as completed or commented, set `object` to the activity object for the SCO, using the SCO IRI as the activity's ID
*  If the statement is about something within the SCO, such as a video or test,
    *  set `object` to the activity object for the SCO -  determination of the activity ID is outside the scope of this profile
    *  set `context.contextActivities.parent` array to include the activity object for the SCO
*  Set `context.contextActivities.grouping` array to include the attempt activity and the course activity  
*  Set `context.contextActivities.category` array to include the xAPI SCORM Profile activity ([See context for profile activity](#context))
*  Set `timestamp` to the time the attempt was initialized, see [timestamp](https://github.com/adlnet/xAPI-Spec/blob/master/xAPI.md#417-timestamp) for details

### Terminating an attempt  
*  Create a Statement  
    *  Set `actor` to the learner's agent object  
    *  Set `verb` to the ADL Verb [terminated](http://adlnet.gov/expapi/verbs/terminated)  
    *  Set `object` to the activity object for the SCO, using the SCO IRI as the activity's ID  
    *  Set `object.definition.type` to `http://adlnet.gov/expapi/activities/lesson`
    *  Set `context.contextActivities.grouping` array to include the attempt activity and the course activity  
    *  Set `context.contextActivities.category` array to include the xAPI SCORM Profile activity ([See context for profile activity](#context))  
    *  Set `timestamp` to the time the attempt was terminated, see [timestamp](https://github.com/adlnet/xAPI-Spec/blob/master/xAPI.md#417-timestamp) for details
    *  Set `result` to the overall result for the SCO
         *  If success_status of the SCO is known, `success` is `true` if success_status is passed, and `false` if success_status is failed
         *  If completion_status of the SCO is known, `completion` is `true` if completion_status is completed, and `false` if completion_status is incomplete
         *  If score of the SCO is known, use the appropriate score property to store SCORM score data model elements, such as `score.scaled` for `cmi.score.scaled`

([See an example in the Appendix](#terminate-a-sco))  

### Suspending an attempt
To suspend a SCO attempt,  
 *  Create a Statement  
    *  Set `actor` to the learner's agent object  
    *  Set `verb` to the ADL Verb [suspended](http://adlnet.gov/expapi/verbs/suspended)  
    *  Set `object` to the activity object for the SCO, using the SCO IRI as the activity's ID  
    *  Set `object.definition.type` to `http://adlnet.gov/expapi/activities/lesson`
    *  Set `context.contextActivities.grouping` array to include the attempt activity and the course activity  
    *  Set `context.contextActivities.category` array to include the xAPI SCORM Profile activity ([See context for profile activity](#context))  
    *  Set `timestamp` to the time the attempt was suspended, see [timestamp](https://github.com/adlnet/xAPI-Spec/blob/master/xAPI.md#417-timestamp) for details
    *  (Optional) Set `result` to the overall result for the SCO
         *  If success_status of the SCO is known, `success` is `true` if success_status is passed, and `false` if success_status is failed
         *  If completion_status of the SCO is known, `completion` is `true` if completion_status is completed, and `false` if completion_status is incomplete
         *  If score of the SCO is known, use the appropriate score property to store SCORM score data model elements, such as `score.scaled` for `cmi.score.scaled`  
*  (Optional) Set the [attempt state values](#scorm-activity-attempt-state)  

([See an example in the Appendix](#suspend-a-sco))  

### Resuming an attempt
To resume the SCO attempt,  
*  Create a Statement  
    *  Set `actor` to the learner's agent object  
    *  Set `verb` to the ADL Verb [resumed](http://adlnet.gov/expapi/verbs/resumed)  
    *  Set `object` to the activity object for the SCO, using the SCO IRI as the activity's ID  
    *  Set `object.definition.type` to `http://adlnet.gov/expapi/activities/lesson`
    *  Set `context.contextActivities.grouping` array to include the attempt activity, created during the original initialization of the SCO, and the course activity  
    *  Set `context.contextActivities.category` array to include the xAPI SCORM Profile activity ([See context for profile activity](#context))  
    *  Set `timestamp` to the time the attempt was initialized, see [timestamp](https://github.com/adlnet/xAPI-Spec/blob/master/xAPI.md#417-timestamp) for details    

([See an example in the Appendix](##resume-a-sco))  

### Querying the LRS for Statements in an attempt  
Querying systems can find the the list of attempt IRIs for a SCO by [getting the Activity State](https://github.com/adlnet/xAPI-Spec/blob/master/xAPI.md#74-state-api). The resulting JSON object contains an `attempts` array containing the attempt IRIs ordered from first to latest attempt. The querying system can get the Statements from the LRS by [querying for all Statements](#find-all-statements-from-the-latest-attempt) with the attempt IRI. See the Appendix for [query examples](#query-examples).  

### Representing the temporal model with xAPI Statements  
This section describes when to issue the statements outlined above to represent the SCORM temporal model.  

#### New attempt with normal exit
 * Send an [initialize](#initializing-an-attempt) statement
 * Send various statements about the activity
 * Send a [terminate](#terminating-an-attempt) statement

#### New attempt with suspend
 * Send an [initialize](#initializing-an-attempt) statement
 * Send various statements about the activity
 * Send a [suspend](#suspending-an-attempt) statement

#### Resume attempt with suspend
 * Send an [resume](#resuming-an-attempt) statement
 * Send various statements about the activity
 * Send a [suspend](#suspending-an-attempt) statement

#### Resume attempt with normal exit
 * Send an [resume](#resuming-an-attempt) statement
 * Send various statements about the activity
 * Send a [terminate](#terminating-an-attempt) statement

## 6.0 Mapping the SCORM Data Model to xAPI Statements
The following is a list of SCORM data model elements and the equivalent xAPI statement. Using this mapping will allow systems to interpret the xAPI statements in an interoperable way.   

### Providing support data
Some SCORM data model elements represent data that is not about learner experiences or performance. Elements such as launch data, suspend data and learner preferences may be important or necessary, but are not expected to be reported as xAPI Statements. This data can be stored in the LRS document storage, such as Activity Profile and Activity State. A complete representation of the document data and formats is defined in the [Appendix](#xapi-scorm-data-objects).  

#### Comments From Learner
SCORM 1.2 Comments and SCORM 2004 Comments from Learner mapped to an Experience API Statement. The `commented` ADL Verb is used with the comment as the xAPI Statement result response value. For SCORM 2004 where there is also a timestamp and a location, use the statement timestamp attribute for the comment timestamp value and the Activity URI as the location.  
__SCORM 2004:__ `cmi.comments_from_learner`  
__SCORM 1.2:__ `cmi.comments`  
__Experience API Statement:__   
``` javascript
{
   "actor":{
      "account":{
         "homePage":"http://lms.adlnet.gov/",
         "name":"500-627-490"
      }
   },
   "verb":{
      "id":"http://adlnet.gov/expapi/verbs/commented",
      "display":{
         "en-US":"commented"
      }
   },
   "object":{
      "id":"http://adlnet.gov/courses/compsci/CS204/lesson01/01",
      "definition":{
         "name":{
            "en-US":"lesson 01"
         },
         "description":{
            "en-US":"The first lesson of CS204"
         },
         "type": "http://adlnet.gov/expapi/activities/lesson"
      }
   },
   "result":{
      "response":"This is a great lesson. You do such a wonderful job teaching!"
   },
   "timestamp":"2014-09-29T18:18:24.316Z",
   "context":{
      "contextActivities":{
         "grouping":[
            {
               "id":"http://adlnet.gov/courses/compsci/CS204/",
               "definition":{
                  "name":{
                     "en-US":"CS204"
                  },
                  "description":{
                     "en-US":"The activity representing the course CS204"
                  },
                  "type": "http://adlnet.gov/expapi/activities/course"
               }
            },
            {
               "id":"http://adlnet.gov/courses/compsci/CS204/lesson01/01?attemptId=50fd6961-ab6c-4e75-e6c7-ca42dce50dd6",
               "definition":{
                  "name":{
                     "en-US":"Attempt of CS204 lesson 01"
                  },
                  "description":{
                     "en-US":"The activity representing an attempt of lesson 01 in the course CS204"
                  },
                  "type": "http://adlnet.gov/expapi/activities/attempt"
               }
            }
         ],
         "category": [
            {
               "id": "https://w3id.org/xapi/scorm"
            }
         ]
      }
   }
}
```  

#### Comments From LMS
Comments From LMS allows an activity to see comments about the content. The value is the same for all learners, and is made available for each activity. For those reasons, Comments From LMS is available at the Activity Profile endpoint.  
__SCORM 2004:__ `cmi.comments_from_lms`  
__SCORM 1.2:__ `cmi.comments_from_lms`  
__Experience API:__ `comments_from_lms` in the [SCORM Activity Profile Object](#scorm-activity-profile)  
See [Get xAPI SCORM Activity Profile](#get-xapi-scorm-activity-profile) for retrieving the Activity Profile Object.  

#### Completion Status
Completion indicates if the learner has completed the activity. The use of this Statement is for journaling/auditing purposes and does not necessarily indicate completion of the activity. If it is determined that the activity must have a completion status, set it explicitly as the [result of terminated Statement](#terminating-an-attempt).  

__SCORM 2004:__ `cmi.completion_status=completed`  
__SCORM 1.2:__ `cmi.core.lesson_status=completed`  
__Experience API Statement:__   
``` javascript
{
    "actor": {
        "account": {
            "homePage": "http://lms.adlnet.gov/",
            "name": "500-627-490"
        }
    },
    "verb": {
        "id": "http://adlnet.gov/expapi/verbs/completed",
        "display": {
            "en-US": "completed"
        }
    },
    "object": {
        "id": "http://adlnet.gov/courses/compsci/CS204/lesson01/01",
        "definition": {
            "name": {
               "en-US" : "lesson 01"
            },
            "description" : {
               "en-US" : "The first lesson of CS204"
            },
            "type": "http://adlnet.gov/expapi/activities/lesson"
        }
    },
    "context": {
        "contextActivities": {
            "grouping": [
                {
                  "id":"http://adlnet.gov/courses/compsci/CS204/",
                  "definition":{
                     "name":{
                        "en-US":"CS204"
                     },
                     "description":{
                        "en-US":"The activity representing the course CS204"
                     },
                     "type": "http://adlnet.gov/expapi/activities/course"
                  }
               },
               {
                  "id":"http://adlnet.gov/courses/compsci/CS204/lesson01/01?attemptId=50fd6961-ab6c-4e75-e6c7-ca42dce50dd6",
                  "definition":{
                     "name":{
                        "en-US":"Attempt of CS204 lesson 01"
                     },
                     "description":{
                        "en-US":"The activity representing an attempt of lesson 01 in the course CS204"
                     },
                     "type": "http://adlnet.gov/expapi/activities/attempt"
                  }
               }
            ],
            "category": [
               {
                  "id": "https://w3id.org/xapi/scorm"
               }
            ]
        }
    }
}
```    

#### Completion Threshold
Completion Threshold is a value that can be used to determine if an activity is complete. This value is the same for all learners, and is made available for each activity. For those reasons, Completion Threshold is available at the Activity Profile endpoint.  
__SCORM 2004:__ `cmi.completion_threshold`  
__SCORM 1.2:__ N/A    
__Experience API:__ `completion_threshold` in the [SCORM Activity Profile Object](#scorm-activity-profile)  
See [Get xAPI SCORM Activity Profile](#get-xapi-scorm-activity-profile) for retrieving the Activity Profile Object.  

#### Credit
Credit is used to indicate if an activity attempt status should be credited. This value is can vary for learners, and is made available for each activity. For those reasons, Credit is available at the Activity State endpoint.  
__SCORM 2004:__ `cmi.credit`  
__SCORM 1.2:__ `cmi.core.credit`    
__Experience API:__ `credit` in the [SCORM Activity Attempt State Object](#scorm-activity-attempt-state)  
See [Get xAPI SCORM Activity Attempt State](#get-xapi-scorm-activity-attempt-state) for retrieving the Activity Attempt State Object.  

#### Entry
Entry is used to indicate the attempt state of the activity - is this a new attempt on the activity or a continuation of the previous attempt? There is no direct mapping to an xAPI statement such as “actor entered activity with result ab-initio”. Instead this is implied by issuing a statement with the ADL Verb `initialized` and a new attemptId on the grouping activity.

##### Initialize a new attempt  
__SCORM 2004:__ `cmi.entry=ab-initio`  
__SCORM 1.2:__ `cmi.core.entry=ab-initio`  
__Experience API Statement:__
``` javascript
{
    "actor": {
        "account": {
            "homePage": "http://lms.adlnet.gov/",
            "name": "500-627-490"
        }
    },
    "verb": {
        "id": "http://adlnet.gov/expapi/verbs/initialized",
        "display": {
            "en-US": "initialized"
        }
    },
    "object": {
        "id": "http://adlnet.gov/courses/compsci/CS204/lesson01/01",
        "definition": {
            "name": {
               "en-US" : "lesson 01"
            },
            "description" : {
               "en-US" : "The first lesson of CS204"
            },
            "type": "http://adlnet.gov/expapi/activities/lesson"
        }
    },
    "context": {
        "contextActivities": {
            "grouping": [
               {
                  "id":"http://adlnet.gov/courses/compsci/CS204/",
                  "definition":{
                     "name":{
                        "en-US":"CS204"
                     },
                     "description":{
                        "en-US":"The activity representing the course CS204"
                     },
                     "type": "http://adlnet.gov/expapi/activities/course"
                  }
               },
               {
                  "id":"http://adlnet.gov/courses/compsci/CS204/lesson01/01?attemptId=50fd6961-ab6c-4e75-e6c7-ca42dce50dd6",
                  "definition":{
                     "name":{
                        "en-US":"Attempt of CS204 lesson 01"
                     },
                     "description":{
                        "en-US":"The activity representing an attempt of lesson 01 in the course CS204"
                     },
                     "type": "http://adlnet.gov/expapi/activities/attempt"
                  }
               }
            ],
            "category": [
               {
                  "id": "https://w3id.org/xapi/scorm"
               }
            ]
        }
    }
}
```  


##### Resume a suspended attempt  
__SCORM 2004:__ `cmi.entry=resume`  
__SCORM 1.2:__ `cmi.core.entry=resume`  
__Experience API Statement:__
``` javascript
{
    "actor": {
        "account": {
            "homePage": "http://lms.adlnet.gov/",
            "name": "500-627-490"
        }
    },
    "verb": {
        "id": "http://adlnet.gov/expapi/verbs/resumed",
        "display": {
            "en-US": "resumed"
        }
    },
    "object": {
        "id": "http://adlnet.gov/courses/compsci/CS204/lesson01/01",
        "definition": {
            "name": {
               "en-US" : "lesson 01"
            },
            "description" : {
               "en-US" : "The first lesson of CS204"
            },
            "type": "http://adlnet.gov/expapi/activities/lesson"
        }
    },
    "context": {
        "contextActivities": {
            "grouping": [
               {
                  "id":"http://adlnet.gov/courses/compsci/CS204/",
                  "definition":{
                     "name":{
                        "en-US":"CS204"
                     },
                     "description":{
                        "en-US":"The activity representing the course CS204"
                     },
                     "type": "http://adlnet.gov/expapi/activities/course"
                  }
               },
               {
                  "id":"http://adlnet.gov/courses/compsci/CS204/lesson01/01?attemptId=50fd6961-ab6c-4e75-e6c7-ca42dce50dd6",
                  "definition":{
                     "name":{
                        "en-US":"Attempt of CS204 lesson 01"
                     },
                     "description":{
                        "en-US":"The activity representing an attempt of lesson 01 in the course CS204"
                     },
                     "type": "http://adlnet.gov/expapi/activities/attempt"
                  }
               }
            ],
            "category": [
               {
                  "id": "https://w3id.org/xapi/scorm"
               }
            ]
        }
    }
}
```   

#### Exit
Exit is used to indicate the attempt state at the end of the session. It is possible to send an xAPI exited statement but in most cases the intended meaning is that the session has terminated in either a suspended or terminated state. This is accomplished by issuing a statement with the ADL Verb `suspended` and maintaining the current attemptId for future sessions, or with the ADL Verb `terminated` and a new attemptId for future sessions.

##### Terminate an attempt
__SCORM 2004:__ `cmi.exit=normal`  
__SCORM 1.2:__ `cmi.core.exit=""`  
__Experience API Statement:__
``` javascript
{
    "actor": {
        "account": {
            "homePage": "http://lms.adlnet.gov/",
            "name": "500-627-490"
        }
    },
    "verb": {
        "id": "http://adlnet.gov/expapi/verbs/terminated",
        "display": {
            "en-US": "terminated"
        }
    },
    "object": {
        "id": "http://adlnet.gov/courses/compsci/CS204/lesson01/01",
        "definition": {
            "name": {
               "en-US" : "lesson 01"
            },
            "description" : {
               "en-US" : "The first lesson of CS204"
            },
            "type": "http://adlnet.gov/expapi/activities/lesson"
        }
    },
    "context": {
        "contextActivities": {
            "grouping": [
                {
                  "id":"http://adlnet.gov/courses/compsci/CS204/",
                  "definition":{
                     "name":{
                        "en-US":"CS204"
                     },
                     "description":{
                        "en-US":"The activity representing the course CS204"
                     },
                     "type": "http://adlnet.gov/expapi/activities/course"
                  }
               },
               {
                  "id":"http://adlnet.gov/courses/compsci/CS204/lesson01/01?attemptId=50fd6961-ab6c-4e75-e6c7-ca42dce50dd6",
                  "definition":{
                     "name":{
                        "en-US":"Attempt of CS204 lesson 01"
                     },
                     "description":{
                        "en-US":"The activity representing an attempt of lesson 01 in the course CS204"
                     },
                     "type": "http://adlnet.gov/expapi/activities/attempt"
                  }
               }
            ],
            "category": [
               {
                  "id": "https://w3id.org/xapi/scorm"
               }
            ]
        }
    }
}
```  


##### Suspend an attempt
__SCORM 2004:__ `cmi.exit=suspend`  
__SCORM 1.2:__ `cmi.core.exit=suspend`  
__Experience API Statement:__
``` javascript
{
    "actor": {
        "account": {
            "homePage": "http://lms.adlnet.gov/",
            "name": "500-627-490"
        }
    },
    "verb": {
        "id": "http://adlnet.gov/expapi/verbs/suspended",
        "display": {
            "en-US": "suspended"
        }
    },
    "object": {
        "id": "http://adlnet.gov/courses/compsci/CS204/lesson01/01",
        "definition": {
            "name": {
               "en-US" : "lesson 01"
            },
            "description" : {
               "en-US" : "The first lesson of CS204"
            },
            "type": "http://adlnet.gov/expapi/activities/lesson"
        }
    },
    "context": {
        "contextActivities": {
            "grouping": [
                {
                  "id":"http://adlnet.gov/courses/compsci/CS204/",
                  "definition":{
                     "name":{
                        "en-US":"CS204"
                     },
                     "description":{
                        "en-US":"The activity representing the course CS204"
                     },
                     "type": "http://adlnet.gov/expapi/activities/course"
                  }
               },
               {
                  "id":"http://adlnet.gov/courses/compsci/CS204/lesson01/01?attemptId=50fd6961-ab6c-4e75-e6c7-ca42dce50dd6",
                  "definition":{
                     "name":{
                        "en-US":"Attempt of CS204 lesson 01"
                     },
                     "description":{
                        "en-US":"The activity representing an attempt of lesson 01 in the course CS204"
                     },
                     "type": "http://adlnet.gov/expapi/activities/attempt"
                  }
               }
            ],
            "category": [
               {
                  "id": "https://w3id.org/xapi/scorm"
               }
            ]
        }
    }
}
```  

#### Interactions
Interactions can be recorded using the xAPI. Interactions can be described in the xAPI using a predefined format that maps to SCORM interactions. Activity providers and activities shall use the ADL Verb `http://adlnet.gov/expapi/verbs/responded`, the result.response attribute of a statement for the response, and an activity definition as described in the xAPI specification to report the learner’s responses for an interaction. See the [interaction activities](https://github.com/adlnet/xAPI-Spec/blob/master/xAPI.md#interaction-activities) section and the [interaction appendix](https://github.com/adlnet/xAPI-Spec/blob/master/xAPI.md#AppendixC) for more details.

> NOTE: The IRI used to identify an interaction is recommended to follow the format: `<courseiri>/<scoid>/interaction/<interactionid>`  

#### Launch Data
Launch Data provides data to the activity to help initialize the content. The value is the same for all learners, and is made available for each activity. For those reasons, Launch Data is available at the Activity Profile endpoint.  
__SCORM 2004:__ `cmi.launch_data`  
__SCORM 1.2:__ `cmi.launch_data`  
__Experience API:__ `launch_data` in the [SCORM Activity Profile Object](#scorm-activity-profile)  
See [Get xAPI SCORM Activity Profile](#get-xapi-scorm-activity-profile) for retrieving the Activity Profile Object.  

#### Learner ID
Learner ID contains the identifier associated with a learner in the LMS. This value may be used to generate the [Agent information for launch](#40-launching-and-initializing-activities). This value also may be set in the [Agent Profile Object](#agent-profile).  
__SCORM 2004:__ `cmi.learner_id`   
__SCORM 1.2:__ `cmi.core.student_id`  
__Experience API:__  `learner_id` in the [SCORM Agent Profile Object](#agent-profile)  
See [Get xAPI SCORM Agent Profile](#get-xapi-scorm-agent-profile) for retrieving the Agent Profile Object.  

#### Learner Name
Learner Name contains the name associated with a learner in the LMS. This value may be used to generate the [Agent information for launch](#40-launching-and-initializing-activities). This value also may be set in the [Agent Profile Object](#agent-profile).  
__SCORM 2004:__ `cmi.learner_name`   
__SCORM 1.2:__ `cmi.core.student_name`  
__Experience API:__  `learner_name` in the [SCORM Agent Profile Object](#agent-profile)  
See [Get xAPI SCORM Agent Profile](#get-xapi-scorm-agent-profile) for retrieving the Agent Profile Object.  

#### Learner Preferences
Preferences set by the learner about how the content is presented. These values are editable by the learner and span the attempts on the activity. Due to this, specific learner preference settings may be stored in the [SCORM Activity Attempt State Object](#scorm-activity-attempt-state). SCORM also describes that default values may be defined for the learner. These default values may be stored in the [Agent Profile Object](#agent-profile).
##### Default Values
###### Audio Level
__SCORM 2004:__ `cmi.learner_preference.audio_level`   
__SCORM 1.2:__ `cmi.student_preference.audio`  
__Experience API:__ `audio_level` in the [SCORM Agent Profile Object](#agent-profile)  
See [Get xAPI SCORM Agent Profile](#get-xapi-scorm-agent-profile) for retrieving the Agent Profile Object.  

###### Language
__SCORM 2004:__ `cmi.learner_preference.language`   
__SCORM 1.2:__ `cmi.student_preference.language`  
__Experience API:__  `language` in the [SCORM Agent Profile Object](#agent-profile)  
See [Get xAPI SCORM Agent Profile](#get-xapi-scorm-agent-profile) for retrieving the Agent Profile Object.  

###### Delivery Speed
__SCORM 2004:__ `cmi.learner_preference.delivery_speed`   
__SCORM 1.2:__ `cmi.student_preference.speed`  
__Experience API:__  `delivery_speed` in the [SCORM Agent Profile Object](#agent-profile)  
See [Get xAPI SCORM Agent Profile](#get-xapi-scorm-agent-profile) for retrieving the Agent Profile Object.  

###### Audio Captioning
__SCORM 2004:__ `cmi.learner_preference.audio_captioning`   
__SCORM 1.2:__ `cmi.student_preference.text`  
__Experience API:__ `audio_captioning` in the [SCORM Agent Profile Object](#agent-profile)  
See [Get xAPI SCORM Agent Profile](#get-xapi-scorm-agent-profile) for retrieving the Agent Profile Object.  

##### Content Specific Values
###### Audio Level
__SCORM 2004:__ `cmi.learner_preference.audio_level`   
__SCORM 1.2:__ `cmi.student_preference.audio`  
__Experience API:__ `audio_level` in the [SCORM Activity Attempt State Object](#scorm-activity-attempt-state)   
See [Get xAPI SCORM Activity Attempt State](#get-xapi-scorm-activity-attempt-state) for retrieving the Activity Attempt State Object.  

###### Language
__SCORM 2004:__ `cmi.learner_preference.language`   
__SCORM 1.2:__ `cmi.student_preference.language`  
__Experience API:__ `language` in the [SCORM Activity Attempt State Object](#scorm-activity-attempt-state)   
See [Get xAPI SCORM Activity Attempt State](#get-xapi-scorm-activity-attempt-state) for retrieving the Activity Attempt State Object.  

###### Delivery Speed
__SCORM 2004:__ `cmi.learner_preference.delivery_speed`   
__SCORM 1.2:__ `cmi.student_preference.speed`  
__Experience API:__ `delivery_speed` in the [SCORM Activity Attempt State Object](#scorm-activity-attempt-state)   
See [Get xAPI SCORM Activity Attempt State](#get-xapi-scorm-activity-attempt-state) for retrieving the Activity Attempt State Object.  

###### Audio Captioning
__SCORM 2004:__ `cmi.learner_preference.audio_captioning`   
__SCORM 1.2:__ `cmi.student_preference.text`  
__Experience API:__ `audio_captioning` in the [SCORM Activity Attempt State Object](#scorm-activity-attempt-state)   
See [Get xAPI SCORM Activity Attempt State](#get-xapi-scorm-activity-attempt-state) for retrieving the Activity Attempt State Object.  

#### Location
An element to hold a location for the content. This value is specific to the learner, and the activity, and is available at the Activity Attempt State endpoint.  
__SCORM 2004:__ `cmi.location`  
__SCORM 1.2:__ `cmi.core.lesson_location`    
__Experience API:__ `location` in the [SCORM Activity Attempt State Object](#scorm-activity-attempt-state)   
See [Get xAPI SCORM Activity Attempt State](#get-xapi-scorm-activity-attempt-state) for retrieving the Activity Attempt State Object.  

#### Max Time Allowed
Max Time Allowed defines how long a learner can interact with an activity. This value is the same for all learners, and is made available for each activity. For those reasons, Max Time Allowed is available at the Activity Profile endpoint.  
__SCORM 2004:__ `cmi.max_time_allowed`  
__SCORM 1.2:__ `cmi.student_data.max_time_allowed`   
__Experience API:__ `max_time_allowed` in the [SCORM Activity Profile Object](#scorm-activity-profile)  
See [Get xAPI SCORM Activity Profile](#get-xapi-scorm-activity-profile) for retrieving the Activity Profile Object.

#### Mode
Mode is used to indicate the presentation mode of the activity. This value is can vary for learners, and is made available for each activity. For those reasons, Mode is available at the Activity Attempt State endpoint.  
__SCORM 2004:__ `cmi.mode`  
__SCORM 1.2:__ `cmi.core.lesson_mode`    
__Experience API:__ `mode` in the [SCORM Activity Attempt State Object](#scorm-activity-attempt-state)   
See [Get xAPI SCORM Activity Attempt State](#get-xapi-scorm-activity-attempt-state) for retrieving the Activity Attempt State Object.  

#### Objectives
Objectives are represented as another activity. As such, statements about a learner’s score, success or completion status are reported just as they are for any other activity. But determining a consistent naming scheme for the objective ID makes it easier for reporting systems to understand the statements. For consistency the following guidance is recommended:
- The combination of course IRI, SCO ID, and objective ID should consistently and uniquely identify a single objective
- Use the following IRI syntax when defining an objective:
 - Local objective (SCO or activity level): `<courseIRI>/<SCOID>/objective/<objectiveID>`
 - Course objective (course level): `<courseIRI>/objective/<objectiveID>`
 - Global objective (for all courses): `<user defined IRI>/objective/<objective ID>`

> NOTE: To indicate where this objective statement occurred, include the SCO IRI in the context activities parent array.  

__SCORM 2004:__ `cmi.objectives.n.success_status=passed`  
__SCORM 1.2:__ `cmi.objectives.n.status=passed`  
__Experience API Statement:__  
_Statement with Local Objective_  
``` javascript
{
   "actor":{
      "account":{
         "homePage":"http://lms.adlnet.gov/",
         "name":"500-627-490"
      }
   },
   "verb":{
      "id":"http://adlnet.gov/expapi/verbs/passed",
      "display":{
         "en-US":"passed"
      }
   },
   "object":{
      "id":"http://adlnet.gov/courses/compsci/CS204/lesson01/01/objective/obj-if-else",
      "definition":{
         "name":{
            "en-US":"If-Else Blocks"
         },
         "description":{
            "en-US":"Show proficiency in creating if-else blocks"
         },
         "type": "http://adlnet.gov/expapi/activities/objective"
      }
   },
   "context":{
      "contextActivities":{
         "parent":[
            {
               "id":"http://adlnet.gov/courses/compsci/CS204/lesson01/01",
                  "definition":{
                     "name":{
                        "en-US":"CS204 lesson 01"
                     },
                     "description":{
                        "en-US":"The activity representing lesson 01 in the course CS204"
                     },
                     "type": "http://adlnet.gov/expapi/activities/lesson"
                  }
            }
         ],
         "grouping":[
            {
                  "id":"http://adlnet.gov/courses/compsci/CS204/",
                  "definition":{
                     "name":{
                        "en-US":"CS204"
                     },
                     "description":{
                        "en-US":"The activity representing the course CS204"
                     },
                     "type": "http://adlnet.gov/expapi/activities/course"
                  }
               },
               {
                  "id":"http://adlnet.gov/courses/compsci/CS204/lesson01/01?attemptId=50fd6961-ab6c-4e75-e6c7-ca42dce50dd6",
                  "definition":{
                     "name":{
                        "en-US":"Attempt of CS204 lesson 01"
                     },
                     "description":{
                        "en-US":"The activity representing an attempt of lesson 01 in the course CS204"
                     },
                     "type": "http://adlnet.gov/expapi/activities/attempt"
                  }
               }
         ],
         "category": [
            {
               "id": "https://w3id.org/xapi/scorm"
            }
         ]
      }
   }
}
```  
_Statement with Sequencing and Navigation Global Objective_  
``` javascript
{
   "actor":{
      "account":{
         "homePage":"http://lms.adlnet.gov/",
         "name":"500-627-490"
      }
   },
   "verb":{
      "id":"http://adlnet.gov/expapi/verbs/passed",
      "display":{
         "en-US":"passed"
      }
   },
   "object":{
      "id":"http://myurl.example.com/objective/global-obj-if-else",
      "definition":{
         "name":{
            "en-US":"If-Else Blocks"
         },
         "description":{
            "en-US":"Show proficiency in creating if-else blocks"
         },
         "type": "http://adlnet.gov/expapi/activities/lesson"
      }
   },
   "context":{
      "contextActivities":{
         "parent":[
            {
               "id":"http://adlnet.gov/courses/compsci/CS204/lesson01/01",
                  "definition":{
                     "name":{
                        "en-US":"CS204 lesson 01"
                     },
                     "description":{
                        "en-US":"The activity representing lesson 01 in the course CS204"
                     },
                     "type": "http://adlnet.gov/expapi/activities/lesson"
                  }
            }
         ],
         "grouping":[
            {
                  "id":"http://adlnet.gov/courses/compsci/CS204/",
                  "definition":{
                     "name":{
                        "en-US":"CS204"
                     },
                     "description":{
                        "en-US":"The activity representing the course CS204"
                     },
                     "type": "http://adlnet.gov/expapi/activities/course"
                  }
               },
               {
                  "id":"http://adlnet.gov/courses/compsci/CS204/lesson01/01?attemptId=50fd6961-ab6c-4e75-e6c7-ca42dce50dd6",
                  "definition":{
                     "name":{
                        "en-US":"Attempt of CS204 lesson 01"
                     },
                     "description":{
                        "en-US":"The activity representing an attempt of lesson 01 in the course CS204"
                     },
                     "type": "http://adlnet.gov/expapi/activities/attempt"
                  }
               }
         ],
         "category": [
            {
               "id": "https://w3id.org/xapi/scorm"
            }
         ]
      }
   }
}
```  

#### Progress Measure
Progress Measure indicates how much progress has been made in the activity. This value can be stored as a Statement using the `progressed` ADL Verb and `result.score.scaled` for the value.  
__SCORM 2004:__ `cmi.progress_measure`  
__SCORM 1.2:__ N/A  
__Experience API Statement:__   
``` javascript
{
   "actor":{
      "account":{
         "homePage":"http://lms.adlnet.gov/",
         "name":"500-627-490"
      }
   },
   "verb":{
      "id":"http://adlnet.gov/expapi/verbs/progressed",
      "display":{
         "en-US":"progressed"
      }
   },
   "object":{
      "id":"http://adlnet.gov/courses/compsci/CS204/lesson01/01",
      "definition":{
         "name":{
            "en-US":"lesson 01"
         },
         "description":{
            "en-US":"The first lesson of CS204"
         },
         "type": "http://adlnet.gov/expapi/activities/lesson"
      }
   },
   "result":{
      "score":{
         "scaled":0.75
      }
   },
   "timestamp":"2014-09-29T18:18:24.316Z",
   "context":{
      "contextActivities":{
         "grouping":[
           {
               "id":"http://adlnet.gov/courses/compsci/CS204/",
               "definition":{
                  "name":{
                     "en-US":"CS204"
                  },
                  "description":{
                     "en-US":"The activity representing the course CS204"
                  },
                  "type": "http://adlnet.gov/expapi/activities/course"
               }
            },
            {
               "id":"http://adlnet.gov/courses/compsci/CS204/lesson01/01?attemptId=50fd6961-ab6c-4e75-e6c7-ca42dce50dd6",
               "definition":{
                  "name":{
                     "en-US":"Attempt of CS204 lesson 01"
                  },
                  "description":{
                     "en-US":"The activity representing an attempt of lesson 01 in the course CS204"
                  },
                  "type": "http://adlnet.gov/expapi/activities/attempt"
               }
            }
         ],
         "category": [
            {
               "id": "https://w3id.org/xapi/scorm"
            }
         ]
      }
   }
}
```  

#### Scaled Passing Score
The score required for the learner to pass the content. This value is the same for all learners, and is made available for each activity. For those reasons, Scaled Passing Score is available at the Activity Profile endpoint.  
__SCORM 2004:__ `cmi.scaled_passing_score`  
__SCORM 1.2:__ `cmi.student_data.mastery_score`   
__Experience API:__ `scaled_passing_score` in the [SCORM Activity Profile Object](#scorm-activity-profile)  
See [Get xAPI SCORM Activity Profile](#get-xapi-scorm-activity-profile) for retrieving the Activity Profile Object.  

#### Score
Scores may be reported as supporting information about the learner’s attempt. Since reporting systems may not have a passing threshold to compare the scores the activity provider or activity cannot imply success or completion of an activity solely based on a score. The use of this Statement is for journaling/auditing purposes and does not necessarily indicate the score of the activity. If it is determined that the activity must have a score, set it explicitly as the [result of terminated Statement](#terminating-an-attempt).  

> NOTE: For compatibility between SCORM versions, the value of SCORM 1.2 cmi.core.score.raw divided by 100, and of SCORM 2004 cmi.score.scaled should be reported to xAPI as score.scaled. All other scores -  raw, min, max - may be reported directly as xAPI score.raw, score.min, and score.max.  

__SCORM 2004:__ `cmi.score.scaled=0.95`  
__SCORM 1.2:__ `cmi.core.score.raw=95`  
__Experience API Statement:__
``` javascript
{
    "actor": {
        "account": {
            "homePage": "http://lms.adlnet.gov/",
            "name": "500-627-490"
        }
    },
    "verb": {
        "id": "http://adlnet.gov/expapi/verbs/scored",
        "display": {
            "en-US": "scored"
        }
    },
     "result" : {
        "score" : {
            "scaled" : 0.95
        }
    },
    "object": {
        "id": "http://adlnet.gov/courses/compsci/CS204/lesson01/01",
        "definition": {
            "name": {
               "en-US" : "lesson 01"
            },
            "description" : {
               "en-US" : "The first lesson of CS204"
            },
            "type": "http://adlnet.gov/expapi/activities/lesson"
        }
    },
    "context": {
        "contextActivities": {
            "grouping": [
                {
                  "id":"http://adlnet.gov/courses/compsci/CS204/",
                  "definition":{
                     "name":{
                        "en-US":"CS204"
                     },
                     "description":{
                        "en-US":"The activity representing the course CS204"
                     },
                     "type": "http://adlnet.gov/expapi/activities/course"
                  }
               },
               {
                  "id":"http://adlnet.gov/courses/compsci/CS204/lesson01/01?attemptId=50fd6961-ab6c-4e75-e6c7-ca42dce50dd6",
                  "definition":{
                     "name":{
                        "en-US":"Attempt of CS204 lesson 01"
                     },
                     "description":{
                        "en-US":"The activity representing an attempt of lesson 01 in the course CS204"
                     },
                     "type": "http://adlnet.gov/expapi/activities/attempt"
                  }
               }
            ],
            "category": [
               {
                  "id": "https://w3id.org/xapi/scorm"
               }
            ]
        }
    }
}
```  

#### Session Time
Session Time indicates how much time has been spent in the activity during a specific session. This value can be stored as the `result.duration` property in a `terminated` or `suspended` Statement.  
__SCORM 2004:__ `cmi.session_time`  
__SCORM 1.2:__ `cmi.core.session_time`  
__Experience API Statement:__   
``` javascript
{
   "actor":{
      "account":{
         "homePage":"http://lms.adlnet.gov/",
         "name":"500-627-490"
      }
   },
   "verb":{
      "id":"http://adlnet.gov/expapi/verbs/terminated",
      "display":{
         "en-US":"terminated"
      }
   },
   "object":{
      "id":"http://adlnet.gov/courses/compsci/CS204/lesson01/01",
      "definition":{
         "name":{
            "en-US":"lesson 01"
         },
         "description":{
            "en-US":"The first lesson of CS204"
         },
         "type": "http://adlnet.gov/expapi/activities/lesson"
      }
   },
   "result":{
      "duration":"PT2H30M5S"
   },
   "context":{
      "contextActivities":{
         "grouping":[
           {
               "id":"http://adlnet.gov/courses/compsci/CS204/",
               "definition":{
                  "name":{
                     "en-US":"CS204"
                  },
                  "description":{
                     "en-US":"The activity representing the course CS204"
                  },
                  "type": "http://adlnet.gov/expapi/activities/course"
               }
            },
            {
               "id":"http://adlnet.gov/courses/compsci/CS204/lesson01/01?attemptId=50fd6961-ab6c-4e75-e6c7-ca42dce50dd6",
               "definition":{
                  "name":{
                     "en-US":"Attempt of CS204 lesson 01"
                  },
                  "description":{
                     "en-US":"The activity representing an attempt of lesson 01 in the course CS204"
                  },
                  "type": "http://adlnet.gov/expapi/activities/attempt"
               }
            }
         ],
         "category": [
            {
               "id": "https://w3id.org/xapi/scorm"
            }
         ]
      }
   }
}
```  

#### Success Status  
Success indicates whether the learner’s attempt was successful. The use of this Statement is for journaling/auditing purposes and does not necessarily indicate success of the activity. If it is determined that the activity must have a success status, set it explicitly as the [result of terminated Statement](#terminating-an-attempt).

__SCORM 2004:__ `cmi.success_status=passed`  
__SCORM 1.2:__ `cmi.core.lesson_status=passed`  
__Experience API Statement:__
``` javascript
{
    "actor": {
        "account": {
            "homePage": "http://lms.adlnet.gov/",
            "name": "500-627-490"
        }
    },
    "verb": {
        "id": "http://adlnet.gov/expapi/verbs/passed",
        "display": {
            "en-US": "passed"
        }
    },
    "object": {
        "id": "http://adlnet.gov/courses/compsci/CS204/lesson01/01",
        "definition": {
            "name": {
               "en-US" : "lesson 01"
            },
            "description" : {
               "en-US" : "The first lesson of CS204"
            },
            "type": "http://adlnet.gov/expapi/activities/lesson"
        }
    },
    "context": {
        "contextActivities": {
            "grouping": [
                {
                  "id":"http://adlnet.gov/courses/compsci/CS204/",
                  "definition":{
                     "name":{
                        "en-US":"CS204"
                     },
                     "description":{
                        "en-US":"The activity representing the course CS204"
                     },
                     "type": "http://adlnet.gov/expapi/activities/course"
                  }
               },
               {
                  "id":"http://adlnet.gov/courses/compsci/CS204/lesson01/01?attemptId=50fd6961-ab6c-4e75-e6c7-ca42dce50dd6",
                  "definition":{
                     "name":{
                        "en-US":"Attempt of CS204 lesson 01"
                     },
                     "description":{
                        "en-US":"The activity representing an attempt of lesson 01 in the course CS204"
                     },
                     "type": "http://adlnet.gov/expapi/activities/attempt"
                  }
               }
            ],
            "category": [
               {
                  "id": "https://w3id.org/xapi/scorm"
               }
            ]
        }
    }
}
```  

__SCORM 2004:__ `cmi.success_status=failed`  
__SCORM 1.2:__ `cmi.core.lesson_status=failed`  
__Experience API Statement:__
``` javascript
{
    "actor": {
        "account": {
            "homePage": "http://lms.adlnet.gov/",
            "name": "500-627-490"
        }
    },
    "verb": {
        "id": "http://adlnet.gov/expapi/verbs/failed",
        "display": {
            "en-US": "failed"
        }
    },
    "object": {
        "id": "http://adlnet.gov/courses/compsci/CS204/lesson01/01",
        "definition": {
            "name": {
               "en-US" : "lesson 01"
            },
            "description" : {
               "en-US" : "The first lesson of CS204"
            },
            "type": "http://adlnet.gov/expapi/activities/lesson"
        }
    },
    "context": {
        "contextActivities": {
            "grouping": [
                {
                  "id":"http://adlnet.gov/courses/compsci/CS204/",
                  "definition":{
                     "name":{
                        "en-US":"CS204"
                     },
                     "description":{
                        "en-US":"The activity representing the course CS204"
                     },
                     "type": "http://adlnet.gov/expapi/activities/course"
                  }
               },
               {
                  "id":"http://adlnet.gov/courses/compsci/CS204/lesson01/01?attemptId=50fd6961-ab6c-4e75-e6c7-ca42dce50dd6",
                  "definition":{
                     "name":{
                        "en-US":"Attempt of CS204 lesson 01"
                     },
                     "description":{
                        "en-US":"The activity representing an attempt of lesson 01 in the course CS204"
                     },
                     "type": "http://adlnet.gov/expapi/activities/attempt"
                  }
               }
            ],
            "category": [
               {
                  "id": "https://w3id.org/xapi/scorm"
               }
            ]
        }
    }
}
```  

#### Suspend Data
Suspend Data is the place to store state information of the content. This value may be large. To accomodate for this, suspend data is stored using the xAPI State endpoint, using `https://w3id.org/xapi/scorm/types/adl-suspend-data` as the stateId property value.  
__SCORM 2004:__ `cmi.suspend_data`  
__SCORM 1.2:__ `cmi.suspend_data`    
__Experience API:__ xAPI State Document  
`activityId`: The activity ID for the current attempt  
`agent`: The current learner agent object  
`stateId`: https://w3id.org/xapi/scorm/types/adl-suspend-data  
`registration`: (Optional) Registration UUID associated with the current attempt  

#### Time Limit Action
Time Limit Action defines what the content should do when the time limit has been surpassed. This value is the same for all learners, and is made available for each activity. For those reasons, Time Limit Action is available at the Activity Profile endpoint.  
__SCORM 2004:__ `cmi.time_limit_action`  
__SCORM 1.2:__ `cmi.student_data.time_limit_action`   
__Experience API:__ `time_limit_action` in the [SCORM Activity Profile Object](#scorm-activity-profile)  
See [Get xAPI SCORM Activity Profile](#get-xapi-scorm-activity-profile) for retrieving the Activity Profile Object.

#### Total Time
An element to hold a total time spent interacting with the content. This value is specific to the learner, and the activity, and is available at the Activity State endpoint.  
__SCORM 2004:__ `cmi.total_time`  
__SCORM 1.2:__ `cmi.core.total_time`    
__Experience API:__ `total_time` in the [SCORM Activity Attempt State Object](#scorm-activity-attempt-state)   
See [Get xAPI SCORM Activity Attempt State](#get-xapi-scorm-activity-attempt-state) for retrieving the Activity Attempt State Object.  

#### ADL Data
ADL Data is the place to store arbitrary information about the content. This value may be large and shared across activities. Additionally ADL Data can be allocated on a per SCO, per attempt basis making it difficult to define a standard place or process to store this arbitrary data. Instead this document describes the format and possible solutions. Ultimately, the implementation of this data model element is left largely up to the organization or developer.  

It is recommended that ADL Data is implemented similar to suspend data. Due to the potentially large amount of data that could be stored, each of the ADL Data stores should be individual xAPI activity state documents. To accommodate this, the [SCORM Activity Attempt State Object](#scorm-activity-attempt-state) adl_data property contains an array of [ADL Data State Parameters](#adl-data-state-parameters-object) objects containing parameters necessary to query for the ADL Data.  
__SCORM 2004:__ `adl.data`  
__SCORM 1.2:__ N/A      
__Experience API:__ `adl_data` in the [SCORM Activity Attempt State Object](#scorm-activity-attempt-state)   
See [Get xAPI SCORM Activity Attempt State](#get-xapi-scorm-activity-attempt-state) for retrieving the Activity Attempt State Object.  


## 7.0 Retrieving and Interpreting xAPI Statements
Storing learning experiences in an xAPI LRS is not the only consideration. Retrieving the learning experiences and interpreting what those statements mean is another aspect that needs guidance for consistent reporting and tracking. The following sections discuss the processes to identify results from activities and their meaning.

### Trusting the Statements
Determining which statements are trusted and authoritative is open to the individual organization. The following are a few strategies that can be applied to your organizations’ needs.

#### Private LRS
The safest way to ensure that the available statements in an LRS are trustworthy is to host an LRS within your organization. By controlling the environment that hosts the LRS, you ensure that the data contained in the LRS was submitted by authorized activity providers and activities. In this case, no other evaluation of the statements is necessary.

#### Authority
If the LRS is publicly hosted, the first way to identify trusted statements is to search based on the authority value. Each statement stored in an LRS has an authority value set to the agent who submitted the statement. This value is set by the LRS, and is based on the agent associated with the credentials used to submit the statement. A system wishing to only retrieve statements issued by certain activity providers or activities can filter the LRS results using those providers’ agent information.  

##### Retrieving Statements Based on the Authority
__Decoded:__  
<pre>
GET  
statements?agent={"account":{"homePage":"http://adlnet.gov/accounts/","name":"449-002"}}&related_agents=true
</pre>  

__Encoded:__  
<pre>
GET  
statements?agent=%7B%E2%80%9Caccount%E2%80%9D%3A%7B%E2%80%9ChomePage%E2%80%9D%3A%E2%80%9Chttp%3A%2F%2Fadlnet.gov%2Faccounts%2F%E2%80%9D%2C%E2%80%9Cname%E2%80%9D%3A%E2%80%9C449-002%E2%80%9D%7D%7D&related_agents=true
</pre>
#### Signed Statements
Another option for identifying the authenticity of a statement is by issuing signed statements. A statement is signed by an activity provider attaching a JSON web signature to the statement. This digital signature can be retrieved from the LRS with the statement and verified before considering the statement in the results. See the xAPI Specification for [how to sign](https://github.com/adlnet/xAPI-Spec/blob/master/xAPI.md#44-signed-statements) and [retrieve signed statements](https://github.com/adlnet/xAPI-Spec/blob/master/xAPI.md#723-getstatements).

##### Retrieving Statements with their Attachments
<pre>
GET  
statements?attachments=true
</pre>

### Determining Status
Due to activity providers and activities reporting to an LRS instead of an LMS, the determination of status might not be decided by an LMS. An LMS may still be used for the determination of a learner’s status, but it may also be determined by the activity provider or activities, reporting tools, or other client applications consuming the LRS data.

The method of determining status is up to those developing the activities. For example, activities within a course may report individual status statements and leverage a final piece of content to look at the collection of results and report an overall status for the course. Another example is a reporting tool customized with an organization’s accepted passing threshold collecting scores from a course and evaluating them based on the organization threshold. The results of that evaluation could be reported to the LRS as the success for the course.  


### Resolving Conflicts
Statements in an LRS are stored as a stream of information. It is possible to retrieve statements that conflict. It might be that a learner initially failed a test but later tried again and passed. In the LRS that result would likely appear as two separate, and conflicting, statements. Another issue that might arise is that the SCOs or lessons within a course may report one result while the course reports an overall status of another result. The following rules shall be followed to resolve such conflicts.

#### Granularity
It is possible to report status of a course in three different levels of granularity: course, SCO/lesson, objective. Since an LRS makes no assumptions about the statements it receives and has no rules about how to evaluate the statements contained within, it is recommended that all evaluation, rollup of results and final course status be reported by the activity provider, the activity or a trusted evaluation tool.  

For determining status based on granularity:
- If a system consuming the statements finds a course status, it shall use that result.
- If no course status is found consuming tools may use the status of all activities that include the course IRI in the context activities property.
- And at the most granular level, the consuming tools may use the status of all of the objectives for each of the activities that include the course IRI in the context activities property.  

#### Course Status
Determining and reporting course status is optional. However to maintain consistency of Statements, if course status is reported it must follow the guidance listed below.
- Use the verb [completed](http://adlnet.gov/expapi/verbs/completed/)  
- Set the `object` of the Statement to the course activity
- If known, include the sucess and score in the `result` property of the Statement

See an [example course status](#setting-the-course-status-with-success-and-score-in-result) Statement in the Appendix.

#### SCO Status
Activities shall report as much information about a learner’s status in the `result` property of the [terminated Statement](#terminating-an-attempt) of the activity.  
- At a minimum, completion should be reported in the terminated Statement.  
- Additional status, such as success and score, may be reported in the terminated Statement.  

For tools using these results from the LRS, the activity status is based on the status found in the `result` property of a terminated Statement.  

#### Attempt
If the activity was following the SCORM temporal model, it may be necessary to resolve conflicts by only using results from the latest attempt. See the [example in the Appendix](#find-all-statements-from-the-latest-attempt).

#### Time
All statements submitted by activity providers and activities following this profile are required to include a timestamp. Use of this timestamp property allows systems to create a timeline of the statements. Using this timeline can help resolve conflicts where the same property for the same granularity, authority, and attempt exist. In this case the most recent statement takes precedence. For example, if a SCO starts and reports that the learner failed this attempt, then the learner takes a test and passes this attempt, since the passed statement is the most recent, tools will use this one for the status of the attempt.  

## Appendix

### Common Scenarios

#### Initialize a SCO Attempt
__SCORM 2004:__ Initialize()  
__SCORM 1.2:__ LMSInitialize()  
__xAPI:__ actor 500-627-490 initialized lesson01 with attempt id (x) in course CS204  
``` javascript
{
   "actor":{
      "account":{
         "homePage":"http://lms.adlnet.gov/",
         "name":"500-627-490"
      }
   },
   "verb":{
      "id":"http://adlnet.gov/expapi/verbs/initialized",
      "display":{
         "en-US":"initialized"
      }
   },
   "object":{
      "id":"http://adlnet.gov/courses/compsci/CS204/lesson01/01",
      "definition":{
         "name":{
            "en-US":"lesson 01"
         },
         "description":{
            "en-US":"The first lesson of CS204"
         },
         "type": "http://adlnet.gov/expapi/activities/lesson"
      }
   },
   "context":{
      "contextActivities":{
         "grouping":[
            {
               "id":"http://adlnet.gov/courses/compsci/CS204/",
               "definition":{
                  "name":{
                     "en-US":"CS204"
                  },
                  "description":{
                     "en-US":"The activity representing the course CS204"
                  },
                  "type": "http://adlnet.gov/expapi/activities/course"
               }
            },
            {
               "id":"http://adlnet.gov/courses/compsci/CS204/lesson01/01?attemptId=50fd6961-ab6c-4e75-e6c7-ca42dce50dd6",
               "definition":{
                  "name":{
                     "en-US":"Attempt of CS204 lesson 01"
                  },
                  "description":{
                     "en-US":"The activity representing an attempt of lesson 01 in the course CS204"
                  },
                  "type": "http://adlnet.gov/expapi/activities/attempt"
               }
            }
         ],
         "category": [
            {
               "id": "https://w3id.org/xapi/scorm"
            }
         ]
      }
   },
   "timestamp":"2014-08-01T15:05:04-04:00"
}
```  
#### Terminate a SCO
__SCORM 2004:__ Terminate()  
__SCORM 1.2:__ LMSFinish()  
__xAPI:__ actor 500-627-490 terminated lesson01 with attempt id (x) in the course CS204
``` javascript
{
    "actor": {
        "account": {
            "homePage": "http://lms.adlnet.gov/",
            "name": "500-627-490"
        }
    },
    "verb": {
        "id": "http://adlnet.gov/expapi/verbs/terminated",
        "display": {
            "en-US": "terminated"
        }
    },
    "object": {
        "id": "http://adlnet.gov/courses/compsci/CS204/lesson01/01",
        "definition": {
            "name": {
                "en-US": "lesson 01"
            },
            "description": {
                "en-US": "The first lesson of CS204"
            },
            "type": "http://adlnet.gov/expapi/activities/lesson"
        }
    },
    "context": {
        "contextActivities": {
            "grouping": [
                {
                  "id":"http://adlnet.gov/courses/compsci/CS204/",
                  "definition":{
                     "name":{
                        "en-US":"CS204"
                     },
                     "description":{
                        "en-US":"The activity representing the course CS204"
                     },
                     "type": "http://adlnet.gov/expapi/activities/course"
                 }
               },
               {
                  "id":"http://adlnet.gov/courses/compsci/CS204/lesson01/01?attemptId=50fd6961-ab6c-4e75-e6c7-ca42dce50dd6",
                  "definition":{
                     "name":{
                        "en-US":"Attempt of CS204 lesson 01"
                     },
                     "description":{
                        "en-US":"The activity representing an attempt of lesson 01 in the course CS204"
                     },
                     "type": "http://adlnet.gov/expapi/activities/attempt"
                  }
               }
            ],
            "category": [
               {
                  "id": "https://w3id.org/xapi/scorm"
               }
            ]
        }
    },
    "result": {
        "success": true,
        "completion": true,
        "score": {
            "scaled": 0.95
        }
    },
    "timestamp": "2014-08-01T15:05:04-04:00"
}
```

#### Suspend a SCO
__SCORM 2004:__ cmi.exit=suspend  
__SCORM 1.2:__ cmi.core.exit=suspend  
__xAPI:__ agent 500-627-490 suspended lesson01 with attempt id (x) in the course CS204  
``` javascript
{
    "actor": {
        "account": {
            "homePage": "http://lms.adlnet.gov/",
            "name": "500-627-490"
        }
    },
    "verb": {
        "id": "http://adlnet.gov/expapi/verbs/suspended",
        "display": {
            "en-US": "suspended"
        }
    },
    "object": {
        "id": "http://adlnet.gov/courses/compsci/CS204/lesson01/01",
        "definition": {
            "name": {
               "en-US" : "lesson 01"
            },
            "description" : {
               "en-US" : "The first lesson of CS204"
            },
            "type": "http://adlnet.gov/expapi/activities/lesson"
        }
    },
    "context": {
        "contextActivities": {
            "grouping": [
                {
                  "id":"http://adlnet.gov/courses/compsci/CS204/",
                  "definition":{
                     "name":{
                        "en-US":"CS204"
                     },
                     "description":{
                        "en-US":"The activity representing the course CS204"
                     },
                     "type": "http://adlnet.gov/expapi/activities/course"
                  }
               },
               {
                  "id":"http://adlnet.gov/courses/compsci/CS204/lesson01/01?attemptId=50fd6961-ab6c-4e75-e6c7-ca42dce50dd6",
                  "definition":{
                     "name":{
                        "en-US":"Attempt of CS204 lesson 01"
                     },
                     "description":{
                        "en-US":"The activity representing an attempt of lesson 01 in the course CS204"
                     },
                     "type": "http://adlnet.gov/expapi/activities/attempt"
                  }
               }
            ],
            "category": [
               {
                  "id": "https://w3id.org/xapi/scorm"
               }
            ]
        }
    },
   "timestamp":"2014-08-01T15:05:04-04:00"
}
```

#### Resume a SCO
__SCORM 2004:__ cmi.entry=resume  
__SCORM 1.2:__ cmi.core.entry=resume  
__xAPI:__ agent 500-627-490 resumed lesson01 with same attempt id in the course CS204
``` javascript
{
    "actor": {
        "account": {
            "homePage": "http://lms.adlnet.gov/",
            "name": "500-627-490"
        }
    },
    "verb": {
        "id": "http://adlnet.gov/expapi/verbs/resumed",
        "display": {
            "en-US": "resumed"
        }
    },
    "object": {
        "id": "http://adlnet.gov/courses/compsci/CS204/lesson01/01",
        "definition": {
            "name": {
               "en-US" : "lesson 01"
            },
            "description" : {
               "en-US" : "The first lesson of CS204"
            },
            "type": "http://adlnet.gov/expapi/activities/lesson"
        }
    },
    "context": {
        "contextActivities": {
            "grouping": [
               {
                  "id":"http://adlnet.gov/courses/compsci/CS204/",
                  "definition":{
                     "name":{
                        "en-US":"CS204"
                     },
                     "description":{
                        "en-US":"The activity representing the course CS204"
                     },
                     "type": "http://adlnet.gov/expapi/activities/course"
                  }
               },
               {
                  "id":"http://adlnet.gov/courses/compsci/CS204/lesson01/01?attemptId=50fd6961-ab6c-4e75-e6c7-ca42dce50dd6",
                  "definition":{
                     "name":{
                        "en-US":"Attempt of CS204 lesson 01"
                     },
                     "description":{
                        "en-US":"The activity representing an attempt of lesson 01 in the course CS204"
                     },
                     "type": "http://adlnet.gov/expapi/activities/attempt"
                  }
               }
            ],
            "category": [
               {
                  "id": "https://w3id.org/xapi/scorm"
               }
            ]
        }
    },
   "timestamp":"2014-08-01T15:05:04-04:00"
}
```

#### Setting the course status with success and score in result
__xAPI:__ agent 500-627-490 completed the course CS204 with a score of 0.85 and success true
``` javascript
{
    "actor": {
        "account": {
            "homePage": "http://lms.adlnet.gov/",
            "name": "500-627-490"
        }
    },
    "verb": {
        "id": "http://adlnet.gov/expapi/verbs/completed",
        "display": {
            "en-US": "completed"
        }
    },
    "result": {
        "score": {
            "scaled": 0.85
        },
        "success": true
    },
    "object": {
        "id": "http://adlnet.gov/courses/compsci/CS204/",
        "definition": {
            "name": {
                "en-US": "CS204"
            },
            "description": {
                "en-US": "The CS204 course"
            },
            "type": "http://adlnet.gov/expapi/activities/course"
        }
    },
    "context": {
        "contextActivities": {
            "category": [
               {
                  "id": "https://w3id.org/xapi/scorm"
               }
            ]
        }
    },
   "timestamp":"2014-08-01T15:05:04-04:00"
}
```

### Query Examples  
#### Find Statements by activity IRI  
* Issue a [get Statements](https://github.com/adlnet/xAPI-Spec/blob/master/xAPI.md#723-getstatements) request to the LRS  

<table>
   <tr><th>HTTP Method</th><th>Request Endpoint</th></tr>
   <tr><td>GET</td><td>statements</tr>
   <tr><th>Parameter</th><th>Value</th></tr>
   <tr><td>activity</td><td>IRI</td></tr>
   <tr><td>related_activities</td><td>true</td></tr>
</table>  

_Unencoded and formatted for readability_  
```
GET  
https://lrs.adlnet.gov/xapi/statements
?activity=http://adlnet.gov/courses/compsci/CS204/lesson01/01/attempt/50fd6961-ab6c-4e75-e6c7-ca42dce50dd6
&related_activities=true
```  

*  The response content is a [Statement Result](https://github.com/adlnet/xAPI-Spec/blob/master/xAPI.md#retstmts) of all the Statements that contained an activity with the requested IRI  


#### Find Attempt IRIs for a SCO
*  Issue a [get Activity State](#get-xapi-scorm-activity-state) request to the LRS  
*  The response content is a [SCORM Activity State](#scorm-activity-state) JSON object with the Attempt IRIs stored in the `attempts` property.  

#### Find the Latest Attempt IRI
*  [Find the attempt IRIs for the SCO](#find-attempt-iris-for-a-sco)  
*  The last IRI in the `attempts` parameter of the response [SCORM Activity State](#scorm-activity-state) JSON object is the latest attempt IRI  

#### Find all Statements from the Latest Attempt  
*  [Find the latest attempt IRI](#find-the-latest-attempt-iri) for the SCO  
*  [Find the Statements by the latest attempt IRI](#find-statements-by-activity-iri)  
*  The response content is a [Statement Result](https://github.com/adlnet/xAPI-Spec/blob/master/xAPI.md#retstmts) of all the Statements that contained an activity with the requested IRI  

#### Find all Statements for a SCO  
*  Identify the SCO IRI from launch, activity IRI generation, or out-of-band configuration  
*  [Find the Statements by the SCO IRI](#find-statements-by-activity-iri)  
*  The response content is a [Statement Result](https://github.com/adlnet/xAPI-Spec/blob/master/xAPI.md#retstmts) of all the Statements that contained an activity with the requested IRI  

#### Find all Statements for a course  
*  Identify the course IRI from launch
*  [Find the Statements by the course IRI](#find-statements-by-activity-iri)
*  The response content is a [Statement Result](https://github.com/adlnet/xAPI-Spec/blob/master/xAPI.md#retstmts) of all the Statements that contained an activity with the requested IRI  

#### Find all learner's Statements for a course
*  Identify the course IRI from launch
*  Identify the learner's agent (actor) object from launch
*  Issue a [get Statements](https://github.com/adlnet/xAPI-Spec/blob/master/xAPI.md#723-getstatements) request to the LRS  

<table>
   <tr><th>HTTP Method</th><th>Request Endpoint</th></tr>
   <tr><td>GET</td><td>statements</tr>
   <tr><th>Parameter</th><th>Value</th></tr>
   <tr><td>agent</td><td>leaner agent object</td></tr>
   <tr><td>activity</td><td>course IRI</td></tr>
   <tr><td>related_activities</td><td>true</td></tr>
</table>  

_Unencoded and formatted for readability_  
```
GET  
https://lrs.adlnet.gov/xapi/statements
?agent={"account": {
            "homePage": "http://lms.adlnet.gov/",
            "name": "500-627-490"}}
?activity=http://adlnet.gov/courses/compsci/CS204/lesson01/01/attempt/50fd6961-ab6c-4e75-e6c7-ca42dce50dd6
&related_activities=true
```  

*  The response content is a [Statement Result](https://github.com/adlnet/xAPI-Spec/blob/master/xAPI.md#retstmts) of all the Statements that contained an activity with the requested IRI and the actor as the learner agent.  

#### Find learner's results for each SCO in a course  
*  Identify the course IRI from launch
*  Identify the learner's agent (actor) object from launch
*  Issue a [get Statements](https://github.com/adlnet/xAPI-Spec/blob/master/xAPI.md#723-getstatements) request to the LRS  

<table>
   <tr><th>HTTP Method</th><th>Request Endpoint</th></tr>
   <tr><td>GET</td><td>statements</tr>
   <tr><th>Parameter</th><th>Value</th></tr>
   <tr><td>agent</td><td>leaner agent object</td></tr>
  <tr><td>verb</td><td>ADL verb <a href="http://adlnet.gov/expapi/verbs/terminated">terminated</a>
   <tr><td>activity</td><td>course IRI</td></tr>
   <tr><td>related_activities</td><td>true</td></tr>
</table>  

_Unencoded and formatted for readability_  
```
GET  
https://lrs.adlnet.gov/xapi/statements
?agent={"account": {
            "homePage": "http://lms.adlnet.gov/",
            "name": "500-627-490"}}
?verb=http://adlnet.gov/expapi/verbs/terminated
?activity=http://adlnet.gov/courses/compsci/CS204/lesson01/01/attempt/50fd6961-ab6c-4e75-e6c7-ca42dce50dd6
&related_activities=true
```  

*  The response content is a [Statement Result](https://github.com/adlnet/xAPI-Spec/blob/master/xAPI.md#retstmts) of all the Statements that contained an activity with the requested IRI, the terminated ADL verb and the actor as the learner agent.  
*  Each of these terminated Statements contain the SCO status in the `result` parameter, such as `score`, `completed` and `success`.  

#### Get xAPI SCORM Activity State
*  Issue a [get Activity State](https://github.com/adlnet/xAPI-Spec/blob/master/xAPI.md#74-state-api) request to the LRS  

<table>
   <tr><th>HTTP Method</th><th>Request Endpoint</th></tr>
   <tr><td>GET</td><td>activities/state</tr>
   <tr><th>Parameter</th><th>Value</th></tr>
   <tr><td>activityId</td><td>SCO IRI</td></tr>
   <tr><td>agent</td><td>Learner's Agent object</td></tr>
   <tr><td>stateId</td><td>https://w3id.org/xapi/scorm/activity-state</td></tr>
</table>  

_Unencoded and formatted for readability_  
```
GET
https://lrs.adlnet.gov/xapi/activities/state
?activityId=http://adlnet.gov/courses/compsci/CS204/lesson01/01
&agent={"account": {
            "homePage": "http://lms.adlnet.gov/",
            "name": "500-627-490"}}
&stateId=https://w3id.org/xapi/scorm/activity-state
```  

*  The response content is a [SCORM Activity State](#scorm-activity-state) JSON object.

#### Get xAPI SCORM Activity Attempt State
*  Issue a [get Activity State](https://github.com/adlnet/xAPI-Spec/blob/master/xAPI.md#74-state-api) request to the LRS  

<table>
   <tr><th>HTTP Method</th><th>Request Endpoint</th></tr>
   <tr><td>GET</td><td>activities/state</tr>
   <tr><th>Parameter</th><th>Value</th></tr>
   <tr><td>activityId</td><td>attempt IRI</td></tr>
   <tr><td>agent</td><td>Learner's Agent object</td></tr>
   <tr><td>stateId</td><td>https://w3id.org/xapi/scorm/attempt-state</td></tr>
</table>  

_Unencoded and formatted for readability_  
```
GET
https://lrs.adlnet.gov/xapi/activities/state
?activityId=http://adlnet.gov/courses/compsci/CS204/lesson01/01/attempt/01
&agent={"account": {
            "homePage": "http://lms.adlnet.gov/",
            "name": "500-627-490"}}
&stateId=https://w3id.org/xapi/scorm/attempt-state
```  

*  The response content is a [SCORM Attempt State](#scorm-attempt-state) JSON object.  

#### Get xAPI SCORM Activity Profile
*  Issue a [get Activity Profile](https://github.com/adlnet/xAPI-Spec/blob/master/xAPI.md#actprofapi) request to the LRS  

<table>
   <tr><th>HTTP Method</th><th>Request Endpoint</th></tr>
   <tr><td>GET</td><td>activities/profile</tr>
   <tr><th>Parameter</th><th>Value</th></tr>
   <tr><td>activityId</td><td>Activity IRI</td></tr>
   <tr><td>profileId</td><td>https://w3id.org/xapi/scorm/activity-profile</td></tr>
</table>  

_Unencoded and formatted for readability_  
```
GET
https://lrs.adlnet.gov/xapi/activities/profile
?activityId=http://adlnet.gov/courses/compsci/CS204/lesson01/01/
&profileId=https://w3id.org/xapi/scorm/activity-profile
```  

*  The response content is a [SCORM Activity Profile](#scorm-activity-profile) JSON object.  

#### Get xAPI SCORM Agent Profile
*  Issue a [get Agent Profile](https://github.com/adlnet/xAPI-Spec/blob/master/xAPI.md#76-agent-profile-api) request to the LRS  

<table>
   <tr><th>HTTP Method</th><th>Request Endpoint</th></tr>
   <tr><td>GET</td><td>agents/profile</tr>
   <tr><th>Parameter</th><th>Value</th></tr>
   <tr><td>agent</td><td>Agent object</td></tr>
   <tr><td>profileId</td><td>https://w3id.org/xapi/scorm/agent-profile</td></tr>
</table>  

_Unencoded and formatted for readability_  
```
GET
https://lrs.adlnet.gov/xapi/agents/profile
&agent={"account": {
            "homePage": "http://lms.adlnet.gov/",
            "name": "500-627-490"}}
&profileId=https://w3id.org/xapi/scorm/agent-profile
```  

*  The response content is a [SCORM Agent Profile](#agent-profile) JSON object.  

#### Get attempt state for current attempt  
*  Identify the current attempt IRI through launch, attempt IRI generation, or out-of-band configuration  
*  Issue a [get Activity Attempt State](#get-xapi-scorm-activity-attempt-state) request to the LRS  

#### Set attempt state for current attempt  
*  Identify the current attempt IRI through launch, attempt IRI generation, or out-of-band configuration  
*  Attempt to [Get the attempt state JSON object](#get-attempt-state-for-current-attempt) from the LRS
*  If the response returns the attempt state,
    *  update with current values
    *  issue a POST activity state request with the updated JSON object
*  If the response returns a `404 Not Found`,
    *  create a new [attempt state JSON object](#scorm-activity-attempt-state) with current values
    *  issue a PUT activity state request with the new JSON object  
>NOTE: The request method change of POST or PUT is based on xAPI requirements for updating vs creating a new document. This example demonstrates a generalized case. Organizations are free to update/create the document however works best within the [rules defined in xAPI](https://github.com/adlnet/xAPI-Spec/blob/master/xAPI.md#json-procedure-with-requirements).

<table>
   <tr><th>HTTP Method</th><th>Request Endpoint</th></tr>
   <tr><td>GET</td><td>activities/state</tr>
   <tr><th>Parameter</th><th>Value</th></tr>
   <tr><td>activityId</td><td>attempt IRI</td></tr>
   <tr><td>agent</td><td>Learner's Agent object</td></tr>
   <tr><td>stateId</td><td>https://w3id.org/xapi/scorm/attempt-state</td></tr>
</table>  

_Unencoded and formatted for readability_  
```
POST/PUT
https://lrs.adlnet.gov/xapi/activities/state
?activityId=http://adlnet.gov/courses/compsci/CS204/lesson01/01/attempt/01
&agent={"account": {
            "homePage": "http://lms.adlnet.gov/",
            "name": "500-627-490"}}
&stateId=https://w3id.org/xapi/scorm/attempt-state

Content Body
{
    "location":"page-02",
    "total_time":"PT0H20M"
}
```  


### XAPI SCORM Data Objects
#### SCORM Activity State
__State ID:__ https://w3id.org/xapi/scorm/activity-state
<table>
<tr><th>Property</th><th>Description</th></tr>
<tr>
 <td>attempts</td>
 <td>Array of Activity Attempt IRIs</td>
</tr>
</table>  

#### SCORM Activity Attempt State
__State ID:__ https://w3id.org/xapi/scorm/attempt-state
<table>
<tr><th>Property</th><th>Description</th></tr>
<tr>
 <td>credit</td>
 <td>String ("credit", "no-credit")</td>
</tr>
<tr>
 <td>mode</td>
 <td>String ("browse", "normal", "review")</td>
</tr>
<tr>
 <td>location</td>
 <td>String</td>
</tr>
<tr>
 <td>preferences</td>
 <td><a href="#preferences-object">Preferences Object</a></td>
</tr>
<tr>
 <td>total_time</td>
 <td>Formatted <a href="https://en.wikipedia.org/wiki/ISO_8601#Durations">ISO 8601 Duration</a> with a precision of 0.01 seconds</td>
</tr>
<tr>
 <td>adl_data</td>
 <td>Array of <a href="#adl-data-state-parameters-object">ADL Data State Parameter Objects</a></td>
</tr>
</table>

#### SCORM Activity Profile
__Profile ID:__ https://w3id.org/xapi/scorm/activity-profile
<table>
<tr><th>Property</th><th>Description</th></tr>
<tr>
 <td>comments_from_lms</td>
 <td><a href="#scorm-activity-profile-comment-object">SCORM Activity Profile Comment Object</a></td>
</tr>
<tr>
 <td>completion_threshold</td>
 <td>Number (0 to 1)</td>
</tr>
<tr>
 <td>launch_data</td>
 <td>String</td>
</tr>
<tr>
 <td>max_time_allowed</td>
 <td>Number (0 to *)</td>
</tr>
<tr>
 <td>scaled_passing_score</td>
 <td>Number (-1 to 1)</td>
</tr>
<tr>
 <td>time_limit_action</td>
 <td>String ("exit,message", "continue,message", "exit,no message", "continue,no message")</td>
</tr>
</table>


#### Agent Profile
__Profile ID:__ https://w3id.org/xapi/scorm/agent-profile
<table>
<tr><th>Property</th><th>Description</th></tr>
<tr>
 <td>learner_id</td>
 <td>String</td>
</tr>
<tr>
 <td>learner_name</td>
 <td>String</td>
</tr>
<tr>
 <td>preferences</td>
 <td><a href="#preferences-object">Preferences Object</a></td>
</tr>
</table>

#### SCORM Activity Profile Comment Object
<table>
<tr><th>Property</th><th>Description</th></tr>
<tr>
 <td>comment</td>
 <td>String</td>
</tr>
<tr>
 <td>location</td>
 <td>String</td>
</tr>
<tr>
 <td>timestamp</td>
 <td>Timestamp <a href="https://github.com/adlnet/xAPI-Spec/blob/master/xAPI.md#417-timestamp">ISO 8601</a></td>
</table>

#### ADL Data State Parameters Object
<table>
<tr><th>Property</th><th>Description</th></tr>
<tr>
 <td>activityId</td>
 <td>IRI</td>
</tr>
<tr>
 <td>agent</td>
 <td>Agent object</td>
</tr>
<tr>
 <td>stateId</td>
 <td>String</td>
</tr>
<tr>
 <td>registration</td>
 <td>UUID (Optional)</td>
</tr>
</table>

#### Preferences Object
<table>
<tr><th>Property</th><th>Description</th></tr>
<tr>
 <td>audio_level</td>
 <td>Number (0 to *)</td>
</tr>
<tr>
 <td>language</td>
 <td>String (language code <a href="http://tools.ietf.org/html/rfc5646">RFC 5646</a></td>
</tr>
<tr>
 <td>delivery_speed</td>
 <td>Number (0 to *)</td>
</tr>
<tr>
 <td>audio_captioning</td>
 <td>Number (-1 [off], 0 [no change], 1 [on])</td>
</tr>
</table>

### References
Advanced Distributed Learning Initiative. (2012). _SCORM 2004 4th Edition Run-Time Environment (RTE) Version 1.1_. (SCORM 2004 4th Edition Specification). Alexandria, VA: Author.
