---
Description: WMCDC Device Management Model
title: WMCDC デバイスの管理モデル
ms.localizationpriority: medium
ms.date: 01/07/2019
ms.openlocfilehash: f5a884549c6e16184c8752637743a6ac8e6acddb
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56580887"
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
<td><p>参照</p></td>
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
<td><pre space="preserve"><code class="language-syntax">USB\Vid_%04x&amp;Pid_%04x&amp;Rev_%04x&amp;Cdc_09&amp;MI_%02x
USB\Vid_%04x&amp;Pid_%04x&amp;Rev_%04x&amp;Cdc_09
USB\Vid_%04x&amp;Pid_%04x&amp;Cdc_09&amp;MI_%02x
USB\Vid_%04x&amp;Pid_%04x&amp;Cdc_09</code></pre></td>
</tr>
<tr class="even">
<td><p>互換性 Id</p></td>
<td><pre space="preserve"><code class="language-syntax">USB\Class_02&amp;SubClass_09&amp;Prot_%02X
USB\Class_02&amp;SubClass_09
USB\Class_02</code></pre></td>
</tr>
<tr class="odd">
<td><p>特別な処理</p></td>
<td><p>このコントロール モデルでは、共用体機能記述子 (UFD) は使用しません。</p></td>
</tr>
</tbody>
</table>

 

 

 




