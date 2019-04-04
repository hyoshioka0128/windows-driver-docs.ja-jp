---
title: amli lc
description: Amli lc 拡張機能には、アクティブなすべての ACPI コンテキストが一覧表示します。
ms.assetid: 070db570-ab8c-47ce-88fa-dc5f16c1c2ee
keywords:
- Windows デバッグ amli lc
ms.date: 09/17/2018
topic_type:
- apiref
api_name:
- amli lc
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: ff147399d03ba9688024a7a6468e09ccb3937741
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56582057"
---
# <a name="amli-lc"></a>!amli lc


**! Amli lc**拡張機能は、アクティブなすべての ACPI コンテキストを一覧表示されます。

構文

```dbgcmd
   !amli lc
```

## <span id="ddk__amli_lc_dbg"></span><span id="DDK__AMLI_LC_DBG"></span>


### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

Kdexts.dll

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>追加情報

関連するコマンドとその用途については、[AMLI デバッガー](the-amli-debugger.md)を参照してください。

<a name="remarks"></a>コメント
-------

各コンテキストは、AML インタープリターで現在実行されているメソッドに対応します。

以下に例を示します。

```console
AMLI(? for help)-> lc
 Ctxt=80e3f000, ThID=00000000, Flgs=A--C-----, pbOp=00000000, Obj=\_SB.LNKA._STA
 Ctxt=80e41000, ThID=00000000, Flgs=A--C-----, pbOp=00000000, Obj=\_SB.LNKB._STA
 Ctxt=80e9a000, ThID=00000000, Flgs=A--C-----, pbOp=00000000, Obj=\_SB.LNKC._STA
 Ctxt=80ea8000, ThID=00000000, Flgs=A--C-----, pbOp=00000000, Obj=\_SB.LNKD._STA
*Ctxt=80e12000, ThID=80e6eda8, Flgs=---CR----, pbOp=80e5d5ac, Obj=\_SB.LNKA._STA
```

**Obj** ACPI テーブルに表示されるフィールドは、完全なパスと、メソッドの名前。

**Ctxt**フィールドはコンテキスト ブロックのアドレスを与えます。 アスタリスク (**\\**<em>) を示す、* 現在のコンテキスト</em>します。 これは、中断が発生したときに、インタープリターで実行されていたコンテキストです。

省略形**pbOp**命令ポインター (二項演算のコードへのポインター) を示します。

表示可能な 9 つのフラグがあります、 **Flgs**セクション。 フラグが設定されていない場合は、ハイフンが代わりに表示されます。 フラグの完全な一覧は次のとおりです。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">Flag</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>A</p></td>
<td align="left"><p>非同期の評価</p></td>
</tr>
<tr class="even">
<td align="left"><p>N</p></td>
<td align="left"><p>入れ子になった評価</p></td>
</tr>
<tr class="odd">
<td align="left"><p>Q</p></td>
<td align="left"><p>準備完了キュー</p></td>
</tr>
<tr class="even">
<td align="left"><p>C</p></td>
<td align="left"><p>コールバックを必要があります。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>R</p></td>
<td align="left"><p>実行中</p></td>
</tr>
<tr class="even">
<td align="left"><p>W</p></td>
<td align="left"><p>準備完了</p></td>
</tr>
<tr class="odd">
<td align="left"><p>T</p></td>
<td align="left"><p>タイムアウト</p></td>
</tr>
<tr class="even">
<td align="left"><p>D</p></td>
<td align="left"><p>タイマーのディスパッチ</p></td>
</tr>
<tr class="odd">
<td align="left"><p>P</p></td>
<td align="left"><p>保留中のタイマー</p></td>
</tr>
</tbody>
</table>

 

 

 





