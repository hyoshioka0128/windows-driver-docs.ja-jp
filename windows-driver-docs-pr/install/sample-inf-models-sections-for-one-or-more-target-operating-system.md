---
title: サンプル INF ターゲットのオペレーティング システムのセクションをモデル化します。
description: 1 つ以上のターゲット オペレーティング システム用のサンプルの INF モデル セクション
ms.assetid: bc1d9a5f-573f-4773-8716-8ac53478d0ee
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a1a11f39ddd9ea284eae37c9bcf6971a2b42b77a
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63348702"
---
# <a name="sample-inf-models-sections-for-one-or-more-target-operating-systems"></a>1 つ以上のターゲット オペレーティング システム用のサンプルの INF モデル セクション


このトピックでは、さまざまなオペレーティング システムとプラットフォームでドライバー パッケージをインストールするサンプルの INF ファイルを示します。 この INF ファイルには、次の INF セクションとディレクティブがあります。

- 修飾された[ **INF 製造元セクション**](inf-manufacturer-section.md)と各種[ **INF*モデル*セクション**](inf-models-section.md)デバイス実行している x86 ベースのシステムのインストール:

  -   Microsoft Windows 2000

  -   Windows XP

  -   Windows Vista または Windows の以降のバージョン

- 修飾された[ **INF 製造元セクション**](inf-manufacturer-section.md)と各種[ **INF*モデル*セクション**](inf-models-section.md)デバイスx86-および AMD64 インストール-ベースの Windows Vista または Windows の以降のバージョンを実行しているシステム。

- [ **INF *DDInstall***  ](inf-ddinstall-section.md)と[ * **DDInstall *。サービス**](inf-ddinstall-services-section.md)ターゲット x86-および AMD64 サービスおよびレジストリ エントリを作成する-ベースのシステムです。

- [**INF CopyFiles ディレクティブ**](inf-copyfiles-directive.md)ターゲット x86-および AMD64 プラットフォームに固有のファイルをコピーする-ベースのシステムです。

```cpp
[Version]
Signature       = "$Windows NT$"
Class           = Net
ClassGUID       = {4d36e972-e325-11ce-bfc1-08002be10318}
Provider        = %Msft%
DriverVer       = 10/01/2002,6.0.5019.0

[Manufacturer]
%Msft%          = Msft, NTx86.6.0, NTamd64.6.0

; ----------------------------------------------------------------------
; Models Section
; ----------------------------------------------------------------------

;For Windows 2000 and Windows XP

[Msft]
%NetVMini.DeviceDesc%   = NetVMini.NTx86.ndi, root\NetVMini ; Root enumerated 
%NetVMini.DeviceDesc%   = NetVMini.NTx86.ndi, {b85b7c50-6a01-11d2-b841-00c04fad5171}\NetVMini ; Toaster Bus enumerated 

;For Windows Vista and later

[Msft.NTx86.6.0]
%NetVMini.DeviceDesc%    = NetVMini.NTx86.ndi, root\NetVMini ; Root enumerated 
%NetVMini.DeviceDesc%    = NetVMini.NTx86.ndi, {b85b7c50-6a01-11d2-b841-00c04fad5171}\NetVMini ; Toaster Bus enumerated 

[Msft.NTamd64.6.0]
%NetVMini.DeviceDesc%    = NetVMini.NTamd64.ndi, root\NetVMini ; Root enumerated 
%NetVMini.DeviceDesc%    = NetVMini.NTamd64.ndi, {b85b7c50-6a01-11d2-b841-00c04fad5171}\NetVMini ; Toaster Bus enumerated 

; ----------------------------------------------------------------------
; NT x86 DDInstall and DDInstall.Service Sections
; ----------------------------------------------------------------------
[NetVMini.NTx86.ndi]
Characteristics = 0x1 ; NCF_VIRTUAL
AddReg          = NetVMini.Reg
CopyFiles       = NetVMini.NTx86.CopyFiles

[NetVMini.NTx86.ndi.Services]
AddService      = NetVMini, 2, NetVMini.NTx86.Service

[NetVMini.NTx86.Service]
DisplayName     = %NetVMini.Service.DispName%
ServiceType     = 1 ;SERVICE_KERNEL_DRIVER
StartType       = 3 ;SERVICE_DEMAND_START
ErrorControl    = 1 ;SERVICE_ERROR_NORMAL
ServiceBinary   = %12%\netvmini_32.sys
LoadOrderGroup  = NDIS
AddReg          = TextModeFlags.Reg

; ----------------------------------------------------------------------
; NT x64 DDInstall and DDInstall.Service Sections
; ----------------------------------------------------------------------
[NetVMini.NTamd64.ndi]
Characteristics = 0x1 ; NCF_VIRTUAL
AddReg          = NetVMini.Reg
CopyFiles       = NetVMini.NTamd64.CopyFiles

[NetVMini.NTamd64.ndi.Services]
AddService      = NetVMini, 2, NetVMini.NTamd64.Service

[NetVMini.NTamd64.Service]
DisplayName     = %NetVMini.Service.DispName%
ServiceType     = 1 ;SERVICE_KERNEL_DRIVER
StartType       = 3 ;SERVICE_DEMAND_START
ErrorControl    = 1 ;SERVICE_ERROR_NORMAL
ServiceBinary   = %12%\netvmini_64.sys
LoadOrderGroup  = NDIS
AddReg          = TextModeFlags.Reg

; ----------------------------------------------------------------------
; Registry Section
; ----------------------------------------------------------------------
[NetVMini.Reg]
HKR,    ,               BusNumber,           0, "0" 
HKR, Ndi,               Service,             0, "NetVMini"
HKR, Ndi\Interfaces,    UpperRange,          0, "ndis5"
HKR, Ndi\Interfaces,    LowerRange,          0, "Ethernet"

[TextModeFlags.Reg]
HKR, , TextModeFlags,    0x00010001, 0x0001

; ----------------------------------------------------------------------
; Disk/FIle Sections
; ----------------------------------------------------------------------
[SourceDisksNames]
1 = %DiskId1%,"",,

[SourceDisksFiles]
netvmini_32.sys = 1,,
netvmini_64.sys = 1,,

[DestinationDirs]
DefaultDestDir             = 12
NetVMini.NTx86.CopyFiles   = 12
NetVMini.NTamd64.CopyFiles = 12

[NetVMini.NTx86.CopyFiles]
netvmini_32.sys,,,2

[NetVMini.NTamd64.CopyFiles]
netvmini_64.sys,,,2

; ----------------------------------------------------------------------
; Strings Section
; ----------------------------------------------------------------------
[Strings]
Msft                       = "Microsoft"      

NetVMini.DeviceDesc        = "Microsoft Virtual Ethernet Adapter"
NetVMini.Service.DispName  = "Microsoft Virtual Miniport"
DiskId1                    = "Microsoft Virtual Miniport Device Installation Disk #1"
```

サンプルの INF ファイル (*MultiOS.inf*)、Windows Driver Kit (WDK) で含まれている 1 つの INF ファイルを使用して、複数のバージョンの Windows デバイスをインストールする方法を示しています。 このファイルは、 *src\\印刷\\inf\\MultiOS* WDK のディレクトリ。

 

 





