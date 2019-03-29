---
title: nstree
description: Nstree 拡張機能は、名前空間ツリーで、ACPI 名前空間のオブジェクトとその子を表示します。
ms.assetid: 0dec2a5a-ca77-4f91-9128-2d3dd8cd035f
keywords:
- Windows デバッグ nstree
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- nstree
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: a4b13fa75fec8c3efae4629c20843d76bf338bf5
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56581743"
---
# <a name="nstree"></a>!nstree


**! Nstree**拡張機能を ACPI 名前空間のオブジェクトとその子名前空間ツリーで表示します。

構文

```dbgcmd
!nstree [Address]
```

## <a name="span-idddknstreedbgspanspan-idddknstreedbgspanparameters"></a><span id="ddk__nstree_dbg"></span><span id="DDK__NSTREE_DBG"></span>パラメーター


<span id="_______Address______"></span><span id="_______address______"></span><span id="_______ADDRESS______"></span> *アドレス*   
名前空間オブジェクトのアドレスを指定します。 このオブジェクトと下位にある名前空間の全体のツリーが表示されます。 場合*アドレス*は省略すると、名前空間の全体のツリーが表示されます。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

Kdexts.dll

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>追加情報

詳細については、次を参照してください。 [ACPI デバッグ](acpi-debugging.md)します。

<a name="remarks"></a>コメント
-------

この拡張機能は等しく[ **! amli dns/s**](-amli-dns.md)します。

 

 





