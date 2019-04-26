---
title: 並列デバイスのインターフェイス、内部名、シンボリック リンク
description: 並列デバイスのインターフェイス、内部名、シンボリック リンク
ms.assetid: 859e20bb-e411-4572-a393-a6faf534cf15
keywords:
- システム提供平行ドライバー WDK、デバイス インターフェイス
- システム提供平行ドライバー WDK、内部名
- システム提供平行ドライバー WDK、シンボリック リンク
- デバイス インターフェイスの WDK 並列ドライバー
- シンボリック リンク WDK 並列ドライバー
- WDK 並列ドライバーの内部名
- WDK 並列ドライバー名
- 保護されていないシンボリック リンク WDK
- 並列デバイス WDK、デバイス インターフェイス
- デバイス オブジェクトの WDK 並列ドライバー
- 並列デバイス WDK、内部名
- 並列デバイス WDK、シンボリック リンク
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e9c42d60a12a90939048987b3b75d78058b71586
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63351952"
---
# <a name="parallel-device-interfaces-internal-names-and-symbolic-links"></a>並列デバイスのインターフェイス、内部名、シンボリック リンク





このセクションでは、デバイス インターフェイスや内部名は、パラレル ポートおよびパラレル ポートに接続されたデバイスのシステム提供平行ドライバーによって作成されるシンボリック リンクについて説明します。

システムに列挙された各パラレル ポートおよびパラレル ポートに列挙されている各並列デバイスでは、並列のドライバーのデバイス オブジェクト、インターフェイス、内部の名前、および保護されていないシンボリック リンクよう作成します。

<table>
<colgroup>
<col width="20%" />
<col width="20%" />
<col width="20%" />
<col width="20%" />
<col width="20%" />
</colgroup>
<thead>
<tr class="header">
<th>デバイスの種類</th>
<th>デバイス オブジェクト</th>
<th>デバイス インターフェイス</th>
<th>内部名</th>
<th>シンボリック リンク</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>パラレル ポート</p></td>
<td><p>FDO</p></td>
<td><p>GUID_PARALLEL_DEVICE</p></td>
<td><p>"\Device\ParallelPort<em>m",</em></p>
<p><em>m &gt; =</em>  0</p></td>
<td><p>なし</p></td>
</tr>
<tr class="even">
<td><p>生の並列デバイス</p></td>
<td><p>PDO</p></td>
<td><p>GUID_PARCLASS_DEVICE</p></td>
<td><p>"\Device\Parallel<em>m</em>",</p>
<p><em>m &gt; =</em>  0</p></td>
<td><p>"LPT<em>n</em>"、</p>
<p><em>n = m +</em> 1</p></td>
</tr>
<tr class="odd">
<td><p>IEEE 1284.3 デバイス</p></td>
<td><p>PDO</p></td>
<td><p>なし</p></td>
<td><p>"\Device\Parallel<em>m.x</em>",</p>
<p><em>m &gt; =</em>  0<em>、</em></p>
<p>Windows 2000 の場合: <em>x =</em> 0<em>に</em>3</p>
<p>Windows XP 以降: <em>x =</em> 0<em>または</em>1</p></td>
<td><p>"LPT<em>n.x</em>",</p>
<p><em>n = m +</em>1</p></td>
</tr>
<tr class="even">
<td><p>IEEE 1284 チェーンの最後のデバイス</p></td>
<td><p>PDO</p></td>
<td><p>なし</p></td>
<td><p>"\Device\Parallel<em>m.</em>4"</p>
<p><em>m</em> &gt;= 0</p></td>
<td><p>"LPT<em>n.</em>4"</p>
<p><em>n = m +</em>1</p></td>
</tr>
</tbody>
</table>

 

次のデバイス名とシンボリック リンクが、割り当てられている"\\デバイス\\ParallelPort0"を持つ 2 つの IEEE 1284.3 デイジー チェーン接続デバイスや、IEEE 1284 チェーンの最後のデバイスが接続しています。

<table>
<colgroup>
<col width="25%" />
<col width="25%" />
<col width="25%" />
<col width="25%" />
</colgroup>
<thead>
<tr class="header">
<th>デバイスの種類</th>
<th>デバイス オブジェクト</th>
<th>内部名</th>
<th>シンボリック リンク</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>パラレル ポート</p></td>
<td><p>FDO</p></td>
<td><p>"\Device\ParallelPort0"</p></td>
<td><p>なし</p></td>
</tr>
<tr class="even">
<td><p>IEEE 1284.3 デバイス</p></td>
<td><p>PDO</p></td>
<td><p>"\Device\Parallel0.0"</p></td>
<td><p>"LPT1.0"</p></td>
</tr>
<tr class="odd">
<td><p>IEEE 1284.3 デバイス</p></td>
<td><p>PDO</p></td>
<td><p>"\Device\Parallel0.1"</p></td>
<td><p>"LPT1.1"</p></td>
</tr>
<tr class="even">
<td><p>IEEE 1284 チェーンの最後のデバイス</p></td>
<td><p>PDO</p></td>
<td><p>"\Device\Parallel0.4"</p></td>
<td><p>"LPT1.4"</p></td>
</tr>
</tbody>
</table>

 

 

 




