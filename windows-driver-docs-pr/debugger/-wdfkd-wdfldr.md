---
title: wdfkd.wdfldr
description: Wdfkd.wdfldr 拡張機能では、KMDF ドライバーおよび UMDF ドライバー、Windows Driver Frameworks に動的に現在バインドされている情報が表示されます。
ms.assetid: 0965632d-922b-4812-9cfb-7663af0e3847
keywords:
- デバッグ wdfkd.wdfldr Windows
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- wdfkd.wdfldr
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: f3e0abd7ceb32014f6edfaa5beb5b0e2679a033a
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63323464"
---
# <a name="wdfkdwdfldr"></a>!wdfkd.wdfldr


**! Wdfkd.wdfldr**拡張機能には、Windows Driver Frameworks に動的に現在バインドされているドライバーに関する情報が表示されます。 これには、カーネル モード ドライバー フレームワーク (KMDF) とユーザー モード ドライバー フレームワーク (UMDF) の両方が含まれます。

```dbgcmd
!wdfkd.wdfldr [DriverName]
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>パラメーター


<span id="_______DriverName______"></span><span id="_______drivername______"></span><span id="_______DRIVERNAME______"></span> *ドライバー名*   
ファイル名拡張子を含む、ドライバーの名前。 ドライバー名を指定する場合、このコマンドは、1 つのドライバーに関する詳細情報を表示します。 ドライブ名を指定しない場合、このコマンドは、Windows Driver Frameworks にバインドされているすべてのドライバーに関する情報を表示します。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

Wdfkd.dll

### <a name="span-idframeworksspanspan-idframeworksspanspan-idframeworksspanframeworks"></a><span id="Frameworks"></span><span id="frameworks"></span><span id="FRAMEWORKS"></span>フレームワーク

KMDF 1, 1, UMDF UMDF 2

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>追加情報

詳細については、次を参照してください。[カーネル モード ドライバー フレームワークのデバッグ](kernel-mode-driver-framework-debugging.md)します。

<a name="remarks"></a>注釈
-------

出力の例を次に示します **! wdfldr**します。

```dbgcmd
## 0: kd> !wdfkd.wdfldr

##  KMDF Drivers

##  LoadedModuleList      0xfffff800003b61f8

LIBRARY_MODULE  0xffffe0000039f7c0
  Version       v1.13
  Service       \Registry\Machine\System\CurrentControlSet\Services\Wdf01000
  ImageName     Wdf01000.sys
  ImageAddress  0xfffff800002e7000
  ImageSize     0xc5000
  Associated Clients: 16

  ImageName                      Ver   WdfGlobals         FxGlobals          ImageAddress       ImageSize
  peauth.sys                     v1.7  0xffffe00003a95880 0xffffe00003a956e0 0xfffff80002678000 0x000ab000
  monitor.sys                    v1.11 0xffffe000001abc70 0xffffe000001abad0 0xfffff800022e7000 0x0000e000
  UsbHub3.sys                    v1.11 0xffffe000028a47b0 0xffffe000028a4610 0xfffff8000220b000 0x00077000
##   ...

## Total: 1 library loaded

##  UMDF Drivers

  DriverManagerProcess: 0xffffe00003470500

  ImageName                      Ver
  MyUmdfDriver.dll               v1.11 
  SomeUmdf2Driver.dll            v2.0  
  MyUmdf2Driver.dll              v2.0
```

ドライバー名を提供する別の例を次に示します。

```dbgcmd
0: kd> !wdfldr MyUmdf2Driver.dll

Version    v2.0
Service    \Registry\Machine\System\CurrentControlSet\Services\MyUmdf2Driver

## !wdflogdump  MyUmdf2Driver.dll

##  UMDF Device Instances using MyUmdf2Driver.dll

Process             DevStack           DeviceId
0xffffe00000c32900  a5a3ab5f70         \Device\00000052 !wdfdriverinfo
```

 

 





