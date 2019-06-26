---
title: 列挙キーワード
description: 列挙キーワード
ms.assetid: ac1fb871-7720-4497-b9f7-8f592fe19bd0
keywords:
- インストールのキーワードの WDK ネットワー キング、列挙型のキーワード
- 列挙型のキーワードの WDK NDIS ミニポート
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7db8feca170edc2f17035b7b46bd9cfee2d19aa9
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67384563"
---
# <a name="enumeration-keywords"></a>列挙キーワード





NDIS 6.0 および以降のバージョンの NDIS ミニポート ドライバーのネットワーク デバイスの標準化された列挙型のキーワードを提供します。 列挙型のキーワードは、メニューのリストとして表示される値に関連付けられます。

次の例では、列挙型、キーワードの INF ファイルの定義を示します。

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

一般的な列挙型のキーワードは次のとおりです。

<a href="" id="-speedduplex"></a> **\*SpeedDuplex**  
速度と、デバイスをサポートする双方向の設定。 デバイスの INF ファイルには、関連付けられているデバイスがサポートされる設定のみが一覧表示します。 つまり、全二重モードのみをサポートできる 10/100 イーサネット デバイスの場合、ギガビットまたはより高速または半二重モードの設定は、関連付けられている INF ファイルには表示されませんする必要があります。

数値を直接 Mbps の値として 0 ~ 10 の列挙の値を既に持つ具体的には定義されていない速度値を設定できます。  直接の値は、少なくとも 1,000 Mbps である必要があります (1 Gbps) 以上です。  速度を直接指定するためのいくつかの例を次に示します。

| SpeedDuplex 値 | 結果として得られる速度 |
| ---| ---|
| 1,000 | 1 Gbps |
| 10,000 | 10 Gbps |
| 25,000 | 25 Gbps |
| 50,000 | 50 Gbps |
| 100,000 | 100 Gbps |

<a href="" id="-flowcontrol"></a> **\*FlowControl**  
有効またはフローを無効にするデバイスの機能では、送信を制御またはパスを受信します。

**注**  現時点イーサネット デバイスは、フローの制御をサポートし、LAN の Windows 8 のインボックス ドライバーがあるフロー制御が既定で有効にします。 これらの LAN アダプターのいずれかにカーネル デバッガーをアタッチします、ネットワークへのフロー制御の一時停止のフレームのプッシュ、NIC が開始されます。 ほとんどのネットワーク スイッチは、一時的に同じハブに接続されているその他のすべてのコンピューターのネットワーク停止させるして対応されます。 これは一般的な開発シナ リオであり、エンド ユーザー エクスペリエンスが望ましくないと、診断が難しい。

このため、Windows 8 以降では、NDIS が無効になりますフロー制御に自動的にコンピューターでデバッグが有効になっているときに (」と入力して、たとえば、 **bcdedit/set でデバッグ**コマンドラインで)。 カーネル デバッグを有効な場合に、ミニポート呼び出し[**エミュレーター** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisreadconfiguration)渡します"\*FlowControl"用、*キーワード*パラメーター、NDIS は構成済みの値をオーバーライドし、0 を返します。

NDIS は、デバッグ中にフロー制御を有効にする必要がある場合、 **AllowFlowControlUnderDebugger**を実行できるようにするレジストリ値。 **AllowFlowControlUnderDebugger**レジストリ値は、NDIS がフローの制御を無効にでき、Nic が構成されている動作を維持します。 次のレジストリ キーの下で見つかります。

**HKEY\_LOCAL\_MACHINE**\\**System**\\**CurrentControlSet**\\**Services**\\**NDIS**\\**Parameters**

このレジストリ値を 0x00000001 に設定します。

存在しない場合、名前の値を作成することができます**AllowFlowControlUnderDebugger**と種類**REG\_DWORD** 0x00000001 に設定します。

 

<a href="" id="-priorityvlantag"></a> **\*PriorityVLANTag**  
デバイスが有効になっているまたは 802.1 q を挿入する機能を無効になっているかどうかを示す値のタグをパケットの優先順位と仮想 Lan (Vlan)。 このキーワードは、デバイスが有効になっていること、またはパケットの優先順位または VLAN タグを無効になっているかどうかは示されません。 代わりに、次について説明します。

-   デバイスが 802.1 q を挿入するかどうか、送信操作中にタグ
-   かどうか 802.1 q タグ情報が表示されます、 [ **NET\_バッファー\_一覧**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_net_buffer_list)アウト オブ バンド (OOB) の情報
-   デバイス コピー 802.1 q タグの中に OOB が操作を受信するかどうか

ミニポート ドライバーは、802.1 q を削除する必要がありますすべてからヘッダーに関係なくパケットの受信、  **\*PriorityVLANTag**設定します。 場合、802.1 q ヘッダーは、パケットに残される、その他のドライバーでは、パケットを正しく解析できない可能性があります。

