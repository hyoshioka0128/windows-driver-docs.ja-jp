---
title: UVC INF ファイルの提供
description: UVC INF ファイルの提供
ms.assetid: 44311eb8-1035-466c-878b-a5d964b34490
keywords:
- INF ファイル WDK USB ビデオ クラス
- UVC INF ファイル WDK USB ビデオ クラス
- UVC INF ファイルのサンプル コードの WDK USB ビデオ クラス
- サンプル コード WDK USB ビデオ クラス、UVC INF ファイル
ms.date: 09/12/2018
ms.localizationpriority: medium
ms.openlocfilehash: 50ff6912c15ae7686a297bed448f8db329176fcd
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56573289"
---
# <a name="providing-a-uvc-inf-file"></a>UVC INF ファイルの提供

このセクションでは、デバイスに固有の INF ファイルのさまざまな部分を示しています。

または、拡張ユニット プラグインを登録するデバイスに固有の名前を指定する、次のような INF ファイルを使用できます。

一般に、セットアップ パッケージを提供するベンダーは、INF ファイルは、ベンダーの場合に提供しないセットアップ パッケージを使用して、プラグインの DLL を登録できます。 ドライバーの署名を簡単に特定のデバイスの INF ファイルではなくのセットアップ パッケージを提供する場合があります。

注意、ただし、INF ファイルを使用してこの特定のサンプルをインストールする必要があります。

これを行うには、次のコード ファイルに含める、INF 任意という名前*Xuplgin.inf*:

```INF
; Copyright (c) CompanyName. All rights reserved.

[Version]
Signature="$CHICAGO$"
Class=Image
ClassGUID={6bdd1fc6-810f-11d0-bec7-08002be2092f}
Provider=%CompanyName%

[SourceDisksNames]
1=%Package%

[SourceDisksFiles.x86]
MyPlugin.ax=1

[ControlFlags]
ExcludeFromSelect=*

[DestinationDirs]
MyDevice.CopyList=11    ; %systemroot%\system32 on 
   NT-based systems

[Manufacturer]
%CompanyName%=CompanyName
```

デバイスに固有の INF ファイルは VID/PID 識別子に基づいて、デバイスと一致します。 この場合、デバイスに固有の INF ファイルよりも優先*Usbvideo.inf*します。

```INF
[CompanyName]
%MyDevice.DeviceDesc%=MyDevice,USB\Vid_XXXX&Pid_XXXX&MI_XX

[MyDevice.NT]
Include=usbvideo.inf, ks.inf, kscaptur.inf, dshowext.inf
Needs=USBVideo.NT, KS.Registration, KSCAPTUR.Registration.NT,
DSHOWEXT.Registration
AddReg=MyDevice.Plugins
CopyFiles=MyDevice.CopyList
```

INF ファイルの次の部分は表示拡張機能ノード ベース ユニットのレジストリ エントリをプラグインします。 参照してください*Usbvideo.inf*例については似ています。

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

