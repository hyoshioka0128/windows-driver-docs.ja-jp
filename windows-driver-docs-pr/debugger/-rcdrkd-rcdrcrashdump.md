---
title: rcdrkd.rcdrcrashdump
description: Rcdrkd.rcdrcrashdump 拡張機能は、(ログ、ミニダンプに存在する場合)、レコーダー ログを表示するミニダンプ ファイルで使用されます。
ms.assetid: 61DB0462-31F1-4756-87BB-60188887ACAF
keywords:
- デバッグ rcdrkd.rcdrcrashdump Windows
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- rcdrkd.rcdrcrashdump
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 300ece52f120062e4aeaad46b549d06a17883b7a
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56538875"
---
# <a name="rcdrkdrcdrcrashdump"></a>!rcdrkd.rcdrcrashdump


[ **! Rcdrkd.rcdrcrashdump** ](-usb3kd-device-info.md) (ログ、ミニダンプに存在する場合)、レコーダー ログを表示するミニダンプ ファイルを使用して拡張機能を使用します。

```dbgcmd
!rcdrkd.rcdrcrashdump TraceProviderGuid
!rcdrkd.rcdrcrashdump DriverName
```

## <a name="span-idddkdevobjdbgspanspan-idddkdevobjdbgspanparameters"></a><span id="ddk__devobj_dbg"></span><span id="DDK__DEVOBJ_DBG"></span>パラメーター


<span id="_______TraceProviderGuid______"></span><span id="_______traceproviderguid______"></span><span id="_______TRACEPROVIDERGUID______"></span> *TraceProviderGuid*   
トレース プロバイダーの GUID です。 このパラメーターは、中かっこを含める必要があります: {*guid*}

<span id="_______DriverName______"></span><span id="_______drivername______"></span><span id="_______DRIVERNAME______"></span> *ドライバー名*   
ドライバーの名前。 転送トレース レコーダー (IFR) を使用するドライバーのトレース プロバイダー GUID ではなく、ドライバー名を使用できます。

## <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL


Rcdrkd.dll

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>参照してください。


[RCDRKD 拡張機能](rcdrkd-extensions.md)

 

 






