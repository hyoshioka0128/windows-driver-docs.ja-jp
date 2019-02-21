---
title: ubp
description: Ubp 拡張機能では、ユーザー領域で、ブレークポイントを設定します。
ms.assetid: 1aaa6bec-59d3-4e37-a1c6-af3554da809f
keywords:
- Windows デバッグ ubp
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- ubp
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 9703b641e383cc2cf036817379b9b9e7373a6b48
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56531340"
---
# <a name="ubp"></a>! ubp


**! Ubp**拡張機能は、ユーザー領域で、ブレークポイントを設定します。

```dbgcmd
!ubp Address 
```

## <a name="span-idddkubpdbgspanspan-idddkubpdbgspanparameters"></a><span id="ddk__ubp_dbg"></span><span id="DDK__UBP_DBG"></span>パラメーター


<span id="_______Address______"></span><span id="_______address______"></span><span id="_______ADDRESS______"></span> *アドレス*   
ブレークポイントが設定されるユーザー領域では、位置の 16 進数の仮想アドレスを指定します。

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
<td align="left"><p>Kdexts.dll</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>注釈
-------

**! Ubp**拡張機能は、ユーザー領域で、ブレークポイントを設定します。 実際の物理ページ仮想ページだけでなく、ブレークポイントが設定されます。

物理的なブレークポイントを設定すると、予期しない結果をページのすべての仮想コピーを同時に変更します。 1 つの考えられる結果は、バグ チェックやその他のシステム クラッシュことによると、システム状態の破損です。 したがって、これらのブレークポイントは、場合、すべての慎重に行って、使用する必要があります。

この拡張機能を使用して、メモリ不足のスワップの完了ページにブレークポイントを設定できません。 ブレークポイントを設定した後のメモリ不足、ページの交換の場合、ブレークポイントは存在しなくなります。

ページのテーブルまたはページのディレクトリ内にブレークポイントを設定することはできません。

各ブレークポイントが割り当てられている、*ブレークポイント番号*します。 割り当てられているブレークポイント番号を確認するには使用[ **! ubl**](-ubl.md)します。 作成時に、ブレークポイントが有効にします。 ブレークポイントにステップ イン、する必要があります最初に無効にすることを使用して[ **! スキャナー**](-ubd.md)します。 ブレークポイントをクリアする[ **! ubc**](-ubc.md)します。

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>参照してください。


[**!ubc**](-ubc.md)

[**! スキャナー**](-ubd.md)

[**! ube**](-ube.md)

[**!ubl**](-ubl.md)

[ユーザー領域とシステム領域](user-space-and-system-space.md)

 

 






