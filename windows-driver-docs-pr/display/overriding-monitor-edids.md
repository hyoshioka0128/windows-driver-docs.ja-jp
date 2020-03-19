---
title: INF でモニター EDIDs を上書きする
description: INF ファイルを使用すると、任意のモニターの拡張ディスプレイ識別データ (EDID) を上書きできます。
ms.assetid: AA7DC29B-54D5-461A-8252-600D84F0F581
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1ce33823e5d8bf7a586e087c0f95e5c6b913ed54
ms.sourcegitcommit: 347bd952a4164fd75fd2e4c56d46973bbb90e5a5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/18/2020
ms.locfileid: "79504409"
---
# <a name="overriding-monitor-edids-with-an-inf"></a>INF でモニター EDIDs を上書きする


INF ファイルを使用すると、任意のモニターの拡張ディスプレイ識別データ (EDID) を上書きできます。 この方法を示すサンプル INF ファイル Monsamp は、windows 7 (WDK バージョン 7600) を通じて Windows Driver Kit (WDK) に付属しています。 Monsamp がここで再現されます。

Monsamp を使用および変更する方法の詳細については、「 [MONITOR Inf File」セクション](monitor-inf-file-sections.md)を参照してください。

## <a name="span-idapproaches_to_correcting_edidsspanspan-idapproaches_to_correcting_edidsspanspan-idapproaches_to_correcting_edidsspanapproaches-to-correcting-edids"></a><span id="Approaches_to_correcting_EDIDs"></span><span id="approaches_to_correcting_edids"></span><span id="APPROACHES_TO_CORRECTING_EDIDS"></span>EDIDs を修正する方法


すべてのモニター (アナログまたはデジタル) は EDID をサポートする必要があります。これには、モニターの識別子、製造元のデータ、ハードウェア識別子、タイミング情報などの情報が含まれます。 このデータは、ビデオエレクトロニクス標準協会 (VESA) によって指定された形式でモニターの EEPROM に格納されます。

モニターは、EDID を Microsoft Windows コンポーネント、ディスプレイドライバー、および一部のユーザーモードアプリケーションに提供します。 たとえば、初期化中に、モニタードライバーは Windows Display Driver Model (WDDM) ドライバーに対して、その明るさクエリインターフェイスと、EDID にあるデバイスドライバーインターフェイス (DDI) のサポートを照会します。 モニターの EEPROM の EDID 情報が正しくないか無効なため、表示モードの設定が正しくないなどの問題が発生する可能性があります。

EDIDs を修正するには、次の2つの方法があります。

-   標準的な解決策は、お客様がモニターを製造元に送り返すようにすることです。この場合、reflashes が正しい EDID で EEPROM を取得し、モニターを顧客に返します。
-   ここでは、製造元が正しい EDID 情報を含む INF ファイルを実装し、モニターに接続されているコンピューターにダウンロードすることをお勧めします。 Windows は、更新された EDID 情報を INF から抽出し、EEPROM EDID からの情報ではなくコンポーネントに提供して、EEPROM EDID を効果的にオーバーライドします。

ここで説明されているように、EDID 情報を置き換えるだけでなく、ベンダーはモニター名と推奨される表示解像度を上書きすることができます。 このような上書きは、出荷ボックスの Windows Update またはデジタルメディアを使用して、多くの場合、顧客に提供されます。 このようなオーバーライドは、ここで説明した EDID の上書きよりも優先順位が高くなります。 これを実現するためのガイドラインについては、「 [MONITOR INF File」セクション](monitor-inf-file-sections.md)を参照してください。

## <a name="span-idedid_formatspanspan-idedid_formatspanspan-idedid_formatspanedid-format"></a><span id="EDID_format"></span><span id="edid_format"></span><span id="EDID_FORMAT"></span>EDID 形式


EDID データは1つ以上の128バイトのブロックとして書式設定されます。

-   EDID のバージョン1.0 から1.2 は、VESA 仕様に従って、1つのデータブロックで構成されています。
-   EDID バージョン1.3 または拡張 EDID (E EDID) を使用すると、製造元はプライマリブロックに加えて、1つまたは複数の拡張ブロックを指定できます。

