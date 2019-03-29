---
title: tokenfields
description: Tokenfields 拡張機能では、名前とアクセス トークンのオブジェクト (トークンの構造) 内のフィールドのオフセットが表示されます。
ms.assetid: dfadfdb0-1ed8-4c21-9207-dc02d7435475
keywords:
- トークン
- Windows デバッグ tokenfields
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- tokenfields
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 1d0e0e7574e229e8edb9b26fc7f9d0eea43628b7
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56579678"
---
# <a name="tokenfields"></a>!tokenfields


**! Tokenfields**拡張機能は、名前とアクセス トークンのオブジェクト (トークンの構造) 内のフィールドのオフセットが表示されます。

```dbgcmd
!tokenfields
```

## <span id="ddk__tokenfields_dbg"></span><span id="DDK__TOKENFIELDS_DBG"></span>


### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>Windows 2000</strong></p></td>
<td align="left"><p>Kdextx86.dll</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>Windows XP 以降</strong></p></td>
<td align="left"><p>利用不可 (「解説」を参照してください)</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>追加情報

トークンの構造については、次を参照してください。 *Microsoft Windows internals 』*、Mark Russinovich と David Solomon します。 この本は、いくつかの言語と国でできない場合があります。(Microsoft Windows SDK のドキュメントで説明されているユーザー モードのトークン構造は、若干異なる)。

<a name="remarks"></a>コメント
-------

この拡張機能のコマンドは、Windows XP または Windows の以降のバージョンでご利用いただけません。 代わりに、使用、 [ **dt (表示の種類)** ](dt--display-type-.md)トークンの構造を直接表示するコマンド。

```dbgcmd
kd> dt nt!_TOKEN 
```

トークンの構造の特定のインスタンスを表示する、 [ **! トークン**](-token.md)拡張機能。

次の例に示します **! tokenfields** Windows 2000 システムから。

```dbgcmd
kd> !tokenfields
 TOKEN structure offsets:
    TokenSource:           0x0
    AuthenticationId:      0x18
    ExpirationTime:        0x28
    ModifiedId:            0x30
    UserAndGroupCount:     0x3c
    PrivilegeCount:        0x44
    VariableLength:        0x48
    DynamicCharged:        0x4c
    DynamicAvailable:      0x50
    DefaultOwnerIndex:     0x54
    DefaultDacl:           0x6c
    TokenType:             0x70
    ImpersonationLevel:    0x74
    TokenFlags:            0x78
    TokenInUse:            0x79
 ProxyData:             0x7c
    AuditData:             0x80
    VariablePart:          0x84
```

 

 





