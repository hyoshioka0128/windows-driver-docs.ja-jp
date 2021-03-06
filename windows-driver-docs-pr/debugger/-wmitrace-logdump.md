---
title: wmitrace.logdump
description: Wmitrace.logdump 拡張機能は、トレース セッションのトレースのバッファーの内容を表示します。 指定されたプロバイダーからのトレース メッセージを表示を制限できます。
ms.assetid: 073338c6-68c4-4ae0-b69e-392256277236
keywords:
- デバッグ wmitrace.logdump Windows
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- wmitrace.logdump
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: e54c51edff5593b048ca03d33fa92d23c478e6bc
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67363068"
---
# <a name="wmitracelogdump"></a>!wmitrace.logdump


**! Wmitrace.logdump**拡張機能は、トレース セッションのトレースのバッファーの内容を表示します。 指定されたプロバイダーからのトレース メッセージを表示を制限できます。

```dbgcmd
!wmitrace.logdump [-t Count] [{LoggerID|LoggerName} [GUIDFile]] 
```

## <a name="span-idddkwmitracelogdumpdbgspanspan-idddkwmitracelogdumpdbgspanparameters"></a><span id="ddk__wmitrace_logdump_dbg"></span><span id="DDK__WMITRACE_LOGDUMP_DBG"></span>パラメーター


<span id="_______-t_______Count______"></span><span id="_______-t_______count______"></span><span id="_______-T_______COUNT______"></span> **-t** *数*   
最新のメッセージへの出力を制限します。 *カウント*を表示するメッセージの数を指定します。

<span id="_______LoggerID______"></span><span id="_______loggerid______"></span><span id="_______LOGGERID______"></span> *LoggerID*   
トレース セッションを指定します。 *LoggerID*は序数をコンピューター上の各トレース セッションに割り当てられます。 パラメーターが指定されていない場合は、id 1 と等しく、トレース セッションが使用されます。

<span id="_______LoggerName______"></span><span id="_______loggername______"></span><span id="_______LOGGERNAME______"></span> *LoggerName*   
トレース セッションを指定します。 *ロガー*テキスト名を指定は、トレース セッションが開始されたとき。

<span id="_______GUIDFile______"></span><span id="_______guidfile______"></span><span id="_______GUIDFILE______"></span> *GUIDFile*   
トレースで指定されたプロバイダーからのメッセージのみを表示、 *GUIDFile*ファイル。 *GUIDFile*コントロール .guid .ctl ファイルなど、1 つまたは複数のトレース プロバイダーの Guid を含むテキスト ファイルのファイル名とパス (省略可能) を表します。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

この拡張機能は、Wmitrace.dll によってエクスポートされます。

この拡張機能は、Windows 2000 以降のバージョンの Windows で使用できます。 Windows 2000 でこの拡張機能を使用する場合は、w2kfre サブディレクトリに Wmitrace.dll ファイルを Windows 内のデバッグ ツールのインストール ディレクトリの winxp サブディレクトリからまずコピーする必要があります。

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>追加情報

イベントのトレースの概念的な概要については、Microsoft Windows SDK を参照してください。 トレース ログの詳細については、Windows Driver Kit (WDK) で「トレース ログ」を参照してください。

<a name="remarks"></a>注釈
-------

Windows ソフトウェア トレース プリプロセッサ (WPP) ソフトウェア トレース、中にトレース セッションのバッファーを使用して、ログ ファイルまたはリアルタイム表示用のトレース コンシューマーがフラッシュされるまでに、トレース メッセージを格納します。 **! Wmitrace.logdump**拡張機能は、物理メモリ内のバッファーの内容を表示します。 デバッガー コマンド ウィンドウで、表示が表示されます。

この拡張機能は、クラッシュが発生したときに、最新のトレースを回復して、クラッシュ ダンプ ファイルに格納されているトレースを表示するには特に便利です。

この拡張機能を使用する前に使用して、 [ **! wmitrace.searchpath** ](-wmitrace-searchpath.md)または[ **! wmitrace.tmffile** ](-wmitrace-tmffile.md)トレース メッセージの形式のファイルを指定します。 システムでは、人間が判読できるテキストとして表示できるように、バッファー内のバイナリ トレース メッセージの書式を設定するのにトレース メッセージのフォーマット ファイルを使用します。

**注**  、ドライバーは、UMDF バージョン 1.11 以降を使用している場合を使用する必要はありません[ **! wmitrace.searchpath** ](-wmitrace-searchpath.md)または[ **! wmitrace.tmffile**](-wmitrace-tmffile.md).

 

循環バッファー トレース セッションを開始するトレース ログを使用する場合 (-バッファリング)、この拡張機能を使用して、バッファーの内容を表示します。

トレース セッションのロガーの ID を検索するには、使用、 [ **! wmitrace.strdump** ](-wmitrace-strdump.md)拡張機能。 Tracelog コマンドのトレース ログ l を使用してトレース セッションとロガー ID などの基本的なプロパティを一覧表示または、

この拡張機能は、WPP ソフトウェア トレース、およびイベント トレースの Windows の以前の (レガシー) メソッドの中にのみ役立ちます。 Manifested 他のプロバイダーによって生成されるトレース イベントはトレース メッセージの形式 (TMF) ファイルを使用しないと、この拡張機能でその内容が表示されないためです。

この拡張機能はのような[ **! wmitrace.eventlogdump** ](-wmitrace-eventlogdump.md)点を除いて、拡張機能の出力 **! wmitrace.logdump** WPP スタイル、およびの出力で書式設定 **! wmitrace.eventlogdump**イベント ログ スタイルで書式設定されます。 その形式は、データを表示するのに適切な拡張機能を選択する必要があります。

UMDF トレース ログを表示する方法については、次を参照してください。 [UMDF ベースのドライバーで WPP ソフトウェア トレースを使用して](https://docs.microsoft.com/windows-hardware/drivers/wdf/using-wpp-software-tracing-in-umdf-drivers#viewing-the-umdf-trace-log)します。

 

 





