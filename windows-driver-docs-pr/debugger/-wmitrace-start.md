---
title: wmitrace
description: Wmitrace 拡張機能は、ターゲットコンピューターで Windows イベントトレーシング (ETW) logger を開始します。
ms.assetid: 52ed0c5a-6ca9-4890-bae5-54394bc43d51
keywords:
- wmitrace Windows のデバッグを開始します。
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- wmitrace.start
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 7b3fc43f3ca1575e9598c139f97d47ed85c2d379
ms.sourcegitcommit: dadc9ced1670d667e31eb0cb58d6a622f0f09c46
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/09/2020
ms.locfileid: "84533967"
---
# <a name="wmitracestart"></a>!wmitrace.start


**! Wmitrace**拡張機能は、ターゲットコンピューターで WINDOWS イベントトレーシング (ETW) logger を開始します。

```dbgcmd
!wmitrace.start LoggerName [-cir Size | -seq Size] [-f File] [-b Size] [-max Num] [-min Num] [-kd] [-ft Time] 
```

## <a name="span-idddk__wmitrace_strdump_dbgspanspan-idddk__wmitrace_strdump_dbgspanparameters"></a><span id="ddk__wmitrace_strdump_dbg"></span><span id="DDK__WMITRACE_STRDUMP_DBG"></span>パラメータ


<span id="_______LoggerName______"></span><span id="_______loggername______"></span><span id="_______LOGGERNAME______"></span>*LoggerName*   
トレースセッションに使用する名前を指定します。 *LoggerName*には、スペースまたは引用符を含めることはできません。

<span id="_______-cir_______Size______"></span><span id="_______-cir_______size______"></span><span id="_______-CIR_______SIZE______"></span>**-cir** *サイズ*   
ログファイルが循環して書き込まれます。 *サイズ*最大ファイルサイズをバイト単位で指定します。 ファイルがこの長さに達すると、新しいデータは循環してファイルに書き込まれ、ファイルが最初から最後まで上書きされます。 これは、 **-seq**パラメーターと組み合わせることはできません。 **-Cir**も **-seq**も指定されていない場合、ファイルはバッファーモードで書き込まれます。

<span id="_______-seq_______Num______"></span><span id="_______-seq_______num______"></span><span id="_______-SEQ_______NUM______"></span>**-seq** *Num*   
ログファイルがシーケンシャルに書き込まれます。 *サイズ*最大ファイルサイズをバイト単位で指定します。 ファイルがこの長さに達すると、新しいデータが末尾に追加されるたびに、ファイルの先頭から最も古いデータが削除されます。 これは、 **-cir**パラメーターと組み合わせることはできません。 **-Cir**も **-seq**も指定されていない場合、ファイルはバッファーモードで書き込まれます。

<span id="_______-f_______File______"></span><span id="_______-f_______file______"></span><span id="_______-F_______FILE______"></span>**-f** *ファイル*   
ターゲットコンピューターに作成するログファイルの名前を指定します。 *ファイル*には絶対ディレクトリパスを含める必要があり、スペースや引用符を含めることはできません。

<span id="_______-b_______Size______"></span><span id="_______-b_______size______"></span><span id="_______-B_______SIZE______"></span>**-b** *サイズ*   
各バッファーのサイズをキロバイト単位で指定します。 許容範囲の*サイズ*は、1 ~ 2048 の範囲です。

<span id="_______-max_______Num______"></span><span id="_______-max_______num______"></span><span id="_______-MAX_______NUM______"></span>**-最大** *Num*   
使用するバッファーの最大数を指定します。 *Num*には、正の整数を指定できます。

<span id="_______-min_______Num______"></span><span id="_______-min_______num______"></span><span id="_______-MIN_______NUM______"></span>**-最小** *Num*数   
使用するバッファーの最小数を指定します。 *Num*には、正の整数を指定できます。

<span id="_______-kd______"></span><span id="_______-KD______"></span>**-kd**   
KD フィルターモードを有効にします。 メッセージはカーネルデバッガーに送信され、画面に表示されます。

<span id="_______-ft_______Time______"></span><span id="_______-ft_______time______"></span><span id="_______-FT_______TIME______"></span>**-ft** *時間*   
フラッシュタイマーの期間を秒単位で指定します。 Windows 8 以降では、*時間*の値に**ミリ秒**を付加することによって、フラッシュタイマーの期間をミリ秒単位で指定できます。 たとえば、 **-ft 100 ミリ秒**のようになります。

**メモ**   KD フィルターモード (**-KD**) でトレースセッションを開始すると、ターゲットコンピューター上のトレースバッファーは、ホストコンピューター上のデバッガーに送信されて表示されます。 このパラメーターは、ターゲットコンピューター上のバッファーをフラッシュし、ホストコンピューターに送信する頻度を指定します。

 

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

この拡張機能は、Wmitrace によってエクスポートされます。

この拡張機能は、windows 7 以降のバージョンの Windows で使用できます。

### <a name="span-idadditional_informationspanspan-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>追加情報

この拡張機能のパラメーターの詳細については、「 [Starttracea 関数](https://docs.microsoft.com/windows/win32/api/evntrace/nf-evntrace-starttracea)と[イベント \_ トレースの \_ プロパティ](https://docs.microsoft.com/windows/win32/api/evntrace/ns-evntrace-event_trace_properties)」を参照してください。 イベントトレースの概念の概要については、Microsoft Windows SDK を参照してください。 トレースツールの詳細については、「Windows Driver Kit (WDK)」を参照してください。

<a name="remarks"></a>注釈
-------

この拡張機能を使用した後、プログラムを有効にするには、プログラムの実行を再開する必要があります (たとえば、 [**g (移動)**](g--go-.md)コマンドを使用します)。 短い時間が経過すると、対象のコンピューターは自動的にデバッガーに自動的に中断します。

トレースセッションが開始されると、システムによって序数 ( *LOGGER ID*) が割り当てられます。 その後、ロガー名またはロガー ID でセッションを参照できます。

ETW logger を停止するには、 [**! wmitrace**](-wmitrace-stop.md)を使用します。

 

 





