---
Description: マルチ チャネルの CDC ISDN コントロール モデル
title: マルチ チャネルの CDC ISDN コントロール モデル
ms.localizationpriority: medium
ms.date: 01/07/2019
ms.openlocfilehash: 31168fbb4acb51d27f69ecdac3dcc6a332ec20f9
ms.sourcegitcommit: 6dff49ca5880466c396be5b889c44481dfed44ec
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/17/2019
ms.locfileid: "67161344"
---
# <a name="cdc-multi-channel-isdn-control-model"></a>マルチ チャネルの CDC ISDN コントロール モデル


USB CDC マルチ チャンネル ISDN コントロール モデル (MCCM) インターフェイスのコレクションには、次のプロパティがあります。

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
<td><p><em>ユニバーサル シリアル バス クラスの定義の通信デバイス</em>、バージョン 1.1 では、3.7.1</p></td>
</tr>
<tr class="even">
<td><p>マスターのインターフェイスのクラス</p></td>
<td><p>通信インターフェイス クラス (0x02)</p></td>
</tr>
<tr class="odd">
<td><p>マスターのインターフェイスのサブクラス</p></td>
<td><p>MCCM (0X04)</p></td>
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
<td><p>Union 関数型記述子 (UFD) を参照する複数のデータ クラス インターフェイス。</p></td>
</tr>
<tr class="odd">
<td><p>ハードウェア Id</p></td>
<td><pre space="preserve"><code class="language-syntax">USB\Vid_%04x&Pid_%04x&Rev_%04x&Cdc_04&MI_%02x
USB\Vid_%04x&Pid_%04x&Rev_%04x&Cdc_04
USB\Vid_%04x&Pid_%04x&Cdc_04&MI_%02x
USB\Vid_%04x&Pid_%04x&Cdc_04</code></pre></td>
</tr>
<tr class="even">
<td><p>互換性 Id</p></td>
<td><pre space="preserve"><code class="language-syntax">USB\Class_02&SubClass_04&Prot_00
USB\Class_02&SubClass_04
USB\Class_02</code></pre></td>
</tr>
<tr class="odd">
<td><p>特別な処理</p></td>
<td><p>なし</p></td>
</tr>
</tbody>
</table>

 

 

 




