---
title: レジストリ値を使用して、接続のオフロードを無効にするには
description: レジストリ値を使用して、接続のオフロードを無効にするには
ms.assetid: dd5d1e8a-0c6f-40d2-8a33-4d6fc70c17d5
keywords:
- 接続の負荷を軽減 WDK TCP/IP トランスポート、レジストリ値
- レジストリ WDK TCP/IP の負荷を軽減します。
- 接続の負荷を軽減 WDK TCP/IP トランスポートは、サービスを有効にします。
- 接続の負荷を軽減 WDK TCP/IP トランスポートは、サービスを無効にします。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1e825b74a670a3931ffbfc11f37b8d8c5367ffe3
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56536890"
---
# <a name="using-registry-values-to-enable-and-disable-connection-offloading"></a>レジストリ値を使用して、接続のオフロードを無効にするには





デバッグするときに、ドライバーの接続が機能をオフロード、有効または無効で、レジストリ キー設定の接続のオフロード サービスに役に立つ場合があります。 INF ファイルとレジストリを定義する標準化されたキーワードが指定されています。 標準化されたキーワードの詳細については、次を参照してください。[ネットワーク デバイスの標準化された INF キーワード](standardized-inf-keywords-for-network-devices.md)します。

接続のオフロード キーワードの定義は次のとおりです。

<a href="" id="-tcpconnectionoffloadipv4"></a>**\*TCPConnectionOffloadIPv4**  
デバイスが有効になっていること、または ipv4 TCP 接続のオフロードを無効になっているかどうかについて説明します。

<a href="" id="-tcpconnectionoffloadipv6"></a>**\*TCPConnectionOffloadIPv6**  
デバイスが有効になっていること、または IPv6 経由で TCP 接続のオフロードを無効になっているかどうかについて説明します。

次の表では、オフロード サービスの構成に使用できるグループ化されたキーワードについて説明します。

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
<th align="left">Value</th>
<th align="left">EnumDesc</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong><em>TCPConnectionOffloadIPv4</strong></p></td>
<td align="left"><p>TCP 接続のオフロード (IPv4)</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>無効</p></td>
</tr>
<tr class="even">
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>1 (既定)</p></td>
<td align="left"><p>有効</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong></em>TCPConnectionOffloadIPv6</strong></p></td>
<td align="left"><p>TCP 接続のオフロード (IPv6)</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>無効</p></td>
</tr>
<tr class="even">
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>1 (既定)</p></td>
<td align="left"><p>有効</p></td>
</tr>
</tbody>
</table>

 

 

 





