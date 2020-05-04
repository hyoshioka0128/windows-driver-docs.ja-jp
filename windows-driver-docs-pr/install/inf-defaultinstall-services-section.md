---
title: INF DefaultInstall.Services セクション
description: DefaultInstall セクションには、INF ファイルで追加の INF ライター定義セクションを参照している AddService ディレクティブが1つ以上含まれています。
ms.assetid: 2b066cf9-b6b7-42d0-b147-9b1849ff04db
keywords:
- INF DefaultInstall セクションデバイスとドライバーのインストール
topic_type:
- apiref
api_name:
- INF DefaultInstall.Services Section
api_type:
- NA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b5c7622d2507bbb05551332ac7667d9afc360c4e
ms.sourcegitcommit: a55489992dbf0a7e9d09f237e13514799711647a
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/28/2020
ms.locfileid: "82223210"
---
# <a name="inf-defaultinstallservices-section"></a>INF DefaultInstall.Services セクション


**注**  ユニバーサルまたはモバイルのドライバーパッケージを作成する場合、このセクションは無効です。 「[ユニバーサル INF ファイルの使用」を](using-a-universal-inf-file.md)参照してください。

 

**DefaultInstall**セクションには、inf ファイルで追加の inf ライター定義セクションを参照している[**addservice**](inf-addservice-directive.md)ディレクティブが1つ以上含まれています。 このセクションは、 [**INF *ddinstall*に相当します。サービス**](inf-ddinstall-services-section.md)セクション、および[**INF DefaultInstall**](inf-defaultinstall-section.md)セクションとの関連付けに使用されます。

```inf
[DefaultInstall.Services] |
[DefaultInstall.nt.Services] |
[DefaultInstall.ntx86.Services] |
[DefaultInstall.ntarm.Services] | (Windows 8 and later versions of Windows)
[DefaultInstall.ntarm64.Services]  (Windows 10 version 1709 and later versions of Windows)
[DefaultInstall.ntia64.Services] | (Windows XP and later versions of Windows)
[DefaultInstall.ntamd64.Services]  (Windows XP and later versions of Windows)
 
AddService=ServiceName,[flags],service-install-section
                             [,event-log-install-section[,[EventLogType][,EventName]]]...]
[DelService=ServiceName[,[flags][,[EventLogType][,EventName]]]...]
[Include=filename.inf[,filename2.inf]...]
[Needs=inf-section-name[,inf-section-name]...]
```

## <a name="entries"></a>エントリ


<a href="" id="addservice-servicename--flags--service-install-section"></a>**Addservice =**<em>ServiceName</em>**、**\[*flags*\]**、**<em>service-section</em>  

<a href="" id="-----------------------------------------------------------------------------------------event-log-install-section---eventlogtype---eventname------"></a>                                                   \[**、**<em>イベントログ-セクション</em>\[**、**\[*EventLogType*\]\[<strong>、</strong>\]EventName\]...\]  
このディレクティブは、inf ライターで定義された*サービスのインストール*セクションを参照します。また、場合によっては、inf ファイル内の他の場所で、この[**DefaultInstall**](inf-defaultinstall-section.md)セクションでカバーされているデバイスのドライバー用の*イベントログのインストール*セクションを参照します。

詳細については、「 [**INF AddService ディレクティブ**](inf-addservice-directive.md)」を参照してください。

<a href="" id="delservice-servicename---flags----eventlogtype---eventname------"></a>**Delservice =**<em>ServiceName</em>\[**、**\[*flags*\]\[*EventLogType***,**<em>EventName</em>**,**\]、EventLogType\]、EventName\]...\]\[\[  
このディレクティブは、以前にインストールされたサービスをターゲットコンピューターから削除します。 このディレクティブはほとんど使用されません。

詳細については、「 [**INF DelService ディレクティブ**](inf-delservice-directive.md)」を参照してください。

<a href="" id="include-filename-inf--filename2-inf----"></a>**Include =**<em>filename</em>**. .inf**\[**,**<em>filename2</em>**.inf**\]...  
この省略可能なエントリは、このデバイスをインストールするために必要なセクションを含む、システムが提供する追加の INF ファイルを1つ以上指定します。 このエントリが指定されている場合は、通常、**必要**なエントリです。

**インクルード**エントリとその使用に関する制限の詳細については、「[デバイスファイルのソースとターゲットの場所の指定](specifying-the-source-and-target-locations-for-device-files.md)」を参照してください。

<a href="" id="needs-inf-section-name--inf-section-name----"></a>**必要な =**<em>inf-name</em>\[**,**<em>inf-name</em>\]...  
この省略可能なエントリは、このデバイスのインストール中に処理する必要がある特定の名前付きセクションを指定します。 通常、このような名前付きセクションは、 <em>Ddinstall</em>**です。****インクルード**エントリに記載されている、システム提供の INF ファイル内の Services セクション。 ただし、このような<em>Ddinstall</em>内で参照される任意のセクションを指定でき**ます。サービス**セクション。

**必要**なエントリを入れ子にすることはできません。 **必要**なエントリとその使用に関する制限の詳細については、「[デバイスファイルのソースとターゲットの場所の指定](specifying-the-source-and-target-locations-for-device-files.md)」を参照してください。

<a name="remarks"></a>解説
-------

[**Addservice**](inf-addservice-directive.md)ディレクティブは、特定のドライバーのサービスがどのように読み込まれるか、他のサービスまたは基になる (レガシ) ドライバーに依存しているかなどを制御します。 必要に応じて、ドライバーのイベントログサービスをセットアップすることもできます。

**注**  inf ファイルでは、 [**inf DefaultInstall**](inf-defaultinstall-section.md)セクションも使用している場合にのみ、 **DefaultInstall**セクションを使用します。 それ以外の場合は、 [**INF *ddinstall*を使用します。サービス**](inf-ddinstall-services-section.md)セクションと[**INF *ddinstall* **](inf-ddinstall-section.md)セクション。

 

**DefaultInstall**セクションには、関連する**DefaultInstall**セクションと同じプラットフォームとオペレーティングシステムの装飾が必要です。 たとえば、ntx86 セクションには、対応する**DefaultInstall**セクションが**DefaultInstall**ます。 システム定義の**nt**、 **ntx86**、. **ntia64**、. **ntamd64**、. **ntarm**、および**ntarm64**の各拡張機能の使用方法の詳細については、「[複数のプラットフォームおよびオペレーティングシステム用の INF ファイルの作成](creating-inf-files-for-multiple-platforms-and-operating-systems.md)」を参照してください。

<a name="examples"></a>例
--------

[**INF *ddinstall*の例を参照してください。サービス**](inf-ddinstall-services-section.md)セクション。

## <a name="see-also"></a>関連項目


[***DDInstall***](inf-ddinstall-section.md)

[**DefaultInstall**](inf-defaultinstall-section.md)

 

 






