---
title: nsobj
description: Nsobj 拡張機能は、ACPI 名前空間オブジェクトを表示します。
ms.assetid: 348aeb42-41c6-42de-bb43-b075f55076c4
keywords:
- Windows デバッグ nsobj
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- nsobj
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 6fa7464ca3cd5439aad8367189283e02f8f27d4d
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56552471"
---
# <a name="nsobj"></a>!nsobj


**! Nsobj**拡張機能は、ACPI 名前空間オブジェクトを表示します。

構文

```dbgcmd
!nsobj [Address]
```

## <a name="span-idddknsobjdbgspanspan-idddknsobjdbgspanparameters"></a><span id="ddk__nsobj_dbg"></span><span id="DDK__NSOBJ_DBG"></span>パラメーター


<span id="_______Address______"></span><span id="_______address______"></span><span id="_______ADDRESS______"></span> *アドレス*   
名前空間オブジェクトのアドレスを指定します。 これを省略すると、名前空間ツリーのルートが使用されます。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

Kdexts.dll

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>追加情報

詳細については、[ACPI デバッグ](acpi-debugging.md)を参照してください。

<a name="remarks"></a>注釈
-------

この拡張機能は等しく[ **! amli dns**](-amli-dns.md)します。

 

 





