---
title: rcdrkd.rcdrlogsave
description: Rcdrkd.rcdrlogsave 拡張機能は、ドライバーのレコーダー バッファーを保存します。
ms.assetid: 2A79064C-A899-4351-A8A6-D8DF31CF9A17
keywords:
- デバッグ rcdrkd.rcdrlogsave Windows
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- rcdrkd.rcdrlogsave
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: b4bbaee0bf93d852827e71c617e4bb0fc4b28423
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63334326"
---
# <a name="rcdrkdrcdrlogsave"></a>!rcdrkd.rcdrlogsave


**! Rcdrkd.rcdrlogsave**拡張機能のドライバーのレコーダー バッファーを保存します。

```dbgcmd
!rcdrkd.rcdrlogsave DriverName [CaptureFilename ]
```

## <a name="span-idddkdevobjdbgspanspan-idddkdevobjdbgspanparameters"></a><span id="ddk__devobj_dbg"></span><span id="DDK__DEVOBJ_DBG"></span>パラメーター


<span id="_______DriverName______"></span><span id="_______drivername______"></span><span id="_______DRIVERNAME______"></span> *ドライバー名*   
.Sys 拡張子を含まない、ドライバーの名前。

<span id="_______CaptureFileName______"></span><span id="_______capturefilename______"></span><span id="_______CAPTUREFILENAME______"></span> *CaptureFileName*   
レコーダーのバッファーを保存するファイル (.etl 拡張子を含まない) の名前。 場合*CaptureFileName*が指定されていない、レコーダー バッファーに保存*DriverName*.etl します。

## <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL


Rcdrkd.dll

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>参照してください。


[RCDRKD 拡張機能](rcdrkd-extensions.md)

 

 






