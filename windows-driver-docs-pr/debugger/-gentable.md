---
title: gentable
description: Gentable 拡張機能では、RTL_GENERIC_TABLE が表示されます。
ms.assetid: acf85ff8-9004-4c8e-b67f-20202c577aab
keywords:
- Windows デバッグ gentable
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- gentable
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: cde0ff5119e6eb4848fc825ccbd4aeb1e1857548
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63336848"
---
# <a name="gentable"></a>!gentable


**! Gentable**拡張機能の表示、RTL\_ジェネリック\_テーブル。

構文

```dbgcmd
!gentable Address[Flag]
```

## <a name="span-idddkgentabledbgspanspan-idddkgentabledbgspanparameters"></a><span id="ddk__gentable_dbg"></span><span id="DDK__GENTABLE_DBG"></span>パラメーター


<span id="_______Address______"></span><span id="_______address______"></span><span id="_______ADDRESS______"></span> *アドレス*   
RTL のアドレス指定\_ジェネリック\_テーブル。

<span id="_______Flag______"></span><span id="_______flag______"></span><span id="_______FLAG______"></span> *フラグ*   
テーブル ソースを指定します。 場合*フラグ*1 に設定されて、AVL テーブルを使用します。 場合*フラグ*が 0 または省略すると、非 AVL テーブルを使用します。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

Kdexts.dll

 

 





