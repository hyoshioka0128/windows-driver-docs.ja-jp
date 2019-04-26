---
title: HID over USB デバイスのセレクティブ サスペンド
description: ユニバーサル シリアル バス仕様のバージョン 2.0 では、USB のセレクティブ サスペンドの機能を指定します。
ms.assetid: A4560D7C-8A32-4A91-95B6-4377E0F0D0C1
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: db622b90b32fff0e64e92fc8738edd0939d3d0da
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63345448"
---
# <a name="selective-suspend-for-hid-over-usb-devices"></a>HID over USB デバイスのセレクティブ サスペンド


バージョン 2.0、*ユニバーサル シリアル バス仕様*USB のセレクティブ サスペンドの機能を指定します。 この機能を使用すると、Windows オペレーティング システムがアイドル状態の USB デバイスをセレクティブ サスペンドことができます。 これにより、Windows システム全体の電力を効率的に管理できます。 Windows で USB のセレクティブをサポートする方法の詳細については、機能を中断しを参照してください[USB のセレクティブ サスペンド](../usbcon/usb-selective-suspend.md)します。 (このリソースできない場合がありますのいくつかの言語および国。)

既定では、USB のセレクティブがサスペンド一貫したユーザー エクスペリエンスを提供するために、選択的から再開の待機時間を回避するために Windows では無効を中断します。

選択的なサポートを中断する HID デバイスをデザインする必要があります。

-   選択的からの復帰を一時停止とは、最初の入力、タッチ、移動、またはキーを押してを保持します。
-   選択的からのスリープ解除時に移動を中断します。
-   (該当する) 場合は、ワイヤレスのリンクを保持します。
-   CAPS lock、NUM lock などのアクティブな状態の Led に電源を管理します。
-   ユーザーが認識される遅延なく選択的からの復帰を中断します。

Windows 8 には、HID USB デバイスをセレクティブ サスペンドを有効にするための 2 つのメソッドがサポートしています。 それらは次のとおりです。

1.  **Microsoft OS ディスクリプター\[優先\]**:USB HID セレクティブ サスペンドをサポートするために必要なレジストリ キーを記述する、Microsoft OS ディスクリプターの拡張プロパティの記述子を使用できます。
2.  **ベンダー提供の INF**:ハードウェアの製造元は、適切なレジストリ キーをインストールする (HID devnode の USB ハードウェア ID に一致) する INF ファイルを提供できます。

ハードウェア ベンダーと PC 製造元のどちらが USB HID セレクティブ サスペンドを有効にする最初のオプションを使用することをお勧めします。 このオプションの利点は次のとおりです。

-   ハードウェア ベンダーと PC 製造元は、追加の INF ファイルをインストールする必要は。
-   必要なレジストリ設定は新しい Windows 8 のインストールで自動的に設定されます。
-   必要なレジストリ設定は、Windows 8 へのアップグレードで保持されます。
-   ユーザーことはできませんが失われる (または無効にする)、INF をアンインストールすることによって機能をセレクティブ サスペンドです。

ただし、ハードウェア ベンダーと PC 製造元 INF のアプローチを引き続き使用する場合は、次の例を使用できます。 Windows での HID デバイス向けには、この USB 機能を有効にする方法を示すサンプルの INF ファイルを次に示します。

```ManagedCPlusPlus
; Vendor INF File for USB HID devices
;
; A sample INF for a stand-alone USB HID device that supports 
; selective suspend

[Version]
Signature   ="$WINDOWS NT$"
Class       =HIDClass
ClassGuid   ={745a17a0-74d3-11d0-b6fe-00a0c90f57da}
Provider    =%VendorName%
DriverVer   =09/19/2008,6.0.0.0
CatalogFile =VendorXYZ.cat

; ================= Class section =====================
[ControlFlags]
ExcludeFromSelect=*

[SourceDisksNames]
1 = %DiskName%,,,""

;*****************************************
; Install Section
;*****************************************

[Manufacturer]
%VendorName% = VendorXYZDevice,NTx86,NTamd64,NTarm

[VendorXYZDevice.NTx86]
%VendorXYZ.DeviceDesc% = VendorXYZDevice_Install, USB\VID_045E&PID_00B4

[VendorXYZDevice.NTamd64]
%VendorXYZ.DeviceDesc% = VendorXYZDevice_Install, USB\VID_045E&PID_00B4

[VendorXYZDevice.NTarm]
%VendorXYZ.DeviceDesc% = VendorXYZDevice_Install, USB\VID_045E&PID_00B4


[VendorXYZDevice_Install.NT] 
include     = input.inf
needs       = HID_SelSus_Inst.NT

[VendorXYZDevice_Install.NT.HW]
include     = input.inf
needs       = HID_SelSus_Inst.NT.HW

[VendorXYZDevice_Install.NT.Services]
include     = input.inf
needs       = HID_SelSus_Inst.NT.Services

[Strings]
VendorName = "Vendor XYZ"
DiskName   = "Vendor XYZ Installation Disk"
VendorXYZ.DeviceDesc = "VendorXYZ Device"
```

各項目の意味は次のとおりです。

1.  [ **INF バージョン セクション**](https://msdn.microsoft.com/library/windows/hardware/ff547502)する必要がありますが、 **CLASSGUID**と**DriverVer**ディレクティブは次のように設定。

    -   **CLASSGUID**ディレクティブは、HID デバイスの Microsoft クラス GUID を指定する必要があります。 この GUID は、{745a17a0-74d3-11d0-b6fe-00a0c90f57da} 値を持ちます。

    -   **DriverVer**ディレクティブは、新しい日付とで指定された値よりも大きいバージョン番号を持つ値を持つ必要があります、 **DriverVer** Input.inf ディレクティブ。

2.  2. VendorXYZDevice\*のセクションでは、ベンダーの HID デバイスのハードウェア識別子 (ID) を指定します。 ハードウェア ID は、販売元の識別子 (VID) と製品 id (PID) で構成されます。 各ハードウェア ID、デバイスを製造元とデバイスに固有の VID/PID 値が必要です。 これにより、同じハードウェア ID が複数の名前と設定に対応していません

3.  3. VendorXYZDevice\_Install.NT と VendorXYZDevice\_Install.NT.HW セクションは、 [ **INF DDInstall セクション**](https://msdn.microsoft.com/library/windows/hardware/ff547344)します。 この例では、これらのセクションでは、INF を含めることが**Include**と**必要がある**ディレクティブ。

    **Include**ディレクティブ参照システム提供 Input.inf ファイル、USB のセレクティブを有効にするために必要な INF セクションが含まれますが、ベンダーの HID デバイスの機能を中断します。

    **必要がある**ディレクティブを示す Input.inf からセクションは、デバイスのインストール中に処理する必要があります。 この場合は、HID\_SelSus\_HID 既定ではなく命令セクションが選択されている\_命令のセクションで、選択的でサポートされていない中断します。

4.  4. VendorXYZDevice\_Install.NT.Services セクションは、 [ **INF DDInstall.HW セクション**](https://msdn.microsoft.com/library/windows/hardware/ff547330)します。 この例で、セクションも含まれていますと同じ値、INF の**Include**と**必要がある**ディレクティブ。

 

 




