---
title: プリンターの INF ファイルのプラグ アンド プレイ Id
description: プリンターの INF ファイルのプラグ アンド プレイ Id
ms.assetid: 4adb9203-1267-466e-89d8-63988ffa56e9
keywords:
- WDK の INF ファイルを印刷するプラグ アンド プレイ Id
- 印刷の PnP ID WDK
- プラグ アンド プレイ Id WDK を印刷します。
- 識別子の WDK プリンター
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: fe581d2784461db3c7248c93c7883690a36020a0
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56537125"
---
# <a name="plug-and-play-ids-for-printer-inf-files"></a>プリンターの INF ファイルのプラグ アンド プレイ Id


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
<td><p>ID は、具体的には常に&quot;1394&quot; ID 文字列。</p></td>
</tr>
<tr class="even">
<td><p>Parallel</p></td>
<td><p>ID が含まれています&quot;LPTENUM&amp;quot; ID 文字列。</p></td>
</tr>
<tr class="odd">
<td><p>USB</p></td>
<td><p>ID が含まれています&quot;USBPRINT&amp;quot; ID 文字列。</p></td>
</tr>
<tr class="even">
<td><p>Dot4</p></td>
<td><p>ID が含まれています&quot;DOT4PRT&amp;quot; ID 文字列。 この ID は、Dot4USB と並列に適用されます。 .</p></td>
</tr>
<tr class="odd">
<td><p>Bluetooth</p></td>
<td><p>ID が含まれています&quot;BTHPRINT&amp;quot; ID 文字列。</p></td>
</tr>
<tr class="even">
<td><p>WSD</p></td>
<td><p>ID が含まれています&quot;WSDPRINT&amp;quot; ID 文字列。</p></td>
</tr>
</tbody>
</table>

 

 

 




