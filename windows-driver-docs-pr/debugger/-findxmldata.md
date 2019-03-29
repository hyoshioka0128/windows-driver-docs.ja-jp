---
title: findxmldata
description: Findxmldata 拡張機能は、カーネル モードの最小メモリ ダンプ ファイルを含んでいる CAB ファイルから XML データを取得します。
ms.assetid: 6d0b5294-b086-4b33-ac0d-0428521a3489
keywords:
- CAB ファイルの XML データ
- sysdata.xml
- Windows デバッグ findxmldata
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- findxmldata
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: be71b499f13e007b1948fb46d191f13b77c22cbe
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56571759"
---
# <a name="findxmldata"></a>!findxmldata


**! Findxmldata**拡張機能は、カーネル モードの最小メモリ ダンプ ファイルを含んでいる CAB ファイルから XML データを取得します。

```dbgcmd
!findxmldata [ -d DeviceName | -h HwId ] 
!findxmldata -r Driver 
!findxmldata -chksum [ -z CabFile ]
!findxmldata -v 
```

## <a name="span-idddkfindxmldatadbgspanspan-idddkfindxmldatadbgspanparameters"></a><span id="ddk__findxmldata_dbg"></span><span id="DDK__FINDXMLDATA_DBG"></span>パラメーター


<span id="_______-d_______DeviceName______"></span><span id="_______-d_______devicename______"></span><span id="_______-D_______DEVICENAME______"></span> **-d** *DeviceName*   
デバイスの名前の文字列を含むすべてのデバイスを表示する*DeviceName*を指定します。

<span id="_______-h_______HwId______"></span><span id="_______-h_______hwid______"></span><span id="_______-H_______HWID______"></span> **-h** *HwId*   
ハードウェア Id を持つには、文字列が含まれているすべてのデバイスを表示する*HwId*を指定します。 両方を使用する場合 **-d**と **-h**デバッガーを両方の一致を満たすデバイスのみが表示されます。

<span id="_______-r_______Driver______"></span><span id="_______-r_______driver______"></span><span id="_______-R_______DRIVER______"></span> **-r** *ドライバー*   
ドライバーに関する情報を表示する、*ドライバー*このドライバーを使用するすべてのデバイスなどのパラメーターを指定します。

<span id="_______-chksum______"></span><span id="_______-CHKSUM______"></span> **-chksum**   
XML ファイルのチェックサムが表示されます。

<span id="_______-z_______CabFile______"></span><span id="_______-z_______cabfile______"></span><span id="_______-Z_______CABFILE______"></span> **-z** *CabFile*   
キャビネットのパラメーターを指定します、CAB ファイルのチェックサムを実行することができますの代わりに既定の Sysdata.xml ファイルにします。

<span id="_______-v______"></span><span id="_______-V______"></span> **-v**   
システムのバージョン情報が表示されます。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>Windows 2000</strong></p></td>
<td align="left"><p>Ext.dll</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>Windows XP 以降</strong></p></td>
<td align="left"><p>Ext.dll</p></td>
</tr>
</tbody>
</table>

 

**! Findxmldata**拡張機能は、CAB ファイルに格納されているカーネル モード最小メモリ ダンプのファイルでのみ機能します。

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>追加情報

CAB ファイルにダンプ ファイルを配置する方法の詳細については、次を参照してください。 [ **.dumpcab (ダンプ ファイル CAB の作成)**](-dumpcab--create-dump-file-cab-.md)します。 CAB ファイルに保存されているダンプ ファイルを含む、カーネル モードのダンプ ファイルをデバッグする方法の詳細については、次を参照してください。[カーネル モードのダンプ ファイルの分析](analyzing-a-kernel-mode-dump-file.md)します。

<a name="remarks"></a>コメント
-------

**! Findxmldata**カーネル モードを含む CAB ファイルに格納されている Sysdata.xml ファイルからデータを取得する拡張機能[最小メモリ ダンプ](small-memory-dump.md)ファイル。

任意のオプションを使用しないと、拡張機能には、すべてのデバイスが表示されます。

次の例は、使用する方法を表示 **! findxmldata**します。

```dbgcmd
kd> !findxmldata -v
SYSTEM Info:
OSVER: 5.1.2600 2.0
OSLANGUAGE: 2052
OSNAME: Microsoft Windows XP Home Edition
kd> !findxmldata -d MIDI
Node DEVICE
 DESCRIPTION    : MPU-401 Compatible MIDI Device
        HARDWAREID     : ACPI\PNPB006
        SERVICE        : ms_mpu401
        DRIVER         : msmpu401.sys

kd> !findxmldata -r msmpu
Node DRIVER
 FILENAME       : msmpu401.sys
        FILESIZE       : 2944
        CREATIONDATE   : 05-06-2005 09:18:34
        VERSION        : 5.1.2600.0
        MANUFACTURER   : Microsoft Corporation
        PRODUCTNAME    : Microsoft« Windows« Operating System
Node DEVICE
        DESCRIPTION    : MPU-401 Compatible MIDI Device
 HARDWAREID     : ACPI\PNPB006
        SERVICE        : ms_mpu401
        DRIVER         : msmpu401.sys

kd> !findxmldata -h PCI\VEN_8086&DEV_24C3&SUBSYS_24C28086
Node DEVICE
 DESCRIPTION    : Intel(R) 82801DB/DBM SMBus Controller - 24C3
        HARDWAREID     : PCI\VEN_8086&DEV_24C3&SUBSYS_24C28086&REV_01
kd> !findxmldata -h USB\ROOT_HUB&VID8086&PID24C4&REV0001
Node DEVICE
        DESCRIPTION    : USB Root Hub
 HARDWAREID     : USB\ROOT_HUB&VID8086&PID24C4&REV0001
        SERVICE        : usbhub
        DRIVER         : usbhub.sys

kd> !findxmldata -h ACPI\PNPB006
Node DEVICE
        DESCRIPTION    : MPU-401 Compatible MIDI Device
 HARDWAREID     : ACPI\PNPB006
        SERVICE        : ms_mpu401
        DRIVER         : msmpu401.sys
```

 

 





