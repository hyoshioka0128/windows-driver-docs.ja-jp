---
title: Netmap.inf ファイル内の ID のマッピング
description: Netmap.inf ファイル内の ID のマッピング
ms.assetid: 7cab4aa1-8b0b-4cdc-a093-b91be6170961
keywords:
- ネットワーク コンポーネントのアップグレード WDK、netmap.inf ファイルのファイル
- ネットワーク コンポーネント、WDK netmap.inf ファイルのファイルをアップグレードします。
- WDK netmap.inf ファイルのファイル
- マッピングのネットワーク コンポーネント Id
- ID マッピングの WDK netmap.inf ファイル
- デバイス Id の WDK netmap.inf ファイル
- ベンダーから提供されたファイルの WDK netmap.inf ファイルのファイル
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d3a4342a2285ad86a97619b78b68baee07ee2a14
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63343474"
---
# <a name="mapping-ids-in-a-netmapinf-file"></a>Netmap.inf ファイル内の ID のマッピング





**注**  Microsoft Windows XP では、ベンダーから提供されたネットワークのアップグレードはサポートされていない (SP1 以降)、Microsoft Windows Server 2003、および以降のオペレーティング システム。

 

Netmap.inf ファイルのファイルには、次のセクションでは、最上位レベルの 1 つ以上が含まれています。 各セクションに表示されているコンポーネントの ID のマッピングが含まれています、**マップ**列。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">セクション</th>
<th align="left">マップ</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>OemNetAdapters</strong></p></td>
<td align="left"><p>非同期アダプターを除く、ネットワーク アダプター</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>OemAsyncAdapters</strong></p></td>
<td align="left"><p>非同期のネットワーク アダプター</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>OemNetProtocols</strong></p></td>
<td align="left"><p>ネットワーク プロトコルのドライバー</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>OemNetServices</strong></p></td>
<td align="left"><p>ネットワーク サービス</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>OemNetClients</strong></p></td>
<td align="left"><p>ネットワーク クライアント</p></td>
</tr>
</tbody>
</table>

 

セクション内の各エントリにマップ ネットワーク コンポーネントのアップグレード前のデバイス、ハードウェア、または互換性 ID、対応する Windows 2000 以降の id。 各エントリでは、いずれかを指定します*一対一*ID マッピングまたは*一対多*ID マッピングします。 これらのマッピング方法は、次のとおりです。

ネットワーク クライアントが Windows NT 3.51 と Windows NT 4.0; として定義されていませんそのため、以前のネットワーク サービスでは、Windows 2000 またはそれ以降は、ネットワーク クライアントになると、そのデバイス ID のマッピングに記述する必要、 **OemNetClients**セクションではなく、 **OemNetServices**セクション。

 

 





