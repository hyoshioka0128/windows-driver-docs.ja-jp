---
title: 列挙キーワード
description: 列挙キーワード
ms.assetid: ac1fb871-7720-4497-b9f7-8f592fe19bd0
keywords:
- インストールキーワード WDK ネットワーク、列挙型キーワード
- 列挙型キーワード WDK NDIS ミニポート
ms.date: 4/08/2020
ms.localizationpriority: medium
ms.openlocfilehash: ac351f2042e41f4e31a15f506064e5609c435258
ms.sourcegitcommit: b481c9513a9ea7f824ecabd1ae18876548032252
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/17/2020
ms.locfileid: "84879032"
---
# <a name="enumeration-keywords"></a>列挙キーワード

Ndis 6.0 以降のバージョンの NDIS では、ネットワークデバイスのミニポートドライバー用の標準化された列挙キーワードを提供しています。 列挙キーワードは、メニューの一覧として表示される値に関連付けられています。

次の例は、列挙型キーワードの INF ファイル定義を示しています。

```INF
HKR, Ndi\params\<SubkeyName>, ParamDesc, 0, "%<SubkeyName>%"
HKR, Ndi\params\<SubkeyName>, Type, 0, "enum"
HKR, Ndi\params\<SubkeyName>, Default, 0, "3"
HKR, Ndi\params\<SubkeyName>, Optional, 0, "0"
HKR, Ndi\params\<SubkeyName>\enum, "0", 0, "%Disabled%"
HKR, Ndi\params\<SubkeyName>\enum, "1", 0, "%Tx Enabled%"
HKR, Ndi\params\<SubkeyName>\enum, "2", 0, "%Rx Enabled%"
HKR, Ndi\params\<SubkeyName>\enum, "3", 0, "%Rx & Tx Enabled%"
```

一般的な列挙キーワードは次のとおりです。

<a href="" id="-speedduplex"></a>**\*SpeedDuplex**  
デバイスがサポートする速度と双方向の設定。 デバイスの INF ファイルには、関連付けられているデバイスがサポートする設定のみが表示されます。 つまり、全二重モードのみをサポートするイーサネット10/100 デバイスの場合、ギガビット以上の速度または半二重の設定は、関連する INF ファイルに記載されていない必要があります。

明示的に定義されていない速度値 (0 ~ 10 の列挙値) は、値が直接 Mbps で設定される数値として設定できます。  直接値は、1000 Mbps 以上である必要があります。  速度を直接指定するいくつかの例を次に示します。

| SpeedDuplex 値 | 結果の速度 |
| ---| ---|
| 1,000 | 1 Gbps |
| 10,000 | 10 Gbps |
| 25,000 | 25 Gbps |
| 50,000 | 50 Gbps |
| 100,000 | 100 Gbps |

<a href="" id="-flowcontrol"></a>**\*FlowControl**  
デバイスが送信または受信パスのフロー制御を有効または無効にする機能。

**メモ**   現在、イーサネットデバイスではフロー制御がサポートされており、LAN の Windows 8 インボックスドライバーでは既定でフロー制御が有効になっています。 カーネルデバッガーがこれらの LAN アダプターのいずれかに接続すると、NIC はネットワークへのフロー制御の一時停止フレームのプッシュを開始します。 ほとんどのネットワークスイッチは、同じハブに接続されている他のすべてのコンピューターに対して、一時的にネットワークをダウンさせることで反応します。 これは一般的な開発シナリオであり、エンドユーザーエクスペリエンスは望ましくないため、診断が困難です。

**メモ**   クライアントとサーバーの既定値は同じではありません。以下の既定のテーブルを参照してください。

このため、Windows 8 以降では、コンピューターでデバッグが有効になっている場合 (たとえば、コマンドラインで「 **bcdedit/set debug** 」と入力した場合など)、NDIS はフロー制御を自動的に無効にします。 カーネルデバッグが有効になっていて、ミニポートが[**NdisReadConfiguration**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisreadconfiguration)を呼び出し、 \* *キーワード*パラメーターに "flowcontrol" を渡した場合、NDIS は構成された値をオーバーライドし、0を返します。

