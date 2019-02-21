---
title: wmitrace.dumpmini
description: Wmitrace.dumpmini 拡張機能では、ダンプ ファイルに格納されているシステム トレース フラグメントが表示されます。
ms.assetid: c6b4c09f-3a73-4467-849b-8570477bc9af
keywords:
- デバッグ wmitrace.dumpmini Windows
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- wmitrace.dumpmini
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: ee4b78a48d3b20ee2a72f550f08da81499562f40
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56557041"
---
# <a name="wmitracedumpmini"></a>!wmitrace.dumpmini


**! Wmitrace.dumpmini**拡張機能には、ダンプ ファイルに格納されているシステム トレース フラグメントが表示されます。

```dbgcmd
!wmitrace.dumpmini
```

## <span id="ddk__wmitrace_strdump_dbg"></span><span id="DDK__WMITRACE_STRDUMP_DBG"></span>


### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

この拡張機能は、Wmitrace.dll によってエクスポートされます。

この拡張機能は、Windows Vista および Windows の以降のバージョンで使用できます。

ミニダンプ ファイルまたは完全なダンプ ファイルをデバッグする場合にのみ、この拡張機能は便利です。

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>追加情報

イベントのトレースの概念的な概要については、Microsoft Windows SDK を参照してください。 トレース ツールについては、Windows Driver Kit (WDK) を参照してください。

<a name="remarks"></a>注釈
-------

*システム トレース フラグメント*システム コンテキストのログの最後のバッファーの内容のコピーです。 通常の状況では、これは、ロガー ID を持つ 2 は、トレース セッションです。

 

 





