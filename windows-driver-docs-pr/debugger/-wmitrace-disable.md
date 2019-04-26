---
title: wmitrace.disable
description: Wmitrace.disable 拡張機能では、指定された Event Tracing for Windows (ETW) トレース セッションのプロバイダーを無効にします。
ms.assetid: b993bfa4-2d3d-4739-9d5e-0cb714369742
keywords:
- デバッグ wmitrace.disable Windows
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- wmitrace.disable
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 4fb49cbd5fcf8b1fc1139e7601b8644458b3e379
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63344223"
---
# <a name="wmitracedisable"></a>!wmitrace.disable


**! Wmitrace.disable**拡張機能は、指定された Event Tracing for Windows (ETW) トレース セッションのプロバイダーを無効にします。

```dbgcmd
!wmitrace.disable { LoggerID | LoggerName } GUID 
```

## <a name="span-idddkwmitracestrdumpdbgspanspan-idddkwmitracestrdumpdbgspanparameters"></a><span id="ddk__wmitrace_strdump_dbg"></span><span id="DDK__WMITRACE_STRDUMP_DBG"></span>パラメーター


<span id="_______LoggerID______"></span><span id="_______loggerid______"></span><span id="_______LOGGERID______"></span> *LoggerID*   
トレース セッションを指定します。 *LoggerID*は序数をコンピューター上の各トレース セッションに割り当てられます。

<span id="_______LoggerName______"></span><span id="_______loggername______"></span><span id="_______LOGGERNAME______"></span> *LoggerName*   
トレース セッションを指定します。 *ロガー*テキスト名を指定は、トレース セッションが開始されたとき。

<span id="_______GUID______"></span><span id="_______guid______"></span> *GUID*   
無効にするプロバイダーの GUID を指定します。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

この拡張機能は、Wmitrace.dll によってエクスポートされます。

この拡張機能は、Windows 7 および Windows の以降のバージョンで使用できます。

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>追加情報

イベントのトレースの概念的な概要については、Microsoft Windows SDK を参照してください。 トレース ツールについては、Windows Driver Kit (WDK) を参照してください。

<a name="remarks"></a>注釈
-------

この拡張機能を使用した後は、プログラムの実行を再開する必要があります (たとえばを使用して、 [ **g (移動)** ](g--go-.md)コマンド) を有効にするために。 簡単な後は、ターゲット コンピューターに自動的にデバッガーを中断もう一度です。

プロバイダーを有効にするには、 [ **! wmitrace.enable**](-wmitrace-enable.md)します。

 

 





