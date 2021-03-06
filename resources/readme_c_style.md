# Example Code: {{fullname}}

## Building {{language.upper()}} Example
Before compiling or running the example, make sure the environment variable
`NDDSHOME` is set to the directory where your version of *RTI Connext* is
installed.

Run *rtiddsgen* with the `-example` option and the target architecture of your
choice (e.g., *{{archwindows}}* or *{{archlinux}}*). The *RTI Connext Core
Libraries and Utilities Getting Started Guide* describes this process in detail.
Follow the same procedure to generate the code and build the examples. **Do not
use the `-replace` option.** Assuming you want to generate an example for
*{{archwindows}}* run:
```
rtiddsgen -language {{language}} -example {{archwindows}} {{idlname}}.idl
```

You will see messages that look like:
```
WARN com.rti.ndds.nddsgen.emitters.FileEmitter File exists and will not be
overwritten : /some/path/{{idlname}}_subscriber.{{"c" if language == "c" else  "cxx"}}
WARN com.rti.ndds.nddsgen.emitters.FileEmitter File exists and will not be
overwritten : /some/path/{{idlname}}_publisher.{{"c" if language == "c" else  "cxx"}}
```

This is normal and is only informing you that the subscriber/publisher code has
not been replaced, which is fine since all the source files for the example are
already provided.

Use the generated makefile of *Visual Studio* project to compile your
application.

## Running {{language.upper()}} Example
In two separate command prompt windows for the publisher and subscriber. Run
the following commands from the example directory (this is necessary to ensure
the application loads the QoS defined in *USER_QOS_PROFILES.xml*):

```sh
# Do not forget to replace the path separator to "\" on Windows.
objs/<arch_name>/{{idlname}}_publisher.exe  <domain_id> <samples_to_send>
objs/<arch_name>/{{idlname}}_subscriber.exe <domain_id> <sleep_periods>
```

The applications accept up to two arguments:

1. The `<domain_id>`. Both applications must use the same domain ID in order to
communicate. The default is 0.
2. How long the examples should run, measured in samples for the publisher
and sleep periods for the subscriber. A value of '0' instructs the
application to run forever; this is the default.
