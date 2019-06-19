---
Description: WMCDC デバイスの管理モデル
title: WMCDC デバイスの管理モデル
ms.localizationpriority: medium
ms.date: 01/07/2019
ms.openlocfilehash: 81849e1e2b1fa86332d264b106b6798b090050ab
ms.sourcegitcommit: 6dff49ca5880466c396be5b889c44481dfed44ec
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/17/2019
ms.locfileid: "67161582"
---
# <a name="wmcdc-device-management-model"></a>WMCDC デバイスの管理モデル


USB WMCDC デバイスの管理モデル (DMM) インターフェイスのコレクションには、次のプロパティがあります。

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
<td><p><em>ユニバーサル シリアル バス CDC サブクラス仕様のワイヤレス モバイル通信デバイス</em>、バージョン 1.0 では、セクション 6.6 します。</p></td>
</tr>
<tr class="even">
<td><p>マスターのインターフェイスのクラス</p></td>
<td><p>通信インターフェイス クラス (0x02) です。</p></td>
</tr>
<tr class="odd">
<td><p>マスターのインターフェイスのサブクラス</p></td>
<td><p>DMM (0X09)。</p></td>
</tr>
<tr class="even">
<td><p>プロトコル</p></td>
<td><p>任意です。</p></td>
</tr>
<tr class="odd">
<td><p>列挙</p></td>
<td><p>[はい]。</p></td>
</tr>
<tr class="even">
<td><p>関連するインターフェイス</p></td>
<td><p>なし。</p></td>
</tr>
<tr class="odd">
<td><p>ハードウェア Id</p></td>
<td><pre space="preserve"><code class="language-syntax">USB\Vid_%04x&Pid_%04x&Rev_%04x&Cdc_09&MI_%02x
USB\Vid_%04x&Pid_%04x&Rev_%04x&Cdc_09
USB\Vid_%04x&Pid_%04x&Cdc_09&MI_%02x
USB\Vid_%04x&Pid_%04x&Cdc_09</code></pre></td>
</tr>
<tr class="even">
<td><p>互換性 Id</p></td>
<td><pre space="preserve"><code class="language-syntax">USB\Class_02&SubClass_09&Prot_%02X
USB\Class_02&SubClass_09
USB\Class_02</code></pre></td>
</tr>
<tr class="odd">
<td><p>特別な処理</p></td>
<td><p>このコントロール モデルでは、共用体機能記述子 (UFD) は使用しません。</p></td>
</tr>
</tbody>
</table>

 

 

 




