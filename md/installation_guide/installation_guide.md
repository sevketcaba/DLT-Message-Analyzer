[**Go to the previous page**](../../README.md)

----

# Installation guide

- Clone the dlt-viewer project from the **[following location]( https://github.com/GENIVI/dlt-viewer )**.

> git clone git@github.com:GENIVI/dlt-viewer.git

----

> **Note!**
> 
> Currently plugin can be built against the v2.24.0 release.
>
> The build under the earlier versions, down to the the v2.19.0 is also supported. But you will need to use the compatibility mode. Such an option is described below later on down this page. Search for the "PLUGIN_INTERFACE_VERSION" keyword.
>
> Make sure, that you've checked out the compatible base-line and used required build options. 

----

- Clone DLT-Message-Analyzer's git repository ( the one which you are observing right now ) as a nested one inside the **"./dlt-viewer/plugin"** location.
Your target path to the plugin should look like **"./dlt-viewer/plugin/DLT-Message-Analyzer"**:

>```
> cd ./dlt-viewer/plugin
> git clone git@github.com:svlad-90/DLT-Message-Analyzer.git
> ```

![Screenshot of DLT Message Analyzer plugin location inside the dlt-viewer project](./installation_guide_plugin_location.png)

----

- modify also the **"./dlt-viewer/plugin/CMakeLists.txt"**:

<pre>add_subdirectory(DLT-Message-Analyzer/dltmessageanalyzerplugin/src)</pre>

![Screenshot of plugin.pro cmakelists.txt modification](./installation_guide_cmakelists_modification.png)

----

### Linux console build

- Open console in the "./dlt-viewer" folder:

![Screenshot of console](./installation_guide_console.png)

- Run the following set of commands in it:

<pre>mkdir build
cd build
cmake ..
make -j4
</pre>

----

### Qt Creator IDE set up

- Specify the location of CMake in QT Creator:

![Screenshot of "Specify CMake location" menu in QT Creator](./installation_guide_cmake_location.png)

Afterward, open the dlt-viewer's CMake project, which is located in the root of the dlt-viewer repo:

![Screenshot of "Open project" context menu in the Qt Creator](./installation_guide_open_project_menu.png)

![Screenshot of project file selection in the Qt Creator](./installation_guide_select_project.png)

> **Important note for Windows compilation!**
>
> In addition to the already mentioned steps, for Windows you will need to modify the dlt-viewer's root CMakeLists.txt.
> Open the same file, which is mentioned in previous screenshot in the text editor, and add the following 2 lines:
> 
> if(NOT CMAKE_CXX_COMPILER_ID MATCHES "MSVC") # new line
>
> SET(CMAKE_C_FLAGS  "${CMAKE_C_FLAGS} -std=gnu99")
>
> add_definitions( "-Wall" )
>
> add_definitions( "-Wextra" )
>
> add_definitions( "-Wno-variadic-macros" )
>
> add_definitions( "-pedantic" )
>
> add_definitions( "-Wno-strict-aliasing" )
>
> endif()                                      # new line
>
> That will allow you to build plugin with CMake + MSVC + jom, avoiding compilation errors related to misusage of the GCC compiler flags.
>
> This issue is already raised in dlt-viewer's repo:
> https://github.com/GENIVI/dlt-viewer/issues/113
>
> Hopefully it will be fixed soon. Afterward, this step will become obsolete and will be removed from this guide.

----

> **Important note for Linux compilation!**
>
> On Linux the compilation might fail, if you do not have installed uuid-dev package.
> That one is used by antlr, which is used by the DLT-Message-Analyzer.
> 
> Thus, please, install it before making attempt to build the project:
> sudo DEBIAN_FRONTEND=noninteractive apt-get -yq install uuid-dev

----

## qmake *.pro based build

Such a build option was dropped.
DLT-Message-Analyzer has started to use antlr generator, which has only CMake support.
Thus the decision was finally made to support ONLY CMake builds for all supported platforms.
As of now, they are Linux and Windows.

----

### Linux and Windows QT creator build

- Select build type:

![Screenshot of a selection of the build type in the Qt Creator](./installation_guide_select_build_type.png)

- Clear CMake configuration:

![Screenshot of "Clear CMake configuration" option in the Qt Creator](./installation_guide_clear_cmake_configuration.png)

- Run CMake:

![Screenshot of "Run CMake" option in the Qt Creator](./installation_guide_run_cmake.png)

- Press build button:

![Screenshot of build button in QT Creator](./installation_guide_build.png)

----

### Run dlt-viewer and enable the plugin

- Proceed to the build's artifacts folder and run the dlt-viewer. It should already include and load the dynamic library of the DLT-Message-Analyzer plugin
- Enable and show the DLT-Message-Analyzer plugin:

![Screenshot of enabling the plugin](./installation_guide_enable_plugin.png)

----

### Build dependencies and settings

#### Build dependencies

> **Note!** 
> 
> For Linux build you will need to install the uuid-dev package. 
> It is required to build the antlr4 runtime library.
> To do that you can use the following commands:
>
> ```
> sudo apt update
> sudo apt-get install uuid-dev
> ```
>

----

> **Note!** 
> 
> If you want to have a compatible build with PLUGIN_INTERFACE_VERSION "1.0.0", enable the following define in the 
> **./dlt-viewer/plugin/ DLT-Message-Analyzer/ dltmessageanalyzerplugin/ src/ CMakeLists.txt**:
> 
> ![Screenshot enable 1.0.0 compatibility define in CMakeLists.txt](./installation_guide_enable_define_cmake.png)

----

> **Note!** 
> 
> To run dlt-viewer and DLT_Message-Analyzer, which are built with msvc, you will need to install the corresponding version of the Visual C++ Redistributable package.
> 
> Here is a link, by which you can find such packages for 2015, 2017, 2019 versions of the msvc - https://support.microsoft.com/en-us/help/2977003/the-latest-supported-visual-c-downloads
>
> In case if the link will become irrelevant, just google for the "Visual C++ Redistributable package" keyword in your browser.
> 

----

#### Build settings

> **Note!** 
> 
> If build fails due to missing qt5serialport5 package, perform the following commands:
>```
> sudo apt-get install libqt5serialport5
> sudo apt-get install libqt5serialport5-dev
>```
> for Qt6 [__qtserialport__](https://doc.qt.io/qt-6/qtserialport-index.html) module needs to be installed.

----

[**Go to the previous page**](../../README.md)