ミニポート ドライバーが削除された 802.1 q をコピーする必要があります受信パスに Rx フラグが有効な場合に、OOB ヘッダー。

それ以外の場合、Rx フラグが無効になっている場合、ミニポート ドライバーにコピー、削除された 802.1 q ヘッダーではありませんが OOB にください。

Tx フラグは、送信パスに有効になっている、ミニポート ドライバーが、次の操作にする必要があります。

-   それぞれに挿入、802.1 q ヘッダーは、パケットを送信と、これデータを入力 OOB から (OOB 内のゼロ以外のデータが存在する) 場合です。
-   適切なアドバタイズ**MacOptions**で[ **NDIS\_ミニポート\_アダプター\_全般\_属性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_miniport_adapter_general_attributes) (**NDIS\_MAC\_オプション\_8021 P\_優先度**と**NDIS\_MAC\_オプション\_8021Q\_VLAN**)。

それ以外の場合、Tx フラグが無効な場合。

-   ミニポート フィルターは、802.1 q を考慮する必要があります OOB 内の情報 (と任意のタグは挿入できません)。
-   ミニポート フィルターが適切なにアドバタイズする必要がありますしない**MacOptions**で[ **NDIS\_ミニポート\_アダプター\_全般\_属性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_miniport_adapter_general_attributes).

**注**  読み取る必要がありますもミニポート ドライバーでは、NDIS サービスの品質 (QoS) をサポートする場合、  **\*QOS**キーワード値。 に基づいて、  **\*QOS**キーワードの値、  **\*PriorityVLANTag**キーワードの値が異なる方法で解釈されます。 詳細については、次を参照してください。[の NDIS QoS の標準化された INF キーワード](standardized-inf-keywords-for-ndis-qos.md)します。

 

<a href="" id="-interruptmoderation"></a> **\*InterruptModeration**  
デバイスが有効になっていること、または割り込み節度を無効になっているかどうかを示す値。 割り込み節度アルゴリズムは、デバイスに依存します。 デバイスの製造元は、アルゴリズムの設定をサポートするために、非標準化されたキーワードを使用できます。 割り込み調整の詳細については、次を参照してください。[割り込み節度](interrupt-moderation.md)します。

<a href="" id="-rss"></a> **\*RSS**  
デバイスが有効または無効になっているかどうかを示す値を受信側 scaling (RSS)。 RSS の詳細については、次を参照してください。 [Receive Side Scaling](ndis-receive-side-scaling2.md)します。

<a href="" id="-headerdatasplit"></a> **\*HeaderDataSplit**  
デバイスが有効になっていること、またはヘッダー データの分割を無効になっているかどうかを示す値。 ヘッダー データの分割の詳細については、次を参照してください。[ヘッダー データの分割](header-data-split.md)します。

次のキーワードは、接続のオフロード サービスに関連付けられました。

**\*TCPConnectionOffloadIPv4**

**\*TCPConnectionOffloadIPv6**

接続のオフロード キーワードの詳細については、次を参照してください。[接続オフロードを無効にするレジストリ値を使用して](using-registry-values-to-enable-and-disable-connection-offloading.md)します。

次のキーワードは、タスクのオフロード サービスに関連付けられました。

**\*IPChecksumOffloadIPv4**

**\*TCPChecksumOffloadIPv4**

**\*TCPChecksumOffloadIPv6**

**\*UDPChecksumOffloadIPv4**

**\*UDPChecksumOffloadIPv6**

**\*LsoV1IPv4**

**\*LsoV2IPv4**

**注**  の両方をサポートするデバイス大量送信オフロード バージョン 1 (LSOv1) および ipv4 のみ LSOv2、  **\*LsoV2IPv4**キーワードは、INF ファイルおよびレジストリ値で使用する必要があります。 例については、場合、  **\*LsoV2IPv4**キーワードは、INF ファイルに表示されます、  **\*LsoV1IPv4**キーワードは、レジストリに (またはその逆) が表示されます、  **\*LsoV2IPv4**キーワードは常に優先します。

 

**\*LsoV2IPv6**

**\*IPsecOffloadV1IPv4**

**\*IPsecOffloadV2**

**\*IPsecOffloadV2IPv4**

**\*TCPUDPChecksumOffloadIPv4**

**\*TCPUDPChecksumOffloadIPv6**

TCP/IP のオフロード キーワードの詳細については、次を参照してください。[タスク オフロードを無効にするレジストリ値を使用して](using-registry-values-to-enable-and-disable-task-offloading.md)します。

このトピックの最後にテーブルの列には、列挙型のキーワードは次の属性について説明します。

<a href="" id="subkeyname"></a>SubkeyName  
レジストリ内の INF ファイルに指定する必要があります、キーワードの名前が表示されます。

<a href="" id="paramdesc"></a>ParamDesc  
表示テキストに関連付けられている**SubkeyName**します。

<a href="" id="value"></a>値  
リスト内の各オプションに関連付けられている列挙の整数値。 この値は**NDI\\params\\** <em>SubkeyName</em> **\\** <em>値</em>します。

