---
title: wdfkd.wdfdevext
description: Wdfkd.wdfdevext 拡張機能には、Microsoft Windows Driver Model (WDM) DEVICE_OBJECT 構造体の DeviceExtension メンバーに関連付けられている情報が表示されます。
ms.assetid: 89559cae-7323-4c91-b20a-7d42069cdb93
keywords:
- デバッグ wdfkd.wdfdevext Windows
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- wdfkd.wdfdevext
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 2e8bfffaaa59aec3c82713d0229cc6dbb558a9e9
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56549847"
---
# <a name="wdfkdwdfdevext"></a>!wdfkd.wdfdevext


**! Wdfkd.wdfdevext**拡張機能に関連付けられている情報を表示する、 **DeviceExtension**メンバーの Microsoft Windows Driver Model (WDM) デバイス\_オブジェクトの構造体。

```dbgcmd
!wdfkd.wdfdevext DeviceExtension
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>パラメーター


<span id="_______DeviceExtension______"></span><span id="_______deviceextension______"></span><span id="_______DEVICEEXTENSION______"></span> *DeviceExtension*   
デバイスの拡張機能へのポインター。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

Wdfkd.dll

### <a name="span-idframeworksspanspan-idframeworksspanspan-idframeworksspanframeworks"></a><span id="Frameworks"></span><span id="frameworks"></span><span id="FRAMEWORKS"></span>フレームワーク

KMDF 1, 1, UMDF UMDF 2

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>追加情報

詳細については、[カーネル モード ドライバー フレームワークのデバッグ](kernel-mode-driver-framework-debugging.md)を参照してください。

<a name="remarks"></a>注釈
-------

KMDF ドライバーである、HdAudBus.sys の例を示します。 使用[ **! devnode** ](-devnode.md)関数ドライバーとして HdAudBus のあるデバイスのノードを検索します。 渡すし、出力から物理デバイス オブジェクト (PDO) [ **! devstack**](-devstack.md)します。 出力からデバイスの拡張機能のアドレスを取得する **! devstack**に渡すと **! wdfdevext**します。

```dbgcmd
0: kd> !devnode 0 1 hdaudbus
Dumping IopRootDeviceNode (= 0xffffe000002cfd30)
DevNode 0xffffe000009b7a50 for PDO 0xffffe00000226880
  InstancePath is "PCI\VEN_8086&DEV_293E&SUBSYS_2819103C&REV_02\3&33fd14ca&0&D8"
  ServiceName is "HDAudBus"
  ...
0: kd> !devstack 0xffffe00000226880
  !DevObj           !DrvObj            !DevExt           ObjectName
  ffffe00001351e20  \Driver\HDAudBus   ffffe000009a3c00  
> ffffe00000226880  \Driver\pci        ffffe000002269d0  NTPNP_PCI0009
!DevNode ffffe000009b7a50 :
  DeviceInst is "PCI\VEN_8086&DEV_293E&SUBSYS_2819103C&REV_02\3&33fd14ca&0&D8"
  ServiceName is "HDAudBus"
0: kd> *
0: kd> !wdfdevext ffffe000009a3c00
Device context is 0xffffe000009a3c00
    context:  dt 0xffffe000009a3c00 HDAudBus!HDAudioDeviceExtension (size is 0xa8 bytes)
    EvtCleanupCallback fffff80001f35950 HDAudBus!HdAudBusEvtDeviceCleanupCallback

!wdfdevice 0x00001fffff65c6e8                        
!wdfobject 0xffffe000009a3910
```

Wudfrd.sys で、2 の UMDF ドライバー スタックのカーネル モードの部分の関数のドライバーの例を示します。 使用[ **! devnode** ](-devnode.md)関数ドライバーとして Wudfrd のあるデバイスのノードを検索します。 渡すし、出力から物理デバイス オブジェクト (PDO) [ **! devstack**](-devstack.md)します。 出力からデバイスの拡張機能のアドレスを取得する **! devstack**に渡すと **! wdfdevext**します。

```dbgcmd
0: kd> !devnode 0 1 wudfrd
Dumping IopRootDeviceNode (= 0xffffe000002cfd30)
DevNode 0xffffe00000a1e530 for PDO 0xffffe00000b15b00
  InstancePath is "ROOT\SAMPLE\0001"
  ServiceName is "WUDFRd"
  ...
0: kd> !devstack 0xffffe00000b15b00
  !DevObj           !DrvObj            !DevExt           ObjectName
  ffffe00000c11040  \Driver\WUDFRd     ffffe00000c11190  
> ffffe00000b15b00  \Driver\PnpManager 00000000  00000052
!DevNode ffffe00000a1e530 :
  DeviceInst is "ROOT\SAMPLE\0001"
  ServiceName is "WUDFRd"
0: kd> *
0: kd> !wdfdevext ffffe00000c11190
## Device context is 0xffffe00000c11190

##  UMDF Device Instances for this Redirector extension

  DriverManagerProcess: 0xffffe00003470500

  ImageName              Ver   DevStack           HostProcess        DeviceID      
  MyUmdf2Driver.dll      v2.0  0x000000a5a3ab5f70 0xffffe00000c32900  \Device\00000052
```

 

 





