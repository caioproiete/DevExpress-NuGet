# DevExpress-NuGet

NuGet Packages for the DevExpress .NET Components - [http://www.devexpress.com](http://www.devexpress.com).


## Introduction

> Here are unofficial NuGet specification files (nuspec) that I've created in order to generate NuGet packages for the .NET components developed by [DevExpress](http://www.devexpress.com).

> [If DevExpress ever authorizes me to publicly distribute their assemblies in NuGet packages](https://www.devexpress.com/support/center/Question/Details/S139898), I'll be happy to publish them on the [NuGet.org](http://nuget.org) feed. In the meantime, if you are a DevExpress licensed user, feel free to use these nuspec files to generate the packages and host on your own private/company feed.


### Call To Action
If you too think that [DevExpress](http://www.devexpress.com) should provide us with official NuGet packages for their .NET components, send an e-mail to **<management@devexpress.com>**, or **[post a comment on their forum](https://www.devexpress.com/support/center/Question/Details/S139898)**.  


### Disclaimer from DevExpress
*Please note that according to DevExpress [EULA](https://www.devexpress.com/Support/EULAs/NetComponents.xml), every person working with DevExpress components should have a separate license. To properly register our components on your machine, use the DevExpress installer as described in the [How to activate my DevExpress license article](https://www.devexpress.com/Support/Center/Question/Details/KA18604). Working with DevExpress components using libraries got from NuGet without proper registration may result in licensing violation*.


## Packaging Strategy

I've created one NuGet package specification for every single assembly included in the DevExpress .NET controls, which in turn can be used to generate a NuGet package.

For example, the file `nuspec\Unofficial.DevExpress.Xpf.Ribbon.nuspec` is the corresponding NuGet specification for the assembly `DevExpress.Xpf.Ribbon.v17.1.dll`.


### Dependencies between NuGet packages

The dependencies between NuGet packages are created based on direct references to other DevExpress assemblies.

For example, if the assembly `DevExpress.Xpf.Ribbon.v17.1.dll` directly references `DevExpress.Data.v17.1.dll`, `DevExpress.Mvvm.v17.1.dll` and `DevExpress.Xpf.Core.v17.1.dll`, the NuGet specification will declare a dependency to each of the three NuGet packages corresponding to these assemblies:

    <?xml version="1.0"?>
    <package xmlns="http://schemas.microsoft.com/packaging/2012/06/nuspec.xsd">
      <metadata>
        <id>Unofficial.DevExpress.Xpf.Ribbon</id>
        <version>17.1.4.0</version>
        <!-- ... (omitted for brevity) -->
        <dependencies>
          <group targetFramework=".NETFramework4.0">
            <dependency id="Unofficial.DevExpress.Xpf.Core" version="17.1.4.0" />
            <dependency id="Unofficial.DevExpress.Data" version="17.1.4.0" />
            <dependency id="Unofficial.DevExpress.Mvvm" version="17.1.4.0" />
          </group>
       </dependencies>
      </metadata>
      <files>
        <file src="lib\DevExpress.Xpf.Ribbon.v17.1.dll" target="lib\net40" />
        <file src="lib\DevExpress.Xpf.Ribbon.v17.1.xml" target="lib\net40" />
      </files>
    </package>


## Folder Structure

- **src**
  - **lib**
      - This is where you put the DevExpress assemblies before you generate the NuGet packages. You will typically copy the contents of the folder `C:\Program Files (x86)\DevExpress 17.1\Components\Bin\Framework` and paste it here, including sub-folders;
  - **nupkg**
      - This is the output folder where the NuGet packages will be generated; 
  - **nuspec**
      - This is where all the NuGet specification files are; 
  - **tools**
      - This contains a simple Powershell script used by the NuGet packages related to assemblies that are only needed for design-time (i.e. assemblies in `lib\Design`). This script runs during the installation of these packages only to set the `CopyLocal` attribute of these assemblies to `false`, given that they are not meant to be deployed with the application. 


## How to generate the NuGet packages

To generate all NuGet packages, just run the powershell file `src\nuget-pack.ps1`, or if you prefer to manually generate specific packages, just use the `nuget.exe` command line utility. For example:

    nuget.exe pack ".\src\nuspec\Unofficial.DevExpress.Data.nuspec" -BasePath ".\src" -OutputDirectory ".\src\nupkg"


## Known issues / Things to do

- The nuspec files are currently being generated by a quick-and-dirty C# app that I wrote, which is not ready to be shared with the world :). Once I get some free time to rewrite it (or make it a Powershell script), I'll definitely publish it here;

- The language-specific assemblies for German, Spanish, Japanese, and Russian are currently not being included in any of the NuGet packages;

- I use a very specific set of components, which means that there are a number of NuGet packages that I have not extensively tested. You've been warned;

- Instead of generating a NuGet package for every assembly, the script could analyze the dependency chain and build clusters when possible - I'm not sure if it is worth the effort, though. I'm interested in hearing your opinion.

Please [report any issues](https://github.com/CaioProiete/DevExpress-NuGet/issues) you find and I'll try to fix as soon I can, and **remember you can always send a pull-request** ;).


## Release History
 * **v17.1.4.0** - 2017-08-24
   - Contains NuGet specs for the DevExpress Components 17.1.4 released on June 29, 2017

 * **v17.1.3.0** - 2017-05-26
   - Contains NuGet specs for the DevExpress Components 17.1.3 released on May 17, 2017

 * **v16.2.7.0** - 2017-05-25
   - Contains NuGet specs for the DevExpress Components 16.2.7 released on May 24, 2017

   * **v16.2.6.0** - 2017-05-25
   - Contains NuGet specs for the DevExpress Components 16.2.6 released on March 29, 2017

 * **v16.2.5.0** - 2017-03-06
   - Contains NuGet specs for the DevExpress Components 16.2.5 released on February 28, 2017

 * **v16.2.4.0** - 2017-03-05
   - Contains NuGet specs for the DevExpress Components 16.2.4 released on January 18, 2017

 * **v16.2.3.0** - 2017-01-11
   - Contains NuGet specs for the DevExpress Components 16.2.3 released on December 14, 2016

 * **v16.1.8.0** - 2016-11-19
   - Contains NuGet specs for the DevExpress Components 16.1.8 released on November 16, 2016

 * **v16.1.7.0** - 2016-10-13
   - Contains NuGet specs for the DevExpress Components 16.1.7 released on October 13, 2016

 * **v16.1.6.0** - 2016-09-16
   - Contains NuGet specs for the DevExpress Components 16.1.6 released on September 08, 2016

 * **v16.1.5.0** - 2016-08-07
   - Contains NuGet specs for the DevExpress Components 16.1.5 released on August 02, 2016

 * **v16.1.4.0** - 2016-07-02
   - Contains NuGet specs for the DevExpress Components 16.1.4 released on June 22, 2016

 * **v15.2.11.0** - 2016-07-02
   - Contains NuGet specs for the DevExpress Components 15.2.11 released on June 22, 2016

 * **v15.2.10.0** - 2016-04-26
   - Contains NuGet specs for the DevExpress Components 15.2.10 released on June 01, 2016

 * **v15.2.9.0** - 2016-04-26
   - Contains NuGet specs for the DevExpress Components 15.2.9 released on April 07, 2016

 * **v15.2.7.0** - 2016-03-07
   - Contains NuGet specs for the DevExpress Components 15.2.7 released on March 07, 2016

 * **v15.2.6.0** - 2016-03-03
   - Contains NuGet specs for the DevExpress Components 15.2.6 released on March 02, 2016

 * **v15.2.5.0** - 2016-02-20
   - Contains NuGet specs for the DevExpress Components 15.2.5 released on February 01, 2016

 * **v15.2.4.0** - 2015-12-09
   - Contains NuGet specs for the DevExpress Components 15.2.4 released on December 09, 2015

 * **v15.2.3.0** - 2015-12-09
   - Contains NuGet specs for the DevExpress Components 15.2.3 released on December 02, 2015

 * **v15.1.8.0** - 2015-11-16
   - Contains NuGet specs for the DevExpress Components 15.1.8 released on November 12, 2015

 * **v15.1.7.0** - 2015-09-25
   - Contains NuGet specs for the DevExpress Components 15.1.7 released on September 23, 2015

 * **v15.1.6.0** - 2015-09-15
   - Contains NuGet specs for the DevExpress Components 15.1.6 released on August 24, 2015

 * **v15.1.5.0** - 2015-09-15
   - Contains NuGet specs for the DevExpress Components 15.1.5 released on July 20, 2015

 * **v15.1.4.0** - 2015-06-29
   - Contains NuGet specs for the DevExpress Components 15.1.4 released on June 23, 2015

 * **v15.1.3.0** - 2015-06-03
   - Contains NuGet specs for the DevExpress Components 15.1.3 released on June 03, 2015

 * **v14.2.7.0** - 2015-04-30
   - Contains NuGet specs for the DevExpress Components 14.2.7 released on April 22, 2015

 * **v14.2.6.0** - 2015-03-18
   - Contains NuGet specs for the DevExpress Components 14.2.6 released on March 18, 2015

 * **v14.2.5.0** - 2015-02-20
   - Contains NuGet specs for the DevExpress Components 14.2.5 released on February 18, 2015

 * **v14.2.4.0** - 2015-02-08
   - Contains NuGet specs for the DevExpress Components 14.2.4 released on January 19, 2015

 * **v14.2.3.0** - 2015-02-08
   - Contains NuGet specs for the DevExpress Components 14.2.3 released on December 04, 2014

 * **v14.1.9.0** - 2015-02-08
   - Contains NuGet specs for the DevExpress Components 14.1.9 released on January 20, 2015

 * **v14.1.8.0** - 2015-02-08
   - Contains NuGet specs for the DevExpress Components 14.1.8 released on November 06, 2014

 * **v14.1.7.0** - 2014-10-22
   - Contains NuGet specs for the DevExpress Components 14.1.7 released on September 24, 2014

## License   
Copyright 2014-2017 Caio Proiete

Licensed under the Apache License, Version 2.0 (the "License");
you may not use this file except in compliance with the License.
You may obtain a copy of the License at

[http://www.apache.org/licenses/LICENSE-2.0](http://www.apache.org/licenses/LICENSE-2.0)

Unless required by applicable law or agreed to in writing, software
distributed under the License is distributed on an "AS IS" BASIS,
WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
See the License for the specific language governing permissions and
limitations under the License.

---

The DevExpress components and trademark are Copyright (C) 2000-2017 Developer Express Inc. and their end-user license agreement is available at [https://www.devexpress.com/Support/EULAs/NetComponents.xml](https://www.devexpress.com/Support/EULAs/NetComponents.xml).
