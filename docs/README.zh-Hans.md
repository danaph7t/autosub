# Autosub

<escape><a href="https://travis-ci.org/BingLingGroup/autosub"><img src="https://travis-ci.org/BingLingGroup/autosub.svg?branch=alpha"></img></a> <a href="https://app.fossa.io/projects/git%2Bgithub.com%2FBingLingGroup%2Fautosub"><img src="https://app.fossa.io/api/projects/git%2Bgithub.com%2FBingLingGroup%2Fautosub.svg?type=shield"></img></a> <a href="https://t.me/autosubs"><img src="https://img.shields.io/badge/Channel-Telegram-blue"></img></a></escape>

[English](../README.md)

本仓库不同于[原仓库](https://github.com/agermanidis/autosub)。

本仓库由多人修改过，请查看[更新日志](CHANGELOG.zh-Hans.md)。

<escape><img src="../docs/icon/autosub.png" width="128px"></escape>

[autosub图标](docs/icon/autosub.svg)由冰灵制作。

软件: [inkscape](https://inkscape.org/zh/)

字体: [思源黑体](https://github.com/adobe-fonts/source-han-sans) ([SIL](https://github.com/adobe-fonts/source-han-sans/blob/master/LICENSE.txt))

颜色: [Solarized](https://en.wikipedia.org/wiki/Solarized_(color_scheme)#Colors)

### 目录

1. [介绍](#介绍)
2. [证书](#证书)
3. [依赖](#依赖)
4. [下载和安装](#下载和安装)
   - 4.1 [分支](#分支)
   - 4.2 [在Ubuntu上安装](#在Ubuntu上安装)
   - 4.3 [在Windows上安装](#在Windows上安装)
5. [工作流程](#工作流程)
   - 5.1 [输入](#输入)
   - 5.2 [分割](#分割)
   - 5.3 [语音转文字/翻译API请求](#语音转文字翻译api请求)
   - 5.4 [语音转文字/翻译语言支持](#语音转文字翻译语言支持)
   - 5.5 [输出](#输出)
6. [使用方法](#使用方法)
   - 6.1 [典型用法](#典型用法)
     - 6.1.1 [音频预处理](#音频预处理)
     - 6.1.2 [检测语音区域](#检测语音区域)
     - 6.1.3 [分割音频](#分割音频)
     - 6.1.4 [语音转录为字幕](#语音转录为字幕)
     - 6.1.5 [翻译字幕](#翻译字幕)
   - 6.2 [选项](#选项)
   - 6.3 [国际化](#国际化)
7. [常见问题](#常见问题)
   - 7.1 [其他API的支持](#其他API的支持)
   - 7.2 [批量处理](#批量处理)
   - 7.3 [代理支持](#代理支持)
8. [问题反馈](#问题反馈)
9. [构建](#构建)

点击上箭头以返回目录。

### 介绍

Autosub是一个字幕自动生成工具。它能使用Auditok来自动检测语音区域，通过ffmpeg根据语音区域来切割音频，通过[Google-Speech-v2](https://github.com/gillesdemey/google-speech-v2)([Chrome-Web-Speech-api](https://github.com/agermanidis/autosub/issues/1))将语音转为文字，以及通过py-googletrans将字幕文本翻译。目前暂时不支持最新的Google Cloud API。

上方提到的一些新功能仅在autosub-0.5.0a(0.5.0-alpha)后提供。PyPI或者原仓库中的代码并没有这些功能。

### 证书

这个仓库和[原仓库](https://github.com/agermanidis/autosub)的证书不一样。

[GPLv3](../LICENSE)

[![FOSSA Status](https://app.fossa.io/api/projects/git%2Bgithub.com%2FBingLingGroup%2Fautosub.svg?type=large)](https://app.fossa.io/projects/git%2Bgithub.com%2FBingLingGroup%2Fautosub)

### 依赖

Autosub依赖于这些第三方的软件或者Python的site-packages。非常感谢以下这些项目的工作。

- [ffmpeg](https://ffmpeg.org/)
- [auditok](https://github.com/amsehili/auditok)
- [pysubs2](https://github.com/tkarabela/pysubs2)
- [py-googletrans](https://github.com/ssut/py-googletrans)
- [langcodes](https://github.com/LuminosoInsight/langcodes)
- [ffmpeg-normalize](https://github.com/slhck/ffmpeg-normalize)

其他的依赖项目参见：[requirements.txt](requirements.txt)。

以及如何安装这些依赖，参见[下载和安装](#下载和安装)。

<escape><a href = "#目录">&nbsp;↑&nbsp;</a></escape>

### 下载与安装

除去PyPI版本的代码和原仓库的一致，其他的安装方式均包含非原仓库的代码。

在autosub-0.4.0之后，所有的代码都是Python3和Python2.7兼容的。所以后面的安装指令中的Python版本你可以随便改。

至于依赖的安装，如果你是通过pip来安装的autosub，那么ffmpeg和ffmpeg-normalize不会被一块儿安装，不像site-packages那样列在`setup.py`或者`requirements.txt`里面自动安装了。你需要分别安装它们。当然安装是可选的，如果你只是翻译字幕，不需要安装这两个软件。

至于git的安装，如果你不想通过pip的[VCS](https://pip.pypa.io/en/stable/reference/pip_install/#vcs-support)支持来安装python包或者只是不想碰git的环境变量这些东西，你可以手动点击clone and download来下载源码并在[本地](https://pip.pypa.io/en/stable/reference/pip_install/#description)进行安装。指令如下。

```batch
cd 有源码的目录
pip install .
```

因为autosub的PyPI版本是被原repo的拥有者所维护的，我无法修改它，也无法上传一个有着相同名字的项目。也许等到这个项目变得更加稳定的时候，我会重命名并复制这个仓库，然后再把它传到PyPI去。

#### 分支

[alpha分支](https://github.com/BingLingGroup/autosub/tree/alpha)

- 包括大量在[原仓库代码](https://github.com/agermanidis/autosub)基础上的改动。详见[更新日志](CHANGELOG.zh-Hans.md)。代码仅在发布alpha版本时更新，相对来讲会比dev分支稳定。

[origin分支](https://github.com/BingLingGroup/autosub/tree/origin)

- 不包含[alpha分支](https://github.com/BingLingGroup/autosub/tree/alpha)中添加的新功能，仅包含最少的改动来让程序能在Windows上正常运行，可以看作只是[原仓库](https://github.com/agermanidis/autosub)的版本的修复版，而不会遇到各种各样的问题。现在不再维护。

[dev分支](https://github.com/BingLingGroup/autosub/tree/dev)

- 开发中代码所在分支，如果没有问题，代码会在发布新版本时合并到alpha分支。
- 只被用来测试或者提出拉取请求。除非你知道自己在干什么，否则不要安装它们。

<escape><a href = "#目录">&nbsp;↑&nbsp;</a></escape>

#### 在Ubuntu上安装

第一行包含依赖的安装。

从`alpha`分支安装。（最新alpha发布版）

```bash
apt install ffmpeg python python-pip git -y
pip install git+https://github.com/BingLingGroup/autosub.git@alpha ffmpeg-normalize
```

从`origin`分支安装。（autosub-0.4.0a）

```bash
apt install ffmpeg python python-pip git -y
pip install git+https://github.com/BingLingGroup/autosub.git@origin
```

从PyPI安装。（autosub-0.3.12）

```bash
apt install ffmpeg python python-pip -y
pip install autosub
```

<escape><a href = "#目录">&nbsp;↑&nbsp;</a></escape>

#### 在Windows上安装

你可以直接去[发布页](https://github.com/BingLingGroup/autosub/releases)下载Windows的最新发布版。包内自带懒人批处理。你可以使用Notepad++对其进行手动修改。或者把含有exe的目录放到系统环境变量里，这样你就可以在别的目录也使用autosub了，前提是那个目录没有权限限制。

建议：`Shift - 右键`是打开当前目录Powershell的快捷键。Powershell打开当前目录的exe需要输入这样的格式`.\autosub`。

- 发布包里没有pyinstaller后缀的是Nuitka编译的。它比pyinstaller的版本快，因为它是编译的，不同于pyinstaller只是把程序进行了打包。
- ffmpeg和ffmpeg-normalize也在发布包内。原本ffmpeg-normalize没有独立运行的版本。这个独立运行的ffmpeg-normalize是另外构建的。代码在[这里]((https://github.com/BingLingGroup/ffmpeg-normalize))。
- 如果在使用发布包时遇到任何问题，或者包的大小太大或者遇到了什么烦人的事情，你依然可以采用下方所说的通过pip的方法进行安装。

或者通过choco来安装Python环境（如果你还没有），然后安装这个包。

推荐在windows上使用[chocolatey](https://chocolatey.org)来安装环境和依赖。

命令行安装choco的指令如下。（不是Powershell）

```batch
@"%SystemRoot%\System32\WindowsPowerShell\v1.0\powershell.exe" -NoProfile -InputFormat None -ExecutionPolicy Bypass -Command "iex ((New-Object System.Net.WebClient).DownloadString('https://chocolatey.org/install.ps1'))" && SET "PATH=%PATH%;%ALLUSERSPROFILE%\chocolatey\bin"
```

从`alpha`分支安装。（最新alpha发布版）

```batch
choco install git python2 curl ffmpeg -y
curl https://bootstrap.pypa.io/get-pip.py -o get-pip.py
python get-pip.py
pip install git+https://github.com/BingLingGroup/autosub.git@alpha ffmpeg-normalize
```

从`origin`分支安装。（autosub-0.4.0a）

```batch
choco install git python2 curl ffmpeg -y
curl https://bootstrap.pypa.io/get-pip.py -o get-pip.py
python get-pip.py
pip install git+https://github.com/BingLingGroup/autosub.git@origin
```

PyPI的版本（autosub-0.3.12）不推荐在windows上使用，因为它无法成功运行。查看[origin分支的更新日志](CHANGELOG.zh-Hans.md#040-alpha---2019-02-17)来了解详情。

<escape><a href = "#目录">&nbsp;↑&nbsp;</a></escape>

### 工作流程

#### 输入

一个视频/音频/字幕文件。

如果是一个视频或者音频文件，使用ffmpeg来将格式转换为[API支持的格式](https://github.com/gillesdemey/google-speech-v2#data)。当前提供给[Google-Speech-v2](https://github.com/gillesdemey/google-speech-v2)的默认格式是24bit/44100Hz/单声道flac。API只接受单声道文件，而非那个仓库里所说的那样。

你也可以使用自带的音频预处理功能。默认的[音频预处理指令](https://github.com/agermanidis/autosub/issues/40)同时依赖于ffmpeg和ffmpeg-normalize。这些命令包含三个子命令。[第一个](https://trac.ffmpeg.org/wiki/AudioChannelManipulation)是用来把双声道的音频转换为单声道的。[第二个](https://superuser.com/questions/733061/reduce-background-noise-and-optimize-the-speech-from-an-audio-clip-using-ffmpeg)是通过人声的频率范围来过滤噪音的。第三个则是正常化音频的音量来确保它的音量不是太大或者太小。如果你对默认指令的效果不满意，你也可以通过输入`-apc`选项来自行修改。

如果输入是字幕文件，同时你提供的参数适合，程序仅会将其通过py-googletrans来翻译。

#### 分割

因为语音转文字API只支持10到15秒这样的[短片段音频](https://github.com/gillesdemey/google-speech-v2#caveats)，我们需要将音频文件分割为若干包含语音的小片段。Autosub使用Auditok来检测语音区域。

或者使用外部文件提供的时间码来作为语音区域输入，支持pysubs2支持的文件格式，如`.ass`或者`.srt`。这样你就可以使用外部工具先制作时间轴然后让程序使用并得到精确度更高的识别结果。

#### 语音转文字/翻译API请求

使用Python的多进程库对API请求进行并行化处理，来加速转录速度。一个语音片段一次请求。识别速度主要取决于你网络的上传速度。

- 可能需要对字幕文件行进行手动后处理，某些行可能长度过长，导致无法被放在视频画面长度中的同一行。

在语音转文字之后，把字幕翻译成别的语言。将多行文本融合为一块长文本然后送去请求。详见[issue #49](https://github.com/BingLingGroup/autosub/issues/49)。最后再把结果保存在本地。

<escape><a href = "#目录">&nbsp;↑&nbsp;</a></escape>

#### 语音转文字/翻译语言支持

语音转文字的语言代码和翻译的语言代码是不一样的，因为这俩API并不相同。当然啦，这些语言代码的格式是*谷歌化*的，和iso标准不一样，会导致用户使用时很迷惑。

为了解决这个问题，autosub使用[langcodes](https://github.com/LuminosoInsight/langcodes)来检测输入的语言代码并在语言代码清单中找到与其最匹配的一项来使用。默认并不会启用这个功能。需要在不同的阶段都启动这个功能，可以使用选项`-bm all`。

为了手动匹配或者查看本程序允许使用的语言代码，你可以通过输入参数`-lsc`/`--list-speech-to-text-codes`以及`-ltc`/`--list-translation-codes`来获得。或者你也可以打开[constants.py](../autosub/constants.py)来查看。

为了得到某个字幕文件第一行的语言，你可以使用`-dsl`选项去检测。

- 现在，如果autosub使用[Google-Speech-v2](https://github.com/gillesdemey/google-speech-v2)作为语音转文字的方法，它会允许发送不在`--list-speech-codes`清单中的语言代码，意味着在这种情况下程序不会终止运行。

- 尽管你可以输入任何你想输入的语言代码，需要指出的是如果你使用了不在清单上的语言代码但是API接受了，[Google-Speech-v2](https://github.com/gillesdemey/google-speech-v2)可能会按照你的IP地址机型个性化识别，而这是不受你控制的。这是一个已知的问题，我已经在原仓库申请了[拉取请求](https://github.com/agermanidis/autosub/pull/136)。

- 另外一方面，[py-googletrans](https://github.com/ssut/py-googletrans)更加严格。当它收到了一个不在它清单内的语言代码，它会直接抛出异常。当然这可以设计成一个抛出-捕获的代码块，并允许用户再次输入语言代码，不过我目前还没加入这个支持，所以不适合的翻译语言代码会终止程序运行，除非你使用前面提到的最佳匹配功能。

- 除了用户输入的部分，另外一个显著的更改是我将`-S`选项分为了两部分，一个是`-S`一个是`-SRC`。`-S`选项是给语音识别的语言代码使用的。`-SRC`则是给翻译源语言代码使用的。如果不输入`-SRC`的参数时，autosub会使用[langcodes](https://github.com/LuminosoInsight/langcodes)来匹配`-S`的参数来获得其在翻译支持的语言代码清单中的最佳匹配，尽管[py-googletrans](https://github.com/ssut/py-googletrans)可以自动检测翻译源语言。当然你可以手动配置`-SRC`选项。而`-D`还是给目标翻译语言使用的，和之前一样。

<escape><a href = "#目录">&nbsp;↑&nbsp;</a></escape>

#### 输出

目前支持以下这些输出格式。

```Python
OUTPUT_FORMAT = {
    'srt': 'SubRip',
    'ass': 'Advanced SubStation Alpha',
    'ssa': 'SubStation Alpha',
    'sub': 'MicroDVD Subtitle',
    'mpl2.txt': 'Similar to MicroDVD',
    'tmp': 'TMP Player Subtitle Format',
    'vtt': 'WebVTT',
    'json': 'json(Only times and text)',
    'ass.json': 'json(Complex ass content json)',
    'txt': 'Plain Text(Text or times)'
}
```

或者其他的字幕种类/输出模式，取决于你的需要。帮助中有更多的相关信息。

```Python
DEFAULT_MODE_SET = {
    'regions',
    'src',
    'dst',
    'bilingual'}
```

<escape><a href = "#目录">&nbsp;↑&nbsp;</a></escape>

### 使用方法

对于原版autosub的使用，可以参见这篇[简体中文使用指南](https://binglinggroup.github.io/archives/autosub安装使用指南(windows及ubuntu).html)。

对于alpha分支autosub的使用，可以参考以下典型用法。

#### 典型用法

<escape><div title="Typical usage" align="middle"><img src="workflow.zh-Hans.png"></div></escape>

##### 音频预处理

使用默认的[音频预处理](https://github.com/agermanidis/autosub/issues/40)。

仅音频预处理。

```
autosub -i 输入文件 -ap o
```

音频预处理只是处理过程中的一部分。

```
autosub -i 输入文件 -ap y ...(其他选项)
```

##### 检测语音区域

使用Auditok检测语音区域。

仅得到时间轴。

```
autosub -i 输入文件
```

得到时间轴只是处理过程中的一部分。

```
autosub -i 输入文件 -of regions ...(其他选项)
```

<escape><a href = "#目录">&nbsp;↑&nbsp;</a></escape>

##### 分割音频

根据语音区域得到音频片段。

根据自动语音区域检测，只获取音频片段。

```
autosub -i 输入文件 -ap s
```

根据外部语音区域输入，只获取音频片段。

```
autosub -i 输入文件 -ap s -er 时间轴字幕
```

获取音频片段只是处理过程中的一部分。

```
autosub -i 输入文件 -k ...(其他选项)
```

##### 语音转录为字幕

语音音频片段转为语音语言字幕。

仅得到语音语言字幕。

```
autosub -i 输入文件 -S 语言代码
```

得到语音语言字幕只是处理过程中的一部分。

```
autosub -i 输入文件 -S 语言代码 -of src ...(其他选项)
```

<escape><a href = "#目录">&nbsp;↑&nbsp;</a></escape>

##### 翻译字幕

将字幕翻译为别的语言。

从音频/视频文件翻译字幕。

```
autosub -i 输入文件 -S 语言代码 (-Src 语言代码) -D 语言代码
```

从字幕文件翻译字幕。

```
autosub -i 输入文件 -Src 语言代码 -D 语言代码
```

<escape><a href = "#目录">&nbsp;↑&nbsp;</a></escape>

#### 选项

帮助信息的完整列表。

```
$ autosub -h
usage:
用法：autosub [-i 路径] [选项]

为视频/音频/字幕文件自动生成字幕。

输入选项:
  控制输入的选项。

  -i 路径, --input 路径     用于生成字幕文件的视频/音频/字幕文件。如果输入文件是字幕文件，程序仅会对其进行翻译。（参数个数为1）
  -er 路径, --ext-regions 路径
                        提供外部语音区域（时间轴）的字幕文件。该字幕文件格式需要是pysubs2所支持的。使用后会替换掉默认的 自动寻
                        找语音区域（时间轴）的功能。（参数个数为1）
  -sty [路径], --styles [路径]
                        当输出格式为"ass"/"ssa"时有效。为你的字幕文件提供"ass"/"ssa"样式的字幕文件。如果不提供
                        参数，它会使用来自"-esr"/"--external-speech-
                        regions"选项提供的样式。更多信息详见"-sn"/"--styles-name"。（参数个数为0或1）
  -sn [样式名 [样式名 ...]], --styles-name [样式名 [样式名 ...]]
                        当输出格式为"ass"/"ssa"且"-sty"/"--styles"选项提供参数时有效。给输出字幕文件行提
                        供"ass"/"ssa"字幕的样式名。如果不提供该选项，字幕行会使用文件中的第一个样式名。如果参数个数为1，
                        字幕行会使用来自"-sty"/"--styles"的参数作为样式名。如果参数个数为2，源语言字幕行会使用第一
                        个参数作为样式名。目标语言行使用第二个。（参数个数为1或2）

语言选项:
  控制语言的选项。

  -S 语言代码, --speech-language 语言代码
                        用于语音识别的语言代码/语言标识符。推荐使用Google Cloud Speech的参考语言代码。错误的输入
                        不会终止程序。但是后果自负。参考：https://cloud.google.com/speech-to-
                        text/docs/languages（参数个数为1）（默认参数： None）
  -SRC 语言代码, --src-language 语言代码
                        用于翻译的源语言的语言代码/语言标识符。如果没有提供，会使用langcodes-
                        py2从列表里获取一个最佳匹配选项"-S"/"--speech-language"的语言代码。如果使用py-
                        googletrans作为翻译的方法，错误的输入会终止运行。（参数个数为1）（默认参数为None）
  -D 语言代码, --dst-language 语言代码
                        用于翻译的目标语言的语言代码/语言标识符。同样的注意参考选项"-Src"/"--src-
                        language"。（参数个数为1）（默认参数为None）
  -bm [模式 [模式 ...]], --best-match [模式 [模式 ...]]
                        在输入有误的情况下，允许langcodes-py2为输入获取一个最佳匹配的语言代码。仅在使用py-
                        googletrans和Google Speech V2时起作用。可选的模式：s, src, d,
                        all。"s"指"-S"/"--speech-language"。"src"指"-Src"/"--src-
                        language"。"d"指"-D"/"--dst-language"。（参数个数在1到3之间）
  -mns integer, --min-score integer
                        一个介于0和100之间的整数用于控制以下两个选项的匹配结果组，"-lsc"/"--list-speech-
                        codes"以及"-ltc"/"--list-translation-codes"或者在"-bm"/"--
                        best-
                        match"选项中的最佳匹配结果。结果会是一组“好的匹配”，其分数需要超过这个参数的值。（参数个数为1 ）

输出选项:
  控制输出的选项。

  -o 路径, --output 路径    输出字幕文件的路径。（默认值是"input"路径和适当的文件名后缀的结合）（参数个数为1）
  -F 格式, --format 格式    输出字幕的格式。如果没有提供该选项，使用"-o"/"--output"参数中的后缀。如果"-o"/"--
                        output"参数也没有提供扩展名，那么使用"srt"。在这种情况下，如果"-i"/"--
                        input"的参数是一个字幕文件，那么使用和字幕文件相同的扩展名。（参数个数为1）（默认参数为srt）
  -y, --yes             避免任何运行中的暂停和覆写文件的行为。如果参数有误，会直接停止程序。（参数个数为0）
  -of [种类 [种类 ...]], --output-files [种类 [种类 ...]]
                        输出更多的文件。可选种类：regions, src, dst, bilingual, all.（时间轴，源语
                        言字幕，目标语言字幕，双语字幕，所有）（参数个数在4和1之间）（默认参数为['dst']）
  -fps float, --sub-fps float
                        当输出格式为"sub"时有效。如果提供了该参数，它会取代原有的对输入文件的帧率检查。参考：https://p
                        ysubs2.readthedocs.io/en/latest/api-
                        reference.html#supported-input-output-formats（参数个数为1）
  -der, --drop-empty-regions
                        删除所有没有文本的空轴。（参数个数为0）

语音选项:
  控制语音转文字的选项。

  -gsv2 key, --gspeechv2 key
                        用于Google Speech V2 API的key。如果没有提供，会使用免费API
                        key。（参数个数为1）
  -mnc float, --min-confidence float
                        Google Speech V2 API用于识别可信度的回应参数。一个介于0和1之间的浮点数。可信度越高意味
                        着结果越好。输入这个参数会导致所有低于这个结果的识别结果被删除。参考：https://github.com/
                        BingLingGroup/google-
                        speech-v2#response（参数个数为1）（默认参数为0.0）
  -sc integer, --speech-concurrency integer
                        用于Google Speech V2 requests请求的并行数量。（参数个数为1）（默认参数为10）

py-googletrans选项:
  控制翻译的选项。同时也是默认的翻译方法。可能随时会被谷歌爸爸封。

  -slp 秒, --sleep-seconds 秒
                        （实验性）在两次翻译请求之间睡眠（暂停）的时间。（参数个数为1）（默认参数为5）
  -surl [URL [URL ...]], --service-urls [URL [URL ...]]
                        （实验性）自定义多个请求URL。参考：https://py-
                        googletrans.readthedocs.io/en/latest/（参数个数为1）
  -ua User-Agent header, --user-agent User-Agent header
                        （实验性）自定义用户代理（User-Agent）头部。同样的参考文档如上。（参数个数为1）

Google Speech V2选项:
  控制翻译的选项。（未被测试过）如果提供了API key，它会取代py-googletrans的翻译方法。

  -gtv2 key, --gtransv2 key
                        用于Google Translate V2的API key。如果没有提供，则使用免费的API也就是py-
                        googletrans。（参数个数为1）
  -lpt integer, --lines-per-trans integer
                        Google Translate V2请求的每行行数。（参数个数为1）（默认参数为15）
  -tc integer, --trans-concurrency integer
                        Google translate V2 API请求的并行数量。（参数个数为1）（默认参数为10）

网络选项:
  控制网络的选项。

  -hsa, --http-speech-api
                        将Google Speech V2 API的URL改为http类型。（参数个数为0）
  -hsp [URL], --https-proxy [URL]
                        通过设置环境变量的方式添加https代理。如果参数个数是0，使用const里的代理URL。（参数个数为0或1
                        ）（const为https://127.0.0.1:1080）
  -hp [URL], --http-proxy [URL]
                        通过设置环境变量的方式添加http代理。如果参数个数是0，使用const里的代理URL。（参数个数为0或1）
                        （const为http://127.0.0.1:1080）
  -pu 用户名, --proxy-username 用户名
                        设置代理用户名。（参数个数为1）
  -pp 密码, --proxy-password 密码
                        设置代理密码。（参数个数为1）

其他选项:
  控制其他东西的选项。

  -h, --help            显示autosub的帮助信息并退出。（参数个数为0）
  -V, --version         显示autosub的版本信息并退出。（参数个数为0）

音频处理选项:
  控制音频处理的选项。

  -ap [模式 [模式 ...]], --audio-process [模式 [模式 ...]]
                        控制音频处理的选项。如果没有提供选项，进行正常的格式转换工作。"y"：它会先预处理输入文件，如果成 功了，在语
                        音转文字之前不会对音频进行额外的处理。"o"：只会预处理输入音频。（"-k"/"--
                        keep"选项自动置为真）"s"：只会分割输入音频。（"-k"/"--keep"选项自动置为真）"n"：在语
                        音转文字的步骤之前，强制去除多余的格式检查或者转换工作。以下是用于处理音频的默认命令：ffmpeg
                        -hide_banner -i "{in_}" -af "asplit[a],aphasemeter=vid
                        eo=0,ametadata=select:key=lavfi.aphasemeter.phase:valu
                        e=-0.005:function=less,pan=1c|c0=c0,aresample=async=1:
                        first_pts=0,[a]amix" -ac 1 -f flac "{out_}" | ffmpeg
                        -hide_banner -i "{in_}" -af lowpass=3000,highpass=200
                        "{out_}" | ffmpeg-normalize -v "{in_}" -ar 44100 -ofmt
                        flac -c:a flac -pr -p -o "{out_}"（参考：https://github.co
                        m/stevenj/autosub/blob/master/scripts/subgen.sh
                        https://ffmpeg.org/ffmpeg-filters.html）（参数个数介于1和2之间）
  -k, --keep            将音频处理中产生的文件放在输出路径中。（参数个数为0）
  -apc [命令 [命令 ...]], --audio-process-cmd [命令 [命令 ...]]
                        这个参数会取代默认的音频处理命令。每行命令需要放在一个引号内。输入文件名写为{in_}。输出文件名写 为{ou
                        t_}。（参数个数大于1）
  -ac integer, --audio-concurrency integer
                        用于ffmpeg音频切割的进程并行数量。（参数个数为1）（默认参数为10）
  -acc 命令, --audio-conversion-cmd 命令
                        （实验性）这个参数会取代默认的音频转换命令。需要遵循原有的python参考关键词参数写法。以下是用于处理音频
                        的默认命令：ffmpeg -hide_banner -y -i "{in_}" -ac {channel}
                        -ar {sample_rate} "{out_}"（默认参数为1）
  -asc 命令, --audio-split-cmd 命令
                        （实验性）这个参数会取代默认的音频转换命令。相同的注意如上。默认：ffmpeg -ss {start} -t
                        {dura} -y -i "{in_}" -c copy -loglevel error
                        "{out_}"（参数个数为1）
  -asf 文件名后缀, --api-suffix 文件名后缀
                        （实验性）这个参数会取代默认的给API使用的音频文件后缀。（默认参数为.flac）
  -asr 采样率, --api-sample-rate 采样率
                        （实验性）这个参数会取代默认的给API使用的音频采样率（赫兹）。（参数个数为1）（默认参数为44100）
  -aac 声道数, --api-audio-channel 声道数
                        （实验性）这个参数会取代默认的给API使用的音频声道数量。（参数个数为1）（默认参数为1）

Auditok的选项:
  不使用外部语音区域控制时，用于控制Auditok的选项。

  -et 能量（相对值）, --energy-threshold 能量（相对值）
                        用于检测是否是语音区域的能量水平。参考：https://auditok.readthedocs.io/en/
                        latest/apitutorial.html#examples-using-real-audio-
                        data（参数个数为1）（默认参数为45）
  -mnrs 秒, --min-region-size 秒
                        最小语音区域大小。同样的参考文档如上。（参数个数为1）（默认参数为0.5）
  -mxrs 秒, --max-region-size 秒
                        最大音频区域大小。同样的参考文档如上。（参数个数为1）（默认参数为6.0）
  -mxcs 秒, --max-continuous-silence 秒
                        在一段有效的音频活动区域中可以容忍的最大（连续）安静区域。同样的参考文档如上。（参数个数为1）（ 默认参数为0
                        .3）
  -sml, --strict-min-length
                        参考：https://auditok.readthedocs.io/en/latest/core.html#
                        class-summary（参数个数为0）
  -dts, --drop-trailing-silence
                        参考：https://auditok.readthedocs.io/en/latest/core.html#
                        class-summary（参数个数为0）

列表选项:
  列出所有可选参数。

  -lf, --list-formats   列出所有可用的字幕文件格式。如果的你想要的格式不支持，请使用ffmpeg或者SubtitleEdit来对其进
                        行转换。如果输出格式是"sub"且输入文件是音频无法获取到视频帧率时，你需要提供fps选项指定帧率。（参数个
                        数为0）
  -lsc [语言代码], --list-speech-codes [语言代码]
                        列出所有推荐的"-S"/"--speech-language"Google Speech V2语言代码。如果
                        参数没有给出，列出全部语言代码。默认的“好的匹配”标准是匹配分数超过90分（匹配分数介于0和100之间）。参
                        考：https://tools.ietf.org/html/bcp47 https://github.com
                        /LuminosoInsight/langcodes/blob/master/langcodes/__ini
                        t__.py 语言代码范例：语言文字种类-（扩展语言文字种类）-变体（或方言）-使用区域-
                        变体（或方言）-扩展-私有（https://www.zhihu.com/question/21980689/
                        answer/93615123）（参数个数为0或1）
  -ltc [语言代码], --list-translation-codes [语言代码]
                        列出所有可用的"-SRC"/"--src-language"也就是py-googletrans可用的翻译用的
                        语言代码。否则会给出一个“好的匹配”的清单。同样的参考文档如上。（参数个数为0或1）
  -dsl 路径, --detect-sub-language 路径
                        使用py-googletrans去检测一个字幕文件的第一行的语言。并列出一个和该语言匹配的推荐Google
                        Speech V2语言代码清单（"-S"/"--speech-
                        language"选项所用到的）。参考：https://cloud.google.com/speech-
                        to-text/docs/languages（参数个数为1）（默认参数 None）

确保有空格的参数被引号包围。
默认参数指的是，
如果选项没有在命令行中提供时会使用的参数。
"参数个数"指的是如果提供了选项，
该选项所需要的参数个数。
作者: Anastasis Germanidis
Email: agermanidis@gmail.com
问题反馈: https://github.com/agermanidis/autosub
```

<escape><a href = "#目录">&nbsp;↑&nbsp;</a></escape>

#### 国际化

Autosub通过[GNU gettext](https://www.gnu.org/software/gettext/)支持多语言命令行界面。现在支持`zh_CN`和`en_US`。关于这种语言代码的格式可见[此文档](https://www.gnu.org/software/gettext/manual/gettext.html#Locale-Names)。程序会自动检测操作系统的语言，并选择其支持的语言。对于windows 10而言，只要修改`区域`-`区域格式`即可。

当然，autosub提供了不依靠操作系统语言来加载语言的方法。只要创建一个txt文件，去掉它的文件扩展名，命名为`locale`，在文件开头的位置输入语言代码，同时该文件放在运行autosub命令行的目录，autosub就会自动检测并读取这个文件里的语言代码，如果支持就会自动加载该语言。

如果你想把这个程序翻译成别的语言，首先安装gettext工具。然后你可以运行`python scripts/update_po_files.py lang_code`来创建你要翻译的语言文件。然后使用[POEditor](https://poeditor.com/)来编辑po文件。[update_po_files.py](../scripts/update_po_files.py)也可以自动合并位置信息到旧的po文件，并将po文件编译成程序使用的mo文件。所以如果代码改变时，你可以通过这个脚本，自动地将位置信息变化合并到翻译中。

<escape><a href = "#目录">&nbsp;↑&nbsp;</a></escape>

### 常见问题

#### 其他API的支持

[issue #11](https://github.com/BingLingGroup/autosub/issues/11), [issue 10](https://github.com/BingLingGroup/autosub/issues/10)

如果以后不忙了，我会考虑添加。当然欢迎各位的拉取请求。

#### 批量处理

[issue #13](https://github.com/BingLingGroup/autosub/issues/13)

同上。现在不会添加。你可以通过batch/powershell/bash来实现。

batch的例子：（在当前目录运行）

```batch
@echo off
set "in_format=*.mp4 *.m4a"

@echo on
for /f "delims=^" %%i in ('dir /b %in_format%') do (
    autosub -i "%%i" ...(other options)
)
@echo off
```

如果你想递归地遍历目录的子文件夹，将指令`'dir /b %in_format%'`替换为`'dir /b/s/a:-d %in_format%'`即可。[参考](https://docs.microsoft.com/en-us/windows-server/administration/windows-commands/dir)。

#### 代理支持

[issue #17](https://github.com/BingLingGroup/autosub/issues/17)

现在我只实现了和设置环境变量一个原理的命令行代理支持。所以你需要在本地先打开一个http/https代理服务器，像是[shadowsocks-windows](https://github.com/shadowsocks/shadowsocks-windows/releases)或者[shadowsocks](https://github.com/shadowsocks/shadowsocks/tree/master)。

如果你总是在语音转文字或者字幕翻译时遇到空白的结果或者连接错误，你可能需要换一个好点的proxy，这样才能更稳定地连接到Google服务器，或者干脆租个能连接到Google服务器的Linux服务器。

<escape><a href = "#目录">&nbsp;↑&nbsp;</a></escape>

### 问题反馈

问题和建议可以反馈在[issues](https://github.com/BingLingGroup/autosub/issues)。

### 构建

我只写了在windows上构建独立运行程序的脚本，一个用于[Nuitka](../scripts/nuitka_build.bat)一个用于[pyinstaller](../scripts/pyinstaller_build.bat)。

Nuitka的构建有点麻烦。我使用anaconda作为包管理器，因为[Nuitka readme](https://github.com/Nuitka/Nuitka#id6)是这么建议的。我使用anaconda的Python3.5和[m2w64-gcc](https://anaconda.org/msys2/m2w64-gcc)来构建。[m2w64-gcc](https://anaconda.org/msys2/m2w64-gcc)在这种情况也许是最稳定的64位C编译器。其他的C编译器或者Python环境可能在编译时失败，原因不明。对于那些操作系统语言不是`en_US`，请在构建前先设置成`en_US`。否则你会遇到这个[已知问题](https://github.com/Nuitka/Nuitka/issues/193)。

Pyinstaller的构建就比较稳定。只要配置文件写好了就没遇到问题。

[create_release.py](../scripts/create_release.py)是用来创建两个发布包的。如果你想创建一个“完全”独立运行的发布包像我制作的那样，你需要创建一个`binaries`文件夹，里面包含ffmpeg和ffmpeg-normalize的可执行文件。我使用的`ffmpeg.exe`和`ffprobe.exe`都来自[Zeranoe的ffmpeg windows构建](https://ffmpeg.zeranoe.com/builds/)。它的文件目录应该如下。

```
binaries\ffmpeg.exe
binaries\ffprobe.exe
binaries\ffmpeg-normalize-Nuitka\ffmpeg-normalize.exe
binaries\ffmpeg-normalize-pyinstaller\ffmpeg-normalize.exe
```
