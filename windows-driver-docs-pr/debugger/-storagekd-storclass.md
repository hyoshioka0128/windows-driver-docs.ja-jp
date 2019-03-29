---
title: storagekd.storclass
description: Storagekd.storclass 拡張機能では、指定した classpnp デバイスに関する情報が表示されます。
ms.assetid: EC5B44F5-540E-4F25-80AA-09BE4F78BF72
keywords:
- デバッグ storagekd.storclass Windows
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- storagekd.storclass
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: a9b6875f23e6430fc05c50a3e89148d590cfb1e1
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56581278"
---
# <a name="storagekdstorclass"></a>!storagekd.storclass


**! Storagekd.storclass**拡張機能は、指定した情報を表示します。 *classpnp*デバイス。

```dbgcmd
!storagekd.storclass [Address [Level]] 
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>パラメーター


<span id="_______Address"></span><span id="_______address"></span><span id="_______ADDRESS"></span> *アドレス*  
Classpnp デバイスのデバイスの拡張機能またはデバイス オブジェクトにアドレスを指定します。 場合*アドレス*は省略すると、すべての classpnp 拡張機能の一覧が表示されます。

<span id="_______Level"></span><span id="_______level"></span><span id="_______LEVEL"></span> *レベル*  
表示する詳細情報の量を指定します。 このパラメーターは、0、1、または 2、および提供することが最も詳細 0 が最も低い 2 に設定できます。 既定値は 0 です。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>Windows 8 以降</strong></p></td>
<td align="left"><p>Storagekd.dll</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>コメント
-------

次の例に示します、 **! storagekd.storclass**表示。

**1: kd&gt; !storagekd.storclass**

```dbgcmd
Storage class devices:

* !storclass fffffa80043dc060 [1,2] ST3160812AS Paging Disk       
  !storclass fffffa8006581740 [1,2] Msft Virtual Disk Disk       

Usage: !storclass <class device> <level [0-2]>
```

**1: kd&gt; !storagekd.storclass fffffa80043dc060 1**

```dbgcmd
Storage class device fffffa80043dc060 with extension at fffffa80043dc1b0

Classpnp Internal Information at fffffa8003bec360

    Transfer Packet Engine:

     Packet          Status  DL Irp          Opcode  Sector/ListId   UL Irp 
    --------         ------ --------         ------ --------------- --------

    Pending Idle Requests: 0x0


    -- dt classpnp!_CLASS_PRIVATE_FDO_DATA fffffa8003bec360 --

Classpnp External Information at fffffa80043dc1b0

    ST3160812AS 3.ADH             9LS20QRL 

    Minidriver information at fffffa80043dc670
    Attached device object at fffffa800410a060
    Physical device object at fffffa800410a060

    Media Geometry:

        Bytes in a Sector = 512
        Sectors per Track = 63
        Tracks / Cylinder = 255
        Media Length      = 160000000000 bytes = ~149 GB

    -- dt classpnp!_FUNCTIONAL_DEVICE_EXTENSION fffffa80043dc1b0 --
```

 

 





