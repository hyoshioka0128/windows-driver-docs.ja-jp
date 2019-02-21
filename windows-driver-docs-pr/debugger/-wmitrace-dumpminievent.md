---
title: wmitrace.dumpminievent
description: Wmitrace.dumpminievent 拡張機能では、ダンプ ファイルに格納されているシステム イベント ログ トレース フラグメントが表示されます。
ms.assetid: 94debe5f-d125-44d0-99c4-90d8794525df
keywords:
- デバッグ wmitrace.dumpminievent Windows
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- wmitrace.dumpminievent
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 2881cbcef477c2b111d43cf0e40ee55566614813
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56559077"
---
# <a name="wmitracedumpminievent"></a>!wmitrace.dumpminievent


**! Wmitrace.dumpminievent**拡張機能には、ダンプ ファイルに格納されているシステム イベント ログ トレース フラグメントが表示されます。

```dbgcmd
!wmitrace.dumpminievent
```

## <span id="ddk__wmitrace_strdump_dbg"></span><span id="DDK__WMITRACE_STRDUMP_DBG"></span>


### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

この拡張機能は、Wmitrace.dll によってエクスポートされます。

この拡張機能は、Windows Vista Service Pack 1 (SP1) および以降のバージョンの Windows で使用できます。

ミニダンプ ファイルまたは完全なダンプ ファイルをデバッグする場合にのみ、この拡張機能は便利です。

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>追加情報

イベントのトレースの概念的な概要については、Microsoft Windows SDK を参照してください。 トレース ツールについては、Windows Driver Kit (WDK) を参照してください。

<a name="remarks"></a>注釈
-------

*システム イベント ログのトレース フラグメント*システム イベント ログの最後のバッファーの内容のコピーです。 **! Wmitrace.dumpminievent**拡張機能は、イベント ログの形式でその内容を表示します。

 

 





