---
title: wmitrace.logger
description: Wmitrace.logger 拡張機能には、セッションの構成データを含む、トレース セッションに関するデータが表示されます。 この拡張機能では、セッション中に生成されたトレース メッセージは表示されません。
ms.assetid: 2bc456db-3e97-49f8-9c57-75ee5fee0f9d
keywords:
- デバッグ wmitrace.logger Windows
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- wmitrace.logger
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 0e3224872752045ad29a6f0c57a70d638050cd40
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56551701"
---
# <a name="wmitracelogger"></a>!wmitrace.logger


**! Wmitrace.logger**拡張機能には、セッションの構成データを含む、トレース セッションに関するデータが表示されます。 この拡張機能では、セッション中に生成されたトレース メッセージは表示されません。

```dbgcmd
!wmitrace.logger [ LoggerID | LoggerName ]
```

## <a name="span-idddkwmittraceloggerdbgspanspan-idddkwmittraceloggerdbgspanparameters"></a><span id="ddk__wmittrace_logger_dbg"></span><span id="DDK__WMITTRACE_LOGGER_DBG"></span>パラメーター


<span id="_______LoggerID______"></span><span id="_______loggerid______"></span><span id="_______LOGGERID______"></span> *LoggerID*   
トレース セッションを指定します。 *LoggerID*は序数をコンピューター上の各トレース セッションに割り当てられます。 パラメーターが指定されていない場合は、id 1 と等しく、トレース セッションが使用されます。

<span id="_______LoggerName______"></span><span id="_______loggername______"></span><span id="_______LOGGERNAME______"></span> *LoggerName*   
トレース セッションを指定します。 *ロガー*テキスト名を指定は、トレース セッションが開始されたとき。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

この拡張機能は、Wmitrace.dll によってエクスポートされます。

この拡張機能は、Windows 2000 以降のバージョンの Windows で使用できます。 Windows 2000 でこの拡張機能を使用する場合は、w2kfre サブディレクトリに Wmitrace.dll ファイルを Windows 内のデバッグ ツールのインストール ディレクトリの winxp サブディレクトリからまずコピーする必要があります。

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>追加情報

イベントのトレースの概念的な概要については、Microsoft Windows SDK を参照してください。

<a name="remarks"></a>注釈
-------

この拡張機能は、パフォーマンス ログとイベントで、人間が判読できる表示用にフォーマットできませんに設計されています。 ヘッダーのデータと共に、トレース セッション バッファーにトレース メッセージを表示するには使用[ **! wmitrace.logdump**](-wmitrace-logdump.md)します。

トレース セッションのロガーの ID を検索するには、使用、 [ **! wmitrace.strdump** ](-wmitrace-strdump.md)拡張機能。 Tracelog コマンドのトレース ログ l を使用してトレース セッションとロガー ID などの基本的なプロパティを一覧表示または、

 

 





