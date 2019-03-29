---
title: amli ds
description: Amli ds 拡張機能では、AML スタックを表示します。
ms.assetid: 62a1a1dd-c0d8-4509-a29f-16ad2b96b412
keywords:
- Windows デバッグ amli ds
ms.date: 09/17/2018
topic_type:
- apiref
api_name:
- amli ds
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: bfc0817c355b763646b49e0fa6515736042184a6
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56581785"
---
# <a name="amli-ds"></a>!amli ds


**! Amli ds**拡張機能には、AML スタックが表示されます。

構文

```dbgcmd
    !amli ds [/v] [Address] 
```

## <a name="span-idddkamlidsdbgspanspan-idddkamlidsdbgspanparameters"></a><span id="ddk__amli_ds_dbg"></span><span id="DDK__AMLI_DS_DBG"></span>パラメーター


<span id="________v______"></span><span id="________V______"></span> **/v**   
詳細情報の表示をによりします。 Windows 2000 では、このオプションはこの拡張機能のチェック ビルドを使用している場合にのみ使用できます (w2kchk\\Acpikd.dll)。

<span id="_______Address______"></span><span id="_______address______"></span><span id="_______ADDRESS______"></span> *アドレス*   
スタックが必要なコンテキスト ブロックのアドレスを指定します。 場合*アドレス*は省略すると、現在のコンテキストが使用されます。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

! スタックの拡張機能は、カーネル スタックに関する情報を表示します。

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>追加情報

関連するコマンドとその用途については、次を参照してください。 [AMLI デバッガー](the-amli-debugger.md)します。

 

 





