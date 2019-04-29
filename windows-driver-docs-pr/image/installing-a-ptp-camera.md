---
title: PTP カメラのインストール
description: PTP カメラのインストール
ms.assetid: bf18a245-1344-47f1-83bc-3c369627bcdf
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7c0aaf85660f250c1afb8fac6479e691318c1266
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63326072"
---
# <a name="installing-a-ptp-camera"></a>PTP カメラのインストール





カメラでは、PTP をサポートする場合、WIA デバイスとしてインストールされているため、デバイスを接続が行う必要があるすべて。 Microsoft の PTP WIA ミニドライバーは、残りの部分で行われます。

追加または PTP カメラに追加する拡張機能がある場合は、INF ファイルを作成する必要があります。

INF ファイルにセクションが含まれることに注意してください。 *sti.inf*します。 これにより、今後の更新には、Microsoft *sti.inf* 、必要なときに、INF の影響を与えずにファイルします。

USB Device Working Group には、まだイメージのカメラのクラス ID 0x06 が割り当てられます。 Windows の今後のリリースで、Microsoft はこのクラスの id として PTP ドライバーをロードする INF ファイルを出荷する*互換性 ID*と一致します。 つまり、ベンダーが含む INF ファイルを配布してでカスタム ドライバーを読み込むことができますもこと、*ハードウェア ID*します。 Windows インストーラー クラス ID と一致するよりもハードウェア ID に一致する優先順位の高い配置します。 Windows では、ハードウェア ID を持つ INF ファイルが付属していない、ベンダーのドライバーは自動的に読み込まれません。 ただし、CD の自動実行プログラムを呼び出すことができます[ **UpdateDriverForPlugAndPlayDevices** ](https://msdn.microsoft.com/library/windows/hardware/ff553534)を簡単に、ベンダーのドライバーを更新します。

PTP カメラの例の INF ファイル:

```INF
; PTPCAMERA.INF  -- PTP Camera setup file
; Copyright (c) 2002 PTP Camera Company
; Manufacturer:  PTP Camera Company

[Version]
Signature=$WINDOWS NT$
Class=Image
ClassGUID={6bdd1fc6-810f-11d0-bec7-08002be2092f}
Provider=%Mfg%
DriverVer=06/26/2001,1.0
CatalogFile=wia.cat

[Manufacturer]
%Mfg%=Models

[Models]
%PTPCamera100.DeviceDesc%=PTP100, USB\VID_000&PID_0100

[PTP100]
Include=sti.inf
Needs=STI.PTPUSBSection

AddReg=PTP100.AddReg
DeviceData=PTP100.DeviceData
SubClass=StillImage
DeviceType=2
Capabilities=0x35
Events=PTP100.Events
ICMProfiles="sRGB Color Space Profile.icm"

[PTP100.Services]
Include=sti.inf
Needs=STI.USBSection.Services

[PTP100.DeviceData]
Model=PTP
QueryDeviceForName=1,1
Server=local
UI DLL=sti.dll
UI Class ID={4DB1AD10-3391-11D2-9A33-00C04FA36145}

[PTP100.Events]
Connected=%PTP.Connected%,{A28BBADE-64B6-11d2-A231-00C04FA31809},*
Disconnected=%PTP.Disconnected%,{143E4E83-6497-11d2-A231-00C04FA31809},*

[PTP100.AddReg]

[Strings]
Mfg="PTP Camera Company"
PTPCamera100.DeviceDesc="PTP Camera Model 100"
PTP.Connected="PTP Camera Connected"
PTP.Disconnected="PTP Camera Disconnected"
```

 

 




