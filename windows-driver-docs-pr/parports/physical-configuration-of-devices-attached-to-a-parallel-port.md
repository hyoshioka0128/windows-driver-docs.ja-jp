---
title: パラレル ポートに接続されているデバイスの物理構成
description: パラレル ポートに接続されているデバイスの物理構成
ms.assetid: ae90fcc6-7ea8-4cb1-89a1-1fbf1ad5c05e
keywords:
- IEEE 1284 WDK
- パラレル ポート WDK、デバイスの構成
- デイジー チェーン デバイス WDK
- デバイスの物理的な構成、WDK を並列します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a2a18430701f9a851b06f06f9bb2ab2364cdf4b9
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63349347"
---
# <a name="physical-configuration-of-devices-attached-to-a-parallel-port"></a>パラレル ポートに接続されているデバイスの物理構成





このセクションでは、パラレル ポートに接続されているデバイスの一般的な物理構成について説明します。

次の図は、並列のデバイスには、パラレル ポートが接続されているを示します。

![パラレル ポートに接続されている並列のデバイスを示す図](images/parport2.png)

Microsoft Windows には、レガシ デバイスまたは IEEE 1284 規格に準拠しているプラグ アンド プレイ デバイスを指定できますが、パラレル ポートに接続された 1 つの並列デバイスがサポートされています。

次の図は、IEEE 1284.3 デバイスおよびパラレル ポートに同時に接続されている最後のチェーンの IEEE 1284 デバイスを示します。

![パラレル ポートに接続されている ieee 1284.3 デイジー チェーン デバイス](images/parport3.png)

IEEE 1284.3 標準では、ことデイジー チェーンの 4 つまでデバイスと最後のチェーンのデバイスを同時に接続できるパラレル ポートを指定します。

次の表では、Windows の各バージョンでサポートされている IEEE 1284.3 デバイスの数を指定します。

<table>
<colgroup>
<col width="25%" />
<col width="25%" />
<col width="25%" />
<col width="25%" />
</colgroup>
<thead>
<tr class="header">
<th>Windows のバージョン</th>
<th>デイジー チェーン接続デバイスの最大数</th>
<th>IEEE 1284.3 デバイス Id</th>
<th>コメント</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Windows Me</p></td>
<td><p>0</p></td>
<td><p>なし</p></td>
<td><p>システム指定のドライバーによってサポートされていません。</p></td>
</tr>
<tr class="even">
<td><p>Windows 2000</p></td>
<td><p>次の 4 つ</p></td>
<td><p>0 ~ 3</p></td>
<td><p>信頼性の高い操作を確実には、Microsoft では最大で 2 つのデバイスをお勧めします。</p></td>
</tr>
<tr class="odd">
<td><p>Windows XP 以降</p></td>
<td><p>2</p></td>
<td><p>0 または 1</p></td>
<td></td>
</tr>
</tbody>
</table>

 

IEEE 1284.3 デバイスのサポートの詳細についてを参照してください。

[並列デバイス インターフェイス、内部名は、シンボリック リンク](parallel-device-interfaces--internal-names--and-symbolic-links.md)

[選択して、パラレル ポートに接続されている IEEE 1284 デバイスの選択を解除](selecting-and-deselecting-an-ieee-1284-device-attached-to-a-parallel-p.md)

 

 




