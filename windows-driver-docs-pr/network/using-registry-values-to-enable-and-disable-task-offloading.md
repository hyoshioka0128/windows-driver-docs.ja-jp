---
title: タスク オフロードを有効および無効にするレジストリ値の使用
description: タスク オフロードを有効および無効にするレジストリ値の使用
ms.assetid: 32efd685-365c-4347-9599-fe429569d35b
keywords:
- タスクのオフロード WDK TCP/IP トランスポート、レジストリ値
- レジストリ WDK TCP/IP の負荷を軽減します。
- タスクのオフロード WDK TCP/IP トランスポートは、サービスを有効にします。
- タスクのオフロード WDK TCP/IP トランスポートは、サービスを無効にします。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0cceb9b5b163ebe8750402363c42a074edf202c7
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56577947"
---
# <a name="using-registry-values-to-enable-and-disable-task-offloading"></a>タスク オフロードを有効および無効にするレジストリ値の使用





デバッグするときにドライバーのタスクのオフロード機能を有効または無効で、レジストリ キー設定タスク オフロード サービスに役に立つ場合があります。 INF ファイルとレジストリを定義する標準化されたキーワードが指定されています。 標準化されたキーワードの詳細については、次を参照してください。[ネットワーク デバイスの標準化された INF キーワード](standardized-inf-keywords-for-network-devices.md)します。

2 つのグループのいずれかに属しているタスク オフロード キーワード: 細かいキーワードまたはグループ化されたキーワードです。 *詳細なキーワード*トランスポート層の差別化、IP プロトコルの差別化オフロード機能 - ごとのキーワードを提供します。 *キーワードをグループ化*トランスポート層で結合されたキーワードの機能を提供します。

詳細なキーワードの定義は次のとおりです。

<a href="" id="-ipchecksumoffloadipv4"></a>**\*IPChecksumOffloadIPv4**  
デバイスが有効になっていること、または IPv4 チェックサムの計算を無効になっているかどうかについて説明します。

<a href="" id="-tcpchecksumoffloadipv4"></a>**\*TCPChecksumOffloadIPv4**  
デバイスが有効になっていること、または IPv4 パケットを TCP チェックサムの計算を無効になっているかどうかについて説明します。

<a href="" id="-tcpchecksumoffloadipv6"></a>**\*TCPChecksumOffloadIPv6**  
デバイスが有効になっていること、または IPv6 パケットを TCP チェックサムの計算を無効になっているかどうかについて説明します。

<a href="" id="-udpchecksumoffloadipv4"></a>**\*UDPChecksumOffloadIPv4**  
デバイスが有効になっていること、または IPv4 パケットに対する UDP チェックサムの計算を無効になっているかどうかについて説明します。

<a href="" id="-udpchecksumoffloadipv6"></a>**\*UDPChecksumOffloadIPv6**  
デバイスが有効になっているまたは IPv6 パケットを UDP チェックサムの計算を無効になっているかどうかについて説明します。

<a href="" id="-lsov1ipv4"></a>**\*LsoV1IPv4**  
デバイスが有効になっているまたは大量送信オフロード バージョン 1 (LSOv1) に対して IPv4 による大きな TCP パケットのセグメント化を無効になっているかどうかについて説明します。

<a href="" id="-lsov2ipv4"></a>**\*LsoV2IPv4**  
デバイスが有効になっているまたは大量送信オフロード バージョン 2 (LSOv2) に対して IPv4 による大きな TCP パケットのセグメント化を無効になっているかどうかについて説明します。

<a href="" id="-lsov2ipv6"></a>**\*LsoV2IPv6**  
デバイスが有効になっているまたは IPv6 経由で大量送信オフロード バージョン 2 (LSOv2) 大きな TCP パケットのセグメント化を無効にするかどうかについて説明します。

<a href="" id="-ipsecoffloadv1ipv4"></a>**\*IPsecOffloadV1IPv4**  
デバイスが有効になっているまたは ipv4 ヘッダーの IPsec の計算を無効になっているかどうかについて説明します。

<a href="" id="-ipsecoffloadv2"></a>**\*IPsecOffloadV2**  
デバイスが有効になっていること、または IPsec オフロード バージョン 2 (IPsecOV2) を無効になっているかどうかについて説明します。 IPsecOV2 は、追加の暗号化アルゴリズム、IPv6、および大量送信オフロード バージョン 2 (LSOv2) との共存をサポートします。

<a href="" id="-ipsecoffloadv2ipv4"></a>**\*IPsecOffloadV2IPv4**  
デバイスが有効になっていること、または IPsecOV2 で IPv4 のみ無効かどうかについて説明します。

