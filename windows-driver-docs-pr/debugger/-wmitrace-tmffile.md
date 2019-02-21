---
title: wmitrace.tmffile
description: Wmitrace.tmffile 拡張機能では、トレース メッセージの形式 (TMF) ファイルを指定します。 この拡張機能で指定されたファイルは、表示またはほかの WMI のトレースの拡張機能によって書き込まれたトレース メッセージを書式設定に使用されます。
ms.assetid: 37ad335b-7604-466b-b328-7aebbc2fb5c1
keywords:
- デバッグ wmitrace.tmffile Windows
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- wmitrace.tmffile
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: e59697564d43fb52c23aa1dabd3a5e99bb39a684
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56535608"
---
# <a name="wmitracetmffile"></a>!wmitrace.tmffile


**! Wmitrace.tmffile**拡張機能は、トレース メッセージの形式 (TMF) ファイルを指定します。 この拡張機能で指定されたファイルは、表示またはほかの WMI のトレースの拡張機能によって書き込まれたトレース メッセージを書式設定に使用されます。

```dbgcmd
!wmitrace.tmffile TMFFile 
```

## <a name="span-idddkwmitracetmffiledbgspanspan-idddkwmitracetmffiledbgspanparameters"></a><span id="ddk__wmitrace_tmffile_dbg"></span><span id="DDK__WMITRACE_TMFFILE_DBG"></span>パラメーター


<span id="_______TMFFile______"></span><span id="_______tmffile______"></span><span id="_______TMFFILE______"></span> *TMFFile*   
トレース メッセージのフォーマット ファイルを指定します。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

この拡張機能は、Wmitrace.dll によってエクスポートされます。

この拡張機能は、Windows 2000 以降のバージョンの Windows で使用できます。 Windows 2000 でこの拡張機能を使用する場合は、w2kfre サブディレクトリに Wmitrace.dll ファイルを Windows 内のデバッグ ツールのインストール ディレクトリの winxp サブディレクトリからまずコピーする必要があります。

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>追加情報

イベントのトレースの概念的な概要については、Microsoft Windows SDK を参照してください。 トレース メッセージのフォーマット ファイルについては、Windows Driver Kit (WDK) で「トレース メッセージのフォーマット ファイル」のトピックを参照してください。

<a name="remarks"></a>注釈
-------

*トレース メッセージの形式のファイル*(.tmf) は、Windows ソフトウェア トレース プリプロセッサ (WPP) ソフトウェア トレース中に作成される構造化テキスト ファイルです。 これらのファイルには、人間が判読できる形式で表示できるように、トレース バイナリ トレース メッセージの書式設定の手順が含まれます。

トレース バッファー内のトレース メッセージを表示するために ([**! wmitrace.logdump**](-wmitrace-logdump.md)) ファイルへの書き込みまたは[ **(! wmitrace.logsave**](-wmitrace-logsave.md))、まず、トレース メッセージの TMF ファイルを識別する必要があります。

使用することができます[ **! wmitrace.searchpath** ](-wmitrace-searchpath.md)どの TMF ファイルが格納されるディレクトリを指定します。 システムでは、メッセージの書式設定命令を含む TMF ファイルのディレクトリが検索されます。 (を使用して、メッセージの GUID、メッセージを関連付ける正しい TMF ファイル。)

ただし、使用することができます **! wmitrace.tmffile**特定 TMF ファイルを指定します。 使用する必要があります **! wmitrace.tmffile** TMF ファイル名がメッセージに .tmf 拡張子 GUID ではない場合。 それ以外の場合、システムが見つけられない。

いずれかを使用しない場合[ **! wmitrace.searchpath** ](-wmitrace-searchpath.md)または **! wmitrace.tmffile**、システムは、トレースの値を使用して\_形式\_検索\_PATH 環境変数。 その変数が存在しない場合は、default.tmf ファイルが使用されます。 システムで、トレース メッセージの書式に関する情報が見つからない場合は、トレース メッセージの内容ではなく、「の書式情報が見つかりません」エラー メッセージを書き込みます。

**注**  、ドライバーは、UMDF バージョン 1.11 以降を使用している場合を使用する必要はありません[ **! wmitrace.searchpath** ](-wmitrace-searchpath.md)または **! wmitrace.tmffile**します。

 

この拡張機能は、WPP ソフトウェア トレース、およびイベント トレースの Windows の以前の (レガシー) メソッドの中にのみ役立ちます。 Manifested 他のプロバイダーによって生成されるトレース イベントはトレース メッセージの形式 (TMF) ファイルを使用しないと、それらでそのためこの拡張機能は使用できません。

 

 





