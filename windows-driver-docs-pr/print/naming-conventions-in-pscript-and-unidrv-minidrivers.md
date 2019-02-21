---
title: Pscript と Unidrv ミニドライバーの名前付け規則
description: Pscript と Unidrv ミニドライバーの名前付け規則
ms.assetid: d15c72e9-781d-4c71-bcf5-b3d08ec603ca
keywords:
- ボックスの自動構成サポートの WDK プリンター、名前付け規則
- WDK プリンター自動構成の名前
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 04d23c45a9d84f6728f456946a72679916f998e4
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56528263"
---
# <a name="naming-conventions-in-pscript-and-unidrv-minidrivers"></a>Pscript と Unidrv ミニドライバーの名前付け規則


その Pscript5 または Unidrv ミニドライバーで自動構成をサポートするハードウェア ベンダーは、次の名前付け規則に従う必要があります。 プリンター記述ファイルは、プリンターのモデル名に従って名前必要があります。 このトピックで示すように、ファイル名に&lt;printerModelName&gt;プリンターのモデル名のプレース ホルダーです。

### <a href="" id="pscript5-minidrivers"></a> Pscript5 ミニドライバー

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>ファイルの種類</th>
<th>名称に関する規則</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>通常使うプリンターの記述ファイル</p></td>
<td><p>&lt;printerModelName&gt;.PPD</p></td>
</tr>
<tr class="even">
<td><p>プリンターの補助の説明ファイル</p></td>
<td><p>&lt;printerModelName&gt;します。GDL</p></td>
</tr>
</tbody>
</table>

 

補助的なプリンターの記述ファイルには、双方向または自動構成情報が含まれています。

自動構成を有効にする Pscript5 ドライバーを含める必要があります&lt;printerModelName&gt;します。GDL と ps\_schm します。その依存ファイルの一覧で GDL します。 依存ファイルについては、次を参照してください。[プリンター INF ファイルのエントリ](printer-inf-file-entries.md)します。

### <a href="" id="unidrv-minidrivers"></a> Unidrv ミニドライバー

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>ファイルの種類</th>
<th>名称に関する規則</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>通常使うプリンターの記述ファイル</p></td>
<td><p>&lt;printerModelName&gt;します。GPD または&lt;printerModelName&gt;します。GDL</p>
<p>使用されるファイルの種類は、使用されるプリンターの説明形式によって異なります。</p></td>
</tr>
<tr class="even">
<td><p>補助的なプリンターの記述ファイル (省略可能)</p></td>
<td><p>&lt;printerModelName&gt;します。GDL</p></td>
</tr>
</tbody>
</table>

 

Unidrv ミニドライバーの省略可能なされる補助プリンター説明ファイルには、双方向または自動構成情報が含まれています。 または、メインの description ファイル内の自動構成情報を格納できます。

自動構成を有効にする Unidrv ドライバーを含める必要がありますいずれかの&lt;printerModelName&gt;します。GPD または&lt;printerModelName&gt;します。次のファイルとその依存ファイルの一覧で GDL ファイル:

Stddtype.gdl

Stdschem.gdl

Stdschmx.gdl

 

 