各ブロックには、最初のブロックに対して0から始まる番号が付けられます。 EDID 情報を更新するには、製造元の INF で、更新するブロックの番号を指定します。また、元のブロックを置き換えるために、128バイトの EDID データを提供します。 モニタドライバは、修正されたブロックの更新されたデータをレジストリから取得し、残りのブロックには EEPROM データを使用します。

## <a name="span-idupdating_an_edidspanspan-idupdating_an_edidspanspan-idupdating_an_edidspanupdating-an-edid"></a><span id="Updating_an_EDID"></span><span id="updating_an_edid"></span><span id="UPDATING_AN_EDID"></span>EDID の更新


INF を使用して EDID を更新するには、次のようにします。

1.  モニターの製造元は、更新された EDID 情報を含む INF を実装し、ファイルをユーザーのコンピューターにダウンロードします。 これを行うには Windows Update を使用するか、モニターを使用して CD を発送します。
2.  Monitor クラスインストーラーは、更新された EDID 情報を INF から抽出し、その情報を次のレジストリキーの値として格納します。

    ```registry
    HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Enum\DISPLAY
    ```

    各 EDID オーバーライドは、個別のキーの下に格納されます。 次に、例を示します。

    ```registry
    HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Enum\DISPLAY\DELA007\
          5&1608c50f&0&10000090&01&20\Device Parameters\EDID_Override
    ```

3.  モニタードライバーは、初期化中にレジストリを確認し、EEPROM に対応する情報ではなく、そこに格納されている EDID 情報を使用します。 レジストリに追加された EDID 情報は、常に EEPROM の EDID 情報よりも優先されます。
4.  Windows コンポーネントとユーザーモードアプリは、更新された EDID 情報を使用します。

## <a name="span-idoverriding_an_edid_with_an_infspanspan-idoverriding_an_edid_with_an_infspanspan-idoverriding_an_edid_with_an_infspanoverriding-an-edid-with-an-inf"></a><span id="Overriding_an_EDID_with_an_INF"></span><span id="overriding_an_edid_with_an_inf"></span><span id="OVERRIDING_AN_EDID_WITH_AN_INF"></span>SYSPREP.INF を使用した EDID のオーバーライド


EDID をオーバーライドするには、次の形式で、オーバーライドする各ブロックの INF に[**AddReg ディレクティブ**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-addreg-directive)を含めます。

```inf
HKR, EDID_OVERRIDE, BlockNumber, 0x1, Byte 1, Byte 2, Byte 3, Byte 4,...
```

ブロック番号は、オーバーライドする EDID ブロックの0から始まるインデックス値です。 データバイトは、バイナリ EDID データを含む 128 16 進数の整数として書式設定する必要があります。 ブロック番号の後の "0x1" 値は、このレジストリ値にバイナリデータ (FLG_ADDREG_BINVALUETYPE) が含まれていることを示すフラグです。

製造元は、正しくない EDID ブロックだけを更新する必要があります。 システムは、残りのブロックを EEPROM から取得します。 次の例は、EDID ブロック0、4、および5を更新する INF の関連セクションを示しています。 モニタードライバーは、ブロック5に続くすべての拡張ブロックを EEPROM から 1-3 取得します。

```inf
[ABC.DDInstall.HW]
ABC.AddReg
...
[ABC.AddReg]
HKR, EDID_OVERRIDE, 0, 1, 00, FF, ..., 3B
HKR, EDID_OVERRIDE, 4, 1, 1F, 3E, ..., 4E
HKR, EDID_OVERRIDE, 5, 1, 24, 5C, ..., 2D
...
```

