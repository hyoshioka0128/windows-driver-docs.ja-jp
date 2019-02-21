---
title: ks.ohdr
description: Ks.ohdr 拡張機能では、カーネル オブジェクトのヘッダーをストリームの詳細が表示されます。
ms.assetid: 0080565a-537d-44f4-9329-9ebe7fc926a1
keywords:
- デバッグ ks.ohdr Windows
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- ks.ohdr
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: fd0b4e8adee51a098eb9eab51fd96165b1cf151e
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56535612"
---
# <a name="ksohdr"></a>!ks.ohdr


**! Ks.ohdr**拡張機能には、カーネル オブジェクトのヘッダーをストリームの詳細が表示されます。

```dbgcmd
!ks.ohdr Object [Level] [Flags]  
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>パラメーター


<span id="_______Object______"></span><span id="_______object______"></span><span id="_______OBJECT______"></span> *オブジェクト*   
このパラメーターは、KS オブジェクト ヘッダーへのポインターを指定します。 場合*オブジェクト*が無効で、コマンドには、エラーが返されます。

<span id="_______Level______"></span><span id="_______level______"></span><span id="_______LEVEL______"></span> *レベル*   
(省略可能)。 値がの場合と同じ[ **! ks.dump**](-ks-dump.md)します。

<span id="_______Flags______"></span><span id="_______flags______"></span><span id="_______FLAGS______"></span> *フラグ*   
(省略可能)。 値がの場合と同じ[ **! ks.dump**](-ks-dump.md)します。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>Windows 2000</strong></p></td>
<td align="left"><p>winxp\Ks.dll</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>Windows XP 以降</strong></p></td>
<td align="left"><p>Ks.dll</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>追加情報

詳細については、次を参照してください。[ストリーミングのカーネル デバッグ](kernel-streaming-debugging.md)します。

<a name="remarks"></a>注釈
-------

**! Ks.ohdr**コマンドの動作と同様に[ **! ks.objhdr** ](-ks-objhdr.md) KS オブジェクトのヘッダーの詳細が表示されます。 違いは、呼び出し元が関連付けられているファイルのオブジェクトのアドレスではなく、KS オブジェクトのヘッダーの直接のアドレスを提供します。

レベルし、フラグの **! ks.ohdr**で説明したものと同じ[ **! ks.dump**](-ks-dump.md)します。

クエリを実行するデータがページ アウトされない場合は、使用を検討して[ **! ks.dump** ](-ks-dump.md)の代わりに **! ks.ohdr**します。

 

 





