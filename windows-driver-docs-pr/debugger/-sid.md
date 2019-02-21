---
title: sid
description: Sid の拡張機能では、指定したアドレスにセキュリティ識別子 (SID) が表示されます。
ms.assetid: 7b93eb0e-7c0f-4c30-851b-6f40c7df8e1b
keywords:
- sid Windows デバッグ
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- sid
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 9c1e5a1d1afd2814d5b04962a57259af2ebcbac9
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56537681"
---
# <a name="sid"></a>!sid


**! Sid**拡張機能では、指定したアドレスにセキュリティ識別子 (SID) が表示されます。

構文

```dbgcmd
!sid Address [Flags] 
```

## <a name="span-idddksiddbgspanspan-idddksiddbgspanparameters"></a><span id="ddk__sid_dbg"></span><span id="DDK__SID_DBG"></span>パラメーター


<span id="_______Address______"></span><span id="_______address______"></span><span id="_______ADDRESS______"></span> *アドレス*   
SID 構造体のアドレスを指定します。

<span id="_______Flags______"></span><span id="_______flags______"></span><span id="_______FLAGS______"></span> *フラグ*   
これは、1 に設定されている場合、SID の SID の種類、ドメイン、およびユーザー名が表示されます。

これは、1 に設定されている場合は、フレンドリ名が表示されます。 これには、SID のドメインとユーザー名と SID の種類が含まれます。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

Exts.dll

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>追加情報

Sid の詳細については、Microsoft Windows SDK ドキュメントに、Windows Driver Kit (WDK) ドキュメントを参照してください。 または*Microsoft Windows internals 』* Mark Russinovich と David Solomon します。 参照してください[ **! sd** ](-sd.md)と[ **! acl**](-acl.md)します。

<a name="remarks"></a>注釈
-------

次に示すように、フレンドリ名のないと使用の 2 つの例に示します。

```dbgcmd
kd> !sid 0xe1bf35b8
SID is: S-1-5-21-518066528-515770016-299552555-513

kd> !sid 0xe1bf35b8 1
SID is: S-1-5-21-518066528-515770016-299552555-513 (Group: MYGROUP\Domain Users)
```

 

 





