---
title: リモート NDIS INF テンプレート
description: リモート NDIS INF テンプレート
ms.assetid: bbbd3aef-230f-4286-bea2-bb583789865e
keywords:
- リモート NDIS WDK ネットワーク, INF テンプレート
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 35d5ee9e7db90aa4e1b091acf0237f2f53cfe2f6
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842055"
---
# <a name="remote-ndis-inf-template"></a>リモート NDIS INF テンプレート





Microsoft では、NDIS ミニポートドライバー Rndismp を提供しています。このドライバーは、リモート NDIS メッセージセットを実装し、汎用バストランスポートドライバーと通信します。このドライバーは、適切なバスドライバーと通信します。 この NDIS ミニポートドライバーは、Microsoft によって実装および管理され、サポートされているすべての Windows バージョンの一部として配布されます。 これは% SystemRoot%\\System32\\drivers ディレクトリにあります。

リモート NDIS ドライバーを USB デバイスと共に使用するには、次のいずれかのテンプレートに従って、IHV が INF ファイルを提供する必要があります。

-   [NDIS 5.1 用 RNDIS INF テンプレート (Windows XP 以降)](#rndis-inf-template-for-ndis-51-windows-xp-and-later)
-   [NDIS 6.0 の RNDIS INF テンプレート (Windows 7 以降)](#rndis-inf-template-for-ndis-60-windows-7-and-later)

### <a name="rndis-inf-template-for-ndis-51-windows-xp-and-later"></a>NDIS 5.1 用 RNDIS INF テンプレート (Windows XP 以降)

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

### <a name="rndis-inf-template-for-ndis-60-windows-7-and-later"></a>NDIS 6.0 の RNDIS INF テンプレート (Windows 7 以降)

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


[リモート NDIS の概要 (RNDIS)](overview-of-remote-ndis--rndis-.md)

[Windows に含まれる USB クラスドライバー](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)

 

 






