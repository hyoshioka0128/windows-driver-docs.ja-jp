---
title: モニター EDIDs、INF をオーバーライドします。
description: INF ファイルを使用して、拡張 Display Identification Data (EDID) のいずれかのモニターを上書きできます。
ms.assetid: AA7DC29B-54D5-461A-8252-600D84F0F581
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 007e804eb65b6713ae015c6ae16a506bbedc5ed6
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56581247"
---
# <a name="overriding-monitor-edids-with-an-inf"></a>モニター EDIDs、INF をオーバーライドします。


INF ファイルを使用して、拡張 Display Identification Data (EDID) のいずれかのモニターを上書きできます。 Monsamp.inf、これを行う方法を示すサンプル INF ファイルから Windows 7 (WDK バージョン 7600) Windows Driver Kit (WDK) とが指定されています。 Monsamp.inf がここに再掲します。

使用して、および Monsamp.inf を変更する方法については、[INF ファイルのセクションではモニター](monitor-inf-file-sections.md)を参照してください。

## <a name="span-idapproachestocorrectingedidsspanspan-idapproachestocorrectingedidsspanspan-idapproachestocorrectingedidsspanapproaches-to-correcting-edids"></a><span id="Approaches_to_correcting_EDIDs"></span><span id="approaches_to_correcting_edids"></span><span id="APPROACHES_TO_CORRECTING_EDIDS"></span>EDIDs を修正する方法


すべてのモニター、アナログまたはデジタル、EDID で、モニターの識別子、製造元のデータ、ハードウェア id、タイミングについては、具合などの情報が含まれていますをサポートする必要があります。 このデータは、ビデオ Electronics Standards アソシエーション (VESA) によって指定された形式で、モニターの EEPROM に格納されます。

モニタでは、Microsoft Windows のコンポーネントに EDID の提供、ドライバー、および一部のユーザー モード アプリケーションを表示します。 たとえば、初期化中にモニター ドライバーはその明るさクエリ インターフェイスおよびデバイス ドライバー インターフェイス (DDI) のサポート、EDID 内にある Windows Display Driver Model (WDDM) ドライバーを照会します。 モニターの EEPROM に正しくないか、無効な EDID の情報したがって、不適切な表示モードを設定するなどの問題につながります。

EDIDs を修正する 2 つの方法はあります。

-   標準的なソリューションでは、お客様に、モニターをユーザーに適切な EDID EEPROM reflashes を顧客にモニターを返します、製造元に送信します。
-   優れたソリューションでは、ここで説明するには、メーカー側では、適切な EDID 情報を含む INF ファイルを実装するためには、およびお客様に、モニターに接続されているコンピューターにダウンロードします。 Windows では、INF から EDID の最新の情報を抽出し、EEPROM EDID を効果的にオーバーライド、EEPROM EDID から、情報の代わりにコンポーネントを提供します。

」の説明に従って EDID 情報の置き換え、に加えて仕入先は名前とディスプレイの解像度、モニターの上書きを提供できます。 このようなオーバーライドは Windows Update または梱包された箱でデジタル メディアを使用して顧客を頻繁に提供されます。 このようなオーバーライドでは、ここで説明した EDID オーバーライドより高い優先順位を受け取ります。 これを実現するためのガイドラインが記載[INF ファイルのセクションではモニター](monitor-inf-file-sections.md)します。

## <a name="span-idedidformatspanspan-idedidformatspanspan-idedidformatspanedid-format"></a><span id="EDID_format"></span><span id="edid_format"></span><span id="EDID_FORMAT"></span>EDID 形式


EDID データは、1 つまたは複数の 128 バイトのブロックとして書式設定します。

-   EDID バージョン 1.0 ~ 1.2 は、VESA 仕様ごとのデータの 1 つのブロックで構成されます。
-   EDID version 1.3 または強化された EDID (E EDID) では、製造元は、主要なブロックだけでなく、1 つ以上の拡張機能ブロックを指定できます。

各ブロックは、最初のブロックの 0 から始まる番号が。 EDID 情報を更新するには、製造元の INF は、更新するブロックの数を指定し、128 バイトの元のブロックを置き換える EDID データを提供します。 モニター ドライバーでは、レジストリから、更新されたデータの修正後のブロックを取得し、残りのブロックの EEPROM データを使用します。

## <a name="span-idupdatinganedidspanspan-idupdatinganedidspanspan-idupdatinganedidspanupdating-an-edid"></a><span id="Updating_an_EDID"></span><span id="updating_an_edid"></span><span id="UPDATING_AN_EDID"></span>EDID を更新しています


INF を使用して、EDID を更新します。

1.  モニターの製造元は、INF を EDID の最新の情報を含み、ユーザーのコンピューターにファイルがダウンロードを実装します。 これは、Windows Update またはモニターの CD を送付して実行できます。
2.  Monitor クラスのインストーラーは、INF から EDID の最新の情報を抽出し、このレジストリ キーの値として、情報を格納します。

    ```registry
    HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Enum\DISPLAY
    ```

    各 EDID オーバーライドは、個別のキーの下に格納されます。 例:

    ```registry
    HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Enum\DISPLAY\DELA007\
          5&1608c50f&0&10000090&01&20\Device Parameters\EDID_Override
    ```

3.  モニター ドライバーでは、初期化中にレジストリを確認し、EEPROM に対応する情報ではなく保管されている任意の EDID 情報を使用します。 常に、レジストリに追加されている EDID 情報 EEPROM EDID 情報よりも優先されます。
4.  Windows コンポーネントとユーザー モードのアプリは、更新された EDID 情報を使用します。

## <a name="span-idoverridinganedidwithaninfspanspan-idoverridinganedidwithaninfspanspan-idoverridinganedidwithaninfspanoverriding-an-edid-with-an-inf"></a><span id="Overriding_an_EDID_with_an_INF"></span><span id="overriding_an_edid_with_an_inf"></span><span id="OVERRIDING_AN_EDID_WITH_AN_INF"></span>INF、EDID をオーバーライドします。


EDID をオーバーライドするには、 [ **AddReg ディレクティブ**](https://msdn.microsoft.com/library/windows/hardware/ff546320)次の形式で、無効にする各ブロックに対して、INF で。

```inf
HKR, EDID_OVERRIDE, BlockNumber, Byte 1, Byte 2, Byte 3, Byte 4,...
```

ブロックの数には、バイナリ EDID データが含まれている 128 の 16 進数の整数が続きます。

製造元は、正しくない EDID ブロックだけを更新する必要があります。 システムでは、EEPROM から、残りの要素を取得します。 次の例では、0、4、および 5 EDID ブロックを更新する、INF の関連セクションを示します。 モニター ドライバーでは、ブロック EEPROM から 5 のブロックに続く 1 ~ 3 と任意の拡張機能のブロックを取得します。

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

一般に、Inf の詳細について、 **AddReg**と**DDInstall**具体的を参照してください[INF ファイルを作成する](https://msdn.microsoft.com/library/windows/hardware/ff538378)します。

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

 

 





