---
title: UVC INF ファイルの提供
description: UVC INF ファイルの提供
ms.assetid: 44311eb8-1035-466c-878b-a5d964b34490
keywords:
- INF ファイル WDK USB ビデオクラス
- UVC INF ファイル WDK USB ビデオクラス
- UVC INF ファイル WDK USB ビデオクラス、サンプルコード
- サンプルコード WDK USB ビデオクラス、UVC INF ファイル
ms.date: 09/12/2018
ms.localizationpriority: medium
ms.openlocfilehash: daee1d82ff9f64741fcb92a843e3bc900c2f8ae4
ms.sourcegitcommit: 48c4b6d3a504583d2f588ed892a4a281d4b58301
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/06/2019
ms.locfileid: "70387067"
---
# <a name="providing-a-uvc-inf-file"></a>UVC INF ファイルの提供

このセクションでは、デバイス固有の INF ファイルのさまざまな部分について説明します。

このような INF ファイルは、デバイス固有の名前を指定したり、拡張機能単体プラグインを登録したりするために使用できます。

一般に、セットアップパッケージを提供するベンダーは、セットアップパッケージを使用してプラグイン DLL を登録できます。この場合、ベンダーは INF ファイルを提供しません。 ドライバーの署名については、デバイス固有の INF ファイルではなく、セットアップパッケージを使用する方が簡単な場合があります。

ただし、INF ファイルを使用してこの特定のサンプルをインストールする必要があることに注意してください。

これを行うには、 *Xuplgin*という名前の次のコードを INF ファイルに追加します。

```INF
; Copyright (c) CompanyName. All rights reserved.

[Version]
Signature="$Windows NT$"
Class=Image
ClassGUID={6bdd1fc6-810f-11d0-bec7-08002be2092f}
Provider=%CompanyName%

[SourceDisksNames]
1=%Package%

[SourceDisksFiles]
MyPlugin.ax=1

[ControlFlags]
ExcludeFromSelect=*

[DestinationDirs]
MyDevice.CopyList=11    ; %systemroot%\system32 on NT-based systems

[Manufacturer]
%CompanyName%=CompanyName,NT$ARCH$
```

デバイス固有の INF ファイルは、VID/PID 識別子に基づいてデバイスと照合されます。 この場合、デバイス固有の INF ファイルの方が*Usbvideo .inf*よりも優先されます。

```INF
[CompanyName.NT$ARCH$]
%MyDevice.DeviceDesc%=MyDevice,USB\Vid_XXXX&Pid_XXXX&MI_XX

[MyDevice]
Include=usbvideo.inf, ks.inf, kscaptur.inf, dshowext.inf
Needs=USBVideo.NT, KS.Registration, KSCAPTUR.Registration.NT, DSHOWEXT.Registration
AddReg=MyDevice.Plugins
CopyFiles=MyDevice.CopyList
```

INF には、プラグインをシステムフォルダーにコピーするための CopyFiles セクションも必要です。
```INF
[MyDevice.CopyList]
MyPlugin.ax
```

次の INF AddReg セクションの最初の部分では、プラグインを登録します。  このセクションの残りの部分では、ノードベースの拡張機能単体プラグインのレジストリエントリを示します。 同様の例については、「 *Usbvideo .inf* 」を参照してください。

```INF
[MyDevice.PlugIns]
HKCR,CLSID\%Plugin.CLSID%,,,%PlugIn_IExtensionUnit%
HKCR,CLSID\%Plugin.CLSID%\InprocServer32,,,MyPlugin.ax
HKCR,CLSID\%Plugin.CLSID%\InprocServer32,ThreadingModel,,Both

; The IID is aggregated onto the node given the GUID of the property set
HKLM,System\CurrentControlSet\Control\NodeInterfaces\%XU_GUID%,,,
   %PlugIn_IExtensionUnit%
; IID in Little-Endian form
HKLM,System\CurrentControlSet\Control\NodeInterfaces\%XU_GUID%,IID,
   1,yy,yy,yy,yy,yy,yy,yy,yy,yy,yy,yy,yy,yy,yy,yy,yy
;CLSID in Little-Endian form
HKLM,System\CurrentControlSet\Control\NodeInterfaces\%XU_GUID%,
   CLSID,1,zz,zz,zz,zz,zz,zz,zz,zz,zz,zz,zz,zz,zz,zz,zz,zz
```

次の INF セクションは、インターフェイス固有のレジストリエントリを設定する方法を示しています。