デバッグ中にフロー制御を有効にする必要がある場合は、NDIS によって**Allowflowcontrol過小デバッガー**レジストリ値が提供され、これを行うことができます。 **Allowflowcontrol過小デバッガー**のレジストリ値は、NDIS によってフロー制御が無効にされないようにし、nic が構成済みの動作を保持できるようにします。 これは、次のレジストリキーの下にあります。

**HKEY \_ローカル \_ コンピューター** \\ **システム**の \\ **CurrentControlSet** \\ **サービス**の \\ **NDIS** \\ **パラメーター**

このレジストリ値を0x00000001 に設定します。

名前が存在しない場合は、 **Allowflowcontrol過小デバッガー**と型**REG \_ DWORD**を使用して値を作成し、0x00000001 に設定できます。

<a href="" id="-priorityvlantag"></a>**\*PriorityVLANTag**  
パケットの優先順位および仮想 Lan (Vlan) の 802.1 Q タグを挿入する機能をデバイスが有効または無効にしているかどうかを示す値。 このキーワードは、デバイスがパケットの優先順位または VLAN タグを有効または無効にしているかどうかを示すものではありません。 代わりに、次のことについて説明します。

- 送信操作中にデバイスが 802.1 Q タグを挿入するかどうか
- 802.1 Q タグ情報が、 [**NET \_ BUFFER \_ LIST**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)の帯域外 (OOB) 情報で使用できるかどうか
- 受信操作中にデバイスが OOB に 802.1 Q タグをコピーするかどうか

ミニポートドライバーは、 ** \* PriorityVLANTag**の設定に関係なく、すべての受信パケットから 802.1 q ヘッダーを削除する必要があります。 802.1 Q ヘッダーがパケットに残されている場合、他のドライバーがパケットを正しく解析できない可能性があります。

受信パスで Rx フラグが有効になっている場合、ミニポートドライバーは、削除された 802.1 Q ヘッダーを OOB にコピーする必要があります。

それ以外の場合、Rx フラグが無効になっていると、ミニポートドライバーは、削除された 802.1 Q ヘッダーを OOB にコピーしません。

送信パスで Tx フラグが有効になっている場合、ミニポートドライバーは次の操作を実行します。

- 各送信パケットに 802.1 Q ヘッダーを挿入し、OOB のデータを入力します (OOB にゼロ以外のデータが存在する場合)。
- [**Ndis \_ ミニポート \_ アダプターの \_ 一般 \_ 属性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_miniport_adapter_general_attributes)(**ndis \_ mac \_ オプション \_ 8021P \_ PRIORITY**および**Ndis \_ mac \_ option \_ 8021q \_ VLAN**) で、適切な**macoptions**を提供します。

それ以外の場合、Tx フラグが無効になっている場合は、次のようになります。

- ミニポートフィルターでは、OOB の 802.1 Q 情報を無視する (したがって、タグを挿入しない) ことはできません。
- ミニポートフィルターでは、 [**NDIS \_ ミニポート \_ アダプターの \_ 一般 \_ 属性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_miniport_adapter_general_attributes)で適切な**macoptions**をアドバタイズしないでください。

**メモ**   ミニポートドライバーが NDIS quality of service (QoS) をサポートしている場合は、 ** \* qos**キーワード値も読み取る必要があります。 ** \* QOS**キーワードの値に基づいて、 ** \* PriorityVLANTag**キーワードの値が異なる方法で解釈されます。 詳細については、「 [NDIS QoS の標準化](standardized-inf-keywords-for-ndis-qos.md)された INF キーワード」を参照してください。

 <a href="" id="-interruptmoderation"></a>**\*InterruptModeration**  
デバイスで割り込みモデレーションを有効または無効にするかどうかを示す値。 割り込みモデレーションアルゴリズムは、デバイスに依存します。 デバイスの製造元は、標準化されていないキーワードを使用して、アルゴリズムの設定をサポートできます。 割り込みモデレーションの詳細については、「[割り込みモデレーション](interrupt-moderation.md)」を参照してください。

<a href="" id="-rss"></a>**\*RSS**  
デバイスの receive side scaling (RSS) を有効にするか無効にするかを示す値です。 RSS の詳細については、「 [Receive Side Scaling](ndis-receive-side-scaling2.md)」を参照してください。

<a href="" id="-headerdatasplit"></a>**\*HeaderDataSplit**  
デバイスの有効または無効になっているヘッダーデータの分割を示す値。 ヘッダーデータの分割の詳細については、「 [header-データの分割](header-data-split.md)」を参照してください。

