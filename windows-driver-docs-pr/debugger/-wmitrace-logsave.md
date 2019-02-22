---
title: wmitrace.logsave
description: Wmitrace.logsave 拡張機能は、トレース セッションのトレース バッファーの現在の内容をファイルに書き込みます。
ms.assetid: 713fea09-d405-4142-b2e8-29c813a4c3b6
keywords:
- デバッグ wmitrace.logsave Windows
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- wmitrace.logsave
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 161bd2db2b65095be689769cfa5e2733024b2653
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56551423"
---
# <a name="wmitracelogsave"></a>!wmitrace.logsave


**! Wmitrace.logsave**拡張機能は、トレース セッションのトレース バッファーの現在の内容をファイルに書き込みます。

```dbgcmd
!wmitrace.logsave {LoggerID|LoggerName} Filename 
```

## <a name="span-idddkwmitracelogsavedbgspanspan-idddkwmitracelogsavedbgspanparameters"></a><span id="ddk__wmitrace_logsave_dbg"></span><span id="DDK__WMITRACE_LOGSAVE_DBG"></span>パラメーター


<span id="_______LoggerID______"></span><span id="_______loggerid______"></span><span id="_______LOGGERID______"></span> *LoggerID*   
トレース セッションを指定します。 *LoggerID*は序数をコンピューター上の各トレース セッションに割り当てられます。

<span id="_______LoggerName______"></span><span id="_______loggername______"></span><span id="_______LOGGERNAME______"></span> *LoggerName*   
トレース セッションを指定します。 *ロガー*テキスト名を指定は、トレース セッションが開始されたとき。

<span id="_______Filename______"></span><span id="_______filename______"></span><span id="_______FILENAME______"></span> *ファイル名*   
パス (省略可能) と出力ファイルのファイル名を指定します。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

この拡張機能は、Wmitrace.dll によってエクスポートされます。

この拡張機能は、Windows 2000 以降のバージョンの Windows で使用できます。 Windows 2000 でこの拡張機能を使用する場合は、w2kfre サブディレクトリに Wmitrace.dll ファイルを Windows 内のデバッグ ツールのインストール ディレクトリの winxp サブディレクトリからまずコピーする必要があります。

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>追加情報

イベントのトレースの概念的な概要については、Microsoft Windows SDK を参照してください。 トレース ログの詳細については、Windows Driver Kit (WDK) で「トレース ログ」を参照してください。

<a name="remarks"></a>注釈
-------

この拡張機能では、時にメモリ内のトレースだけが表示されます。 バッファーからフラッシュされ、イベント トレース ログ ファイルまたはトレース コンシューマーに配信されているトレース メッセージは表示されません。

トレース セッション バッファーは、ログ ファイルまたはリアルタイム表示用のトレース コンシューマーがフラッシュされるまで、トレース メッセージを保存します。 この拡張機能は、指定されたファイルの物理メモリ内のバッファーの内容を保存します。

出力は、バイナリ形式で記述されます。 通常、これらのファイルは、.etl (イベント トレース ログ) のファイル名拡張子を使用します。

循環バッファー トレース セッションを開始するトレース ログを使用する場合 (-バッファリング)、この拡張機能を使用して、現在のバッファーの内容を保存することができます。

トレース セッションのロガーの ID を検索するには、使用、 [ **! wmitrace.strdump** ](-wmitrace-strdump.md)拡張機能。 Tracelog コマンドのトレース ログ l を使用してトレース セッションとロガー ID などの基本的なプロパティを一覧表示または、

 

 





