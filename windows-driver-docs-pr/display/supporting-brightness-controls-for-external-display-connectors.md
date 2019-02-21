---
title: コネクタの外付けディスプレイの明るさコントロール
description: この機能は、外部のコネクタのディスプレイの明るさコントロールをサポートしている Windows に示すために Oem のみできます。
keywords:
- WDK のディスプレイの明るさ
- Acpi の明るさのホット キー WDK の表示
- WDK の表示の明るさのホット キーを通知します。
- BIOS の明るさコントロール WDK の表示
- 自動明るさ WDK の表示
ms.date: 12/06/2018
ms.localizationpriority: medium
ms.custom: seodec18
ms.openlocfilehash: 33a85da16641344aea282f7ffff9ec8792220ee2
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56561127"
---
# <a name="brightness-controls-for-external-display-connectors"></a>コネクタの外付けディスプレイの明るさコントロール

一部の OEM システムでは、HDMI などの外部のコネクタを使用して接続されている内部の表示があります。 Windows では、それらの構成では、システム ソフトウェアの輝度をサポートするために 1 つだけ表示パネルを指定する機能があります。
この機能は、外部のコネクタのディスプレイの明るさコントロールをサポートしている Windows に示すために Oem のみを許可します。Oem のハードウェアの輝度を実装およびのように、グラフィックス ドライバーを使用した統合をする必要がありますが、[コネクタの表示を統合](https://docs.microsoft.com/windows-hardware/drivers/display/supporting-brightness-controls-on-integrated-display-panels)します。 また、この機能には複数表示パネルの個々 のパネルの輝度を制御することはできません。


### <a name="general-requirements"></a>一般的な要件

新しい DWORD レジストリ値が追加されます。"BrightnessControl"。
レジストリ パス:HKLM\SYSTEM\CurrentControlSet\Control\Class\{4D36E96E-E325-11CE-BFC1-08002BE10318} 対象となる個々 の表示用 \XXXX XXXX 場所は。  


*   このレジストリ値の最初のビットは、非内部モニターの明るさコントロールのサポートを定義します。
*   2 番目のビットは、使用する ACPI の明るさを強制する ACPI オーバーライドを定義します。
*   残りの 30bits は予約されており、0 にする必要があります。  

非内部パネルの輝度を有効にするには Oem が独自 monitor.inf を出荷する必要があります (を参照してください inf 以下のサンプル) し、このレジストリ値を適切に設定します。 

必要な場合に Oem だけ"BrightnessControl"レジストリ値を定義する必要があります。 

明るさをサポートするコントロールの変更 (最初のビット) は、任意のディスプレイ アダプターでは、内部コネクタ型に内部の表示がないシステムでのみ使用する必要があります。 場合は、システムでは、内部の表示を内部コネクタは、型がある、最初の列挙型の表示は、明るさコントロールに表示されます。


### <a name="acpi-brightness-override"></a>ACPI の明るさの上書き

ACPI の明るさの上書き明るさコントロールの使用に推奨されるメカニズムがない状況で、完全を期すのために用意されて輝度の他のオプションが存在しません。

ACPI の上書き (2 番目のビット) は、内部および外部の両方の表示では有効が、システム上の 1 つだけの表示にのみ適用する必要があります。

ACPI の上書きは、ディスプレイ ドライバーが輝度調整機能サポートを既に提供されない場合に、明るさ対象の上書きと組み合わせて使用してにするためのものです。  これにより、Oem は ACPI を使用して、独自の表示バックライトの制御を実装できます。 

ACPI 上書きのセカンダリ用途は、輝度調整機能サポートがモバイル システムのいくつかの一般的な理由で発生することが失敗したときに、OS/ドライバーの開発中です。 ここでは、ACPI オーバーライドでは、のみ、暫定的なソリューションです。完成した製品のドライバーの輝度を使用してください。

外部のコネクタのこのレジストリ値が設定されている場合は、OS は公開されている 1 つの明るさコントロールに、システムに制限されます。


### <a name="sample-monitorinf-file-fragment"></a>サンプルのモニタ。INF ファイルのフラグメント

上記で説明されている不完全なサンプル INF を次に示します。

```inf
[Manufacturer]
%MONOEM%=MONOEM,NTx86,NTAMD64 
 
[MONOEM]  
%AIOHDMI_1%  = AIO_HDMI_1, Monitor\OEM1001
%AIOHDMI_2%  = AIO_HDMI_2, Monitor\OEM1002
%Laptop%  = Laptop_1, Monitor\OEM2001
 
[MONOEM.NTx86]
%AIOHDMI_1%  = AIO_HDMI_1, Monitor\OEM1001
%AIOHDMI_2%  = AIO_HDMI_2, Monitor\OEM1002
%Laptop%  = Laptop_1, Monitor\OEM2001
 
[MONOEM.NTAMD64]  
%AIOHDMI_1%  = AIO_HDMI_1, Monitor\OEM1001
%AIOHDMI_2%  = AIO_HDMI_2, Monitor\OEM1002
%Laptop%  = Laptop_1, Monitor\OEM2001
 
[ControlFlags]
ExcludeFromSelect = *
 
[AIO_HDMI_1]
AddReg= AIO_HDMI_1_Driver_Brightness
 
[AIO_HDMI_2]
AddReg= AIO_HDMI_2_ACPI_Brightness
 
[Laptop_1]
AddReg=Laptop_ACPI_Driver_Brightness
                                                                                     
 
; Override brightness to control the HDMI built into the all-in-one system under graphics driver control
[AIO_HDMI_1_Driver_Brightness]
HKR,,BrightnessControl,%REG_DWORD%,%OVERRIDE_BRIGHTNESS_TARGET%
 
; Override brightness to control the HDMI built into the all-in-one system under ACPI firmware control
[AIO_HDMI_2_ACPI_Brightness]
HKR,,BrightnessControl,%REG_DWORD%,%OVERRIDE_BRIGHTNESS_TARGET_AND_CONTROL_TO_ACPI%
 
; Override brightness to control the internal panel under ACPI firmware control instead of the driver
[Laptop_ACPI_Driver_Brightness]
HKR,,BrightnessControl,%REG_DWORD%,%OVERRIDE_BRIGHTNESS_CONTROL_TO_ACPI%
 
[Strings]
; Non-localizable
REG_DWORD = 0x00010001
OVERRIDE_BRIGHTNESS_TARGET = 1
OVERRIDE_BRIGHTNESS_CONTROL_TO_ACPI = 2
OVERRIDE_BRIGHTNESS_TARGET_AND_CONTROL_TO_ACPI = 3
 
; Localizable
MONOEM = “Manufacturer name” 
AIOHDMI_1  = “AIO monitor name one”
AIOHDMI_2  = “AIO monitor name two”
Laptop  = “Laptop monitor name”
```


> [!NOTE]
> Oem は、汎用的な Microsoft monitor.inf が使用されないようにするには、適切なハードウェア ID を持つ monitor.inf ファイルを提供する必要があります。 
