---
title: wmitrace.strdump
description: Wmitrace.strdump 拡張機能では、WMI イベントのトレースの構造が表示されます。 構造体への特定のトレース セッションの表示を制限することができます。
ms.assetid: 3fd1c4d5-c3c6-40b5-90f4-e5453bb56b19
keywords:
- デバッグ wmitrace.strdump Windows
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- wmitrace.strdump
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: eed7fdf94c88568ab767bd8c2d4b72e8d7c0acd3
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56535939"
---
# <a name="wmitracestrdump"></a>!wmitrace.strdump


**! Wmitrace.strdump**拡張機能には、WMI イベントのトレースの構造が表示されます。 構造体への特定のトレース セッションの表示を制限することができます。

```dbgcmd
!wmitrace.strdump [ LoggerID | LoggerName ] 
```

## <a name="span-idddkwmitracestrdumpdbgspanspan-idddkwmitracestrdumpdbgspanparameters"></a><span id="ddk__wmitrace_strdump_dbg"></span><span id="DDK__WMITRACE_STRDUMP_DBG"></span>パラメーター


<span id="_______LoggerID______"></span><span id="_______loggerid______"></span><span id="_______LOGGERID______"></span> *LoggerID*   
指定されたトレース セッションのイベント トレースの構造を表示を制限します。 *LoggerID*トレース セッションを指定します。 コンピューター上の各トレース セッションに、システムを代入する序数になります。 パラメーターが指定されていない場合は、すべてのトレース セッションが表示されます。

<span id="_______LoggerName______"></span><span id="_______loggername______"></span><span id="_______LOGGERNAME______"></span> *LoggerName*   
指定されたトレース セッションのイベント トレースの構造を表示を制限します。 *ロガー*テキスト名を指定は、トレース セッションが開始されたとき。 パラメーターが指定されていない場合は、すべてのトレース セッションが表示されます。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

この拡張機能は、Wmitrace.dll によってエクスポートされます。

この拡張機能は、Windows 2000 以降のバージョンの Windows で使用できます。 Windows 2000 でこの拡張機能を使用する場合は、w2kfre サブディレクトリに Wmitrace.dll ファイルを Windows 内のデバッグ ツールのインストール ディレクトリの winxp サブディレクトリからまずコピーする必要があります。

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>追加情報

イベントのトレースの概念的な概要については、Microsoft Windows SDK を参照してください。 トレース ログの詳細については、Windows Driver Kit (WDK) で「Tracelog」トピックを参照してください。

<a name="remarks"></a>注釈
-------

トレース セッションのロガーの ID を検索するには、使用、 **! wmitrace.strdump**拡張機能。 Tracelog コマンドのトレース ログ l を使用してトレース セッションとロガー ID などの基本的なプロパティを一覧表示または、

 

 