次の表では、オフロード サービスの構成に使用できる詳細なキーワードについて説明します。

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
<th align="left">値</th>
<th align="left">EnumDesc</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong><em>IPChecksumOffloadIPv4</strong></p></td>
<td align="left"><p>IPv4 チェックサム オフロード</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>Disabled</p></td>
</tr>
<tr class="even">
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>1</p></td>
<td align="left"><p>Tx を有効になっています。</p></td>
</tr>
<tr class="odd">
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>2</p></td>
<td align="left"><p>Rx が有効になっています。</p></td>
</tr>
<tr class="even">
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>3 (既定値)</p></td>
<td align="left"><p>Rx &amp; Tx を有効になっています。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong></em>TCPChecksumOffloadIPv4</strong></p></td>
<td align="left"><p>TCP チェックサム オフロード (IPv4)</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>Disabled</p></td>
</tr>
<tr class="even">
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>1</p></td>
<td align="left"><p>Tx を有効になっています。</p></td>
</tr>
<tr class="odd">
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>2</p></td>
<td align="left"><p>Rx が有効になっています。</p></td>
</tr>
<tr class="even">
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>3 (既定値)</p></td>
<td align="left"><p>Rx &amp; Tx を有効になっています。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong><em>TCPChecksumOffloadIPv6</strong></p></td>
<td align="left"><p>TCP チェックサム オフロード (IPv6)</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>Disabled</p></td>
</tr>
<tr class="even">
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>1</p></td>
<td align="left"><p>Tx を有効になっています。</p></td>
</tr>
<tr class="odd">
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>2</p></td>
<td align="left"><p>Rx が有効になっています。</p></td>
</tr>
<tr class="even">
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>3 (既定値)</p></td>
<td align="left"><p>Rx &amp; Tx を有効になっています。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong></em>UDPChecksumOffloadIPv4</strong></p></td>
<td align="left"><p>UDP チェックサム オフロード (IPv4)</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>Disabled</p></td>
</tr>
<tr class="even">
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>1</p></td>
<td align="left"><p>Tx を有効になっています。</p></td>
</tr>
<tr class="odd">
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>2</p></td>
<td align="left"><p>Rx が有効になっています。</p></td>
</tr>
<tr class="even">
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>3 (既定値)</p></td>
<td align="left"><p>Rx &amp; Tx を有効になっています。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong><em>UDPChecksumOffloadIPv6</strong></p></td>
<td align="left"><p>UDP チェックサム オフロード (IPv6)</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>Disabled</p></td>
</tr>
<tr class="even">
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>1</p></td>
<td align="left"><p>Tx を有効になっています。</p></td>
</tr>
<tr class="odd">
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>2</p></td>
<td align="left"><p>Rx が有効になっています。</p></td>
</tr>
<tr class="even">
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>3 (既定値)</p></td>
<td align="left"><p>Rx &amp; Tx を有効になっています。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong></em>LsoV1IPv4</strong></p></td>
<td align="left"><p>大量送信オフロード バージョン 1 (IPv4)</p></td>
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
<td align="left"><p><strong><em>LsoV2IPv4</strong></p></td>
<td align="left"><p>大量送信オフロード V2 (IPv4)</p></td>
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
<td align="left"><p><strong></em>LsoV2IPv6</strong></p></td>
<td align="left"><p>大量送信オフロード V2 (IPv6)</p></td>
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
<td align="left"><p><strong><em>IPsecOffloadV1IPv4</strong></p></td>
<td align="left"><p>IPsec オフロード バージョン 1 (IPv4)</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>Disabled</p></td>
</tr>
<tr class="even">
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>1</p></td>
<td align="left"><p>認証ヘッダーに有効になっています。</p></td>
</tr>
<tr class="odd">
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>2</p></td>
<td align="left"><p>ESP を有効になっています。</p></td>
</tr>
<tr class="even">
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>3 (既定値)</p></td>
<td align="left"><p>Auth ヘッダー &amp; ESP を有効になっています。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong></em>IPsecOffloadV2</strong></p></td>
<td align="left"><p>IPsec オフロード</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>Disabled</p></td>
</tr>
<tr class="even">
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>1</p></td>
<td align="left"><p>認証ヘッダーに有効になっています。</p></td>
</tr>
<tr class="odd">
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>2</p></td>
<td align="left"><p>ESP を有効になっています。</p></td>
</tr>
<tr class="even">
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>3 (既定値)</p></td>
<td align="left"><p>Auth ヘッダー &amp; ESP を有効になっています。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>* IPsecOffloadV2IPv4</strong></p></td>
<td align="left"><p>IPsec オフロード (IPv4 のみ)</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>Disabled</p></td>
</tr>
<tr class="even">
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>1</p></td>
<td align="left"><p>認証ヘッダーに有効になっています。</p></td>
</tr>
<tr class="odd">
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>2</p></td>
<td align="left"><p>ESP を有効になっています。</p></td>
</tr>
<tr class="even">
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>3 (既定値)</p></td>
<td align="left"><p>Auth ヘッダー &amp; ESP を有効になっています。</p></td>
</tr>
</tbody>
</table>

 

