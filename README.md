<p align="center">
  <a href="https://ghpreporter.github.io/"><img src="https://github.com/GHPReporter/GHPReporter.github.io/blob/master/img/logo-small.png?raw=true" alt="Project icon"></a>
  <br><br>
  <b>Some Links:</b><br>
  <a href="https://github.com/GHPReporter/Ghpr.Core">Core</a> |
  <a href="https://github.com/GHPReporter/Ghpr.MSTest">MSTest</a> |
  <a href="https://github.com/GHPReporter/Ghpr.MSTestV2">MSTestV2</a> |
  <a href="https://github.com/GHPReporter/Ghpr.NUnit">NUnit</a> |
  <a href="https://github.com/GHPReporter/Ghpr.SpecFlow">SpecFlow</a> |
  <a href="https://github.com/GHPReporter/Ghpr.Console">Console</a> |
  <a href="https://github.com/GHPReporter/GHPReporter.github.io/">Site Repo</a>
</p>

[![Build status](https://ci.appveyor.com/api/projects/status/edl1eag5luk5v4xs?svg=true)](https://ci.appveyor.com/project/elv1s42/ghpr-nunit)
[![NuGet Version](https://img.shields.io/nuget/v/Ghpr.NUnit.svg)](https://www.nuget.org/packages/Ghpr.NUnit)
[![Codacy Badge](https://api.codacy.com/project/badge/Grade/dcdcf3b7866242fba326fb9aa47871b3)](https://www.codacy.com/app/GHPReporter/Ghpr.NUnit?utm_source=github.com&amp;utm_medium=referral&amp;utm_content=GHPReporter/Ghpr.NUnit&amp;utm_campaign=Badge_Grade)
[![CodeFactor](https://www.codefactor.io/repository/github/ghpreporter/ghpr.nunit/badge)](https://www.codefactor.io/repository/github/ghpreporter/ghpr.nunit)
[![FOSSA Status](https://app.fossa.io/api/projects/git%2Bgithub.com%2FGHPReporter%2FGhpr.NUnit.svg?type=shield)](https://app.fossa.io/projects/git%2Bgithub.com%2FGHPReporter%2FGhpr.NUnit?ref=badge_shield)

# Ghpr.NUnit

## Usage:

### With installed [NUnit 3 Console](https://github.com/nunit/nunit-console/releases)

 - Check you have the [latest version installed](https://github.com/nunit/nunit-console/releases)
 - Download the latest version of Ghpr.NUnit (using NuGet)
 - Add relative path to `Ghpr.NUnit.dll` from build folder of your tests (example: _addins/../../../Users/Evgeniy_Kosjakov/Documents/GitHub/Ghpr.NUnit.Examples/build/Ghpr.NUnit.dll_) into `nunit.bundle.addins` file (file located in *[nunit_console_location]/addins*). Also make sure that your build contains such libraries and files  as `Ghpr.Core.dll`, `Ghpr.NUnit.dll`, `Ghpr.LocalFileSystem.dll`, `Ghpr.NUnit.Settings.json` and `Newtonsoft.Json.dll`: <img src="https://github.com/GHPReporter/Ghpr.NUnit/blob/master/nunit.png?raw=true" alt="Project icon">
 - Run your tests via NUnit Console
 
### With NUnit 3 ConsoleRunner NuGet package

 - Check you have the [latest NuGet package installed](https://www.nuget.org/packages/NUnit.ConsoleRunner/)
 - Download the latest version of Ghpr.NUnit (using NuGet)
 - Add relative path to `Ghpr.NUnit.dll` located in your build folder into `nunit.nuget.addins` in tools directory of NUnit.ConsoleRunner.3.10.0. Also make sure that your build contains such libraries and files  as `Ghpr.Core.dll`, `Ghpr.NUnit.dll`, `Ghpr.LocalFileSystem.dll`, `Ghpr.NUnit.Settings.json` and `Newtonsoft.Json.dll`.
 - Run your tests via NUnit Console Runner
 
## How to publish the report in Jenkins

Please, read [this](https://github.com/GHPReporter/Ghpr.Core#how-to-publish-the-report-in-jenkins) `'How to publish the report in Jenkins'` instruction.

## How to work with screenshots

If you want to add screenshots to your report, you need to implement your own method of taking screenshot as `byte[]`. This is needed because there is no way to take screenshot which will work on any testing framework or CI tool (such as Jenkins or TeamCity). If you are using WebDriver, you can take screenshot using WebDriver. Also NUnit attachments are supported. 

```csharp
[Test]
public void TestMethod()
{
    var bytes = TakeScreenshot(); //your implementation
    //all you need to do is to pass byte[] to ScreenHelper:
    ScreenHelper.SaveScreenshot(bytes);
}
```
If you want to be able to take screenshots for failed tests, you can take a look at this approach:

```csharp
[TearDown]
public void TakeScreenIfFailed()
{
    var res = TestContext.CurrentContext.Result.Outcome;
    if (res.Equals(ResultState.Failure) || res.Equals(ResultState.Error))
    {
        ScreenHelper.SaveScreenshot(TakeScreenshot());
    }
}
```

## Demo Report

You can view [Demo report](http://ghpreporter.github.io/report/) on our [site](http://ghpreporter.github.io/)

## View report locally

Please read [Core instructions](https://github.com/GHPReporter/Ghpr.Core#view-report-locally) or [this comment](https://github.com/GHPReporter/Ghpr.NUnit/issues/16#issuecomment-291445978) about opening report in Chrome

## Contributing

Anyone contributing is welcome. Write [issues](https://github.com/GHPReporter/Ghpr.NUnit/issues), create [pull requests](https://github.com/GHPReporter/Ghpr.NUnit/pulls).

# Release notes

You can find it [here](https://github.com/GHPReporter/Ghpr.Core/blob/master/RELEASE_NOTES.md) for all packages.


## License
[![FOSSA Status](https://app.fossa.io/api/projects/git%2Bgithub.com%2FGHPReporter%2FGhpr.NUnit.svg?type=large)](https://app.fossa.io/projects/git%2Bgithub.com%2FGHPReporter%2FGhpr.NUnit?ref=badge_large)