```INF
[MyDevice.Interfaces]
AddInterface=%KSCATEGORY_CAPTURE%,GLOBAL,MyDevice.Interface
AddInterface=%KSCATEGORY_RENDER%,GLOBAL,MyDevice.Interface
AddInterface=%KSCATEGORY_VIDEO%,GLOBAL,MyDevice.Interface

[MyDevice.Interface]
AddReg=MyDevice.Interface.AddReg
 
[MyDevice.Interface.AddReg]
HKR,,CLSID,,%ProxyVCap.CLSID%
HKR,,FriendlyName,,%MyDevice.DeviceDesc%
HKR,,RTCFlags,0x00010001,0x00000010
```

USB カメラの場合、デバイスインターフェイスのレジストリキーの場所に0以外の値の DWORD レジストリエントリ**EnableDependentStillPinCapture**が含まれていると、そのカメラの依存ピンが写真のキャプチャに使用されます。 レジストリエントリが存在しない場合、または0に設定されている場合は、依存する pin は使用されません。 代わりに、プレビューピンから撮影したフレームを使用して写真キャプチャが実行されます。  次の例では、依存する静止ピンキャプチャを有効にします。

```INF
HKR,,EnableDependentStillPinCapture,0x00010001,1
```

**Uvcflags**というオプションのレジストリ値を定義することもできます。 **Uvcflags**は DWORD 値である必要があります。 デバイスが接続されると、UVC ドライバーは、プラグアンドプレイ (PnP) の開始要求を受信します。 次に、ドライバーはデバイスのレジストリキーで**Uvcflags**を検索します。 DWORD 値はビットマスクで、次の表に示す値を含めることができます。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p><strong>ビットマスク名</strong></p></td>
<td><p><strong>値</strong></p></td>
<td><p><strong>[説明]</strong></p></td>
</tr>
<tr class="even">
<td><p>WORKAROUNDS_DV_INTERLEAVED_DEFAULT_MASK</p></td>
<td><p>0x00000001</p></td>
<td><p>UVC では、ビデオのみのデータ範囲とインターリーブ DV データ範囲がサポートされています。 インターリーブ DV 用にこのビットマスクを設定します。</p></td>
</tr>
<tr class="odd">
<td><p>WORKAROUNDS_SUPPRESS_CLOCK_MASK</p></td>
<td><p>0x00000002</p></td>
<td><p>現在使用されていません。</p></td>
</tr>
<tr class="even">
<td><p>WORKAROUNDS_MPEG2TS_SUPPORT_FID</p></td>
<td><p>0x00000004</p></td>
<td><p>FID マスクは、ストリームヘッダーに FID ビットが含まれていることを示します。</p></td>
</tr>
<tr class="odd">
<td><p>WORKAROUNDS_MPEG2TS_SUPPORT_EOF</p></td>
<td><p>0x00000008</p></td>
<td><p>EOF マスクは、ペイロードヘッダーにフレーム終端ビットが含まれていることを示します。</p></td>
</tr>
<tr class="even">
<td><p>WORKAROUNDS_VARIABLE_FRAME_RATE_MASK</p></td>
<td><p>0x00000010</p></td>
<td><p>デバイスのフレームレートが変化する可能性がある場合は、このマスクを設定します。 固定レート DV デバイスでは、このマスクを設定しないでください。</p></td>
</tr>
</tbody>
</table>

 

適用するビットマスクを指定するには、次の例のような行を含めます。

```INF
HKR,,UvcFlags,0x00010001,0x00000010
```

Windows Server 2003 および Windows Vista 以降のバージョンのオペレーティングシステムで UVC ドライバーを使用している場合は、(MPEG-2 TS などの) ストリームベースの形式で FID および EOF マスクを使用できます。

フレームレートが低い状況では、EOF ビットが、次のフレームの FID ビットよりも完了を報告する場合があります。 EOF ビットを使用すると、MPEG 2 フレームの配信の待機時間を短縮できます。

AddReg ディレクティブの位置指定構文の詳細については、「 [**INF AddReg ディレクティブ**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-addreg-directive)」を参照してください。

この最後のセクションでは、INF の定義が不足しています。

```INF
[Strings]
; Non-localizable
Plugin.CLSID="{zzzzzzzz-zzzz-zzzz-zzzz-zzzzzzzzzzzz}"
ProxyVCap.CLSID="{17CCA71B-ECD7-11D0-B908-00A0C9223196}"
XU_GUID="{xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx}"
KSCATEGORY_RENDER="{65E8773E-8F56-11D0-A3B9-00A0C9223196}"
KSCATEGORY_CAPTURE="{65E8773D-8F56-11D0-A3B9-00A0C9223196}"
KSCATEGORY_VIDEO="{6994AD05-93EF-11D0-A3CC-00A0C9223196}"

; Localizable
CompanyName="CompanyName"
Package="Installation Package"
MyDevice.DeviceDesc="CompanyName Camera"

PlugIn_IMyExtensionUnit="CompanyName Extension Unit Interface"
```
