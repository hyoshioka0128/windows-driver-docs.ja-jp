---
title: INF DDInstall.Services セクション
description: 各モデルあたり DDInstall.Services セクションには、INF ファイルに追加の INF ライター定義セクションを参照する 1 つまたは複数の INF AddService ディレクティブが含まれています。
ms.assetid: 30efb094-cc18-4c01-8851-4bc5dba1ae1d
keywords:
- INF DDInstall.Services セクションのデバイスとドライバーのインストール
topic_type:
- apiref
api_name:
- INF DDInstall.Services Section
api_type:
- NA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: efb03b5b2f1243d6230941206526f119761f4861
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56551332"
---
# <a name="inf-ddinstallservices-section"></a>INF DDInstall.Services セクション


各ごとのモデル<em>DDInstall</em>**します。サービス**セクションは、1 つ以上含まれています。 [ **INF AddService ディレクティブ**](inf-addservice-directive.md) INF ライター定義の追加のセクションで、INF ファイルを参照します。

```ini
[install-section-name.Services] |
[install-section-name.nt.Services] |
[install-section-name.ntx86.Services] |
[install-section-name.ntarm.Services] | (Windows 8 and later versions of Windows)
[install-section-name.ntarm64.Services] | (Windows 10 version 1709 and later versions of Windows)
[install-section-name.ntia64.Services] |  (Windows XP and later versions of Windows)
[install-section-name.ntamd64.Services]  (Windows XP and later versions of Windows)
 
AddService=ServiceName,[flags],service-install-section
                     [,event-log-install-section[,[EventLogType][,EventName]]]...]
[DelService=ServiceName[,[flags][,[EventLogType][,EventName]]]]...
[Include=filename.inf[,filename2.inf]...]
[Needs=inf-section-name[,inf-section-name]...] 
```

行うことができます、 <em>DDInstall</em>**します。サービス**に少なくとも 1 つのセクション**AddService**特定のドライバーのサービスが読み込まれる方法と、他のサービスまたはドライバーへの依存関係を制御するためのディレクティブ。 必要に応じて、イベント ログ サービスを指定することもできます。

## <a name="entries"></a>エントリ

<a href="" id="addservice-servicename--flags--service-install-section"></a>
<a href="" id="------------------------------------------------event-log-install-section---eventlogtype---eventname-------"></a>
**AddService =**<em>ServiceName</em>、\[*フラグ*\]**、**<em>サービス-インストール セクション</em>\[、*イベント ログ-インストール セクション*\[**、**\[*EventLogType* \] \[ **、**<em>EventName</em>\]\]\].\]  
このディレクティブは、INF ライターの定義を参照*サービス-インストール セクション*と、おそらく、*イベント ログ-インストール セクション*別の場所、INF、デバイスのドライバーのファイルで覆われてこの*DDInstall*セクション。 詳細については、[ **INF AddService ディレクティブ**](inf-addservice-directive.md)を参照してください。

<a href="" id="delservice-servicename---flags----eventlogtype---eventname------"></a>**DelService =**<em>ServiceName</em>\[**、**\[*フラグ*\]\[**、**\[ *EventLogType*\]\[**、**<em>EventName</em> \] \] \]...  
このディレクティブは、対象のコンピューターから、以前にインストールされたサービスを削除します。 このディレクティブが使用される非常にまれです。 詳細については、[ **INF DelService ディレクティブ**](inf-delservice-directive.md)を参照してください。

<a href="" id="include-filename-inf--filename2-inf----"></a>**含める =**<em>filename</em>**.inf**\[**、**<em>filename2</em>**.inf**\]...  
この省略可能なエントリでは、1 つまたは複数追加システムが指定した INF ファイルをこのデバイスをインストールするために必要なセクションが含まれているを指定します。 通常、このエントリが指定されている場合は、**必要がある**エントリ。

詳細については、 **Include**エントリと、その使用に関する制限事項を参照してください。[デバイス ファイルのソースとターゲットの場所を指定する](specifying-the-source-and-target-locations-for-device-files.md)します。

<a href="" id="needs-inf-section-name--inf-section-name----"></a>**必要な =**<em>inf セクション名</em>\[**、**<em>inf セクション名</em>\].  
この省略可能なエントリでは、このデバイスのインストール中に処理する必要があるセクションを指定します。 セクションは、通常、 <em>DDInstall</em>**します。サービス**セクションに記載されているシステム指定の INF ファイル内で、 **Include**エントリ。 ただし、内で参照されている任意のセクションがあります、 <em>DDInstall</em>**します。サービス**セクション。

