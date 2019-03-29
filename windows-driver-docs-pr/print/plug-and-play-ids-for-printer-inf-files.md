---
title: プリンター INF ファイルのプラグ アンド プレイ ID
description: プリンター INF ファイルのプラグ アンド プレイ ID
ms.assetid: 4adb9203-1267-466e-89d8-63988ffa56e9
keywords:
- WDK の INF ファイルを印刷するプラグ アンド プレイ Id
- 印刷の PnP ID WDK
- プラグ アンド プレイ Id WDK を印刷します。
- 識別子の WDK プリンター
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 29d5f01490e2e88445e036c1849949588d9208ab
ms.sourcegitcommit: d334150abe0b189faf33049908af7aab1458c13d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2019
ms.locfileid: "57463798"
---
# <a name="plug-and-play-ids-for-printer-inf-files"></a>プリンター INF ファイルのプラグ アンド プレイ ID


指定する必要があります[プラグ アンド プレイ](plug-and-play-for-printers.md)(PnP) 識別子 (Id) で、[プリンター INF ファイルのインストール セクション](printer-inf-file-install-sections.md)します。

プリンターが使用するプロトコルに応じて、次の表に、Id を使用する必要があります。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>プロトコル</th>
<th>プリンター INF ファイルでの PnP ID。</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>IEEE 1394</p></td>
<td><p>ID が固有で、ID 文字列で「1394」では常にします。</p></td>
</tr>
<tr class="even">
<td><p>Parallel</p></td>
<td><p>ID が含まれています"LPTENUM&amp;quot;ID 文字列。</p></td>
</tr>
<tr class="odd">
<td><p>USB</p></td>
<td><p>ID が含まれています"USBPRINT&amp;quot;ID 文字列。</p></td>
</tr>
<tr class="even">
<td><p>Dot4</p></td>
<td><p>ID が含まれています"DOT4PRT&amp;quot;ID 文字列。 この ID は、Dot4USB と並列に適用されます。 .</p></td>
</tr>
<tr class="odd">
<td><p>Bluetooth</p></td>
<td><p>ID が含まれています"BTHPRINT&amp;quot;ID 文字列。</p></td>
</tr>
<tr class="even">
<td><p>WSD</p></td>
<td><p>ID が含まれています"WSDPRINT&amp;quot;ID 文字列。</p></td>
</tr>
</tbody>
</table>

 

 

 