次のキーワードは、接続オフロードサービスに関連付けられています。

**\*TCPConnectionOffloadIPv4**

**\*TCPConnectionOffloadIPv6**

接続のオフロードのキーワードの詳細については、「[レジストリ値を使用した接続オフロードの有効化と無効化](using-registry-values-to-enable-and-disable-connection-offloading.md)」を参照してください。

次のキーワードは、タスクオフロードサービスに関連付けられています。

**\*IPChecksumOffloadIPv4**

**\*TCPChecksumOffloadIPv4**

**\*TCPChecksumOffloadIPv6**

**\*UDPChecksumOffloadIPv4**

**\*UDPChecksumOffloadIPv6**

**\*LsoV1IPv4**

**\*LsoV2IPv4**

**メモ**   Large send offload version 1 (LSOv1) と LSOv2 over IPv4 の両方をサポートするデバイスでは、 ** \* LsoV2IPv4**キーワードのみを INF ファイルとレジストリ値で使用する必要があります。 たとえば、 ** \* LsoV2IPv4**キーワードが INF ファイルに記述されていて、 ** \* LsoV1IPv4**キーワードがレジストリに存在する (またはその逆の場合) 場合、 ** \* LsoV2IPv4**キーワードは常に優先されます。

 **\*LsoV2IPv6**

**\*IPsecOffloadV1IPv4**

**\*IPsecOffloadV2**

**\*IPsecOffloadV2IPv4**

**\*TCPUDPChecksumOffloadIPv4**

**\*TCPUDPChecksumOffloadIPv6**

TCP/IP オフロードのキーワードの詳細については、「[レジストリ値を使用してタスクオフロードを有効または無効にする](using-registry-values-to-enable-and-disable-task-offloading.md)」を参照してください。

このトピックの最後にある表の列では、列挙型キーワードの次の属性について説明します。

<a href="" id="subkeyname"></a>SubkeyName  
INF ファイルで指定する必要があり、レジストリに表示されるキーワードの名前。

<a href="" id="paramdesc"></a>ParamDesc  
**Subkeyname**に関連付けられている表示テキスト。

<a href="" id="value"></a>値  
リスト内の各オプションに関連付けられている列挙整数値。 この値は、 **ndi \\ \\ params**<em>subkeyname</em>値に格納され **\\** <em>Value</em>ます。

<a href="" id="enumdesc"></a>EnumDesc  
メニューに表示される各値に関連付けられている表示テキスト。

<a href="" id="default"></a>標準  
メニューの既定値。

