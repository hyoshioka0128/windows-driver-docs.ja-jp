---
title: wmitrace.stop
description: Wmitrace.stop 拡張機能は、ターゲット コンピューターの Event Tracing for Windows (ETW) のロガーを停止します。
ms.assetid: 38be65ae-efef-400f-bb10-315d1f6b11d8
keywords:
- デバッグ wmitrace.stop Windows
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- wmitrace.stop
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 5405cdff8afb78fede95f8532a77aa69db146f76
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56538812"
---
# <a name="wmitracestop"></a>!wmitrace.stop


**! Wmitrace.stop**拡張機能は、ターゲット コンピューターの Event Tracing for Windows (ETW) logger を停止します。

```dbgcmd
!wmitrace.stop { LoggerID | LoggerName } 
```

## <a name="span-idddkwmitracestrdumpdbgspanspan-idddkwmitracestrdumpdbgspanparameters"></a><span id="ddk__wmitrace_strdump_dbg"></span><span id="DDK__WMITRACE_STRDUMP_DBG"></span>パラメーター


<span id="_______LoggerID______"></span><span id="_______loggerid______"></span><span id="_______LOGGERID______"></span> *LoggerID*   
トレース セッションを指定します。 *LoggerID*は序数をコンピューター上の各トレース セッションに割り当てられます。

<span id="_______LoggerName______"></span><span id="_______loggername______"></span><span id="_______LOGGERNAME______"></span> *LoggerName*   
トレース セッションを指定します。 *ロガー*テキスト名を指定は、トレース セッションが開始されたとき。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

この拡張機能は、Wmitrace.dll によってエクスポートされます。

この拡張機能は、Windows 7 および Windows の以降のバージョンで使用できます。

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>追加情報

イベントのトレースの概念的な概要については、Microsoft Windows SDK を参照してください。 トレース ツールについては、Windows Driver Kit (WDK) を参照してください。

<a name="remarks"></a>注釈
-------

この拡張機能を使用した後は、プログラムの実行を再開する必要があります (たとえばを使用して、 [ **g (移動)** ](g--go-.md)コマンド) を有効にするために。 簡単な後は、ターゲット コンピューターに自動的にデバッガーを中断もう一度です。

ETW のロガーを開始するには、使用[ **! wmitrace.start**](-wmitrace-start.md)します。

 

 





