---
title: INF DDInstall.Services セクション
description: 各モデルの DDInstall. Services セクションには、inf ファイルで追加の INF ライター定義セクションを参照する1つ以上の INF AddService ディレクティブが含まれています。
ms.assetid: 30efb094-cc18-4c01-8851-4bc5dba1ae1d
keywords:
- INF DDInstall. Services セクションデバイスとドライバーのインストール
topic_type:
- apiref
api_name:
- INF DDInstall.Services Section
api_type:
- NA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 72c40dedf327b19ce636ab1ed0d04a00bb439537
ms.sourcegitcommit: a55489992dbf0a7e9d09f237e13514799711647a
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/28/2020
ms.locfileid: "82223224"
---
# <a name="inf-ddinstallservices-section"></a>INF DDInstall.Services セクション


各モデルの<em>Ddinstall がインストール</em>**します。Services**セクションには、inf ファイルで追加の inf ライター定義セクションを参照する1つ以上の[**Inf addservice ディレクティブ**](inf-addservice-directive.md)が含まれています。

```inf
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

<em>Ddinstall</em>を提供でき**ます。サービス**セクション。特定のドライバーのサービスの読み込み方法とタイミング、および他のサービスやドライバーへの依存関係などを制御するための**addservice**ディレクティブが少なくとも1つあります。 必要に応じて、イベントログサービスを指定することもできます。

## <a name="entries"></a>エントリ

<a href="" id="addservice-servicename--flags--service-install-section"></a>
<a href="" id="------------------------------------------------event-log-install-section---eventlogtype---eventname-------"></a>
**Addservice =**<em>ServiceName</em>、\[*flags*\]**、**<em>service-install-section</em>\[EventLogType、*イベントログ-セクション*\[**,**\[*EventLogType*\]\[**、**<em>EventName</em>\]EventName\]......\]\]  
このディレクティブは、inf ライターで定義された*サービスのインストール*セクションを参照します。また、この*ddinstall*セクションでカバーされているデバイスのドライバーの inf ファイルの別の場所で、場合によっては、*イベントログのインストール*セクションを参照します。 詳細については、「 [**INF AddService ディレクティブ**](inf-addservice-directive.md)」を参照してください。

<a href="" id="delservice-servicename---flags----eventlogtype---eventname------"></a>**Delservice =**<em>ServiceName</em>\[**、**\[*flags*\]\[*EventLogType***,**<em>EventName</em>**,**\]、EventLogType\]、EventName\]...\]\[\[  
このディレクティブは、以前にインストールされたサービスをターゲットコンピューターから削除します。 このディレクティブはほとんど使用されません。 詳細については、「 [**INF DelService ディレクティブ**](inf-delservice-directive.md)」を参照してください。

<a href="" id="include-filename-inf--filename2-inf----"></a>**Include =**<em>filename</em>**. .inf**\[**,**<em>filename2</em>**.inf**\]...  
この省略可能なエントリは、このデバイスをインストールするために必要なセクションを含む、システムが提供する追加の INF ファイルを1つ以上指定します。 このエントリが指定されている場合は、通常、**必要**なエントリです。

**インクルード**エントリとその使用に関する制限の詳細については、「[デバイスファイルのソースとターゲットの場所の指定](specifying-the-source-and-target-locations-for-device-files.md)」を参照してください。

<a href="" id="needs-inf-section-name--inf-section-name----"></a>**必要な =**<em>inf-name</em>\[**,**<em>inf-name</em>\]...  
この省略可能なエントリは、このデバイスのインストール中に処理する必要があるセクションを指定します。 通常、このセクションは<em>Ddinstall</em>**です。****インクルード**エントリに記載されている、システム提供の INF ファイル内の Services セクション。 ただし、 <em>Ddinstall</em>内で参照される任意のセクションを指定でき**ます。サービス**セクション。

**必要**なエントリを入れ子にすることはできません。 **必要**なエントリとその使用に関する制限の詳細については、「[デバイスファイルのソースとターゲットの場所の指定](specifying-the-source-and-target-locations-for-device-files.md)」を参照してください。

<a name="remarks"></a>解説
-------

<em>Ddinstall</em>**。サービス**のセクションには、関連する[***ddinstall***](inf-ddinstall-section.md)セクションと同じプラットフォームとオペレーティングシステムの装飾が必要です。 たとえば、**ntx86**セクション<em>には</em>、対応する ntx86 という<em>名前</em>が付いています。**サービス**セクション。

指定された*Ddinstall*セクションは、INF ファイルの "製造元別*モデル*" セクションのデバイス/モデル固有のエントリで参照されている必要があります。 正式な構文のステートメントに示されている*インストールセクション名*の大文字と小文字を区別しない拡張機能は、このような<em>ddinstall</em>に挿入でき**ます。** クロスプラットフォームの INF ファイルのサービスセクション名。

システム定義の**nt**、 **ntx86**、. **ntia64**、. **ntamd64**、. **ntarm**、および**ntarm64**の各拡張機能の使用方法の詳細については、「[複数のプラットフォームおよびオペレーティングシステム用の INF ファイルの作成](creating-inf-files-for-multiple-platforms-and-operating-systems.md)」を参照してください。

<a name="examples"></a>例
--------

この例は、 <em>Ddinstall</em>を示して**います。** **Ser_Inst**セクションのサービスセクションは、 [**INF *ddinstall*セクション**](inf-ddinstall-section.md)の例として示されています。

```inf
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

この例は、<em>インストールセクション名</em>を示して**います。R.**「 [**Inf *ddinstall* 」セクション**](inf-ddinstall-section.md)の例として、システムによって提供される WDM オーディオデバイス/ドライバーの inf ファイルにあるサービスセクションとそのサービスインストールセクション。

```inf
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

<em>Ddinstall</em>のその他の例については、「 [**INF DDINSTALL. HW」セクション**](inf-ddinstall-hw-section.md)を参照してください **。サービスセクション。** [**addservice**](inf-addservice-directive.md)ディレクティブによって参照される*サービスインストール*セクションがあります。 これには、PnP フィルタードライバーの1つが含まれます。

## <a name="see-also"></a>関連項目


[**AddService**](inf-addservice-directive.md)

[***DDInstall***](inf-ddinstall-section.md)

[***DDInstall *。ハードウェア**](inf-ddinstall-hw-section.md)

[**DelService**](inf-delservice-directive.md)

[***モデル***](inf-models-section.md)

 

 