一般的な Inf、特に**AddReg**と**ddinstall**の詳細については、「 [inf ファイルの作成](https://docs.microsoft.com/windows-hardware/drivers/hid/creating-an-inf-file)」を参照してください。

```inf
; monsamp.INF
;
; Copyright (c) Microsoft Corporation.  All rights reserved.
;
; This is a generic INF file for overriding EDIDs 
; of any monitors, starting with Windows Vista.
;

[Version]
signature="$WINDOWS NT$"
Class=Monitor
ClassGuid={4D36E96E-E325-11CE-BFC1-08002BE10318}
Provider="MS_EDID_OVERRIDE"
DriverVer=04/18/2006, 1.0.0.0

; Be sure to add the directive below with the proper catalog file after 
; WHQL certification.
;CatalogFile=Sample.cat


[DestinationDirs]
DefaultDestDir=23

[SourceDisksNames]
1=%SourceDisksNames%

; Enable the following section to copy a monitor profile.
[SourceDisksFiles]
;profile1.icm=1

[Manufacturer]
%MS_EDID_OVERRIDE%=MS_EDID_OVERRIDE,NTx86,NTamd64

; Modify the hardware ID (MON1234) to match that of the monitor being used.
[MS_EDID_OVERRIDE.NTx86]
%MS_EDID_OVERRIDE-1%=MS_EDID_OVERRIDE-1.Install, MONITOR\MON1234

; Modify the hardware ID (MON1234) to match that of the monitor being used.
[MS_EDID_OVERRIDE.NTamd64]
%MS_EDID_OVERRIDE-1%=MS_EDID_OVERRIDE-1.Install.NTamd64, MONITOR\MON1234

[MS_EDID_OVERRIDE-1.Install.NTx86]
DelReg=DEL_CURRENT_REG
AddReg=MS_EDID_OVERRIDE-1.AddReg, 1024, 1280, DPMS
CopyFiles=MS_EDID_OVERRIDE-1.CopyFiles

[MS_EDID_OVERRIDE-1.Install.NTamd64]
DelReg=DEL_CURRENT_REG
AddReg=MS_EDID_OVERRIDE-1.AddReg, 1024, 1280, DPMS
CopyFiles=MS_EDID_OVERRIDE-1.CopyFiles

[MS_EDID_OVERRIDE-1.Install.NTx86.HW]
AddReg=MS_EDID_OVERRIDE-1_AddReg

[MS_EDID_OVERRIDE-1.Install.NTamd64.HW]
AddReg=MS_EDID_OVERRIDE-1_AddReg

[MS_EDID_OVERRIDE-1_AddReg]
HKR,EDID_OVERRIDE,"0",0x01,0x00,0xFF,0xFF,0xFF,0xFF,0xFF,0xFF,0x00,0x35,\
0xEE,0x34,0x12,0x01,0x00,0x00,0x00,0x0A,0x0E,0x01,0x03,0x68,0x22,0x1B,\
0x78,0xEA,0xAE,0xA5,0xA6,0x54,0x4C,0x99,0x26,0x14,0x50,0x54,0xA5,0x4B,\
0x00,0x71,0x4F,0x81,0x80,0xA9,0x40,0x01,0x01,0x01,0x01,0x01,0x01,0x01,\
0x01,0x01,0x01,0x30,0x2A,0x00,0x98,0x51,0x00,0x2A,0x40,0x30,0x70,0x13,\
0x00,0x52,0x0E,0x11,0x00,0x00,0x1E,0x00,0x00,0x00,0xFF,0x00,0x41,0x42,\
0x30,0x30,0x30,0x30,0x30,0x30,0x30,0x30,0x30,0x31,0x0A,0x00,0x00,0x00,\
0xFC,0x00,0x4D,0x53,0x20,0x31,0x32,0x33,0x34,0x0A,0x0A,0x0A,0x0A,0x0A,\
0x0A,0x00,0x00,0x00,0xFD,0x00,0x38,0x4C,0x1F,0x50,0x12,0x00,0x0A,0x20,\
0x20,0x20,0x20,0x20,0x20,0x00,0xDB

[DEL_CURRENT_REG]
HKR,MODES
HKR,,MaxResolution
HKR,,DPMS
HKR,,ICMProfile

; Pre-defined AddReg sections. These can be used for default settings 
; when a given standard resolution is used.

[1024]
HKR,,MaxResolution,,"1024,768"
[1280]
HKR,,MaxResolution,,"1280,1024"

[DPMS]
HKR,,DPMS,,1

[MS_EDID_OVERRIDE-1.AddReg]
HKR,"MODES\1024,768",Mode1,,"31.0-94.0,55.0-160.0,+,+"
HKR,"MODES\1280,1024",Mode1,,"31.0-94.0,55.0-160.0,+,+"

; Enable the following section to copy a monitor profile.
[MS_EDID_OVERRIDE-1.CopyFiles]
;PROFILE1.ICM

[Strings]
MonitorClassName="Monitor"
SourceDisksNames="MS_EDID_OVERRIDE Monitor EDID Override Installation Disk"

MS_EDID_OVERRIDE="MS_EDID_OVERRIDE"
MS_EDID_OVERRIDE-1="MS EDID Override"
```

 

 





