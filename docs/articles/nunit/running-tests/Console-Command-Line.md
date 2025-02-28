---
uid: consolecommandline
---

# Console Command Line

The console interface runner is invoked by a command in the form

```cmd
    NUNIT3-CONSOLE [inputfiles] [options]
```

where **inputfiles** is one or more assemblies or test projects of
a type that NUnit can process and **options** is zero or more options.
Input files and options may be mixed in any order.

## Input Files

The console program must always have an assembly or project specified.
Assemblies are specified by file name or path, which may be absolute or
relative. Relative paths are interpreted based on the current directory.

In addition to assemblies, you may specify any project type that is
understood by NUnit. Out of the box, this includes various
Visual Studio project types as well as NUnit (.nunit) test projects (see [NUnit Test Projects](xref:nunittestprojects) for a description of NUnit test projects).

If the NUnit V2 framework driver is installed, test assemblies may
be run based on any version of the NUnit framework beginning with 2.0.
Without the V2 driver, only version 3.0 and higher tests may be run.

## Options

| Option | Description |
| ------ | ----------- |
|`@FILE` | Specifies the name (or path) of a FILE containing additional command-line arguments to be interpolated at the point where the @FILE expression appears. Each line in the file represents a separate command-line argument.|
|`--test=FULLNAMES` | Comma-separated list of FULLNAMES of tests to run or explore. This option may be repeated. Note that this option is retained for backward compatibility. The --where option can now be used instead. |
|`--testlist=FILE` | The name (or path) of a FILE containing a list of tests to run or explore, one per line. May also include comment lines, indicated by `#` in the first column. |
|`--where=EXPRESSION` | An expression indicating which tests to run. It may specify test names, classes, methods, categories or properties comparing them to actual values with the operators ==, !=, =~ and !~. See [Test Selection Language](Test-Selection-Language.md) for a full description of the syntax. |
|`--testparam:PARAMETER, --tp:PARAMETER` | A test PARAMETER specified in the form NAME=VALUE for consumption by tests. Multiple parameters must be specified separated using a `--testparam` or `--tp` option for each. |
|`--params=PARAMETER, --p=PARAMETER` | (**NOTE:** _this is deprecated and will be removed in a future release. Please use --testparam instead_.) A test PARAMETER specified in the form NAME=VALUE for consumption by tests. Multiple parameters may be specified, separated by semicolons or by repeating the --params option multiple times. Case-sensitive. |
|`--config=NAME` | NAME of a project configuration to load (e.g.: Debug). |
|`--process=PROCESS` | PROCESS isolation for test assemblies. Values: Single, Separate, Multiple. If not specified, defaults to Separate for a single assembly or Multiple for more than one. By default, processes are run in parallel. |
|`--inprocess` | This option is a synonym for --process=Single |
|`--agents=NUMBER` | NUMBER of agents that may be allowed to run simultaneously assuming you are not running inprocess. If not specified, all agent processes run tests at the same time, whatever the number of assemblies. This setting is used to control running your assemblies in parallel. |
|`--domain=DOMAIN` | DOMAIN isolation for test assemblies.  Values: None, Single, Multiple. If not specified, defaults to Single for a single assembly or Multiple for more than one. **NOTE:** `None` is an extremely rarely used option intended for cases where you are testing features that can only run in a primary domain; when choosing this option, you are responsible for copying all needed files, including NUnit components, into a common directory. |
|`--framework=FRAMEWORK` | FRAMEWORK type/version to use for tests. Examples: mono, net-4.5, v4.0, 2.0, mono-4.0. **NOTE:** Only use this option if you are sure all tests will run under the specified runtime. The option does **not** select a particular build from a project with multiple runtime targets. |
|`--x86` | Run tests in a 32-bit process on 64-bit systems. **NOTE:** This option forces all tests to run as 32 bits. It is normally not needed since x86 test assemblies are automatically run as 32 bits. It is needed, however, when a non-x86 test assembly references an x86 assembly. |
|`--dispose-runners` | Dispose each test runner after it has finished running its tests |
|`--timeout=MILLISECONDS` | Set timeout for each test case in MILLISECONDS. |
|`--seed=SEED` | Set the random SEED used to generate test cases. |
|`--workers=NUMBER` | Specify the NUMBER of worker threads to be used in running tests. This setting is used to control running your tests in parallel and is used in conjunction with the [Parallelizable Attribute](xref:parallelizableattribute). If not specified, workers defaults to the number of processors on the machine, or 2, whichever is greater. |
|`--stoponerror` | Stop run immediately upon any test failure or error. |
|`--skipnontestassemblies` | Skip any non-test assemblies specified - or assemblies containing NUnit.Framework.NonTestAssemblyAttribute, without error. |
|`--debug` | Causes NUnit to break into the debugger immediately before it executes your tests. This is particularly useful when the tests are running in a separate process to which you would otherwise have to attach. |
|`--debug-agent` | Available only in debug builds of NUnit, this option is for use by developers in debugging the nunit-agent itself. It breaks in the agent code immediately upon entry of the process. |
|`--pause` | Causes NUnit to immediately open a message box, allowing you to attach a debugger. For cases where --debug does not work. |
|`--wait` | Wait for input before closing console window. |
|`--work=PATH` | PATH of the directory to use for output files. |
|`--output, --out=PATH` | File PATH to contain text output from the tests. |
|`--result=SPEC` | An output SPEC for saving the test results. This option may be repeated. |
|`--explore[=SPEC]` | Display or save test info rather than running tests. Optionally provide an output SPEC for saving the test info. This option may be repeated. |
|`--noresult` | Don't save any test results. |
|`--trace=LEVEL` | Set internal trace LEVEL. Values: Off, Error, Warning, Info, Verbose (Debug) |
|`--labels=VALUE` | Specify whether to write test case names to the output. Values: Off, On, Before, After, or All. If not specified, defaults to Off. **Off**: No labeling is used. Both normal and immediate output appear in the order produced - i.e. immediate first. **On**: A label appears before each sequence of output lines from the same test. Since tests may be run in parallel, output from different tests may be intermixed. **Before**: A label appears at the start of every test, whether it produces output or not. Additional labels are produced as needed if interspersed output takes place, just as for `--labels=On`. Synonym for `--labels=All`. **labels=After**: A label appears at the end of every test, whether it produced output or not. This label includes the pass/fail status of the test in addition to its name. Additional labels are produced as needed if there is any output, just as for `--labels=On`. **All**: A label appears at the start of every test, whether it produces output or not. Additional labels are produced as needed if interspersed output takes place, just as for `--labels=On`. Synonym for `--labels=Before`.|
|`--test-name-format=VALUE` | Specify a non-standard naming pattern to use when generating all test names. See [Template Based Test Naming](Template-Based-Test-Naming.md). |
|`--encoding=CODEPAGE` | Specify the Console CODEPAGE, such as utf-8, ascii, etc. This option is not normally needed unless your output includes special characters. The page specified must be available on the system. |
|`--shadowcopy` | Tells .NET to copy loaded assemblies to the shadowcopy directory. |
|`--teamcity` | Turns on use of TeamCity service messages. |
|`--loaduserprofile` | Causes the user profile to be loaded in any separate test processes. |
|`--list-extensions` | Lists all extension points and the extensions installed on each of them. |
|`--set-principal-policy=POLICY` | Set the principal policy for the test domain to POLICY. Values: UnauthenticatedPrincipal, NoPrincipal, WindowsPrincipal |
|`--noheader, --noh` | Suppress display of program information at start of run. |
|`--nocolor, --noc` | Displays console output without color. |
|`--help, -h` | Display this message and exit. |

### Description

By default, this command runs the tests contained in the
assemblies and projects specified. If the **--explore** option
is used, no tests are executed but a description of the tests
is saved in the specified or default format.

Several options that specify processing of XML output take
an output specification as a value. A SPEC may take one of
the following forms:

* `--OPTION:filename`
* `--OPTION:filename;format=formatname`
* `--OPTION:filename;transform=xsltfile`

The --result option may use any of the following formats:

* nunit3 - the native XML format for NUnit 3
* nunit2 - legacy XML format used by earlier releases of NUnit

The --explore option may use any of the following formats:

* nunit3 - the native XML format for NUnit 3
* cases  - a text file listing the full names of all test cases.

If --explore is used without any specification following, a list of
test cases is output to the console.

If neither --result nor --explore is used,
NUnit saves the results to TestResult.xml in nunit3 format.

Any transforms provided must handle input in the native nunit3 format.
