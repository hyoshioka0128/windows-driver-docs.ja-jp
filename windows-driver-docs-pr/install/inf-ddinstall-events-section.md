---
title: INF DDInstall.Events セクション
author: andylsn
description: 各モデルの DDInstall. Events セクションには、inf ファイルで追加の INF ライター定義セクションを参照する1つ以上の INF AddEventProvider ディレクティブが含まれています。
ms.assetid: ''
keywords:
- INF DDInstall. Events セクションデバイスとドライバーのインストール
topic_type:
- apiref
api_name:
- INF DDInstall.Events Section
api_type:
- NA
ms.date: 06/04/2018
ms.localizationpriority: medium
ms.openlocfilehash: 7fd15c052eb52af092f84c80a19601f4e056cd7c
ms.sourcegitcommit: a55489992dbf0a7e9d09f237e13514799711647a
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/28/2020
ms.locfileid: "82223254"
---
# <a name="inf-ddinstallevents-section"></a>INF DDInstall.Events セクション

各モデルの<em>Ddinstall がインストール</em>**します。Events**セクションには、inf ファイルで追加の inf ライター定義セクションを参照する1つ以上の[**inf AddEventProvider ディレクティブ**](inf-addeventprovider-directive.md)が含まれています。 このセクションは、Windows 10 バージョン1809以降でサポートされています。

```inf
[install-section-name.Events] |
[install-section-name.nt.Events] |
[install-section-name.ntx86.Events] |
[install-section-name.ntia64.Events] |
[install-section-name.ntamd64.Events] |
[install-section-name.ntarm.Events] |
[install-section-name.ntarm64.Events] |

AddEventProvider={ProviderGUID},event-provider-install-section
[Include=filename.inf[,filename2.inf]...]
[Needs=inf-section-name[,inf-section-name]...] 
```

<em>Ddinstall</em>を提供でき**ます。** [Windows イベントトレーシング](https://docs.microsoft.com/windows/desktop/ETW/about-event-tracing)(ETW) プロバイダーを登録するための**AddEventProvider**ディレクティブが少なくとも1つある Events セクション。

## <a name="entries"></a>エントリ

<a href="" id="addeventprovider--providerguid--event-provider-install-section"></a>**AddEventProvider =**{*providerguid*}、*イベントプロバイダー-インストール-セクション*  
このディレクティブは、この*Ddinstall*セクションでカバーされているデバイスのドライバーについて、inf ファイル内の他の場所にある inf ライターが定義した*イベントプロバイダーのインストールセクション*を参照します。 詳細については、「 [**INF AddEventProvider ディレクティブ**](inf-addeventprovider-directive.md)」を参照してください。

<a href="" id="include-filename-inf--filename2-inf----"></a>**Include =**<em>filename</em>**. .inf**\[**,**<em>filename2</em>**.inf**\]...  
この省略可能なエントリは、このデバイスをインストールするために必要なセクションを含む、システムが提供する追加の INF ファイルを1つ以上指定します。 このエントリが指定されている場合は、**必要**なエントリも通常必要です。

**インクルード**エントリとその使用に関する制限の詳細については、「[デバイスファイルのソースとターゲットの場所の指定](specifying-the-source-and-target-locations-for-device-files.md)」を参照してください。

<a href="" id="needs-inf-section-name--inf-section-name----"></a>**必要な =**<em>inf-name</em>\[**,**<em>inf-name</em>\]...  
この省略可能なエントリは、このデバイスのインストール中に処理する必要があるセクションを指定します。 通常、このセクションは<em>Ddinstall</em>**です。****インクルード**エントリに一覧表示されているシステム提供の INF ファイル内の Events セクション。 ただし、 <em>Ddinstall</em>内で参照される任意のセクションを指定でき**ます。イベント**セクション。

**必要**なエントリを入れ子にすることはできません。 **必要**なエントリとその使用に関する制限の詳細については、「[デバイスファイルのソースとターゲットの場所の指定](specifying-the-source-and-target-locations-for-device-files.md)」を参照してください。

<a name="remarks"></a>解説
-------

<em>Ddinstall</em>**。イベント**セクションには、関連する[***ddinstall***](inf-ddinstall-section.md)セクションと同じプラットフォームとオペレーティングシステムの装飾が必要です。 たとえば、**ntx86**セクション<em>には</em>、対応する ntx86 という<em>名前</em>が付いています。**イベント**セクション。

指定された*Ddinstall*セクションは、INF ファイルの "製造元別*モデル*" セクションのデバイス/モデル固有のエントリで参照されている必要があります。 正式な構文のステートメントに示されている*インストールセクション名*の大文字と小文字を区別しない拡張機能は、このような<em>ddinstall</em>に挿入でき**ます。** クロスプラットフォームの INF ファイルの Events セクション名。

システム定義の**nt**、 **ntx86**、. **ntia64**、. **ntamd64**、. **ntarm**、および**ntarm64**の各拡張機能の使用方法の詳細については、「[複数のプラットフォームおよびオペレーティングシステム用の INF ファイルの作成](creating-inf-files-for-multiple-platforms-and-operating-systems.md)」を参照してください。

<a name="examples"></a>例
--------

この例は、<em>インストールセクション名</em>を示して**います。** INF ファイルの Events セクションとそのイベントプロバイダーのインストールセクション。

```inf
[Device_Inst.NT.Events]
AddEventProvider={071acb53-ccfb-42e0-9a68-5336b7301507},foo_Event_Provider_Inst
AddEventProvider={6d3fd9ef-bcbb-42d7-9fbd-1bf2d926b394},bar_Event_Provider_Inst

; entries in the following xxx_Inst sections omitted here for brevity,
; but fully specified as the example for the AddEventProvider directive
;
[foo_Event_Provider_Inst]
; ...

[bar_Event_Provider_Inst]
; ...
```

## <a name="see-also"></a>関連項目


[**AddEventProvider**](inf-addeventprovider-directive.md)

[***DDInstall***](inf-ddinstall-section.md)

 

 





