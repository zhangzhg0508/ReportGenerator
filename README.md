<h1 align="center">

<img src="https://raw.githubusercontent.com/danielpalme/ReportGenerator/main/docs/resources/logo_512.png" alt="ReportGenerator" width="256"/>
<br/>
ReportGenerator
</h1>


<div align="center">
    
<b>Powerful code coverage visualization</b>
    
[![GitHub license](https://img.shields.io/badge/license-Apache%202-blue.svg)](https://raw.githubusercontent.com/danielpalme/ReportGenerator/main/LICENSE.txt)
[![CI-CD](https://github.com/danielpalme/ReportGenerator/actions/workflows/ci.yml/badge.svg)](https://github.com/danielpalme/ReportGenerator/actions/workflows/ci.yml)

</div>

*ReportGenerator* converts coverage reports generated by coverlet, OpenCover, dotCover, Visual Studio, NCover, Cobertura, JaCoCo, Clover, gcov or lcov into human readable reports in various formats.

The reports do not only show the coverage quota, but also include the source code and visualize which lines have been covered.

*ReportGenerator* supports merging several reports into one.

<div align="center">

![Input and output](https://danielpalme.github.io/ReportGenerator/resources/input_output.png)

</div>

## License
- ReportGenerator is licensed under the [Apache License, Version 2.0](https://opensource.org/licenses/Apache-2.0)
- You can support the project by [becoming a sponsor](https://github.com/sponsors/danielpalme).  
I encourage you to do so, especially if you are using ReportGenerator for commercial projects.

## Getting started
*ReportGenerator* is a commandline tool which works with full .NET Framework and .NET Core.  
Use the online [configuration tool](https://danielpalme.github.io/ReportGenerator/usage.html) to get started quickly.

### Install the package matching your platform and needs

|**Package**|**Platforms**|**Installation/Usage**|
|:----------|:------------|:---------------------|
|[ReportGenerator](https://www.nuget.org/packages/ReportGenerator)<br/><br/>[![Nuget](https://img.shields.io/nuget/v/ReportGenerator.svg)![Nuget](https://img.shields.io/nuget/dt/ReportGenerator.svg)](https://www.nuget.org/packages/ReportGenerator)|.NET Core >=3.1<br/>.NET Framework 4.7|Use this package if your project is based on *.NET Framework* or *.NET Core* and you want to use *ReportGenerator* via the command line or a build script.<br/><br/>**Usage**<br/>```dotnet $(UserProfile).nuget\packages\reportgenerator\x.y.z\tools\net6.0\ReportGenerator.dll [options]```<br/>```$(UserProfile).nuget\packages\reportgenerator\x.y.z\tools\net6.0\ReportGenerator.exe [options]```<br/><br/>```$(UserProfile)\.nuget\packages\reportgenerator\x.y.z\tools\net47\ReportGenerator.exe [options]```|
|[dotnet-reportgenerator-globaltool](https://www.nuget.org/packages/dotnet-reportgenerator-globaltool)<br/><br/>[![Nuget](https://img.shields.io/nuget/v/dotnet-reportgenerator-globaltool.svg)![Nuget](https://img.shields.io/nuget/dt/dotnet-reportgenerator-globaltool.svg)](https://www.nuget.org/packages/dotnet-reportgenerator-globaltool)|.NET Core >=3.1 |Use this package if your project is based on *.NET Core* and you want to use *ReportGenerator* as a (global) 'DotnetTool'.<br/><br/>**Installation**<br/>```dotnet tool install -g dotnet-reportgenerator-globaltool```<br/><br/>```dotnet tool install dotnet-reportgenerator-globaltool --tool-path tools```<br/><br/>```dotnet new tool-manifest```<br/>```dotnet tool install dotnet-reportgenerator-globaltool```<br/><br/>**Usage**<br/>```reportgenerator [options]```<br/>```tools\reportgenerator.exe [options]```<br/>```dotnet reportgenerator [options]```|
|[ReportGenerator.Core](https://www.nuget.org/packages/ReportGenerator.Core)<br/><br/>[![Nuget](https://img.shields.io/nuget/v/ReportGenerator.Core.svg)![Nuget](https://img.shields.io/nuget/dt/ReportGenerator.Core.svg)](https://www.nuget.org/packages/ReportGenerator.Core)|.NET Standard 2.0|Use this package if you want to write a custom **plugin** for *ReportGenerator* or if you want to call/execute *ReportGenerator* within your code base.<br/><br/>**Plugin development**<br/>[Custom reports](https://github.com/danielpalme/ReportGenerator/wiki/Custom-reports)<br/>[Custom history storage](https://github.com/danielpalme/ReportGenerator/wiki/Custom-history-storage)|
|[Azure DevOps extension](https://marketplace.visualstudio.com/items?itemName=Palmmedia.reportgenerator)<br/><br/>[![Visual Studio Marketplace Version](https://img.shields.io/visual-studio-marketplace/v/Palmmedia.reportgenerator.svg)![Visual Studio Marketplace Installs - Azure DevOps Extension](https://img.shields.io/visual-studio-marketplace/azure-devops/installs/total/Palmmedia.reportgenerator.svg)](https://marketplace.visualstudio.com/items?itemName=Palmmedia.reportgenerator)|.NET Core >=3.1| Add the Azure DevOps extension to your build pipeline.<br />[Learn more](https://github.com/danielpalme/ReportGenerator/wiki/Integration#azure-devops-extension)|
|[GitHub Actions](https://github.com/marketplace/actions/reportgenerator)|.NET Core >=3.1| Add the GitHub Action to your build pipeline.<br />[Learn more](https://github.com/danielpalme/ReportGenerator/wiki/Integration#github-actions)|

### Usage / Command line parameters
```
Parameters:
    ["]-reports:<report>[;<report>][;<report>]["]
    ["]-targetdir:<target directory>["]
    [["]-reporttypes:<Html|HtmlSummary|...>[;<Html|HtmlSummary|...>]["]]
    [["]-sourcedirs:<directory>[;<directory>][;<directory>]["]]
    [["]-historydir:<history directory>["]]
    [["]-plugins:<plugin>[;<plugin>][;<plugin>]["]]
    [["]-assemblyfilters:<(+|-)filter>[;<(+|-)filter>][;<(+|-)filter>]["]]
    [["]-classfilters:<(+|-)filter>[;<(+|-)filter>][;<(+|-)filter>]["]]
    [["]-filefilters:<(+|-)filter>[;<(+|-)filter>][;<(+|-)filter>]["]]
    [["]-verbosity:<Verbose|Info|Warning|Error|Off>["]]
    [["]-title:<title>["]]
    [["]-tag:<tag>["]]
    [["]-license:<license>["]]

Explanations:
   Reports:            The coverage reports that should be parsed (separated by semicolon).
                       Globbing is supported.
   Target directory:   The directory where the generated report should be saved.
   Report types:       The output formats and scope (separated by semicolon).
                       Values: Badges, Clover, Cobertura, CsvSummary, MarkdownSummary, 
                       Html, Html_Light, Html_Dark,
                       HtmlChart, HtmlInline, HtmlSummary,
                       HtmlInline_AzurePipelines, HtmlInline_AzurePipelines_Light, HtmlInline_AzurePipelines_Dark,
                       JsonSummary, Latex, LatexSummary, lcov, MHtml, PngChart, SonarQube, TeamCitySummary,
                       TextSummary, Xml, XmlSummary
   Source directories: Optional directories which contain the corresponding source code (separated by semicolon).
                       The source directories are used if coverage report contains classes without path information.
                       Globbing is not supported.
   History directory:  Optional directory for storing persistent coverage information.
                       Can be used in future reports to show coverage evolution.
   Plugins:            Optional plugin files for custom reports or custom history storage (separated by semicolon). 
   Assembly filters:   Optional list of assemblies that should be included or excluded in the report.
   Class filters:      Optional list of classes that should be included or excluded in the report.
   File filters:       Optional list of files that should be included or excluded in the report.
                       Exclusion filters take precedence over inclusion filters.                      
                       Wildcards are allowed.
   Verbosity:          The verbosity level of the log messages.
                       Values: Verbose, Info, Warning, Error, Off
   Title:              Optional title.
   Tag:                Optional tag or build version.
   License:            Optional license. Get your license here: https://danielpalme.github.io/ReportGenerator/pro

Default values:
   -reporttypes:Html
   -assemblyfilters:+*
   -classfilters:+*
   -filefilters:+*
   -verbosity:Info

Examples:
   "-reports:coverage.xml" "-targetdir:C:\report"
   "-reports:target\*\*.xml" "-targetdir:C:\report" -reporttypes:Latex;HtmlSummary -title:IntegrationTest -tag:v1.4.5
   "-reports:coverage1.xml;coverage2.xml" "-targetdir:report" "-sourcedirs:C:\MyProject" -plugins:CustomReports.dll
   "-reports:coverage.xml" "-targetdir:C:\report" "-assemblyfilters:+Included;-Excluded.*"
```

#### .netconfig support

All the above parameters can also be persisted in a [.netconfig](https://dotnetconfig.org) file, under a `[ReportGenerator]` 
section. Examples:

```gitconfig
[ReportGenerator]
	reports = coverage.xml
	targetdir = "C:\\report"
	reporttypes = Latex;HtmlSummary
	assemblyfilters = +Test;-Test
	classfilters = +Test2;-Test2
```

All the plural options can also be specified as multiple singular entries, like:

```gitconfig
[ReportGenerator]
	report = coverage1.xml
	report = coverage2.xml
	reporttype = Latex
	reporttype = HtmlSummary
	assemblyfilter = +Test
	assemblyfilter = -Test
	classfilter = +Test2
	classfilter = -Test2
	filefilter = +cs
	filefilter = -vb
	sourcedir = src
	sourcedir = test
```

Adding/removing values is trivial using the [dotnet-config](https://dotnetconfig.org) CLI:

```bash
# set a single-valued variable
dotnet config reportgenerator.reporttypes Latex;HtmlSummary
# add to multi-valued variable
dotnet config --add reportgenerator.report coverage3.xml
# clear all multi-valued entries for a variable
dotnet config --unset-all reportgenerator.assemblyfilter
```

Of course it's equally trivial to just edit the `.netconfig` file by hand.

#### MSBuild
A MSBuild task also exists:

```xml
<?xml version="1.0" encoding="utf-8"?>
<Project DefaultTargets="Coverage" xmlns="http://schemas.microsoft.com/developer/msbuild/2003" ToolsVersion="4.0">
  <ItemGroup>
    <PackageReference Include="ReportGenerator" Version="x.y.z" />
  </ItemGroup>
  <Target Name="Coverage">
    <ItemGroup>
      <CoverageFiles Include="OpenCover.xml" />
    </ItemGroup>
    <ReportGenerator ProjectDirectory="$(MSBuildProjectDirectory)" ReportFiles="@(CoverageFiles)" TargetDirectory="report" ReportTypes="Html;Latex" HistoryDirectory="history" Plugins="CustomReports.dll" AssemblyFilters="+Include;-Excluded" VerbosityLevel="Verbose" />
  </Target>
</Project>
```

The MSBuild task parameters can be complemented with the `.netconfig`, if used. That means that parameters 
can be omitted if they are provided via `.netconfig`, which is useful when reusing fixed settings across 
multiple projects in a solution, where the MSBuild task is only provided the dynamic values for the current 
project:

Given the following `.netconfig`:

```gitconfig
[ReportGenerator]
  reporttypes = Html;Latex
  targetdirectory = report
  historydirectory = history
  assemblyfilters = +Include;-Excluded
  verbosityLevel = Verbose
```

The above target could be simplified as:

```xml
  <Target Name="Coverage">
    <ItemGroup>
      <CoverageFiles Include="OpenCover.xml" />
    </ItemGroup>
    <ReportGenerator ProjectDirectory="$(MSBuildProjectDirectory)"
                     ReportFiles="@(CoverageFiles)" 
                     Plugins="CustomReports.dll" />
  </Target>
```


## Supported input and output file formats
*ReportGenerator* supports several input and output formats.  
The wiki explains the different [output formats](https://github.com/danielpalme/ReportGenerator/wiki/Output-formats) or you can download [sample reports](https://danielpalme.github.io/ReportGenerator/resources/SampleReports.zip) of all formats.  
If you need a custom format, you can create a [plugin](https://github.com/danielpalme/ReportGenerator/wiki/Custom-reports).

| **Input formats** | **Output formats** |
|:------------------|:-------------------|
| <ul><li>[OpenCover](https://github.com/OpenCover/opencover) ([Nuget](https://www.nuget.org/packages/OpenCover))<br/>OpenCover format is also generated by [coverlet](https://github.com/coverlet-coverage/coverlet/) and [altcover](https://github.com/SteveGilham/altcover)</li><li>[dotCover](https://www.jetbrains.com/dotcover/help/dotCover__Console_Runner_Commands.html) ([Nuget](https://www.nuget.org/packages/JetBrains.dotCover.CommandLineTools/), /ReportType=DetailedXML)</li><li>Visual Studio ([vstest.console.exe](https://github.com/danielpalme/ReportGenerator/wiki/Visual-Studio-Coverage-Tools#vstestconsoleexe), [CodeCoverage.exe](https://github.com/danielpalme/ReportGenerator/wiki/Visual-Studio-Coverage-Tools#codecoverageexe))</li><li>[NCover](https://www.ncover.com/info/download) (tested version 1.5.8, other versions may not work)</li><li>[Cobertura](https://github.com/cobertura/cobertura)</li><li>[JaCoCo](https://www.jacoco.org/jacoco/index.html)</li><li>[Clover](https://openclover.org/)</li><li>Mono ([mprof-report](https://www.mono-project.com/docs/debug+profile/profile/profiler/#analyzing-the-profile-data))</li><li>[gcov](https://gcc.gnu.org/onlinedocs/gcc/Gcov.html)</li><li>[lcov](https://github.com/linux-test-project/lcov)</li></ul><br/> | <ul><li>Html, Html_Light, Html_Dark, HtmlSummary, HtmlChart, HtmlInline, HtmlInline_AzurePipelines, HtmlInline_AzurePipelines_Light, HtmlInline_AzurePipelines_Dark, [MHtml](https://en.wikipedia.org/wiki/MHTML)</li><li>Clover</li><li>Cobertura</li><li>[SonarQube](https://docs.sonarqube.org/latest/analysis/generic-test)</li><li>TeamCitySummary</li><li>[lcov](https://github.com/linux-test-project/lcov)</li><li>Xml, XmlSummary</li><li>JsonSummary</li><li>Latex, LatexSummary</li><li>TextSummary</li><li>CsvSummary</li><li>MarkdownSummary</li><li>PngChart</li><li>Badges</li><li>[Custom reports](https://github.com/danielpalme/ReportGenerator/wiki/Custom-reports)</li></ul> |

### Screenshots
The screenshots show two snippets of the generated reports:
![Screenshot 1](https://danielpalme.github.io/ReportGenerator/resources/screenshot1.png)
![Screenshot 2](https://danielpalme.github.io/ReportGenerator/resources/screenshot2.png)

**Badges**  
Badges in SVG and PNG format can be generated if `-reporttypes:Badges` is used:

![Sample badge](https://danielpalme.github.io/ReportGenerator/resources/badge.svg)

## Resources

### Visual Studio extensions
The following extensions exist to visualize coverage in Visual Studio: 
| **Name** | **Coverage tool** | **Links** | **Comment** |
|:---------|:------------------|:----------|:------------|
| AxoCover | [OpenCover](https://github.com/OpenCover/opencover)| [GitHub](https://github.com/axodox/AxoCover)<br/>[Marketplace](https://marketplace.visualstudio.com/items?itemName=axodox1.AxoCover) | VS 2019 is not supported |
| FineCodeCoverage | [coverlet](https://github.com/coverlet-coverage/coverlet/), [OpenCover](https://github.com/OpenCover/opencover) | [GitHub](https://github.com/FortuneN/FineCodeCoverage)<br/>[Marketplace](https://marketplace.visualstudio.com/items?itemName=FortuneNgwenya.FineCodeCoverage) | |
| RunCoverletReport | [coverlet](https://github.com/coverlet-coverage/coverlet/) | [GitHub](https://github.com/the-dext/RunCoverletReport)<br/>[Marketplace](https://marketplace.visualstudio.com/items?itemName=ChrisDexter.RunCoverletReport) | |

### Links
* https://www.palmmedia.de/Blog/2017/12/6/reportgenerator-new-release-with-risk-hotspots-analysis
* https://www.palmmedia.de/Blog/2016/11/6/reportgenerator-new-release-with-enhanced-html-report-and-cobertura-support
* https://www.palmmedia.de/Blog/2015/1/27/reportgenerator-new-beta-with-historytrend-charts
* https://www.palmmedia.de/Blog/2012/4/29/reportgenerator-new-release-with-more-advanced-report-preprocessing

### Download statistics
![Nuget](https://img.shields.io/nuget/dt/ReportGenerator.svg?label=ReportGenerator%40nuget)
![Nuget](https://img.shields.io/nuget/dt/dotnet-reportgenerator-globaltool.svg?label=dotnet-reportgenerator-globaltool%40nuget)
![Nuget](https://img.shields.io/nuget/dt/dotnet-reportgenerator-cli.svg?label=dotnet-reportgenerator-cli%40nuget)
![Nuget](https://img.shields.io/nuget/dt/ReportGenerator.Core.svg?label=ReportGenerator.Core%40nuget)

![Visual Studio Marketplace Installs - Azure DevOps Extension](https://img.shields.io/visual-studio-marketplace/azure-devops/installs/total/Palmmedia.reportgenerator.svg?label=Azure%20DevOps)
![GitHub All Releases](https://img.shields.io/github/downloads/danielpalme/ReportGenerator/total.svg?label=GitHub)
![Chocolatey](https://img.shields.io/chocolatey/dt/reportgenerator.portable.svg?label=Chocolatey)

### Trends
[Nuget downloads](https://nugettrends.com/packages?months=24&ids=ReportGenerator&ids=dotnet-reportgenerator-globaltool&ids=ReportGenerator.Core&ids=dotnet-reportgenerator-cli)  
[GitHub stars](https://star-history.t9t.io/#danielpalme/ReportGenerator)

## Contact

Author: Daniel Palme  
Blog: [www.palmmedia.de](https://www.palmmedia.de)  
Twitter: [@danielpalme](https://twitter.com/danielpalme)  
