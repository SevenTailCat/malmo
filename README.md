# Malmö #
（本文翻译仅供参考，若有偏差，不代表原作者意思。欢迎大家前来帮助这个英语渣还想推广自己喜欢平台的傻孩子。欢迎投稿B站视频教程。）  
原文：[通道-》](https://github.com/microsoft/malmo)  
Malmö项目是一个建立在Minecraft之上的人工智能实验和研究平台。我们的目标是激发新一代研究，以应对这一独特环境带来的新的挑战性问题。

[![Join the chat at https://gitter.im/Microsoft/malmo](https://badges.gitter.im/Microsoft/malmo.svg)](https://gitter.im/Microsoft/malmo?utm_source=badge&utm_medium=badge&utm_campaign=pr-badge&utm_content=badge) [![Build Status](https://travis-ci.org/Microsoft/malmo.svg?branch=master)](https://travis-ci.org/Microsoft/malmo) [![license](https://img.shields.io/github/license/mashape/apistatus.svg?maxAge=2592000)](https://github.com/Microsoft/malmo/blob/master/LICENSE.txt)
----
    
## 开始吧 ##

### *** NEW  *** ###

MamloEnv implements an Open AI "gym"-like environment directly in Python (one to one in a side-car like pattern with Java Minecraft). If you only need this functionallity or are interested in trying it out then please see [MalmoEnv](https://github.com/Microsoft/malmo/tree/master/MalmoEnv). Otherwise either install the "Malmo native wheel" (if available for your platform) or a binary release (more below). The build has been simplified with less required dependencies so building Malmo yourself is always an option!

优点:
    
1. 没有本地代码 - 您无需构建或安装平台相关代码。
2. 用于执行任务的单个网络连接。没有动态端口意味着它对虚拟化。
3. 一种更简单的多代理协调协议。一个Minecraft客户端实例，一个端口用于启动任务。
4. Less impedance miss-match with the gym api.

缺点:

1. 不支持现有的Marlo示例 (因为API不同了)。 Marlo envs应该使用这个[端口](https://github.com/AndKram/marLo/tree/malmoenv).
2. API更受限制（例如选择视频选项） - 可以直接编辑任务xml.

注意: The Marlo competition (for now) uses the original Malmo "AgentHost" api with it's native code implementation. 

### Malmo as a native Python wheel ###

On common Windows, MacOSX and Linux variants it is possible to use ```pip3 install malmo``` to install Malmo as a python with native code package: [Pip install for Malmo](https://github.com/Microsoft/malmo/blob/master/scripts/python-wheel/README.md). Once installed, the malmo Python module can be used to download source and examples and start up Minecraft with the Malmo game mod. 

Alternatively, a pre-built version of Malmo can be installed as follows:

1. [Download the latest *pre-built* version, for Windows, Linux or MacOSX.](https://github.com/Microsoft/malmo/releases)   
      NOTE: This is _not_ the same as downloading a zip of the source from Github. _Doing this **will not work** unless you are planning to build the source code yourself (which is a lengthier process). If you get errors along the lines of "`ImportError: No module named MalmoPython`" it will probably be because you have made this mistake._

2. Install the dependencies for your OS: [Windows](doc/install_windows.md), [Linux](doc/install_linux.md), [MacOSX](doc/install_macosx.md).

3. Launch Minecraft with our Mod installed. Instructions below.

4. Launch one of our sample agents, as Python, C#, C++ or Java. Instructions below.

5. Follow the [Tutorial](https://github.com/Microsoft/malmo/blob/master/Malmo/samples/Python_examples/Tutorial.pdf) 

6. Explore the [Documentation](http://microsoft.github.io/malmo/). This is also available in the readme.html in the release zip.

7. Read the [Blog](http://microsoft.github.io/malmo/blog) for more information.

If you want to build from source then see the build instructions for your OS: [Windows](doc/build_windows.md), [Linux](doc/build_linux.md), [MacOSX](doc/build_macosx.md).

----

## Problems: ##

We're building up a [Troubleshooting](https://github.com/Microsoft/malmo/wiki/Troubleshooting) page of the wiki for frequently encountered situations. If that doesn't work then please ask a question on our [chat page](https://gitter.im/Microsoft/malmo) or open a [new issue](https://github.com/Microsoft/malmo/issues/new).

----

## Launching Minecraft with our Mod: ##

Minecraft需要有可视化窗口或者OpenGL，所以运行此项目的机器需要有可视化桌面。

在解压这个项目的文件夹里执行:

`cd Minecraft`  
`launchClient` (On Windows)  
`./launchClient.sh` (On Linux or MacOSX)

或使用`launchClient -port 10001`来以一个特殊的端口启动Minecraft。

在 Linux 或者 MacOSX 上: `./launchClient.sh -port 10001`

*NB: If you run this from a terminal, the bottom line will say something like "Building 95%" - ignore this - don't wait for 100%! As long as a Minecraft game window has opened and is displaying the main menu, you are good to go.*

By default the Mod chooses port 10000 if available, and will search upwards for a free port if not, up to 11000.
The port chosen is shown in the Mod config page.

To change the port while the Mod is running, use the `portOverride` setting in the Mod config page.

The Mod and the agents use other ports internally, and will find free ones in the range 10000-11000 so if administering
a machine for network use these TCP ports should be open.

----

## 启动一个代理: ##

#### 运行一个Python代理: ####

```
cd Python_Examples
python3 run_mission.py
``` 

#### 运行一个C++代理: ####

`cd Cpp_Examples`

运行一个预先构建的样本:

`run_mission` (on Windows)  
`./run_mission` (on Linux or MacOSX)

构建一个你自己的样例:

`cmake .`  
`cmake --build .`  
`./run_mission` (on Linux or MacOSX)  
`Debug\run_mission.exe` (on Windows)

#### 运行一个C#代理: ####

To run the pre-built sample (on Windows):

`cd CSharp_Examples`  
`CSharpExamples_RunMission.exe`

To build the sample yourself, open CSharp_Examples/RunMission.csproj in Visual Studio.

Or from the command-line:

`cd CSharp_Examples`

然后, on Windows:  
```
msbuild RunMission.csproj /p:Platform=x64
bin\x64\Debug\CSharpExamples_RunMission.exe
```

#### 启动一个JAVA代理: ####

`cd Java_Examples`  
`java -cp MalmoJavaJar.jar:JavaExamples_run_mission.jar -Djava.library.path=. JavaExamples_run_mission` (on Linux or MacOSX)  
`java -cp MalmoJavaJar.jar;JavaExamples_run_mission.jar -Djava.library.path=. JavaExamples_run_mission` (on Windows)

#### 启动一个Atari代理: (Linux only) ####

```
cd Python_Examples
python3 ALE_HAC.py
```

----

# Citations #

Please cite Malmo as:

Johnson M., Hofmann K., Hutton T., Bignell D. (2016) [_The Malmo Platform for Artificial Intelligence Experimentation._](http://www.ijcai.org/Proceedings/16/Papers/643.pdf) [Proc. 25th International Joint Conference on Artificial Intelligence](http://www.ijcai.org/Proceedings/2016), Ed. Kambhampati S., p. 4246. AAAI Press, Palo Alto, California USA. https://github.com/Microsoft/malmo

----

# Code of Conduct #

This project has adopted the [Microsoft Open Source Code of Conduct](https://opensource.microsoft.com/codeofconduct/). For more information see the [Code of Conduct FAQ](https://opensource.microsoft.com/codeofconduct/faq/) or contact [opencode@microsoft.com](mailto:opencode@microsoft.com) with any additional questions or comments.
