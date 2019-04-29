---
title: amli bl
description: Amli bl 拡張機能は、すべての AML ブレークポイントの一覧を表示します。
ms.assetid: 4ce52006-d44e-40ab-b669-2aa9509b6b21
keywords:
- Windows デバッグ amli bl
ms.date: 09/17/2018
topic_type:
- apiref
api_name:
- amli bl
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: aeb69d43659916b55b6b9239733b167ba9e2f363
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63334780"
---
# <a name="amli-bl"></a>!amli bl


**! Amli bl**拡張機能は、すべての AML ブレークポイントの一覧を表示します。

構文

```dbgcmd
   !amli bl
```

## <span id="ddk__amli_bl_dbg"></span><span id="DDK__AMLI_BL_DBG"></span>


### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

Kdexts.dll

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>追加情報

関連するコマンドとその用途については、次を参照してください。 [AMLI デバッガー](the-amli-debugger.md)します。

<a name="remarks"></a>注釈
-------

AMLI デバッガーには、最大 10 個のブレークポイントがサポートしています。

次の例に示します、 **! amli bl**拡張機能。

```console
kd> !amli bl
 0: <e> ffffffff80e5e2f1:[\_SB.LNKD._SRS]
 1: <e> ffffffff80e5d969:[\_SB.LNKB._STA]
 2: <d> ffffffff80e630c9:[\_WAK]
 3: <e> ffffffff80e612c9:[\_SB.MBRD._CRS]
```

最初の列には、ブレークポイント番号が与えられます。 **&lt;E&gt;** と**&lt;d&gt;** マークは、ブレークポイントが有効になっているか、無効になっているかどうかを示します。 ブレークポイントのアドレスは、次回のコラムでは。 最後に、メソッドの先頭に設定されていない場合、ブレークポイントのオフセットで、ブレークポイントを含むメソッドにあります。

 

 





