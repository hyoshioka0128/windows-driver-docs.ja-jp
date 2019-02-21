---
Description: CDC ATM Networking Control Model
title: CDC ATM ネットワーク コントロール モデル
ms.localizationpriority: medium
ms.date: 01/07/2019
ms.openlocfilehash: 3a33ceb4f0c6aefd9710382e6be216b8e96cf829
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56537098"
---
# <a name="cdc-atm-networking-control-model"></a>CDC ATM ネットワーク コントロール モデル


USB CDC ATM ネットワーク コントロール モデル (ANCM) インターフェイスのコレクションには、次のプロパティがあります。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>プロパティ</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>リファレンス</p></td>
<td><p><em>ユニバーサル シリアル バス クラスの定義の通信デバイス</em>、バージョン 1.1 では、セクション 3.8.3</p></td>
</tr>
<tr class="even">
<td><p>マスターのインターフェイスのクラス</p></td>
<td><p>通信インターフェイス クラス (0x02)</p></td>
</tr>
<tr class="odd">
<td><p>マスターのインターフェイスのサブクラス</p></td>
<td><p>ANCM (0x07)</p></td>
</tr>
<tr class="even">
<td><p>プロトコル</p></td>
<td><p>None (0x00)</p></td>
</tr>
<tr class="odd">
<td><p>列挙</p></td>
<td><p>〇</p></td>
</tr>
<tr class="even">
<td><p>関連するインターフェイス</p></td>
<td><p>Union 関数型記述子 (UFD) によって参照される 1 つのデータ クラス インターフェイス</p></td>
</tr>
<tr class="odd">
<td><p>ハードウェア Id</p></td>
<td><pre space="preserve"><code class="language-syntax">USB\Vid_%04x&amp;Pid_%04x&amp;Rev_%04x&amp;Cdc_07&amp;MI_%02x
USB\Vid_%04x&amp;Pid_%04x&amp;Rev_%04x&amp;Cdc_07
USB\Vid_%04x&amp;Pid_%04x&amp;Cdc_07&amp;MI_%02x
USB\Vid_%04x&amp;Pid_%04x&amp;Cdc_07</code></pre></td>
</tr>
<tr class="even">
<td><p>互換性 Id</p></td>
<td><pre space="preserve"><code class="language-syntax">USB\Class_02&amp;SubClass_07&amp;Prot_00
USB\Class_02&amp;SubClass_07
USB\Class_02</code></pre></td>
</tr>
<tr class="odd">
<td><p>特別な処理</p></td>
<td><p>なし</p></td>
</tr>
</tbody>
</table>

 

 

 