**注**  INF ファイルは、UI の高度なプロパティ ページに表示される詳細なキーワードをサポートできます。 ミニポート ドライバーは、表示されていない、NDIS オフロード機能を登録するための設定などの初期化時レジストリからすべての詳細な設定を読み取る必要があります。

 

グループ化されたキーワードの定義は次のとおりです。

<a href="" id="-tcpudpchecksumoffloadipv4"></a>**\*TCPUDPChecksumOffloadIPv4**  
デバイスが有効になっていること、または ipv4 IP、TCP、および UDP チェックサムの計算を無効になっているかどうかについて説明します。

<a href="" id="-tcpudpchecksumoffloadipv6"></a>**\*TCPUDPChecksumOffloadIPv6**  
デバイスが有効になっていること、または IPv6 経由で TCP および UDP チェックサムの計算を無効になっているかどうかについて説明します。

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
<th align="left">値</th>
<th align="left">EnumDesc</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong><em>TCPUDPChecksumOffloadIPv4</strong></p></td>
<td align="left"><p>TCP または UDP チェックサム オフロード (IPv4)</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>Disabled</p></td>
</tr>
<tr class="even">
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>1</p></td>
<td align="left"><p>Tx を有効になっています。</p></td>
</tr>
<tr class="odd">
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>2</p></td>
<td align="left"><p>Rx が有効になっています。</p></td>
</tr>
<tr class="even">
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>3 (既定値)</p></td>
<td align="left"><p>Tx &amp; Rx が有効になっています。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong></em>TCPUDPChecksumOffloadIPv6</strong></p></td>
<td align="left"><p>TCP または UDP チェックサム オフロード (IPv6)</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>Disabled</p></td>
</tr>
<tr class="even">
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>1</p></td>
<td align="left"><p>Tx を有効になっています。</p></td>
</tr>
<tr class="odd">
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>2</p></td>
<td align="left"><p>Rx が有効になっています。</p></td>
</tr>
<tr class="even">
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>3 (既定値)</p></td>
<td align="left"><p>Tx &amp; Rx が有効になっています。</p></td>
</tr>
</tbody>
</table>

 

有効にできるオフロードの組み合わせに対して制限があります。 たとえば、ミニポート アダプターが LSOV1 または LSOV2 をサポートする場合、ミニポート アダプターも ip アドレスと TCP チェックサムを計算します。 有効な組み合わせのオフロードの詳細については、次を参照してください。[結合の種類のタスクをオフロード](combining-types-of-task-offloads.md)します。

プロトコル ドライバーを発行する必要がありますいないレジストリ キーの設定では、タスクのオフロード サービスが無効にした場合、 [OID\_オフロード\_カプセル化](https://msdn.microsoft.com/library/windows/hardware/ff569762)オブジェクト識別子 (OID)。

次のレジストリ値を使用して、有効またはタスク オフロード、TCP/IP プロトコルを無効にできます。

<a href="" id="hkey-local-machine-system-currentcontrolset-services-tcpip-parameters-disabletaskoffload-------"></a>**HKEY\_LOCAL\_MACHINE\\System\\CurrentControlSet\\Services\\TCPIP\\Parameters\\DisableTaskOffload**   
TCP/IP トランスポートからの負荷を軽減すべてタスクの 1 つを無効にするには、この値を設定します。 0 にこの値を設定すると、すべてのタスクのオフロードできます。

<a href="" id="hkey-local-machine-system-currentcontrolset-services-ipsec-enabledoffload-------"></a>**HKEY\_ローカル\_マシン\\システム\\CurrentControlSet\\サービス\\Ipsec\\EnabledOffload**   
この値を 0 に設定すると、TCP/IP トランスポートからのインターネット プロトコル セキュリティ (IPsec) のオフロードが無効にします。 TCP/IP チェックサム タスクのオフロード大量送信オフロード バージョン 1 (LSOV1) および大量送信オフロード バージョン 2 (LSOV2) には影響しません。 IPsec オフロードの 1 つ有効にするには、この値を設定します。

 

 





