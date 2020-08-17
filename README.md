[![Github Downloads](https://img.shields.io/github/downloads/dfirence/mitre-assistant/total)]()
[![Github Stars](https://img.shields.io/github/stars/dfirence/mitre-assistant)]()

# mitre-assistant

A custom, more useful, and much cooler MITRE-CTI-CLIENT.

<br/>

![image](https://user-images.githubusercontent.com/11415591/90009693-8a1daa00-dc6c-11ea-87c7-968da8f400e8.png)

<br/>

```bash
# Assumes you have installed the rust tool chain
# and that you have the `cargo` package manager
#
# Preferably use rust stable channel
#
$> cargo install mitre-assistant
```
<br/>

<br/>

<hr>

## W.I.P - Status
- [x] Mitre Enterprise Matrix
- [ ] Mitre Mobile Matrix
- [ ] Mitre Pre-Attack Matrix
- [ ] Mitre Navigator JSON
    - [ ] Legacy Version
    - [ ] Modern Version with Subtechniques
- [x] Linux - 64bit
- [x] MacOS - 64bit
- [x] Windows - 64bit
- [ ] Data Interchange Format
   - [ ] CSV
   - [ ] JSON
- [ ] Exports
   - [ ] CSV
   - [ ] JSON
   - [ ] Rich Web

<hr>

<br/>
<br/>

# Getting Started
You got 3 ways to start using this `bad-boy`:

**1.** You can go to the releases section, download the pre-compiled binary for your os. Note:  I only provide Debian on Linux

**2.** If you already have rust stable toolchain installed, then simply use `cargo install mitre-assistant`

**3.** Or, if you just love building from source, follow the instructions in the `build from source section` below.


<br/>
<br/>

## Releases - Binaries
Head over to the [releases section](https://github.com/dfirence/mitre-assistant/releases/) and download the binary for your OS.  However, note, I am only supporting binaries for **64 bit versions** of:

* MacOS
* Debian
* Windows

<br/>

## Build From Source
If you use a different Linux distro, install the rust toolchain, preferably the stable channel, and follow these steps:

### Step 1 - Clone this repo

```bash
$> git clone https://github.com/dfirence/mitre-assistant.git
```

<br/>

### Step 2 - Navigate into the repo

```bash
$> cd mitre-assistant
```

<br/>

### Step 3 - Build/Compile

```bash
$> cargo build --release
```
<br/>

### Step 4 - Move your fresh binary to a system path

In this step, if you wanna call the executable from anywhere, add it to your system path or executable path - i.e., /usr/bin
```bash
$> sudo mv /target/release/mitre-assistant /usr/bin
```
<br/>

<br/>
<br/>

# How to **Update** with new releases?

```text
Note:   Because this tool is being actively developed,
        it is recommended to always use the `baseline` subcommand
        to ensure the dev changes made to the custom JSON database
        are in effect.
```

Most of the changes being made until I reach **v.1.0** will affect the
JSON file produced by this tool.  This is because I am exploring how to arrange
the data for the outcomes I am pursuing.

So always ensure you run the `baseline` subcommand after you install or download a new version of the tool, for now.

<hr/>
<br/>
<br/>

## Why are you doing this?
I work in the Security industry for a provider, my work hinges a lot on this resource from The Mitre Corporation.  At some point, if you are like me, you will observe the poor and ridiculous amount of time that is needed to create custom datasets from that resource and collaborate across teams to get into serious work.  This helps me not waste time on silly things - i.e., clicking on some website, or asking important questions so I can incorporate the matrix into some form of tactical plans to defend my network, or support new strategies while working with others.

<br/>

## Why not use other existing community tools for this?
I have seen them, used them, and appreciate those that are writing their own. In the end, I am not gonna wait for anyone to do things the way I need them.

<br/>
<br/>

# **Usage**

This is a modular tool. The main concept of using this tool is:

```text

            (1)                      (2)                       (3)
             |                        |                         |
             |                        |                         |
        [ Extract ]-------------[ Transform ]---------------[ Load ]
             |                        |                         |
             |                        |                         |
             |                        |                         |
             v                        v                         v
       Download A Matrix         Baseline The Matrix        Search - Ask your question
```
<br/>
<br/>

## **Help Menu**
Building from the above concept, let's get into using this bad-boy.

<br/>

```bash
cdiaz@[mitre-assistant]
 >> ./target/release/mitre-assistant -h



mitre-assistant v.0.0.1
carlos diaz | @dfirence

Mitre Attack Assistant

        A more useful utility for the ATT&CK Matrix

USAGE:
    mitre-assistant [SUBCOMMAND]

FLAGS:
    -h, --help       Prints help information
    -V, --version    Prints version information

SUBCOMMANDS:
    baseline    Parse a Matrix into comprehensive insights
    download    Download a Matrix From The Mitre CTI Repo
    help        Prints this message or the help of the given subcommand(s)
    search      Search The Baseline
```
<br/>
<br/>

# *Download*
Use the `download` subcommand to get started, you can specific which matrix to download by using any of the keywords: `enterprise` or `mobile` or `pre-attack`

<br/>

```bash
# Assumes you want to download the `enterprise` matrix
#
$> mitre-assistant download -m enterprise


# Output
===========================================================================================

Downlading Matrix : enterprise
Downloading From  : https://raw.githubusercontent.com/mitre/cti/master/enterprise-attack/enterprise-attack.json

===========================================================================================
        |__(+) New File To Be Created: /Users/alice/.mitre-assistant/matrixes/enterprise.json
```
<br/>
<br/>

# *Baseline*
Use the `baseline` subcommand after you download your matrix to create the custom database that is required before you conduct your searches.

You baseline a matrix with any of the keywords:  `enterprise` or `mobile` or `pre-attack`

<br/>

```bash
$> mitre-assistant baseline -m enterprise


#Output
/Users/alice/.mitre-assistant/matrixes/enterprise.json
  |__(+) New File To Be Created: /Users/alice/.mitre-assistant/baselines/baseline-enterprise.json
```
<br/>
<br/>

# *Search*
Now you are ready to search your matrix.

You have to tell the `search subcommand` which matrix it is going to work with by using:

* the `-m` parameter followed by the name of the matrix 
* the `-t` parameter to provide your search term.

<br/>
<br/>

## *Search Terms*

|TERM|MATRIX|PURPOSE|
|----|------|-------|
|`datasources`|*enterprise*|Returns all datasources from the matrix|
|`deprecated`|*enterprise*|Returns all the deprecated techniques from the matrix|
|`platforms`|*enterprise*|Returns all the platforms (operating systems) from the matrix|
|`nodatasources`|*enterprise*|Returns all techniques or subtechniques **without** datasources|
|`nosub`|*enterprise*|Returns all the active techniques which do not have/use subtechniques|
|`revoked`|*enterprise*|Returns all of the technique id & name references revoked by Mitre|
|`stats`|*enterprise*|Returns an overview of `uniq` counts and `total` counts of key data elements|
|`subtechniques`|*enterprise*|Returns all subtechniques from the matrix|
|`techniques`|*enterprise*|Returns all techniques from the matrix|
|`tactics`|*enterprise*|Returns all tactics from the matrix|
|||
|||
|`initial-access`|*enterprise*|Returns all techniques in the **Initial Access** Tactic|
|`execution`|*enterprise*|Returns all techniques in the **Execution** Tactic|
|`persistence`|*enterprise*|Returns all techniques in the **Persistence** Tactic|
|`privilege-escalation`|*enterprise*|Returns all techniques in the **Privilege Escalation** Tactic|
|`defense-evasion`|*enterprise*|Returns all techniques in the **Defense Evasion** Tactic|
|`credential-access`|*enterprise*|Returns all techniques in the **Credential Access** Tactic|
|`discovery`|*enterprise*|Returns all techniques in the **Discovery** Tactic|
|`lateral-movement`|*enterprise*|Returns all tecniques in **Lateral Movement** Tactic|
|`collection`|*enterprise*|Returns all techniques in the **Collection** Tactic|
|`command-and-control`|*enterprise*|Returns all techniques in the **Command And Control** Tactic|
|`exfiltration`|*enterprise*|Returns all techniques in the **Exfiltration** Tactic|
|`impact`|*enterprise*|Returns all techniques in the **Impact** Tactic|
|||
|||
|`aws`|*enterprise*|Returns all techniques in the **AWS** Platform|
|`azure`|*enterprise*|Returns all techniques in the **AZURE** Platform|
|`azure-ad`|*enterprise*|Returns all techniques in the **AZURE-AD** Platform|
|`gcp`|*enterprise*|Returns all techniques in the **GCP** Platform|
|`linux`|*enterprise*|Returns all techniques in the **LINUX** Platform|
|`macos`|*enterprise*|Returns all techniques in the **MACOS** Platform|
|`office-365`|*enterprise*|Returns all techniques in the **OFFICE-365** Platform|
|`saas`|*enterprise*|Returns all techniques in the **SAAS** Platform|
|`windows`|*enterprise*|Returns all techniques in the **WINDOWS** Platform|
|||
|||
|`xref:datasources:platforms`|*enterprise*|Returns a 2d matrix of active techniques by datasource mapped to platform|
|`xref:datasources:tactics`|*enterprise*|Returns a 2d matrix of active techniques by datasource mapped to tactics|

<br/>
<br/>

## *Searching The Enterprise Matrix For An Overview Stats Summary*
You use the keyword `stats` in your search term, like this

```bash
# Assumed you want the summary of items in the matrix
#
$> mitre-assistant search -m enterprise -t "stats"
```
<br/>
<br/>

<div align="center"><h2>Unique & Total Counts</h2></div>

<hr/>
<div align="center">
    <img src="https://user-images.githubusercontent.com/11415591/89737350-33328d80-da3e-11ea-9f76-311251cfc851.png"></img>
</div>
<hr/>
<br/>
<br/>

<div align="center"><h2>By Platform</h2></div>

| TECHNIQUES | SUBTECHNIQUES|
|------------|--------------|
|![image](https://user-images.githubusercontent.com/11415591/89737360-47768a80-da3e-11ea-95da-81f68342624d.png)|![image](https://user-images.githubusercontent.com/11415591/89737366-54937980-da3e-11ea-981d-06518ef06e43.png)|

<hr/>
<br/>
<br/>

<div align="center"><h2>By Tactic/KillChain</h2></div>

| TACTICS - TECHNIQUES | TACTICS - SUBTECHNIQUES|
|------------|--------------|
|![image](https://user-images.githubusercontent.com/11415591/89737321-0bdbc080-da3e-11ea-9030-849fbd9420b2.png)|![image](https://user-images.githubusercontent.com/11415591/89737328-18f8af80-da3e-11ea-866f-2a09231aeee4.png)|


<hr/>
<br/>
<br/>


<hr/>
<br/>
<br/>

## *Searching The Enterprise Matrix For Techniques By Name*

By default, searching by the **name** of a technique is offered with a **partial match**.  Whereas, searching by technique id is a **full match**.

This means, you can search for techniques by name entering strings that may be incomplete, and the tool finds all references to your input.

Let's take a look at this example, where we search for any technique that has the word **boot**

```bash
# Assumes you want to search for techniques
# that have the word `boot`
#
$> mitre-assistant search -m enterprise -t "boot"
```
<br/>

The command above results in the image below, notice how the word `boot` matches across different techniques.

<br/>

![image](https://user-images.githubusercontent.com/11415591/90316166-50f46c80-deee-11ea-8254-4630516086f2.png)

<br/>
<br/>

## *Searching The Enterprise Matrix For A Single Technique By ID*


<br/>

```bash
# Assumes you want to search/query the enterprise matrix
# All terms must be enclosed by double-quotes
#
$> mitre-assistant search -m enterprise -t "t1021"
```
<br/>

![image](https://user-images.githubusercontent.com/11415591/89109722-cf8edb80-d411-11ea-82b5-3a4dde2d90b1.png)

<br/>

## *Searching The Enterprise Matrix For Many Techniques By ID*
Cool, now you just have to add a comma `,` in your term and launch it again, dead-simple!

<br/>

```bash
# Assumes you want to search for techniques:  T1021 & T1048
#
$> mitre-assistant search -m enterprise -t "t1021,t1048"

```

<br/>

![image](https://user-images.githubusercontent.com/11415591/89109703-ae2def80-d411-11ea-9268-ab7f42527386.png)

<br/>

## *Searching The Enterprise Matrix & Displaying The Subtechniques*
Another cool thing here is display the `subtechniques` for your query by using:

* the `-s` flag after your query

<br/>

```bash
# Assumes you want to see the Subtechniques for T1021
$> mitre-assistant search -m enterprise -t "t1021" -s
```
<br/>

![image](https://user-images.githubusercontent.com/11415591/89109790-69568880-d412-11ea-9869-325a35d7de13.png)

<br/>

## *Searching The Enterprise Matrix By Tactic**
You can ask the tool to give you all the techniques for a specific `Mitre Tactic`. You need to follow the convention used in the tool to get the right tactic.

This section describes how you can quickly ramp up on using tactic queries.

### **Step 1:  List of the Tactics in the Matrix**

* the `-t` parameter with the term `tactics`

```bash
# Assumes you want to know the Tactics
#
$> mitre-assistant search -m enterprise -t "tactics"

# Output 
                +-------+----------------------+
                | INDEX | TACTICS              |
                +-------+----------------------+
                | 1     | collection           |
                +-------+----------------------+
                | 2     | command-and-control  |
                +-------+----------------------+
                | 3     | credential-access    |
                +-------+----------------------+
                | 4     | defense-evasion      |
                +-------+----------------------+
                | 5     | discovery            |
                +-------+----------------------+
                | 6     | execution            |
                +-------+----------------------+
                | 7     | exfiltration         |
                +-------+----------------------+
                | 8     | impact               |
                +-------+----------------------+
                | 9     | initial-access       |
                +-------+----------------------+
                | 10    | lateral-movement     |
                +-------+----------------------+
                | 11    | persistence          |
                +-------+----------------------+
                | 12    | privilege-escalation |
                +-------+----------------------+
```
<br/>
<br/>

### **Step 2: Search By Tactic**

Now you can use any of the tactics above in your search query, like this:

* the `-t` parameter with the term `{{ tactic_name }}`
  
<br/>

```bash
# Assumes you want to search by the `initial-access` tactic
#
$> mitre-assistant search -m enterprse -t "initial-access"

```
<br/>

![image](https://user-images.githubusercontent.com/11415591/90316089-1094ee80-deee-11ea-8c38-f75ed7a3b6e5.png)

<br/>
<br/>

## *Searching For The Revoked Techniques*
Revoked techniques seem to be those that are discontinued and re-arranged now into subtechniques.  You can search for the ones `revoked` in the matrix by using a keyword in your search term:

* the `-t` parameters with the term `revoked`

<br/>

```bash
# Assumes you want to see the Revoked Techniques
#
$> mitre-assistant search -m enterprise -t "revoked"
```
<br/>

<div align="center">
    <img src="https://user-images.githubusercontent.com/11415591/89109865-074a5300-d413-11ea-87e9-5fadeb569e84.png"></img>
</div>


<br/>
<br/>

## *Searching For The Deprecated Techniques*
Deprecated techniques seem to be those that are no longer valid and used in a mtrix.  You can search for the ones `deprecated` in the matrix by using a keyword in your search term:

* the `-t` parameter with the term `deprecated`

<br/>

```bash
# Assumes you want to see the Deprecated Techniques
#
$> mitre-assistant search -m enterprise -t "deprecated"
```
<br/>

<div align="center">
    <img src="https://user-images.githubusercontent.com/11415591/90009017-4c6c5180-dc6b-11ea-83ef-8c8b8b8e75a6.png"></img>
</div>


<br/>
<br/>


## *Searching For The Tactics/KillChains*
Tactics are well, I guess a higher level object where the techniques are organized into. Read their website.

* the `-t` parameter with the term `tactics`

<br/>

```bash
# Assumes you want to see the All Tactics/KillChains
# for the enterprise matrix
#
$> mitre-assistant search -m enterprise -t "tactics"

# Output


                +-------+----------------------+
                | INDEX | TACTICS              |
                +-------+----------------------+
                | 1     | collection           |
                +-------+----------------------+
                | 2     | command-and-control  |
                +-------+----------------------+
                | 3     | credential-access    |
                +-------+----------------------+
                | 4     | defense-evasion      |
                +-------+----------------------+
                | 5     | discovery            |
                +-------+----------------------+
                | 6     | execution            |
                +-------+----------------------+
                | 7     | exfiltration         |
                +-------+----------------------+
                | 8     | impact               |
                +-------+----------------------+
                | 9     | initial-access       |
                +-------+----------------------+
                | 10    | lateral-movement     |
                +-------+----------------------+
                | 11    | persistence          |
                +-------+----------------------+
                | 12    | privilege-escalation |
                +-------+----------------------+
```

<br/>
<br/>


## *Searching For The Platforms*
Platforms are the relevant operating systems where a technique is exercised or abused by an adversary. To get the platforms in the enterprise matrix use the keyword `platforms`.

* the `-t` parameter with the term `platforms`

<br/>

```bash
# Assumes you want to see the All Platforms
# for the enterprise matrix
#
$> mitre-assistant search -m enterprise -t "platforms"

# Output

                    +-------+------------+
                    | INDEX | PLATFORMS  |
                    +-------+------------+
                    | 1     | macos      |
                    +-------+------------+
                    | 2     | azure      |
                    +-------+------------+
                    | 3     | aws        |
                    +-------+------------+
                    | 4     | office-365 |
                    +-------+------------+
                    | 5     | azure-ad   |
                    +-------+------------+
                    | 6     | windows    |
                    +-------+------------+
                    | 7     | saas       |
                    +-------+------------+
                    | 8     | linux      |
                    +-------+------------+
                    | 9     | gcp        |
                    +-------+------------+
```

<br/>
<br/>

## *Searching The Enterprise Matrix For All Techniques By Platform*

You can ask the tool to give you all the **active techniques** based on a specific platform, like this.

* the `-t` parameter with the term `{{ platform_name }}`

<br/>

```bash
# Assumes you want to see the All Techniques By The Linux Platform
#
$> mitre-assistant search -m enterprise -t "linux"
```

<br/>

The query above produces the image below, notice how the `PLATFORMS` column denotes the platform you wanted.

<br/>
<div align="center">
    <img src="https://user-images.githubusercontent.com/11415591/90335096-3084ea80-dfa0-11ea-8a5c-6e16b4c34561.png"></img>
</div>
<br/>
<br/>

## *Searching For The Datasources*

```text
Protip:

1. Do not follow Mitre blindly, you need to curate their content
and organize it.

Example:

1. DLL Monitoring & Loaded DLLs

Mitre currently has these two datasources, what does this mean?

To me in the security Space, there's only one source, not two.
```
<br/>

Datasources are a non-concrete description by Mitre that seems to suggest the context of evidence needed to be successful at pursuing visibility or detection capabilities for the given technique. This query gets you the datasources as provided by Mitre in their CTI github

* the `-t` parameters with the term `datasources`

<br/>

```bash
# Assumes you want to see the All Datasources
# for the enterprise matrix
#
$> mitre-assistant search -m enterprise -t "datasources"

# Output

                +-------+------------------------------------+
                | INDEX | DATASOURCE                         |
                +-------+------------------------------------+
                | 1     | access-tokens                      |
                +-------+------------------------------------+
                | 2     | anti-virus                         |
                +-------+------------------------------------+
                | 3     | api-monitoring                     |
                +-------+------------------------------------+
                | 4     | application-logs                   |
                +-------+------------------------------------+
                | 5     | asset-management                   |
                +-------+------------------------------------+
                | 6     | authentication-logs                |
                +-------+------------------------------------+
                | 7     | aws-cloudtrail-logs                |
                +-------+------------------------------------+
                | 8     | azure-activity-logs                |
                +-------+------------------------------------+
                | 9     | binary-file-metadata               |
                +-------+------------------------------------+
                | 10    | bios                               |
                +-------+------------------------------------+
                | 11    | browser-extensions                 |
                +-------+------------------------------------+
                | 12    | component-firmware                 |
                +-------+------------------------------------+
                | 13    | data-loss-prevention               |
                +-------+------------------------------------+
                | 14    | detonation-chamber                 |
                +-------+------------------------------------+
                | 15    | digital-certificate-logs           |
                +-------+------------------------------------+
                | 16    | disk-forensics                     |
                +-------+------------------------------------+
                | 17    | dll-monitoring                     |
                +-------+------------------------------------+
                | 18    | dns-records                        |
                +-------+------------------------------------+
                | 19    | efi                                |
                +-------+------------------------------------+
                | 20    | email-gateway                      |
                +-------+------------------------------------+
                | 21    | environment-variable               |
                +-------+------------------------------------+
                | 22    | file-monitoring                    |
                +-------+------------------------------------+
                | 23    | gcp-audit-logs                     |
                +-------+------------------------------------+
                | 24    | host-network-interface             |
                +-------+------------------------------------+
                | 25    | kernel-drivers                     |
                +-------+------------------------------------+
                | 26    | loaded-dlls                        |
                +-------+------------------------------------+
                | 27    | mail-server                        |
                +-------+------------------------------------+
                | 28    | malware-reverse-engineering        |
                +-------+------------------------------------+
                | 29    | mbr                                |
                +-------+------------------------------------+
                | 30    | named-pipes                        |
                +-------+------------------------------------+
                | 31    | netflow/enclave-netflow            |
                +-------+------------------------------------+
                | 32    | network-device-logs                |
                +-------+------------------------------------+
                | 33    | network-intrusion-detection-system |
                +-------+------------------------------------+
                | 34    | network-protocol-analysis          |
                +-------+------------------------------------+
                | 35    | oauth-audit-logs                   |
                +-------+------------------------------------+
                | 36    | office-365-account-logs            |
                +-------+------------------------------------+
                | 37    | office-365-audit-logs              |
                +-------+------------------------------------+
                | 38    | office-365-trace-logs              |
                +-------+------------------------------------+
                | 39    | packet-capture                     |
                +-------+------------------------------------+
                | 40    | powershell-logs                    |
                +-------+------------------------------------+
                | 41    | process-command-line-parameters    |
                +-------+------------------------------------+
                | 42    | process-monitoring                 |
                +-------+------------------------------------+
                | 43    | process-use-of-network             |
                +-------+------------------------------------+
                | 44    | sensor-health-and-status           |
                +-------+------------------------------------+
                | 45    | services                           |
                +-------+------------------------------------+
                | 46    | ssl/tls-inspection                 |
                +-------+------------------------------------+
                | 47    | stackdriver-logs                   |
                +-------+------------------------------------+
                | 48    | system-calls                       |
                +-------+------------------------------------+
                | 49    | third-party-application-logs       |
                +-------+------------------------------------+
                | 50    | user-interface                     |
                +-------+------------------------------------+
                | 51    | vbr                                |
                +-------+------------------------------------+
                | 52    | web-application-firewall-logs      |
                +-------+------------------------------------+
                | 53    | web-logs                           |
                +-------+------------------------------------+
                | 54    | web-proxy                          |
                +-------+------------------------------------+
                | 55    | windows-error-reporting            |
                +-------+------------------------------------+
                | 56    | windows-event-logs                 |
                +-------+------------------------------------+
                | 57    | windows-registry                   |
                +-------+------------------------------------+
                | 58    | wmi-objects                        |
                +-------+------------------------------------+
```

<br/>
<br/>

## *Searching Datasources With Cross References: **Experimental***
At this moment, v.0.0.10 and above allow for experimental cross-references of datasources and `platforms`, as well as, `tactics`.

This experiment is to understand, based on the suggested datasources by Mitre, where do they fit according to the platforms or tactics.

**SPECIAL NOTE**:  The queries for cross-references **only compute** counts against the `Active Techniques` total. No Subtechniques are taken into account, yet.

<br/>

To launch a cross-reference query you use a prefix in your term - `xref:`, let's look at an example

* the `-t` parameters with the term `xref:datasources:{{ reference_type }}`
  
<br/>

```bash
# Assumes you want to cross-reference datasources to platforms
#
$> mitre-assistant search -m enterprise -t "xref:datasources:platforms"
```

<br/>

Notice the above command uses a colon "`:`" character to tell the search engne this is a cross-reference query.
The above command results in the image below.

<br/>

![image](https://user-images.githubusercontent.com/11415591/90342001-91c5b180-dfd2-11ea-994f-ba259b06e947.png)

<br/>
<br/>

In contrast, let's launch a cross-reference query against the tactics, like this:

```bash
# Assumes you want to cross-reference datasources to tactics
#
$> mitre-assistant search -m enterprise -t "xref:datasources:tactics"
```

<br/>

And that now produces this image below.

<br/>

![image](https://user-images.githubusercontent.com/11415591/90341975-53c88d80-dfd2-11ea-9106-2db9843e7b8a.png)

<br/>
<br/>

## *Searching For Edge Cases:  Techniques Without a Subtechniques*
Some techniques, do not have subtechniques assigned, or as I like to thunk of it, have not been fully updated by Mitre.

Use the keyword `nosub` to obtain a list of active techniques that may not have an assigned subtechnique by Mitre.

* the `-t` parameter with the term `nosub`

<br/>

```bash
# Assumes you want to see the Techniques that do not have Subtechniques
# for the enterprise matrix
#
$> mitre-assistant search -m enterprise -t "nosub"
```

<br/>
<br/>

![image](https://user-images.githubusercontent.com/11415591/90009417-0663bd80-dc6c-11ea-87d0-ad91d71ecc51.png)

<br/>

## *Searching For Edge Cases:  Techniques Without a Datasource*
This is the edge-case that drove to create this tool for myself.  I found someone's tool incorrectly parsed the matrix and I needed to report to my management the plan of action based on data sources.  This is very important for practitioners who leverage the matrix for real world tactical operations.

Reference this example:  [NO_DATA_SOURCE_SAMPLE](https://user-images.githubusercontent.com/11415591/88487153-a58c7380-cf50-11ea-8547-e03a6b7a9185.png)

Use the keyword `nodatasources` to obtain a list of active techniques that may not have an assigned datasource by Mitre.

* the `-t` parameter with the term `nodatasources`

<br/>

```bash
# Assumes you want to see the Techniques that do not have Datasources
# for the enterprise matrix
#
$> mitre-assistant search -m enterprise -t "nodatasources"
```

<br/>
<br/>

![image](https://user-images.githubusercontent.com/11415591/89842172-dd93d900-db42-11ea-81c9-89d5a5c85961.png)

<br/>



# **Statistical Stuff**
As I mentioned, my work with this matrix is at the provider level, I have to devise coverage plans, or brainstorming workshops with my fellow blue-teamers to understand what an emulation plan means in terms of effort, engineering for new content and consequently sizing our systems to increase our visibility and detection needs.

These experiments were very useful to me a couple of years ago as I started learning about the Mitre ATT&CK matrixes.

<br/>

## TODO: Awesome Stuff here


<br/>
<br/>
<br/>

# References
|SOURCE|URL|
|------|---|
|Mitre CTI Github|[LINK](https://github.com/mitre/cti/blob/master/USAGE.md#working-with-deprecated-and-revoked-objects)|

<br/>
<br/>

# Kudos - RUSTACEANS
Many super kudos, to the amazing RUST Community, for their warm embrace of everyone that wants the journey.  Seemingly, to all of the super creators of loved tools from python being ported into rust.

## TODO - Thank Crates Contributions