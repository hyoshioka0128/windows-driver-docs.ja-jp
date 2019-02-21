---
title: wmitrace.start
description: Wmitrace.start 拡張機能は、ターゲット コンピューターで Event Tracing for Windows (ETW) のロガーを開始します。
ms.assetid: 52ed0c5a-6ca9-4890-bae5-54394bc43d51
keywords:
- デバッグ wmitrace.start Windows
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- wmitrace.start
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 9203a4cfd30c71f844713cd7b3068f8bdc3e9c0d
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56553522"
---
# <a name="wmitracestart"></a>!wmitrace.start


**! Wmitrace.start**拡張機能がターゲット コンピューターの Event Tracing for Windows (ETW) のロガーを起動します。

```dbgcmd
!wmitrace.start LoggerName [-cir Size | -seq Size] [-f File] [-b Size] [-max Num] [-min Num] [-kd] [-ft Time] 
```

## <a name="span-idddkwmitracestrdumpdbgspanspan-idddkwmitracestrdumpdbgspanparameters"></a><span id="ddk__wmitrace_strdump_dbg"></span><span id="DDK__WMITRACE_STRDUMP_DBG"></span>パラメーター


<span id="_______LoggerName______"></span><span id="_______loggername______"></span><span id="_______LOGGERNAME______"></span> *LoggerName*   
トレース セッションに使用する名前を提供します。 *ロガー*スペースや引用符を含めることはできません。

<span id="_______-cir_______Size______"></span><span id="_______-cir_______size______"></span><span id="_______-CIR_______SIZE______"></span> **-cir** *サイズ*   
循環的に書き込まれるログ ファイル。 *サイズ*バイトで、ファイルの最大サイズを指定します。 ファイルには、この長さに達すると、新しいデータを書き込むファイルに循環的に、最初から最後までのファイルを上書きします。 これと組み合わせることはできません、 **-seq**パラメーター。 どちらの場合 **-cir**も **-seq**を指定すると、バッファー モードでファイルが書き込まれます。

<span id="_______-seq_______Num______"></span><span id="_______-seq_______num______"></span><span id="_______-SEQ_______NUM______"></span> **-seq** *Num*   
連続的に書き込まれるログ ファイル。 *サイズ*バイトで、ファイルの最大サイズを指定します。 ファイルには、この長さになると、新しいデータが末尾に追加されるたびに、最も古いデータはファイルの先頭から削除されます。 これと組み合わせることはできません、 **-cir**パラメーター。 どちらの場合 **-cir**も **-seq**を指定すると、バッファー モードでファイルが書き込まれます。

<span id="_______-f_______File______"></span><span id="_______-f_______file______"></span><span id="_______-F_______FILE______"></span> **-f** *ファイル*   
ターゲット コンピューター上に作成されるログ ファイルの名前を指定します。 *ファイル*絶対ディレクトリ パスを含める必要があるあり、スペースや引用符を含めることはできません。

<span id="_______-b_______Size______"></span><span id="_______-b_______size______"></span><span id="_______-B_______SIZE______"></span> **-b** *サイズ*   
各バッファーのサイズをキロバイト単位で指定します。 許容範囲*サイズ*は 1 ~ 2048、包括的です。

<span id="_______-max_______Num______"></span><span id="_______-max_______num______"></span><span id="_______-MAX_______NUM______"></span> **-最大** *Num*   
使用するバッファーの最大数を指定します。 *Num*正の整数を指定できます。

<span id="_______-min_______Num______"></span><span id="_______-min_______num______"></span><span id="_______-MIN_______NUM______"></span> **最小** *Num*   
使用するバッファーの最小数を指定します。 *Num*正の整数を指定できます。

<span id="_______-kd______"></span><span id="_______-KD______"></span> **-kd**   
KD フィルター モードを有効にします。 メッセージは、カーネル デバッガーに送信され、画面に表示します。

<span id="_______-ft_______Time______"></span><span id="_______-ft_______time______"></span><span id="_______-FT_______TIME______"></span> **-ft** *時間*   
フラッシュのタイマーの期間を秒単位で指定します。 Windows 8 以降で指定できますフラッシュ タイマーの継続時間 (ミリ秒) を追加して**ms**を*時間*値。 たとえば、 **ft 100 ミリ秒**します。

**注**  KD フィルターのモードでトレース セッションを開始するかどうか (**-kd**)、ターゲット コンピューター上のトレース バッファーは、表示のデバッガー ホスト コンピューター上に送信されます。 このパラメーターは、ターゲット コンピューター上のバッファーがフラッシュされ、ホスト コンピューターに送信されるどのくらいの頻度を指定します。

 

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

この拡張機能は、Wmitrace.dll によってエクスポートされます。

この拡張機能は、Windows 7 および Windows の以降のバージョンで使用できます。

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>追加情報

この拡張機能のパラメーターの詳細については、次を参照してください。 [StartTrace 関数](https://go.microsoft.com/fwlink/p/?linkid=139652)と[イベント\_トレース\_プロパティ](https://go.microsoft.com/fwlink/p/?linkid=139653)します。 イベントのトレースの概念的な概要については、Microsoft Windows SDK を参照してください。 トレース ツールについては、Windows Driver Kit (WDK) を参照してください。

<a name="remarks"></a>注釈
-------

この拡張機能を使用した後は、プログラムの実行を再開する必要があります (たとえばを使用して、 [ **g (移動)** ](g--go-.md)コマンド) を有効にするために。 簡単な後は、ターゲット コンピューターに自動的にデバッガーを中断もう一度です。

トレース セッションが開始されると、システムによって割り当てられますが、序数 (、*ロガー ID*)。 ロガー名またはロガー ID によって、セッションを参照できます。

ETW のロガーを停止するには使用[ **! wmitrace.stop**](-wmitrace-stop.md)します。

 

 





