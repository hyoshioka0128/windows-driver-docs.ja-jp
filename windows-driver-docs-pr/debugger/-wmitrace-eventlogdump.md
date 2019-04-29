---
title: wmitrace.eventlogdump
description: Wmitrace.eventlogdump 拡張機能には、指定したロガーの内容が表示されます。 表示のイベント ログのような形式です。
ms.assetid: 27254b36-b413-45f0-9834-ff55fbb787c7
keywords:
- デバッグ wmitrace.eventlogdump Windows
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- wmitrace.eventlogdump
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 401564686ba5d3c6e2447ebe3bbd222a32a2fc59
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63332108"
---
# <a name="wmitraceeventlogdump"></a>!wmitrace.eventlogdump


**! Wmitrace.eventlogdump**拡張機能は、指定したロガーの内容を表示します。 表示のイベント ログのような形式です。

```dbgcmd
!wmitrace.eventlogdump { LoggerID | LoggerName }
```

## <a name="span-idddkwmitracestrdumpdbgspanspan-idddkwmitracestrdumpdbgspanparameters"></a><span id="ddk__wmitrace_strdump_dbg"></span><span id="DDK__WMITRACE_STRDUMP_DBG"></span>パラメーター


<span id="_______LoggerID______"></span><span id="_______loggerid______"></span><span id="_______LOGGERID______"></span> *LoggerID*   
トレース セッションを指定します。 *LoggerID*は序数をコンピューター上の各トレース セッションに割り当てられます。

<span id="_______LoggerName______"></span><span id="_______loggername______"></span><span id="_______LOGGERNAME______"></span> *LoggerName*   
トレース セッションを指定します。 *ロガー*テキスト名を指定は、トレース セッションが開始されたとき。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

この拡張機能は、Wmitrace.dll によってエクスポートされます。

この拡張機能は、Windows 2000 以降のバージョンの Windows で使用できます。 Windows 2000 でこの拡張機能を使用する場合は、w2kfre サブディレクトリに Wmitrace.dll ファイルを Windows 内のデバッグ ツールのインストール ディレクトリの winxp サブディレクトリからまずコピーする必要があります。

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>追加情報

イベントのトレースの概念的な概要については、Microsoft Windows SDK を参照してください。 トレース ツールについては、Windows Driver Kit (WDK) を参照してください。

<a name="remarks"></a>注釈
-------

この拡張機能はのような[ **! wmitrace.logdump** ](-wmitrace-logdump.md)点を除いて、拡張機能の出力 **! wmitrace.eventlogdump**でイベント ログ スタイル、および、出力の書式設定 **! wmitrace.logdump** Windows ソフトウェア トレース プリプロセッサ (WPP) スタイルで書式設定されます。 その形式は、データを表示するのに適切な拡張機能を選択する必要があります。

トレース セッションのロガーの ID を検索するには、使用、 [ **! wmitrace.strdump** ](-wmitrace-strdump.md)拡張機能。 Tracelog コマンドのトレース ログ l を使用してトレース セッションとロガー ID などの基本的なプロパティを一覧表示または、

 

 





