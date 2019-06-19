---
Description: CDC ダイレクト行コントロール モデル
title: CDC ダイレクト行コントロール モデル
ms.localizationpriority: medium
ms.date: 01/07/2019
ms.openlocfilehash: 94d5efdcc531c0e028d8c905f1023f20ad8a8bc4
ms.sourcegitcommit: 6dff49ca5880466c396be5b889c44481dfed44ec
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/17/2019
ms.locfileid: "67161584"
---
# <a name="cdc-direct-line-control-model"></a>CDC ダイレクト行コントロール モデル


USB CDC 直接行コントロール モデル (DLCM) インターフェイスのコレクションには、次のプロパティがあります。

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
<td><p><em>ユニバーサル シリアル バス クラスの定義の通信デバイス</em>、バージョン 1.1 では、セクション 3.6.1 します。</p></td>
</tr>
<tr class="even">
<td><p>マスターのインターフェイスのクラス</p></td>
<td><p>通信インターフェイス クラス (0x02) です。</p></td>
</tr>
<tr class="odd">
<td><p>マスターのインターフェイスのサブクラス</p></td>
<td><p>DLCM (0x01).</p></td>
</tr>
<tr class="even">
<td><p>プロトコル</p></td>
<td><p>None (0x00) です。</p></td>
</tr>
<tr class="odd">
<td><p>列挙</p></td>
<td><p>[はい]。</p></td>
</tr>
<tr class="even">
<td><p>関連するインターフェイス</p></td>
<td><p>Union 関数型記述子 (UFD) を参照するオーディオ クラスまたはベンダー定義のインターフェイス。</p></td>
</tr>
<tr class="odd">
<td><p>ハードウェア Id</p></td>
<td><pre space="preserve"><code class="language-syntax">USB\Vid_%04x&Pid_%04x&Rev_%04x&Cdc_01&MI_%02x
USB\Vid_%04x&Pid_%04x&Rev_%04x&Cdc_01
USB\Vid_%04x&Pid_%04x&Cdc_01&MI_%02x
USB\Vid_%04x&Pid_%04x&Cdc_01</code></pre></td>
</tr>
<tr class="even">
<td><p>互換性 Id</p></td>
<td><pre space="preserve"><code class="language-syntax">USB\Class_02&SubClass_01&Prot_00
USB\Class_02&SubClass_01
USB\Class_02</code></pre></td>
</tr>
<tr class="odd">
<td><p>特別な処理</p></td>
<td><p>UFD は、DLCM インターフェイスのコレクションとは無関係に列挙されているオーディオ クラス インターフェイスのコレクションを参照します。</p></td>
</tr>
</tbody>
</table>

 

 

 




