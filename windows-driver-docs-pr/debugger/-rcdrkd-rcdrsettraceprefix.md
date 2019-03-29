---
title: rcdrkd.rcdrsettraceprefix
description: Rcdrkd.rcdrsettraceprefix 拡張機能は、トレース メッセージのプレフィックスを設定します。
ms.assetid: BFA987B8-7013-4112-A674-064ED59741C0
keywords:
- デバッグ rcdrkd.rcdrsettraceprefix Windows
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- rcdrkd.rcdrsettraceprefix
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: a59aaf44176e80aa450a0f99efe799b1a9a1f932
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56570718"
---
# <a name="rcdrkdrcdrsettraceprefix"></a>!rcdrkd.rcdrsettraceprefix


**! Rcdrkd.rcdrsettraceprefix**拡張機能は、トレース メッセージのプレフィックスを設定します。

```dbgcmd
!rcdrkd.rcdrsettraceprefix TracePrefixString 
```

## <a name="span-idddkdevobjdbgspanspan-idddkdevobjdbgspanparameters"></a><span id="ddk__devobj_dbg"></span><span id="DDK__DEVOBJ_DBG"></span>パラメーター


<span id="_______TracePrefixString______"></span><span id="_______traceprefixstring______"></span><span id="_______TRACEPREFIXSTRING______"></span> *TracePrefixString*   
トレース メッセージのプレフィックス文字列。

## <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL


Rcdrkd.dll

<a name="remarks"></a>コメント
-------

レコーダー ログ内の各メッセージには、トレース メッセージのプレフィックス文字列を指定することで制御できる接頭辞が付きます。 詳細については、次を参照してください。[トレース メッセージのプレフィックス](https://msdn.microsoft.com/library/windows/hardware/ff553941)します。

<a name="examples"></a>使用例
--------

次の例では、トレース メッセージのプレフィックスはもともと **%7。: % です。FUNC!-** . パラメーター **%7。** プレフィックスが、メッセージ シーケンス番号が含まれることを指定します。 パラメーター **% です。FUNC!** プレフィックスがメッセージを生成した関数の名前が含まれることを指定します。 例では、 **! rcdrsettraceprefix**にプレフィックス文字列を変更する **%7。** します。 その後、ログの表示はメッセージのシーケンス番号が含まれていますが、関数名には含まれません。

```dbgcmd
0: kd> !rcdrlogdump USBXHCI -a 0xfffffa8010737b60
Trace searchpath is: 

Trace format prefix is: %7!u!: %!FUNC! - 
Trying to extract TMF information from - C:\ProgramData\dbg\sym\usbxhci.pdb\D4C85D5D3E2843879EDE226A334D69552\usbxhci.pdb
--- start of log ---
405: TransferRing_DispatchEventsAndReleaseLock - 1.8.1: Mapping Begin : Path 1 TransferRingState_Mapping Events 0x00000000
406: TransferRing_StageRetrieveFromRequest - 1.8.1: WdfRequest 0x0000057FEE117A88 TransferData 0xFFFFFA8011EE8700 Function 0x9 Length 500 TransferSize 500 BytesProcessed 0
...
---- end of log ----

0: kd> !rcdrsettraceprefix %7!u!: 
SetTracePrefix: "%7!u!: "
0: kd> !rcdrlogdump USBXHCI -a 0xfffffa8010737b60
Trace searchpath is: 

Trace format prefix is: %7!u!: 
Trying to extract TMF information from - C:\ProgramData\dbg\sym\usbxhci.pdb\D4C85D5D3E2843879EDE226A334D69552\usbxhci.pdb
--- start of log ---
405: 1.8.1: Mapping Begin : Path 1 TransferRingState_Mapping Events 0x00000000
406: 1.8.1: WdfRequest 0x0000057FEE117A88 TransferData 0xFFFFFA8011EE8700 Function 0x9 Length 500 TransferSize 500 BytesProcessed 0
...
---- end of log ----
```

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>参照してください。


[RCDRKD 拡張機能](rcdrkd-extensions.md)

 

 






