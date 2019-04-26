---
title: リモート NDIS ファイルの名前付け規則
description: リモート NDIS ファイルの名前付け規則
ms.assetid: 9c5b2cfe-c38f-4314-a91c-f27c77ea1f63
keywords:
- リモートの NDIS WDK のネットワーク、ドライバー名
- リモートの NDIS WDK のネットワーク、オペレーティング システムのサポート
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e82f1ad42a769675ad313e38324466e2c45e210b
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63350899"
---
# <a name="remote-ndis-file-naming-conventions"></a>リモート NDIS ファイルの名前付け規則





従来の NDIS リモート デバイスをサポートするために複数のリモート NDIS ドライバーが含まれているさまざまなバージョンの Windows でします。 次の表には、Windows の各バージョンで使用されるリモート NDIS ドライバー名が一覧表示します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">リモートの NDIS ファイル名</th>
<th align="left">このドライバーの使用可能な Windows バージョン</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>Rndismp.sys Usb8023.sys</p></td>
<td align="left"><p>これらのバイナリはレガシ デバイスのサポートにのみ付属しています。 これらのドライバーを参照する必要がありますリモート NDIS デバイス INF ファイルにはありません。</p></td>
</tr>
<tr class="even">
<td align="left"><p>Rndismpy.sys Usb8023y.sys</p></td>
<td align="left"><p>Windows 2000 です。 オペレーティング システムからは個別に指定されました。 これらは、Microsoft が再配布権を付与するだけのバイナリです。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>Rndismpx.sys Usb8023x.sys Netrndis.inf</p></td>
<td align="left"><ul>
<li><p>Windows XP SP2 以降</p></li>
<li><p>Windows XP x64</p></li>
<li><p>Windows Server 2003 SP1 (x86、x64、ia64) 以降</p></li>
<li><p>Windows Vista (x86、x64) 以降</p></li>
</ul>
<p>Rndismpx.sys と Usb8023x.sys バイナリ、オペレーティング システムの一部として出荷されます。 Netrndis.inf ファイルは、オペレーティング システムの一部である内部ファイルです。 これらのファイルを IHV で提供される INF で参照する必要がありますすべてのファイル」の説明に従って<a href="remote-ndis-inf-template.md" data-raw-source="[Remote NDIS INF Template](remote-ndis-inf-template.md)">リモート NDIS INF テンプレート</a>します。</p></td>
</tr>
</tbody>
</table>

 

**注**  リモート NDIS は Windows 98/Me/SE またはそれ以前のバージョンでサポートされていません。

 

 

 