次の表に、すべてのキーワードの一覧と、上記の属性に対してドライバーが使用する必要がある値について説明します。 キーワードの詳細については、WDK のドキュメントでキーワードを検索してください。

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
<td align="left"><p><strong><em>SpeedDuplex</strong></p></td>
<td align="left"><p>速度 & 両面</p></td>
<td align="left"><p>0 (既定値)</p></td>
<td align="left"><p>自動ネゴシエーション</p></td>
</tr>
<tr class="even">
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>1</p></td>
<td align="left"><p>10 Mbps 半二重</p></td>
</tr>
<tr class="odd">
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>2</p></td>
<td align="left"><p>10 Mbps 全二重</p></td>
</tr>
<tr class="even">
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>3</p></td>
<td align="left"><p>100 Mbps 半二重</p></td>
</tr>
<tr class="odd">
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>4</p></td>
<td align="left"><p>100 Mbps 全二重</p></td>
</tr>
<tr class="even">
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>5</p></td>
<td align="left"><p>1.0 Gbps 半二重</p></td>
</tr>
<tr class="odd">
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>6</p></td>
<td align="left"><p>1.0 Gbps 全二重</p></td>
</tr>
<tr class="even">
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>7</p></td>
<td align="left"><p>10 Gbps 全二重</p></td>
</tr>
<tr class="odd">
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>8</p></td>
<td align="left"><p>20 Gbps 全二重</p></td>
</tr>
<tr class="even">
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>9</p></td>
<td align="left"><p>40 Gbps 全二重</p></td>
</tr>
<tr class="odd">
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>10</p></td>
<td align="left"><p>100 Gbps 全二重</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong></em>FlowControl</strong></p></td>
<td align="left"><p>フロー制御</p></td>
<td align="left"><p>0 (サーバーの既定値)</p></td>
<td align="left"><p>Tx & Rx が無効です</p></td>
</tr>
<tr class="odd">
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>1</p></td>
<td align="left"><p>Tx 有効</p></td>
</tr>
<tr class="even">
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>2</p></td>
<td align="left"><p>Rx 有効</p></td>
</tr>
<tr class="odd">
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>3 (クライアントの既定値)</p></td>
<td align="left"><p>Rx & Tx が有効</p></td>
</tr>
<tr class="even">
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>4</p></td>
<td align="left"><p>自動ネゴシエーション</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong><em>PriorityVLANTag</strong></p></td>
<td align="left"><p>VLAN & パケット優先順位</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>VLAN 無効 & パケット優先順位</p></td>
</tr>
<tr class="even">
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>1</p></td>
<td align="left"><p>パケットの優先順位の有効化</p></td>
</tr>
<tr class="odd">
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>2</p></td>
<td align="left"><p>VLAN 有効</p></td>
</tr>
<tr class="even">
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>3 (既定値)</p></td>
<td align="left"><p>VLAN 有効 & パケット優先順位</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong></em>InterruptModeration</strong></p></td>
<td align="left"><p>割り込み節度</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>無効</p></td>
</tr>
<tr class="even">
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>1 (既定値)</p></td>
<td align="left"><p>Enabled</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong><em>RSS</strong></p></td>
<td align="left"><p>Receive Side Scaling</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>無効</p></td>
</tr>
<tr class="even">
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>1 (既定値)</p></td>
<td align="left"><p>Enabled</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong></em>HeaderDataSplit</strong></p></td>
<td align="left"><p>ヘッダーデータの分割</p></td>
<td align="left"><p>0 (既定値)</p></td>
<td align="left"><p>無効</p></td>
</tr>
<tr class="even">
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>1</p></td>
<td align="left"><p>Enabled</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong><em>TCPConnectionOffloadIPv4</strong></p></td>
<td align="left"><p>TCP 接続オフロード (IPv4)</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>無効</p></td>
</tr>
<tr class="even">
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>1 (既定値)</p></td>
<td align="left"><p>Enabled</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong></em>TCPConnectionOffloadIPv6</strong></p></td>
<td align="left"><p>TCP 接続オフロード (IPv6)</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>無効</p></td>
</tr>
<tr class="even">
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>1 (既定値)</p></td>
<td align="left"><p>Enabled</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong><em>IPChecksumOffloadIPv4</strong></p></td>
<td align="left"><p>IPv4 チェックサムオフロード</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>無効</p></td>
</tr>
<tr class="even">
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>1</p></td>
<td align="left"><p>Tx 有効</p></td>
</tr>
<tr class="odd">
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>2</p></td>
<td align="left"><p>Rx 有効</p></td>
</tr>
<tr class="even">
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>3 (既定値)</p></td>
<td align="left"><p>Rx & Tx が有効</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong></em>TCPChecksumOffloadIPv4</strong></p></td>
<td align="left"><p>TCP チェックサムオフロード (IPv4)</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>無効</p></td>
</tr>
<tr class="even">
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>1</p></td>
<td align="left"><p>Tx 有効</p></td>
</tr>
<tr class="odd">
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>2</p></td>
<td align="left"><p>Rx 有効</p></td>
</tr>
<tr class="even">
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>3 (既定値)</p></td>
<td align="left"><p>Rx & Tx が有効</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong><em>TCPChecksumOffloadIPv6</strong></p></td>
<td align="left"><p>TCP チェックサムオフロード (IPv6)</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>無効</p></td>
</tr>
<tr class="even">
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>1</p></td>
<td align="left"><p>Tx 有効</p></td>
</tr>
<tr class="odd">
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>2</p></td>
<td align="left"><p>Rx 有効</p></td>
</tr>
<tr class="even">
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>3 (既定値)</p></td>
<td align="left"><p>Rx & Tx が有効</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong></em>UDPChecksumOffloadIPv4</strong></p></td>
<td align="left"><p>UDP チェックサムオフロード (IPv4)</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>無効</p></td>
</tr>
<tr class="even">
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>1</p></td>
<td align="left"><p>Tx 有効</p></td>
</tr>
<tr class="odd">
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>2</p></td>
<td align="left"><p>Rx 有効</p></td>
</tr>
<tr class="even">
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>3 (既定値)</p></td>
<td align="left"><p>Rx & Tx が有効</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong><em>UDPChecksumOffloadIPv6</strong></p></td>
<td align="left"><p>UDP チェックサムオフロード (IPv6)</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>無効</p></td>
</tr>
<tr class="even">
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>1</p></td>
<td align="left"><p>Tx 有効</p></td>
</tr>
<tr class="odd">
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>2</p></td>
<td align="left"><p>Rx 有効</p></td>
</tr>
<tr class="even">
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>3 (既定値)</p></td>
<td align="left"><p>Rx & Tx が有効</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong></em>LsoV1IPv4</strong></p></td>
<td align="left"><p>Large Send Offload Version 1 (IPv4)</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>無効</p></td>
</tr>
<tr class="even">
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>1 (既定値)</p></td>
<td align="left"><p>Enabled</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong><em>LsoV2IPv4</strong></p></td>
<td align="left"><p>Large Send Offload Version 2 (IPv4)</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>無効</p></td>
</tr>
<tr class="even">
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>1 (既定値)</p></td>
<td align="left"><p>Enabled</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong></em>LsoV2IPv6</strong></p></td>
<td align="left"><p>Large Send Offload Version 2 (IPv6)</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>無効</p></td>
</tr>
<tr class="even">
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>1 (既定値)</p></td>
<td align="left"><p>Enabled</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong><em>IPsecOffloadV1IPv4</strong></p></td>
<td align="left"><p>IPsec オフロードバージョン 1 (IPv4)</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>無効</p></td>
</tr>
<tr class="even">
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>1</p></td>
<td align="left"><p>認証ヘッダーが有効</p></td>
</tr>
<tr class="odd">
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>2</p></td>
<td align="left"><p>ESP 有効</p></td>
</tr>
<tr class="even">
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>3 (既定値)</p></td>
<td align="left"><p>認証ヘッダー & ESP 有効</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong></em>IPsecOffloadV2</strong></p></td>
<td align="left"><p>IPsec オフロード</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>無効</p></td>
</tr>
<tr class="even">
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>1</p></td>
<td align="left"><p>認証ヘッダーが有効</p></td>
</tr>
<tr class="odd">
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>2</p></td>
<td align="left"><p>ESP 有効</p></td>
</tr>
<tr class="even">
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>3 (既定値)</p></td>
<td align="left"><p>認証ヘッダー & ESP 有効</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong><em>IPsecOffloadV2IPv4</strong></p></td>
<td align="left"><p>IPsec オフロード (IPv4 のみ)</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>無効</p></td>
</tr>
<tr class="even">
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>1</p></td>
<td align="left"><p>認証ヘッダーが有効</p></td>
</tr>
<tr class="odd">
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>2</p></td>
<td align="left"><p>ESP 有効</p></td>
</tr>
<tr class="even">
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>3 (既定値)</p></td>
<td align="left"><p>認証ヘッダー & ESP 有効</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong></em>TCPUDPChecksumOffloadIPv4</strong></p></td>
<td align="left"><p>TCP/UDP チェックサムオフロード (IPv4)</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>無効</p></td>
</tr>
<tr class="even">
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>1</p></td>
<td align="left"><p>Tx 有効</p></td>
</tr>
<tr class="odd">
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>2</p></td>
<td align="left"><p>Rx 有効</p></td>
</tr>
<tr class="even">
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>3 (既定値)</p></td>
<td align="left"><p>Tx と Rx が有効</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>*TCPUDPChecksumOffloadIPv6</strong></p></td>
<td align="left"><p>TCP/UDP チェックサムオフロード (IPv6)</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>無効</p></td>
</tr>
<tr class="even">
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>1</p></td>
<td align="left"><p>Tx 有効</p></td>
</tr>
<tr class="odd">
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>2</p></td>
<td align="left"><p>Rx 有効</p></td>
</tr>
<tr class="even">
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>3 (既定値)</p></td>
<td align="left"><p>Tx と Rx が有効</p></td>
</tr>
</tbody>
</table>
