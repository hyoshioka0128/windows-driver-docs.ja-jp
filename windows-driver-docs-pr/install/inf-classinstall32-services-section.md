---
title: INF ClassInstall32.Services セクション
description: ClassInstall32 セクションでは、新しいクラスにデバイス用の新しいデバイスセットアップクラス (および場合によってはクラスインストーラー) をインストールします。
ms.assetid: 602cf407-f3c0-4342-9e59-87481a0f41ef
keywords:
- INF ClassInstall32 セクションデバイスとドライバーのインストール
topic_type:
- apiref
api_name:
- INF ClassInstall32.Services Section
api_type:
- NA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 994acabafaf442dc479d579fa31f33b62a51cbbc
ms.sourcegitcommit: a55489992dbf0a7e9d09f237e13514799711647a
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/28/2020
ms.locfileid: "82223270"
---
# <a name="inf-classinstall32services-section"></a>INF ClassInstall32.Services セクション


**注**  ユニバーサルまたはモバイルのドライバーパッケージを作成する場合、このセクションは無効です。 「[ユニバーサル INF ファイルの使用」を](using-a-universal-inf-file.md)参照してください。

 

**ClassInstall32**セクションでは、新しいクラスにデバイス用の新しい[デバイスセットアップクラス](device-setup-classes.md)(および場合によってはクラスインストーラー) をインストールします。

```inf
[ClassInstall32.Services] | 
[ClassInstall32.nt.Services] | 
[ClassInstall32.ntx86.Services] | 
[ClassInstall32.ntarm.Services] | (Windows 8 and later versions of Windows)
[ClassInstall32.ntarm64.Services] | (Windows 10 version 1709 and later versions of Windows)
[ClassInstall32.ntia64.Services] |  (Windows XP and later versions of Windows)
[ClassInstall32.ntamd64.Services]  (Windows XP and later versions of Windows)

AddService=ServiceName,[flags],service-install-section
                             [,event-log-install-section[,[EventLogType][,EventName]]]...
[DelService=ServiceName[,[flags][,[EventLogType][,EventName]]]...]
[Include=filename.inf[,filename2.inf]...]
[Needs=inf-section-name[,inf-section-name]...]
```

各**ClassInstall32**セクションには、inf ファイルで追加の inf ライター定義セクションを参照する1つ以上の[**inf addservice ディレクティブ**](inf-addservice-directive.md)が含まれています。

通常、INF ファイルでは、 **ClassInstall32**セクションに少なくとも1つの**addservice**ディレクティブを使用して、特定のデバイスクラスのサービスの読み込み方法とタイミング、および他のサービスに対する依存関係を制御します。 必要に応じて、デバイスクラスのイベントログサービスを設定することもできます。

## <a name="entries"></a>エントリ


<a href="" id="addservice-servicename--flags--service-install-section"></a>**Addservice =**<em>ServiceName</em>、\[*flags*\]**、**<em>service-section</em>  

<a href="" id="----------------------------------------event-log-install-section---eventlogtype---eventname------"></a>                                      \[**、**<em>イベントログ-セクション</em>\[**、**\[*EventLogType*\]\[**、**\]<em>EventName</em>\]...\]  
このディレクティブは、inf ライターで定義されたサービスのインストールセクションを参照します。また、場合によっては、INF ファイル内の他の場所で、 [**ClassInstall32**](inf-classinstall32-section.md)セクションでカバーされているデバイスクラスのドライバーを参照します。 詳細については、「 [**INF AddService ディレクティブ**](inf-addservice-directive.md)」を参照してください。

<a href="" id="delservice-servicename---flags----eventlogtype---eventname------"></a>**Delservice =**<em>ServiceName</em>\[**、**\[*flags*\]\[*EventLogType***,**<em>EventName</em>**,**\]、EventLogType\]、EventName\]...\]\[\[  
このディレクティブは、以前にインストールされたサービスをターゲットコンピューターから削除します。 このディレクティブはほとんど使用されません。 詳細については、「 [**INF DelService ディレクティブ**](inf-delservice-directive.md)」を参照してください。

<a href="" id="include-filename-inf--filename2-inf----"></a>**Include =**<em>filename</em>**. .inf**\[**,**<em>filename2</em>**.inf**\]...  
この省略可能なエントリは、このデバイスクラスをインストールするために必要なセクションを含む、システムによって指定された、追加の名前付き INF ファイルを1つ以上指定します。 このエントリが指定されている場合は、通常、**必要**なエントリです。

**インクルード**エントリとその使用に関する制限の詳細については、「[デバイスファイルのソースとターゲットの場所の指定](specifying-the-source-and-target-locations-for-device-files.md)」を参照してください。

<a href="" id="needs-inf-section-name--inf-section-name----"></a>**必要な =**<em>inf-name</em>\[**,**<em>inf-name</em>\]...  
この省略可能なエントリは、このデバイスクラスのインストール中に処理する必要がある特定の名前付きセクションを指定します。 通常、このような名前付きセクションは、**インクルード**エントリに記載されているシステム提供の INF ファイル内の**ClassInstall32**セクションです。 ただし、このような**ClassInstall32**セクション内で参照される任意のセクションを指定できます。

**必要**なエントリを入れ子にすることはできません。 (**必要**なエントリとその使用に関する制限の詳細については、「[デバイスファイルのソースとターゲットの場所の指定](specifying-the-source-and-target-locations-for-device-files.md)」を参照してください)。

<a name="remarks"></a>解説
-------

**ClassInstall32**セクションには、関連する[**ClassInstall32 セクション**](inf-classinstall32-section.md)と同じプラットフォームとオペレーティングシステムの装飾が必要です。 たとえば、ntx86 セクションには、対応する**ClassInstall32**セクションが**ClassInstall32**ます。

大文字と小文字は区別され**ません。 nt**、 **ntx86**、. **ntia64**、. **ntamd64**、 **. ntarm**、および**ntarm64**の各拡張子は、正式な構文ステートメントで示されているように、クロスプラットフォームの INF ファイルの**ClassInstall32**セクション名に挿入できます。 詳細については、「[複数のプラットフォームおよびオペレーティングシステム用の INF ファイルの作成](creating-inf-files-for-multiple-platforms-and-operating-systems.md)」を参照してください。

## <a name="see-also"></a>関連項目


[**ClassInstall32**](inf-classinstall32-section.md)

[**AddService**](inf-addservice-directive.md)

[***DDInstall***](inf-ddinstall-section.md)

[***DDInstall *。ハードウェア**](inf-ddinstall-hw-section.md)

[**DelService**](inf-delservice-directive.md)

[***モデル***](inf-models-section.md)

 

 