```INF
[MyDevice.NT.Interfaces]
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

デバイス インターフェイスのレジストリ キーの場所には、DWORD レジストリ エントリが含まれている場合、USB カメラ**EnableDependentStillPinCapture**写真撮影の 0 以外の値を含むこのような cameras で依存 pin が使用されます。 レジストリ エントリが存在しない場合は 0 に設定すると、依存 pin は使用されません。 写真のキャプチャを実行する代わりに、プレビューの暗証番号 (pin) から取得したフレームを使用します。

呼ばれるオプションのレジストリ値を定義することもできます。 **UvcFlags**します。 **UvcFlags** DWORD の値を指定する必要があります。 デバイスを接続、UVC ドライバーは、プラグ アンド プレイ (PnP) 開始要求を受信します。 ドライバーを検索し、 **UvcFlags**デバイスのレジストリ キーにします。 DWORD 値はビットマスクを指定し、次の表の値を含めることができます。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p><strong>ビットマスクの名前</strong></p></td>
<td><p><strong>値</strong></p></td>
<td><p><strong>[説明]</strong></p></td>
</tr>
<tr class="even">
<td><p>WORKAROUNDS_DV_INTERLEAVED_DEFAULT_MASK</p></td>
<td><p>0x00000001</p></td>
<td><p>UVC は、ビデオのみのデータの範囲とインターリーブ DV データ範囲をサポートしています。 このビットマスクをインターリーブ DV に設定します。</p></td>
</tr>
<tr class="odd">
<td><p>WORKAROUNDS_SUPPRESS_CLOCK_MASK</p></td>
<td><p>0x00000002</p></td>
<td><p>現在は使用されません。</p></td>
</tr>
<tr class="even">
<td><p>WORKAROUNDS_MPEG2TS_SUPPORT_FID</p></td>
<td><p>0x00000004</p></td>
<td><p>FID マスクは、ストリーム ヘッダーが、FID ビットが含まれていることを示します。</p></td>
</tr>
<tr class="odd">
<td><p>WORKAROUNDS_MPEG2TS_SUPPORT_EOF</p></td>
<td><p>0x00000008</p></td>
<td><p>EOF マスクでは、ペイロードのヘッダーが、最後のフレームのビットを含めることを示します。</p></td>
</tr>
<tr class="even">
<td><p>WORKAROUNDS_VARIABLE_FRAME_RATE_MASK</p></td>
<td><p>0x00000010</p></td>
<td><p>フレーム レート、デバイスが異なる場合は、このマスクを設定します。 固定レート DV デバイスがこのマスクを設定しないでください。</p></td>
</tr>
</tbody>
</table>

 

適用されるビットマスクを指定する次の例のような行を含めます。

```INF
HKR,,UvcFlags,0x00010001,0x00000010
```

UVC ドライバーでは、Windows Server 2003 と Windows Vista またはそれ以降のバージョンのオペレーティング システムを使用している場合は、mpeg-2 TS などのストリーム ベースの形式で FID と EOF マスクを使用できます。

低フレーム レートの条件で EOF ビットは、次のフレームの FID ビットよりも高速完了を報告場合があります。 EOF ビットは、mpeg-2 フレームの配信の待機時間を短縮できます。

AddReg ディレクティブの位置指定の構文の詳細については、[ **INF AddReg ディレクティブ**](https://msdn.microsoft.com/library/windows/hardware/ff546320)を参照してください。

```INF
[MyDevice.NT.Services]
AddService = usbvideo,0x00000002,MyDevice.ServiceInstall

[MyDevice.ServiceInstall]
DisplayName   = %USBVideo.SvcDesc%
ServiceType   = %SERVICE_KERNEL_DRIVER%
StartType     = %SERVICE_DEMAND_START%
ErrorControl  = %SERVICE_ERROR_NORMAL%
ServiceBinary = %10%\System32\Drivers\usbvideo.sys

[MyDevice.CopyList]
MyPlugin.ax
```

```INF
[Strings]
; Non-localizable
Plugin.CLSID="{zzzzzzzz-zzzz-zzzz-zzzz-zzzzzzzzzzzz}"
ProxyVCap.CLSID="{17CCA71B-ECD7-11D0-B908-00A0C9223196}"
XU_GUID="{xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx}"
KSCATEGORY_RENDER="{65E8773E-8F56-11D0-A3B9-00A0C9223196}"
KSCATEGORY_CAPTURE="{65E8773D-8F56-11D0-A3B9-00A0C9223196}"
KSCATEGORY_VIDEO="{6994AD05-93EF-11D0-A3CC-00A0C9223196}"
SERVICE_KERNEL_DRIVER=1
SERVICE_DEMAND_START=3
SERVICE_ERROR_NORMAL=1

; Localizable
CompanyName="CompanyName"
Package="Installation Package"
MyDevice.DeviceDesc="CompanyName Camera"
USBVideo.SvcDesc="USB Video Device (WDM)"

PlugIn_IMyExtensionUnit="CompanyName Extension Unit Interface"
```
