---
title: rcdrkd.rcdrloglist
description: Rcdrkd.rcdrloglist 拡張機能では、ドライバーまたはドライバーのセットが所有するレコーダー ログの一覧が表示されます。
ms.assetid: D4D3C313-EFD4-482B-B4A3-307F2407D2BA
keywords:
- デバッグ rcdrkd.rcdrloglist Windows
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- rcdrkd.rcdrloglist
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: c4de589f5c06e062baa4846a512a688674de7255
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56578159"
---
# <a name="rcdrkdrcdrloglist"></a>!rcdrkd.rcdrloglist


**! Rcdrkd.rcdrloglist**拡張機能は、ドライバーまたはドライバーのセットが所有するレコーダー ログの一覧を表示します。

```dbgcmd
!rcdrkd.rcdrloglist DriverName [DriverName ...]
```

## <a name="span-idddkdevobjdbgspanspan-idddkdevobjdbgspanparameters"></a><span id="ddk__devobj_dbg"></span><span id="DDK__DEVOBJ_DBG"></span>パラメーター


<span id="_______DriverName______"></span><span id="_______drivername______"></span><span id="_______DRIVERNAME______"></span> *ドライバー名*   
.Sys 拡張子を含まない、ドライバーの名前。

## <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL


Rcdrkd.dll

<a name="remarks"></a>コメント
-------

このコマンドは、WppRecorder API を使用してメッセージをさまざまなログに記録するドライバーに対してだけに関連します。

<a name="examples"></a>使用例
--------

次の例では、USB 3.0 ホスト コント ローラー ドライバー (usbxhci.sys) によって所有されているすべてのレコーダー ログの一覧が表示されます。

```dbgcmd
3: kd> !rcdrloglist usbxhci
Log dump command                           Log ID                   Size
================                           ======                   ====
!rcdrlogdump  usbxhci -a fffffa8005ff2b60  03 SLT02 DCI04           1024
!rcdrlogdump  usbxhci -a fffffa8005ff2010  03 SLT02 DCI03           1024
!rcdrlogdump  usbxhci -a fffffa8005b36010  03 SLT01 DCI03           1024
!rcdrlogdump  usbxhci -a fffffa8005b379e0  03 SLT01 DCI04           1024
!rcdrlogdump  usbxhci -a fffffa8005b33350  03 SLT02 DCI01           1024
!rcdrlogdump  usbxhci -a fffffa8005b2bb60  03 SLT01 DCI01           1024
!rcdrlogdump  usbxhci -a fffffa8005a2bb60  03 CMD                   1024
!rcdrlogdump  usbxhci -a fffffa8005a1ab60  03 INT00                 1024
!rcdrlogdump  usbxhci -a fffffa8005085330  03 RUNDOWN               512
!rcdrlogdump  usbxhci -a fffffa8005311780  03 1033 0194             1024
```

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>参照してください。


[RCDRKD 拡張機能](rcdrkd-extensions.md)

 

 






