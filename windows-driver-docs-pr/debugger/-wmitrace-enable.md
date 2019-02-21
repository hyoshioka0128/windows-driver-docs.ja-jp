---
title: wmitrace.enable
description: Wmitrace.enable 拡張機能では、指定された Event Tracing for Windows (ETW) トレース セッションのプロバイダーができます。
ms.assetid: 5a27fa00-7d52-43f7-84f4-82c5b5af1c06
keywords:
- デバッグ wmitrace.enable Windows
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- wmitrace.enable
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 99385a9e0e07abbd7cc60a6b864bdac3c29215a5
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56560479"
---
# <a name="wmitraceenable"></a>!wmitrace.enable


**! Wmitrace.enable**拡張機能、プロバイダー、指定された Event Tracing for Windows (ETW) トレース セッションを有効にします。

```dbgcmd
!wmitrace.enable { LoggerID | LoggerName } GUID [-level Num] [-matchallkw Num] [-matchanykw Num] [-enableproperty Num] [-flag Num] 
```

## <a name="span-idddkwmitracestrdumpdbgspanspan-idddkwmitracestrdumpdbgspanparameters"></a><span id="ddk__wmitrace_strdump_dbg"></span><span id="DDK__WMITRACE_STRDUMP_DBG"></span>パラメーター


<span id="_______LoggerID______"></span><span id="_______loggerid______"></span><span id="_______LOGGERID______"></span> *LoggerID*   
トレース セッションを指定します。 *LoggerID*は序数をコンピューター上の各トレース セッションに割り当てられます。

<span id="_______LoggerName______"></span><span id="_______loggername______"></span><span id="_______LOGGERNAME______"></span> *LoggerName*   
トレース セッションを指定します。 *ロガー*テキスト名を指定は、トレース セッションが開始されたとき。

<span id="_______GUID______"></span><span id="_______guid______"></span> *GUID*   
有効にするプロバイダーの GUID を指定します。

<span id="_______-level_______Num______"></span><span id="_______-level_______num______"></span><span id="_______-LEVEL_______NUM______"></span> **-レベル** *Num*   
レベルを指定します。 *Num*整数を指定できます。

<span id="_______-matchallkw_______Num______"></span><span id="_______-matchallkw_______num______"></span><span id="_______-MATCHALLKW_______NUM______"></span> **-matchallkw** *Num*   
1 つまたは複数のキーワードを指定します。 複数のキーワードが指定されている場合は、すべてのキーワードが一致する場合にのみ、プロバイダーを有効になります。 *Num*整数を指定できます。

<span id="_______-matchanykw_______Num______"></span><span id="_______-matchanykw_______num______"></span><span id="_______-MATCHANYKW_______NUM______"></span> **-matchanykw** *Num*   
1 つまたは複数のキーワードを指定します。 複数のキーワードを指定すると、少なくとも 1 つのキーワードが一致した場合、プロバイダーを有効になります。 *Num*整数を指定できます。 このパラメーターの効果は、効果と重複のフラグ パラメーター。

<span id="_______-enableproperty_______Num______"></span><span id="_______-enableproperty_______num______"></span><span id="_______-ENABLEPROPERTY_______NUM______"></span> **-enableproperty** *Num*   
有効にするプロパティを指定します。 *Num*整数を指定できます。

<span id="_______-flag_______Num______"></span><span id="_______-flag_______num______"></span><span id="_______-FLAG_______NUM______"></span> **-フラグ** *Num*   
1 つまたは複数のフラグを指定します。 *Num*整数を指定できます。 このパラメーターの効果 - matchanykw パラメーターの効果と重複します。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

この拡張機能は、Wmitrace.dll によってエクスポートされます。

この拡張機能は、Windows 7 および Windows の以降のバージョンで使用できます。

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>追加情報

イベントのトレースの概念的な概要については、Microsoft Windows SDK を参照してください。 トレース ツールについては、Windows Driver Kit (WDK) を参照してください。

<a name="remarks"></a>注釈
-------

この拡張機能を使用した後は、プログラムの実行を再開する必要があります (たとえばを使用して、 [ **g (移動)** ](g--go-.md)コマンド) を有効にするために。 簡単な後は、ターゲット コンピューターに自動的にデバッガーを中断もう一度です。

プロバイダーを無効にするには、 [ **! wmitrace.disable**](-wmitrace-disable.md)します。

 

 