**必要がある**エントリを入れ子にすることはできません。 詳細については、**必要がある**エントリと、その使用に関する制限事項を参照してください。[デバイス ファイルのソースとターゲットの場所を指定する](specifying-the-source-and-target-locations-for-device-files.md)します。

<a name="remarks"></a>注釈
-------

<em>DDInstall</em>**します。サービス**のセクションでは、それに関連として同じプラットフォームとオペレーティング システムの装飾が必要[ ***DDInstall*** ](inf-ddinstall-section.md)セクション。 たとえば、<em>インストール セクション名</em>**.ntx86**セクションは、対応する必要が<em>インストール セクション名</em>**.ntx86 します。サービス**セクション。

指定した*DDInstall* - 製造元でデバイス/モデルに固有のエントリでは、セクションを参照する必要があります*モデル*INF ファイルのセクション。 大文字の拡張機能を*インストール セクション名*に示すように正式な構文でステートメントを挿入できる、 <em>DDInstall</em>**します。サービス**クロスプラット フォーム対応の INF ファイルでセクション名。

詳細については、システム定義を使用する方法についての **.nt**、 **.ntx86**、 **.ntia64**、 **.ntamd64**、 **.ntarm**、および **.ntarm64** 、拡張機能を参照してください[INF ファイルを複数のプラットフォームやオペレーティング システムを作成する](creating-inf-files-for-multiple-platforms-and-operating-systems.md)します。

<a name="examples"></a>例
--------

この例では、 <em>DDInstall</em>**します。サービス**のセクション、 **Ser_Inst**セクションの例を示した、 [ **INF *DDInstall*セクション**](inf-ddinstall-section.md)します。

```ini
[Ser_Inst.Services]
AddService=sermouse, 0x00000002, sermouse_Service_Inst,\
                sermouse_EventLog_Inst 
;
; flags value in preceding entry indicates function driver of device
; 
AddService = mouclass,, mouclass_Service_Inst, mouclass_EventLog_Inst 

; entries in the following xxx_Inst sections omitted here for brevity,
; but fully specified as the example for the AddService directive
;
[sermouse_Service_Inst]
; ...

[sermouse_EventLog_Inst]
; ...

[mouclass_Service_Inst]
; ...

[mouclass_EventLog_Inst]
; ...
```

この例では、<em>インストール セクション名</em>**します。NT します。サービス**セクションと、そのサービスのインストール-セクション、INF ファイル、システムによって提供される WDM オーディオ デバイス/ドライバーの例を示した、 [ **INF *DDInstall*セクション**](inf-ddinstall-section.md).

```ini
[WDMPNPB003_Device.NT.Services]
AddService = wdmaud,0x00000000,wdmaud_Service_Inst
AddService = swmidi,0x00000000,swmidi_Service_Inst
AddService = sb16,  0x00000002,sndblst_Service_Inst

[wdmaud_Service_Inst]
DisplayName   = %wdmaud.SvcDesc% ; friendly name (see Strings)
ServiceType   = 1                ; SERVICE_KERNEL_DRIVER
StartType     = 1                ; SERVICE_SYSTEM_START
ErrorControl  = 1                ; SERVICE_ERROR_NORMAL
ServiceBinary = %10%\system32\drivers\wdmaud.sys

[swmidi_Service_Inst]
DisplayName   = %swmidi.SvcDesc% 
ServiceType   = 1 
StartType     = 1 
ErrorControl  = 1 
ServiceBinary = %10%\system32\drivers\swmidi.sys

[sndblst_Service_Inst]
DisplayName   = %sndblst.SvcDesc% 
ServiceType   = 1 
StartType     = 1 
ErrorControl  = 1 
ServiceBinary = %10%\system32\drivers\mssb16.sys

[Strings] ; only immediately preceding %strkey% tokens shown here
%wdmaud.SvcDesc%="Microsoft WDM Virtual Wave Driver (WDM)"
%swmidi.SvcDesc%="Microsoft Software Synthesizer (WDM)"
%sndblst.SvcDesc%="WDM Sample Driver for SB16"
```

参照してください[ **INF DDInstall.HW セクション**](inf-ddinstall-hw-section.md)の例について<em>DDInstall</em>**します。サービス**いくつかのセクションでは*サービス インストール*-セクションによって参照される、 [ **AddService** ](inf-addservice-directive.md)ディレクティブ。 PnP フィルター ドライバーのいずれかが含まれています。

## <a name="see-also"></a>関連項目


[**AddService**](inf-addservice-directive.md)

[***DDInstall***](inf-ddinstall-section.md)

[***DDInstall *。ハードウェア**](inf-ddinstall-hw-section.md)

[**DelService**](inf-delservice-directive.md)

[***モデル***](inf-models-section.md)

 

 