<a href="" id="enumdesc"></a>EnumDesc  
メニューに表示される各値に関連付けられている表示テキスト。

<a href="" id="default"></a>既定値  
メニューの既定値。

次の表は、すべてのキーワードの一覧し、ドライバーは、上記の属性に使用する必要があります値を示します。 キーワードの詳細については、WDK ドキュメントでのキーワードを検索してください。

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
<td align="left"><p><strong><em>SpeedDuplex</strong></p></td>
<td align="left"><p>速度と二重</p></td>
<td align="left"><p>0 (既定)</p></td>
<td align="left"><p>自動ネゴシエーション</p></td>
</tr>
<tr class="even">
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>1</p></td>
<td align="left"><p>半二重を 10 Mbps</p></td>
</tr>
<tr class="odd">
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>2</p></td>
<td align="left"><p>10 Mbps Full Duplex</p></td>
</tr>
<tr class="even">
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>3</p></td>
<td align="left"><p>半二重の 100 Mbps</p></td>
</tr>
<tr class="odd">
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>4</p></td>
<td align="left"><p>100 Mbps Full Duplex</p></td>
</tr>
<tr class="even">
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>5</p></td>
<td align="left"><p>1.0 Gbps 半二重モード</p></td>
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
<td align="left"><p>10 Gbps の完全な双方向</p></td>
</tr>
<tr class="odd">
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>8</p></td>
<td align="left"><p>20 Gbps Full Duplex</p></td>
</tr>
<tr class="even">
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>9</p></td>
<td align="left"><p>40 Gbps Full Duplex</p></td>
</tr>
<tr class="odd">
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>10</p></td>
<td align="left"><p>100 Gbps Full Duplex</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong></em>FlowControl</strong></p></td>
<td align="left"><p>フロー制御</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>Disabled</p></td>
</tr>
<tr class="odd">
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>1</p></td>
<td align="left"><p>Tx を有効になっています。</p></td>
</tr>
<tr class="even">
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>2</p></td>
<td align="left"><p>Rx が有効になっています。</p></td>
</tr>
<tr class="odd">
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>3 (既定値)</p></td>
<td align="left"><p>Rx、Tx を有効になっている、(&)</p></td>
</tr>
<tr class="even">
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>4</p></td>
<td align="left"><p>自動ネゴシエーション</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong><em>PriorityVLANTag</strong></p></td>
<td align="left"><p>パケットの優先順位と VLAN</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>パケットの優先順位と VLAN を無効になっています</p></td>
</tr>
<tr class="even">
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>1</p></td>
<td align="left"><p>パケットの優先順位が有効になっています。</p></td>
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
<td align="left"><p>パケットの優先順位と VLAN を有効になっています。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong></em>InterruptModeration</strong></p></td>
<td align="left"><p>割り込み節度</p></td>
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
<td align="left"><p><strong><em>RSS</strong></p></td>
<td align="left"><p>Receive Side Scaling</p></td>
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
<td align="left"><p><strong></em>HeaderDataSplit</strong></p></td>
<td align="left"><p>ヘッダーのデータの分割</p></td>
<td align="left"><p>0 (既定)</p></td>
<td align="left"><p>無効</p></td>
</tr>
<tr class="even">
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>1</p></td>
<td align="left"><p>有効</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong><em>TCPConnectionOffloadIPv4</strong></p></td>
<td align="left"><p>TCP 接続のオフロード (IPv4)</p></td>
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
<td align="left"><p><strong></em>TCPConnectionOffloadIPv6</strong></p></td>
<td align="left"><p>TCP 接続のオフロード (IPv6)</p></td>
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
<td align="left"><p>Rx、Tx を有効になっている、(&)</p></td>
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
<td align="left"><p>Rx、Tx を有効になっている、(&)</p></td>
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
<td align="left"><p>Rx、Tx を有効になっている、(&)</p></td>
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
<td align="left"><p>Rx、Tx を有効になっている、(&)</p></td>
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
<td align="left"><p>Rx、Tx を有効になっている、(&)</p></td>
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
<td align="left"><p>大量送信オフロード バージョン 2 (IPv4)</p></td>
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
<td align="left"><p>大量送信オフロード バージョン 2 (IPv6)</p></td>
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
<td align="left"><p>Auth ヘッダーと ESP を有効になっています。</p></td>
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
<td align="left"><p>Auth ヘッダーと ESP を有効になっています。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong><em>IPsecOffloadV2IPv4</strong></p></td>
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
<td align="left"><p>Auth ヘッダーと ESP を有効になっています。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong></em>TCPUDPChecksumOffloadIPv4</strong></p></td>
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
<td align="left"><p>テキサス州と Rx が有効になっています。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>*TCPUDPChecksumOffloadIPv6</strong></p></td>
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
<td align="left"><p>テキサス州と Rx が有効になっています。</p></td>
</tr>
</tbody>
</table>

 

 

 





