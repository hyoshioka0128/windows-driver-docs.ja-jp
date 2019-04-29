---
title: Maintain a list of objects for each type
description: Maintain a list of objects for each type
ms.assetid: 845ba6cb-60b3-4053-9d54-f43ed344f82d
keywords:
- (グローバル フラグ) の種類ごとのオブジェクトの一覧を管理します。
ms.date: 10/25/2018
ms.localizationpriority: medium
ms.openlocfilehash: b79010fbef678be9374226caa067e6258ddd223d
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63383311"
---
# <a name="maintain-a-list-of-objects-for-each-type"></a>Maintain a list of objects for each type


## <span id="ddk_maintain_a_list_of_objects_for_each_type_dtools"></span><span id="DDK_MAINTAIN_A_LIST_OF_OBJECTS_FOR_EACH_TYPE_DTOOLS"></span>


**各型のオブジェクトのリストを維持**フラグが収集し、イベント、ミュー テックス、セマフォなどのオブジェクトの種類によってアクティブなオブジェクトのリストを保持します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>省略形</strong></p></td>
<td align="left"><p>otl</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>16 進数の値</strong></p></td>
<td align="left"><p>0x4000</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>シンボリック名</strong></p></td>
<td align="left"><p>FLG_MAINTAIN_OBJECT_TYPELIST</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>Destination (公開先)</strong></p></td>
<td align="left"><p>システム全体のレジストリ エントリ</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idcommentsspanspan-idcommentsspancomments"></a><span id="comments"></span><span id="COMMENTS"></span>コメント

オブジェクトの一覧を表示するには、sysinternals ツールを使用して[処理](https://docs.microsoft.com/sysinternals/downloads/handle)します。

**注**  このフラグを設定するときに作成するリンクのリストは、オブジェクトごとに 8 バイトのオーバーヘッドを使用します。 分析が完了すると、このフラグをオフにしてください。

 

 

 





