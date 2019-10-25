---
title: ストリーム クラスのレジストリ値
description: ストリーム クラスのレジストリ値
ms.assetid: a6800f53-4d55-4a28-839b-47f0cecc17bf
keywords:
- .Sys クラスドライバー WDK Windows 2000 カーネル、レジストリ
- streaming ミニドライバー WDK Windows 2000 カーネル、レジストリ
- ミニドライバー WDK Windows 2000 カーネルストリーミング、レジストリ
- レジストリ WDK streaming ミニドライバー
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7166f776544d495aecae084703fc51317819eb50
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72837685"
---
# <a name="stream-class-registry-values"></a>ストリーム クラスのレジストリ値





ミニドライバー*の下に*インストールするには、ベンダーが[汎用の inf ファイル要件](https://docs.microsoft.com/windows-hardware/drivers/install/inf-file-sections-and-directives)に準拠したデバイス固有の inf ファイルを提供する必要があります。 このファイルでは、stream クラスで実行されているミニドライバーは、デバイス固有の[**AddReg**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-addreg-directive)セクションに特別なレジストリ値を設定できます。 これらのレジストリエントリは、バイナリインジケーターとして機能します。この機能を有効にするには、16進値01に設定します。

ストリームクラスミニドライバーは、次のレジストリ値を使用できます。

<a href="" id="pageoutwhenunopened"></a>**PageOutWhenUnopened 開かない**  
このレジストリエントリは、デバイスドライバーが開かれていないときにページアウトする必要があることを示します。 デバイスが開かれていないときにページアウトできない場合、ドライバー全体でこの機能はオフになっています。

<a href="" id="powerdownwhenunopened"></a>**PowerDownWhenUnopened 未開封**  
このレジストリエントリは、デバイスが開かれていないときに電源を切る必要があることを示します。

<a href="" id="driverusesswenumtoload"></a>**DriverUsesSWEnumToLoad**  
ソフトウェアのみのデバイスドライバーでは、このレジストリ文字列を使用して、デバイスドライバーがハードウェアデバイスドライバーとは異なる*AddRef/DecRef*処理を必要とすることをストリームクラスに通知する必要があります。

次のフラグは、Windows 9x ではサポートされていましたが、NT ベースのオペレーティングシステムでは互換性のために残されています。

<a href="" id="dontsuspendifstreamsarerunning"></a>**DontSuspendIfStreamsAreRunning**  
このレジストリ変数は、Windows 2000 以降の NT ベースのオペレーティングシステムでは廃止されています。 (このリリースでは、DirectShow は power query をリッスンし、低電力のクエリを受信したときにすべてのストリームを一時停止します)。アプリケーションは、 **SetThreadExecutionState**を呼び出すことによって、使用されていることをシステムに通知することができます。 このルーチンについては、Microsoft Windows SDK のドキュメントを参照してください。 または、ドライバーで[**Posetsystemstate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-posetsystemstate)を使用することもできます。

<a href="" id="oktohibernate"></a>**OkToHibernate**  
このレジストリ文字列は、Windows 98 で実行されているドライバーに対してのみ有効です。 NT ベースのオペレーティングシステムでは使用されません。

次に示すのは、これらのレジストリ値を設定する方法を示す、 *Usbintel .inf*ファイルから抜粋したものです。 このファイルは、UsbIntel サンプルに含まれています。 Driver Development Kit (DDK) と windows XP の windows Driver Kit (WDK) で windows 7 (ビルド 7600) から入手できます。

```INF
[Intel.USBDCam]
Include= ks.inf, kscaptur.inf
Needs= KS.Registration,KSCAPTUR.Registration
AddReg= Intel.USBDCam.AddReg
CopyFiles=Intel.USBDCam.Files.Ext
; WIA
SubClass=StillImage
DeviceType=3
DeviceSubType=0x1
Capabilities=0x00000031
DeviceData=Intel.USBDCam.DeviceData
ICMProfiles="sRGB Color Space Profile.icm"
[Intel.USBDCam.AddReg]
HKR,,DevLoader,,*ntkern
HKR,,NTMPDriver,,usbintel.sys
HKR,,PageOutWhenUnopened,3,01
; WIA
HKR,,HardwareConfig,1,1
HKR,,USDClass,,"{0527d1d0-88c2-11d2-82c7-00c04f8ec183}"
```

 

 




