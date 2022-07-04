# OpenAPI Generator for the VidAPI client

## Overview
This is a boiler-plate project to generate your own project derived from an OpenAPI specification.
Its goal is to get you started with the basic plumbing so you can put in your own logic.
It won't work without your changes applied.

## What's OpenAPI
The goal of OpenAPI is to define a standard, language-agnostic interface to REST APIs which allows both humans and computers to discover and understand the capabilities of the service without access to source code, documentation, or through network traffic inspection.
When properly described with OpenAPI, a consumer can understand and interact with the remote service with a minimal amount of implementation logic.
Similar to what interfaces have done for lower-level programming, OpenAPI removes the guesswork in calling the service.

Check out [OpenAPI-Spec](https://github.com/OAI/OpenAPI-Specification) for additional information about the OpenAPI project, including additional libraries with support for other languages and more. 

## How do I use this?
At this point, you've likely generated a client setup.  It will include something along these lines:

```
.
|  // this file
|- README.md
|  // build script
|- pom.xml
|-- src
|--- main
|---- java
|      // generator file
|----- io.moonvision.codegen.PythonVidapiGenerator.java
|---- resources
|      // template files
|----- python-vidapi
|----- META-INF
|------ services
|------- org.openapitools.codegen.CodegenConfig
```

To build the OpenAPI generator run:

```
mvn package
```

In your generator project. A single jar file will be produced in `target`.
You can now use it to generate the API client:

```
java -jar /path/to/your.jar generate \
    -g io.moonvision.codegen.PythonVidapiGenerator \
    -i /path/to/openapi.yaml \
    -o ./test
```
(Do not forget to replace the values `/path/to/your.jar` and `/path/to/openapi.yaml` in the previous command)

## But how do I modify this?
The `PythonVidapiGenerator.java` has comments in it--lots of comments.  There is no good substitute
for reading the code more, though.  See how the `PythonVidapiGenerator` implements `CodegenConfig`.
That class has the signature of all values that can be overridden.

You can also step through PythonVidapiGenerator.java in a debugger.  Just debug the JUnit
test in DebugCodegenLauncher.  That runs the command line tool and lets you inspect what the code is doing.  

For the templates themselves, you have a number of values available to you for generation.
You can execute the `java` command from above while passing different debug flags to show
the object you have available during client generation:

```
# The following additional debug options are available for all
# codegen targets:
# -DdebugOpenAPI         prints the OpenAPI Specification as
#                        interpreted by the codegen
# -DdebugModels          prints models passed to the template
#                        engine
# -DdebugOperations      prints operations passed to the
#                        template engine
# -DdebugSupportingFiles prints additional data passed to the
#                        template engine

java -DdebugOperations -jar /path/to/your.jar generate \
    -g io.moonvision.codegen.PythonVidapiGenerator \
    -i /path/to/openapi.yaml \
    -o ./test
```

Will, for example, output the debug info for operations.
You can use this info in the `api.mustache` file.
