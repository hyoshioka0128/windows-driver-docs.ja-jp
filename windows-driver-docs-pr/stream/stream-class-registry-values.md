---
title: ストリーム クラスのレジストリ値
description: ストリーム クラスのレジストリ値
ms.assetid: a6800f53-4d55-4a28-839b-47f0cecc17bf
keywords:
- Stream.sys クラス ドライバー WDK Windows 2000 のカーネルでは、レジストリ
- ストリーミング ミニドライバー WDK Windows 2000 のカーネル、レジストリ
- WDK Windows 2000 のカーネル ストリーミング ミニドライバー、レジストリ
- レジストリの WDK ストリーミング ミニドライバー
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 880b5c596cd16d4b3ebdb8585a47e370570a9b2d
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56574526"
---
# <a name="stream-class-registry-values"></a>ストリーム クラスのレジストリ値





下のミニドライバーをインストールする*Stream.sys*、仕入先に準拠しているデバイスに固有の INF ファイルを指定する必要があります[INF ファイルの一般的な要件](https://msdn.microsoft.com/library/windows/hardware/ff547433)します。 このファイルで、ストリーム クラスで実行されているミニドライバーがデバイスに固有の特殊なレジストリ値を設定できます[ **AddReg** ](https://msdn.microsoft.com/library/windows/hardware/ff546320)セクション。 これらのレジストリ エントリがバイナリ インジケーターとして使用: 01、機能を有効にする 16 進数の値に設定します。

Stream クラス ミニドライバーでは、次のレジストリ値を使用できます。

<a href="" id="pageoutwhenunopened"></a>**PageOutWhenUnopened**  
このレジストリ エントリは、開かれていないときに、デバイス ドライバーがページングされることを示します。 デバイスは開かれていないときに、ページ アウトできません、この機能は全体のドライバーを無効になります。

<a href="" id="powerdownwhenunopened"></a>**PowerDownWhenUnopened**  
このレジストリ エントリは、開かれていない場合はことデバイスを電源にする必要がありますを示します。

<a href="" id="driverusesswenumtoload"></a>**DriverUsesSWEnumToLoad**  
ソフトウェア専用デバイス ドライバーは、デバイス ドライバーが必要であるさまざまなストリーム クラスを通知するためにこのレジストリ文字列を使用する必要があります*AddRef/DecRef*ハードウェア デバイスのドライバーよりも処理します。

次のフラグが 9 の Windows でサポートされていましたが、x、NT ベースのオペレーティング システムでは古いは。

<a href="" id="dontsuspendifstreamsarerunning"></a>**DontSuspendIfStreamsAreRunning**  
このレジストリ変数は、Windows 2000 以降の NT ベースのオペレーティング システムで廃止されています。 (時点で、このリリースでは、DirectShow power クエリをリッスンおよび低電力のクエリを受信すると、一時停止にすべてのストリームを格納します。)アプリケーションが呼び出すことによって使用されているシステムを通知できますも**SetThreadExecutionState**します。 このルーチンは、Microsoft Windows SDK ドキュメントで説明します。 また、ドライバーを使用できる[ **PoSetSystemState**](https://msdn.microsoft.com/library/windows/hardware/ff559768)します。

<a href="" id="oktohibernate"></a>**OkToHibernate**  
このレジストリ文字列で、Windows 98 で実行されているドライバーのみです。 NT ベースのオペレーティング システムでは使用されません。

抜粋を次に、 *Usbintel.inf*ファイルをこれらのレジストリ値を設定する方法を示します。 このファイルでは、UsbIntel サンプルの一部は、ドライバー開発キット (DDK) および Windows XP、Windows 7 (ビルド 7600) のように、Windows Driver Kit (WDK) で使用できます。

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

 

 




