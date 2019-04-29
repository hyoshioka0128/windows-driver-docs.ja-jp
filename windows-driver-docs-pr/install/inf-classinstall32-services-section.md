---
title: INF ClassInstall32.Services セクション
description: ClassInstall32 セクションは、新しいクラスでのデバイス向けの新しいデバイス セットアップ クラス (と可能性があるクラスのインストーラー) をインストールします。
ms.assetid: 602cf407-f3c0-4342-9e59-87481a0f41ef
keywords:
- INF ClassInstall32.Services セクションのデバイスとドライバーのインストール
topic_type:
- apiref
api_name:
- INF ClassInstall32.Services Section
api_type:
- NA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9a7b4a1e8c5978474b5121eac5626cea06b79d09
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63330917"
---
# <a name="inf-classinstall32services-section"></a>INF ClassInstall32.Services セクション


**注**  ユニバーサルまたはモバイルのドライバー パッケージを作成している場合は、このセクションが無効です。 参照してください[ユニバーサル INF ファイルを使用して](using-a-universal-inf-file.md)します。

 

A **ClassInstall32**セクションは、新しいインストール[デバイス セットアップ クラス](device-setup-classes.md)(およびクラスのインストーラー可能性があります)、新しいクラスでのデバイス向けです。

```ini
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

各**ClassInstall32.Services**セクションは、1 つ以上含まれています。 [ **INF AddService ディレクティブ**](inf-addservice-directive.md) INF ライター定義の追加のセクションで、INF ファイルを参照します。

INF ファイルを使用して、通常、 **ClassInstall32.Services**に少なくとも 1 つのセクション**AddService**特定のデバイス クラスのサービスが読み込まれる方法とタイミングを制御するディレクティブ、すべての依存関係が可能性がありますが、他のサービスになど。 必要に応じて、デバイス クラスのイベント ログ サービスも設定ができます。

## <a name="entries"></a>エントリ


<a href="" id="addservice-servicename--flags--service-install-section"></a>**AddService =**<em>ServiceName</em>、\[*フラグ*\]**、**<em>サービス-インストール セクション</em>  

<a href="" id="----------------------------------------event-log-install-section---eventlogtype---eventname------"></a>                                      \[**,**<em>event-log-install-section</em>\[**,**\[*EventLogType*\]\[**,**<em>EventName</em>\]\]\]...  
このディレクティブは、INF ライターで定義されているサービスのインストール-セクションと、場合によっては、イベントのログ-インストールのセクションで対応するデバイス クラスのドライバーの INF ファイルで別の場所を参照、 [ **ClassInstall32**](inf-classinstall32-section.md)セクション。 詳細については、次を参照してください。 [ **INF AddService ディレクティブ**](inf-addservice-directive.md)します。

<a href="" id="delservice-servicename---flags----eventlogtype---eventname------"></a>**DelService =**<em>ServiceName</em>\[**、**\[*フラグ*\]\[**、**\[ *EventLogType*\]\[**、**<em>EventName</em> \] \] \]...  
このディレクティブは、対象のコンピューターから、以前にインストールされたサービスを削除します。 このディレクティブが使用される非常にまれです。 詳細については、次を参照してください。 [ **INF DelService ディレクティブ**](inf-delservice-directive.md)します。

<a href="" id="include-filename-inf--filename2-inf----"></a>**含める =**<em>filename</em>**.inf**\[**、**<em>filename2</em>**.inf**\]...  
この省略可能なエントリでは、1 つまたは複数追加システムが指定した名前付き INF ファイルをこのデバイス クラスをインストールするために必要なセクションが含まれているを指定します。 通常、このエントリが指定されている場合は、**必要がある**エントリ。

詳細については、 **Include**エントリと、その使用に関する制限事項を参照してください。[デバイス ファイルのソースとターゲットの場所を指定する](specifying-the-source-and-target-locations-for-device-files.md)します。

<a href="" id="needs-inf-section-name--inf-section-name----"></a>**必要な =**<em>inf セクション名</em>\[**、**<em>inf セクション名</em>\].  
この省略可能なエントリでは、特定のセクションでこのデバイス クラスのインストール中に処理する必要があるという名前を指定します。 通常、このような名前付きセクションは、 **ClassInstall32.Services**セクションに記載されているシステム指定の INF ファイル内で、 **Include**エントリ。 ただし、このような内で参照されている任意のセクションがあります、 **ClassInstall32.Services**セクション。

**必要がある**エントリを入れ子にすることはできません。 (の詳細については、**必要がある**エントリと、その使用に関する制限事項を参照してください。[デバイス ファイルのソースとターゲットの場所を指定する](specifying-the-source-and-target-locations-for-device-files.md))。

<a name="remarks"></a>注釈
-------

**ClassInstall32.Services**のセクションでは、それに関連として同じプラットフォームとオペレーティング システムの装飾が必要[ **ClassInstall32 セクション**](inf-classinstall32-section.md)します。 たとえば、 **ClassInstall32.ntx86**セクションは、対応する必要が**ClassInstall32.ntx86.Services**セクション。

大文字、 **.nt**、 **.ntx86**、 **.ntia64**、 **.ntamd64**、 **.ntarm**、および **.ntarm64**に拡張機能を挿入できる、 **ClassInstall32.Services**正式な構文のステートメントのように、クロス プラットフォームの INF ファイルの名前をセクションします。 詳細については、次を参照してください。 [INF ファイルを複数のプラットフォームやオペレーティング システムを作成する](creating-inf-files-for-multiple-platforms-and-operating-systems.md)します。

## <a name="see-also"></a>関連項目


[**ClassInstall32**](inf-classinstall32-section.md)

[**AddService**](inf-addservice-directive.md)

[***DDInstall***](inf-ddinstall-section.md)

[***DDInstall *。ハードウェア**](inf-ddinstall-hw-section.md)

[**DelService**](inf-delservice-directive.md)

[***モデル***](inf-models-section.md)

 

 






