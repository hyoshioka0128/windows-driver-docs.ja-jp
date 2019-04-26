---
title: リモート NDIS INF テンプレート
description: リモート NDIS INF テンプレート
ms.assetid: bbbd3aef-230f-4286-bea2-bb583789865e
keywords:
- リモートの NDIS WDK のネットワー キング、INF テンプレート
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e888e297ed8120e4ac36e78924ea4f159194c48a
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63350888"
---
# <a name="remote-ndis-inf-template"></a>リモート NDIS INF テンプレート





Microsoft では、NDIS ミニポート ドライバー、Rndismp.sys、リモート NDIS メッセージ セットを実装し、ジェネリック bus トランスポート ドライバーは、さらに、適切なバス ドライバーとの通信とは通信を提供します。 この NDIS ミニポート ドライバーが実装され、Microsoft によって管理されサポートされているすべての Windows バージョンの一部として配布されます。 %Systemroot% 見つかります\\System32\\ドライバー ディレクトリ。

で USB デバイスをリモートの NDIS ドライバーを使用するには、IHV は、INF ファイルでは、次のテンプレートのいずれかを指定する必要があります。

-   [NDIS 5.1 RNDIS INF テンプレート (Windows XP 以降)](#rndis-inf-template-for-ndis-51-windows-xp-and-later)
-   [NDIS 6.0 (Windows 7 以降) の RNDIS INF テンプレート](#rndis-inf-template-for-ndis-60-windows-7-and-later)

### <a name="rndis-inf-template-for-ndis-51-windows-xp-and-later"></a>NDIS 5.1 RNDIS INF テンプレート (Windows XP 以降)

```INF
; Remote NDIS template device setup file
; Copyright (c) Microsoft Corporation
;
; This is the template for the INF installation script 
; for the RNDIS-over-USB host driver.
; This INF works for Windows XP SP2, Windows XP x64, 
; Windows Server 2003 SP1 x86, x64, and ia64, and 
 ; Windows Vista x86 and x64.
; This INF will work with Windows XP, Windows XP SP1, 
; and Windows 2003 after applying specific hotfixes.

[Version]
Signature           = "$Windows NT$"
Class               = Net
ClassGUID           = {4d36e972-e325-11ce-bfc1-08002be10318}
Provider            = %Microsoft%
DriverVer           =06/21/2006,6.0.6000.16384
;CatalogFile        = device.cat

[Manufacturer]
%Microsoft%         = RndisDevices,NTx86,NTamd64,NTia64

; Decoration for x86 architecture
[RndisDevices.NTx86]
%RndisDevice%    = RNDIS.NT.5.1, USB\VID_xxxx&PID_yyyy

; Decoration for x64 architecture
[RndisDevices.NTamd64]
%RndisDevice%    = RNDIS.NT.5.1, USB\VID_xxxx&PID_yyyy

; Decoration for ia64 architecture
[RndisDevices.NTia64]
%RndisDevice%    = RNDIS.NT.5.1, USB\VID_xxxx&PID_yyyy

;@@@ This is the common setting for setup
[ControlFlags]
ExcludeFromSelect=*

; DDInstall section
; References the in-build Netrndis.inf
[RNDIS.NT.5.1]
Characteristics = 0x84   ; NCF_PHYSICAL + NCF_HAS_UI
BusType         = 15
; NEVER REMOVE THE FOLLOWING REFERENCE FOR NETRNDIS.INF
include         = netrndis.inf
needs           = Usb_Rndis.ndi
AddReg          = Rndis_AddReg_Vista

; DDInstal.Services section
[RNDIS.NT.5.1.Services]
include     = netrndis.inf
needs       = Usb_Rndis.ndi.Services

; Optional registry settings. You can modify as needed.
[RNDIS_AddReg_Vista] 
HKR, NDI\params\VistaProperty, ParamDesc,  0, %Vista_Property%
HKR, NDI\params\VistaProperty, type,       0, "edit"
HKR, NDI\params\VistaProperty, LimitText,  0, "12"
HKR, NDI\params\VistaProperty, UpperCase,  0, "1"
HKR, NDI\params\VistaProperty, default,    0, " "
HKR, NDI\params\VistaProperty, optional,   0, "1"

; No sys copyfiles - the sys files are already in-build 
; (part of the operating system).

; Modify these strings for your device as needed.
[Strings]
Microsoft             = "Microsoft Corporation"
RndisDevice           = "Remote NDIS based Device"
Vista_Property        = "Optional Vista Property"
```

### <a name="rndis-inf-template-for-ndis-60-windows-7-and-later"></a>NDIS 6.0 (Windows 7 以降) の RNDIS INF テンプレート

```INF
; Remote NDIS template device setup file
; Copyright (c) Microsoft Corporation
;
; This is the template for the INF installation script  for the RNDIS-over-USB
; host driver that leverages the newer NDIS 6.x miniport (rndismp6.sys) for
; improved performance. This INF works for Windows 7, Windows Server 2008 R2,
; and later operating systems on x86, amd64 and ia64 platforms.

[Version]
Signature           = "$Windows NT$"
Class               = Net
ClassGUID           = {4d36e972-e325-11ce-bfc1-08002be10318}
Provider            = %Microsoft%
DriverVer           = 07/21/2008,6.0.6000.16384
;CatalogFile        = device.cat

[Manufacturer]
%Microsoft%         = RndisDevices,NTx86,NTamd64,NTia64

; Decoration for x86 architecture
[RndisDevices.NTx86]
%RndisDevice%    = RNDIS.NT.6.0, USB\VID_xxxx&PID_yyyy

; Decoration for x64 architecture
[RndisDevices.NTamd64]
%RndisDevice%    = RNDIS.NT.6.0, USB\VID_xxxx&PID_yyyy

; Decoration for ia64 architecture
[RndisDevices.NTia64]
%RndisDevice%    = RNDIS.NT.6.0, USB\VID_xxxx&PID_yyyy

;@@@ This is the common setting for setup
[ControlFlags]
ExcludeFromSelect=*

; DDInstall section
; References the in-build Netrndis.inf
[RNDIS.NT.6.0]
Characteristics = 0x84   ; NCF_PHYSICAL + NCF_HAS_UI
BusType         = 15
; NEVER REMOVE THE FOLLOWING REFERENCE FOR NETRNDIS.INF
include         = netrndis.inf
needs           = usbrndis6.ndi
AddReg          = Rndis_AddReg
*IfType            = 6    ; IF_TYPE_ETHERNET_CSMACD.
*MediaType         = 16   ; NdisMediumNative802_11
*PhysicalMediaType = 14   ; NdisPhysicalMedium802_3

; DDInstal.Services section
[RNDIS.NT.6.0.Services]
include     = netrndis.inf
needs       = usbrndis6.ndi.Services

; Optional registry settings. You can modify as needed.
[RNDIS_AddReg] 
HKR, NDI\params\RndisProperty, ParamDesc,  0, %Rndis_Property%
HKR, NDI\params\RndisProperty, type,       0, "edit"
HKR, NDI\params\RndisProperty, LimitText,  0, "12"
HKR, NDI\params\RndisProperty, UpperCase,  0, "1"
HKR, NDI\params\RndisProperty, default,    0, " "
HKR, NDI\params\RndisProperty, optional,   0, "1"

; No sys copyfiles - the sys files are already in-build 
; (part of the operating system).

; Modify these strings for your device as needed.
[Strings]
Microsoft             = "Microsoft Corporation"
RndisDevice           = "Remote NDIS6 based Device"
Rndis_Property         = "Optional RNDIS Property"
```

## <a name="related-topics"></a>関連トピック


[リモートの NDIS (RNDIS) の概要](overview-of-remote-ndis--rndis-.md)

[Windows に含まれる USB クラス ドライバー](https://msdn.microsoft.com/library/windows/hardware/ff538820)

 

 






