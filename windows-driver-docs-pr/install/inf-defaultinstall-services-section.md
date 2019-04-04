---
title: INF DefaultInstall.Services セクション
description: DefaultInstall.Services セクションには、INF ファイルに追加の INF ライター定義セクションを参照する 1 つまたは複数の AddService ディレクティブが含まれています。
ms.assetid: 2b066cf9-b6b7-42d0-b147-9b1849ff04db
keywords:
- INF DefaultInstall.Services セクションのデバイスとドライバーのインストール
topic_type:
- apiref
api_name:
- INF DefaultInstall.Services Section
api_type:
- NA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8be52df2e4c63809585269c414a6f720e7853359
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56572108"
---
# <a name="inf-defaultinstallservices-section"></a>INF DefaultInstall.Services セクション


**注**  ユニバーサルまたはモバイルのドライバー パッケージを作成している場合は、このセクションが無効です。 参照してください[ユニバーサル INF ファイルを使用して](using-a-universal-inf-file.md)します。

 

A **DefaultInstall.Services**セクションは、1 つ以上含まれています。 [ **AddService** ](inf-addservice-directive.md) INF ライター定義の追加のセクションで、INF ファイルを参照するディレクティブ。 このセクションでは、 [ **INF *DDInstall*します。サービス**](inf-ddinstall-services-section.md)セクションし、との関連付けで使用する[ **INF DefaultInstall** ](inf-defaultinstall-section.md)セクション。

```ini
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


<a href="" id="addservice-servicename--flags--service-install-section"></a>**AddService =**<em>ServiceName</em>**、**\[*フラグ*\]**、** <em>サービスのインストール-セクション</em>  

<a href="" id="-----------------------------------------------------------------------------------------event-log-install-section---eventlogtype---eventname------"></a>                                                   \[**,**<em>event-log-install-section</em>\[**,**\[*EventLogType*\]\[<strong>,</strong>EventName\]\]\]...  
このディレクティブは、INF ライターの定義を参照*サービス-インストール セクション*と、おそらく、*イベント ログ-インストール セクション*別の場所、INF、デバイスのドライバーのファイルで覆われてこの[**DefaultInstall** ](inf-defaultinstall-section.md)セクション。

詳細については、[ **INF AddService ディレクティブ**](inf-addservice-directive.md)を参照してください。

<a href="" id="delservice-servicename---flags----eventlogtype---eventname------"></a>**DelService =**<em>ServiceName</em>\[**、**\[*フラグ*\]\[**、**\[ *EventLogType*\]\[**、**<em>EventName</em> \] \] \]...  
このディレクティブは、対象のコンピューターから、以前にインストールされたサービスを削除します。 このディレクティブが使用される非常にまれです。

詳細については、[ **INF DelService ディレクティブ**](inf-delservice-directive.md)を参照してください。

<a href="" id="include-filename-inf--filename2-inf----"></a>**含める =**<em>filename</em>**.inf**\[**、**<em>filename2</em>**.inf**\]...  
この省略可能なエントリでは、1 つまたは複数追加システムが指定した INF ファイルをこのデバイスをインストールするために必要なセクションが含まれているを指定します。 通常、このエントリが指定されている場合は、**必要がある**エントリ。

詳細については、 **Include**エントリと、その使用に関する制限事項を参照してください。[デバイス ファイルのソースとターゲットの場所を指定する](specifying-the-source-and-target-locations-for-device-files.md)します。

<a href="" id="needs-inf-section-name--inf-section-name----"></a>**必要な =**<em>inf セクション名</em>\[**、**<em>inf セクション名</em>\].  
この省略可能なエントリでは、特定のセクションでこのデバイスのインストール中に処理する必要があるという名前を指定します。 通常、このような名前付きセクションは、 <em>DDInstall</em>**します。サービス**セクションに記載されているシステム指定の INF ファイル内で、 **Include**エントリ。 ただし、このような内で参照されている任意のセクションがあります、 <em>DDInstall</em>**します。サービス**セクション。

**必要がある**エントリを入れ子にすることはできません。 詳細については、**必要がある**エントリと、その使用に関する制限事項を参照してください。[デバイス ファイルのソースとターゲットの場所を指定する](specifying-the-source-and-target-locations-for-device-files.md)します。

<a name="remarks"></a>コメント
-------

[ **AddService** ](inf-addservice-directive.md)ディレクティブは、特定のドライバーのサービスが読み込まれる方法と、その他のサービスやがある、しなどがあります (レガシ) ドライバーを基になるには、すべての依存関係を制御します。 必要に応じて、ドライバーものイベント ログ サービスを設定できます。

**注**  INF ファイルを使用して、 **DefaultInstall.Services**セクションも使用している場合にのみ、 [ **INF DefaultInstall** ](inf-defaultinstall-section.md)セクション。 それ以外の場合、それらを使用して[ **INF *DDInstall*します。サービス**](inf-ddinstall-services-section.md)と共にセクション[ **INF *DDInstall***  ](inf-ddinstall-section.md)セクション。

 

**DefaultInstall.Services**のセクションでは、それに関連として同じプラットフォームとオペレーティング システムの装飾が必要**DefaultInstall**セクション。 たとえば、 **DefaultInstall.ntx86**セクションは、対応する必要が**DefaultInstall.ntx86.Services**セクション。 詳細については、システム定義を使用する方法についての **.nt**、 **.ntx86**、 **.ntia64**、 **.ntamd64**、 **.ntarm**、および **.ntarm64** 、拡張機能を参照してください[INF ファイルを複数のプラットフォームやオペレーティング システムを作成する](creating-inf-files-for-multiple-platforms-and-operating-systems.md)します。

<a name="examples"></a>使用例
--------

指定された例を参照してください、 [ **INF *DDInstall*します。サービス**](inf-ddinstall-services-section.md)セクション。

## <a name="see-also"></a>関連項目


[***DDInstall***](inf-ddinstall-section.md)

[**DefaultInstall**](inf-defaultinstall-section.md)

 

 






