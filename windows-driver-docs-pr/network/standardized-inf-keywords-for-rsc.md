---
title: RSC 用の標準化された INF キーワード
description: RSC 用の標準化された INF キーワード
ms.assetid: 7418E02F-FD5A-4E58-AAA5-3055B98ED264
keywords:
- 結合の WDK ネットワーク、受信側に標準化された INF キーワード
- ネットワーク、RSC WDK に標準化された INF キーワード
- 標準化された INF キーワード WDK RSC
- INF エントリ WDK RSC
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 79485aa6f41f1160026353f2b399ad134e8bedfb
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63390656"
---
# <a name="standardized-inf-keywords-for-rsc"></a>RSC 用の標準化された INF キーワード





Windows 8、Windows Server 2012 年以降に受信セグメント coalescing (RSC) インターフェイスのサポート[INF キーワードを標準化](standardized-inf-keywords-for-network-devices.md)をレジストリに表示され、INF ファイルで指定されます。

次に示します列挙[INF キーワードを標準化](standardized-inf-keywords-for-network-devices.md)RSC の。

<a href="" id="-rscipv4"></a>**\*RscIPv4**  
有効または IPv4 データグラムのバージョンについては、RSC のサポートを無効にします。

<a href="" id="---------rscipv6"></a> **\*RscIPv6**  
有効または IPv6 データグラムのバージョンについては、RSC のサポートを無効にします。

列挙に標準化された INF キーワードは、次の属性を指定します。

<a href="" id="subkeyname"></a>**SubkeyName**  
レジストリ内の INF ファイルに指定する必要があります、キーワードの名前が表示されます。

<a href="" id="paramdesc"></a>**ParamDesc**  
表示テキストに関連付けられている**SubkeyName**します。

<a href="" id="value"></a>**値**  
リスト内の各オプションに関連付けられている列挙の整数値。 この値は NDI\\params\\ *SubkeyName*\\*値*します。

<a href="" id="enumdesc"></a>**EnumDesc**  
メニューに表示される各値に関連付けられている表示テキスト。

<a href="" id="default"></a>**既定値**  
メニューの既定値。

次の表では、RSC 列挙型のキーワードの可能な INF エントリについて説明します。

<table>
<colgroup>
<col width="25%" />
<col width="25%" />
<col width="25%" />
<col width="25%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">SubkeyName</th>
<th align="left">ParamDesc</th>
<th align="left">[値]</th>
<th align="left">EnumDesc</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong><em>RscIPv4</strong></p></td>
<td align="left"><p>Recv セグメントの結合 (IPv4)</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>Disabled</p></td>
</tr>
<tr class="even">
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>1 (既定)</p></td>
<td align="left"><p>有効</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong></em>RscIPv6</strong></p></td>
<td align="left"><p>Recv セグメントの結合 (IPv6)</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>Disabled</p></td>
</tr>
<tr class="even">
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>1 (既定)</p></td>
<td align="left"><p>有効</p></td>
</tr>
</tbody>
</table>

 

標準化された INF キーワードの詳細については、次を参照してください。[ネットワーク デバイスの標準化された INF キーワード](standardized-inf-keywords-for-network-devices.md)します。

列挙型のキーワードの使用に関する詳細については、次を参照してください。[列挙キーワード](enumeration-keywords.md)します。

 

 





