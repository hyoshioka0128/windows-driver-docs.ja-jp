---
title: WFP レイヤーの要件と制限
description: WFP レイヤーの要件と制限
ms.assetid: 3677cc12-3242-4fbd-809d-303b9d324139
keywords:
- パケットの処理 WDK Windows フィルタリングプラットフォーム
- パケット処理 WDK Windows フィルタリングプラットフォーム
- パケット処理用のレイヤー (WDK Windows フィルタリングプラットフォーム)
ms.date: 01/22/2019
ms.localizationpriority: medium
ms.openlocfilehash: dc91eb6c100226882bc4e6230e85281997947c2c
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841699"
---
# <a name="wfp-layer-requirements-and-restrictions"></a>WFP レイヤーの要件と制限


次の要件と制限は、WFP レイヤーに適用されます。

<a href="" id="forwarding-layer-------"></a>**転送レイヤー**   
Ip 転送が、コンピューターに割り当てられているアドレスの送信元または送信先のパケットに対して IP 転送が有効になっていて、そのパケットが l のインターフェイスとは異なるインターフェイスで送受信される場合、IP パケットは転送層に配信されます。o) アドレスが割り当てられています。 既定では、IP 転送は無効になっており、IPv4 転送には**netsh interface ipv4 set interface**コマンドを、ipv6 転送には**netsh interface ipv6 set interface**コマンドを使用して有効にすることができます。

転送層は、受信した各フラグメントを受信したとき、または IP ペイロードのフラグメントを保持するときに、すべてのフラグメントが到着してから転送されるまで転送できます。 これは、*フラグメントグループ*と呼ばれます。 フラグメントのグループ化が無効になっている場合 (既定では無効になっています)、転送された IP パケットフラグメントは1回だけ WFP に示されます。 フラグメントのグループ化が有効になっている場合、フラグメントは2回 (最初はフラグメント自体、もう1つは、 [**NET\_\_BUFFER**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)によって記述されているフラグメントグループ内で) 2 回 (1 回目) に示されます。 WFP は、レイヤーのコールアウトを転送するフラグメントグループを示す場合に **\_\_フラグを\_フラグメント\_グループフラグの\_条件**を設定します。 フラグメントグループ化は、 **netsh interface {ipv4 | ipv6} set global groupforwardedfragments = enabled**コマンドを使用して有効にすることができます。 フラグメントのグループ化は、転送先のホストで元の IP パケットを再構築する再構築とは異なります。

転送層で示される[**NET\_BUFFER\_LIST**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)構造体は、完全な ip パケット、ip パケットフラグメント、または ip パケットフラグメントグループを記述できます。 IP パケットフラグメントは、転送レイヤーを通過しますが、コールアウトに2回 (最初はフラグメントとして、もう1つはフラグメントグループ内のフラグメントとして) 示されます。

フラグメントグループが指定されている場合、 **\_フラグ\_の .fwp\_条件は\_フラグメント\_グループ**フラグは、受信した値としてコールアウトドライバーの[*classid*](https://docs.microsoft.com/windows-hardware/drivers/ddi/fwpsk/nc-fwpsk-fwps_callout_classify_fn0)関数に渡されます。 この場合、 *NetBufferList*パラメーターによって示される[**net\_buffer\_list**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)構造体は、各**net\_buffer\_list**がパケットフラグメントを記述したリストチェーン **\_\_** の最初のノードになります。

事前に挿入されたパケットは、どの WFP レイヤーにも表示されません。 挿入されたパケットは、コールアウトドライバーに再度示すことができます。 無限ループを防ぐには、ドライバーはまず、 [**FwpsQueryPacketInjectionState0**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fwpsk/nf-fwpsk-fwpsquerypacketinjectionstate0)関数を呼び出してから、 *classid*の関数の呼び出しを続行する必要があります。また、ドライバーは、挿入状態[**fwps\_wps に\_状態**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fwpsk/ne-fwpsk-fwps_packet_injection_state_)\_セットを含むパケットを許可する必要があります。これは\_**self**または**fwps\_パケット\_によって\_挿入され\_** 変更せずに渡す場合は。\_\_\_\_

次のコマンドを使用して、システムの現在の "グループの転送されたフラグメント" 設定を表示できます: **netsh interface {ipv4 | ipv6} show global**.

<a href="" id="network-layer-------"></a>**ネットワーク層**の   
受信パスに対してのみ指定されている IP パケットフラグメントは、この層の3つのポイント (最初は ip パケット、もう1つは ip フラグメント)、再構築された IP パケットの一部として、3回目に示されます。 ネットワークレイヤーのコールアウトにフラグメントが示されている場合は、WFP によって **\_条件\_フラグ\_\_フラグメントフラグが設定さ**れます。 

たとえば、1つの IP パケットが4つのフラグメントに分割されている場合、このパケットの兆候は次のようになります。

1. "元の" IP パケット (4 つの分類、またはコールアウトの分類関数の呼び出し) ごとに1つの表示
2. "元のフラグメント" ごとに1つの表示 (4 つの分類)
3. 最終再構築 IP パケットの1つの表示 (1 分類)

フィルター条件を追加するときに、 **\_フラグ\_NONE\_SET**は、[\_] を選択して、2番目の表示を回避するために\_**フラグメント**フラグと共に使用できます。\_\_\_ これらの条件フラグは、コールアウトドライバーが考慮しない分類を防ぐことを目的としています。 コールアウトが完全なパケットだけを検査する必要がある場合 (フラグメント化および再構築されていない場合)、ip パケットとして示されているフラグメントの処理を回避するために、IP ヘッダーを解析する必要があります。 コールアウトは、次の手順を実行してこれを実現できます。

1. More Fragment (MF) フラグが設定されているかどうか、またはフラグメントオフセットフィールドが0でないことを確認して、最初の表示をスキップします。
2. **FWP_CONDITION_FLAG_IS_FRAGMENT**が設定されているすべての分類を許可するフィルターを作成します。
3. 再構築されたパケットで必要な処理をすべて実行します。

 また、コールアウトは、トランスポート層でパケットを検査することもできます。

<a href="" id="transport-layer-and-ale-------"></a>**トランスポート層と ALE**   
IPsec 処理と共存できるようにするには、受信トランスポート層でパケットを検査するコールアウトも、ALE 受信および受け入れレイヤーに登録する必要があります。 このようなコールアウトは、トランスポート層でのほとんどのトラフィックを検査または変更できますが、ALE 受信/受け入れレイヤーに割り当てられているパケットも許可する必要があります。 このようなコールアウトは、ALE レイヤーのパケットを検査または変更する必要もあります。 WFP は、ale 検査を必要とするパケットをトランスポート層に示すときに、 **\_フィールド\_ale\_分類\_必要な**メタデータフラグを設定します。\_します。 IPsec 処理は、初期の "接続" を作成し、接続を再承認するために必要なパケットが ALE レイヤーに達するまで、遅延されます。

トランスポート層と ALE レイヤーのコールアウトは、ユニバーサルサブレイヤーよりも重みが低いサブレイヤーに自身を登録する必要があります。 組み込みの IPsec/ALE 強制コールアウトは、ユニバーサルサブレイヤーに存在します。

次の表は、ALE 層で示されるパケットの種類を示しています。 一部の ALE レイヤーには、常に示されたパケットが関連付けられていないことに注意してください。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">ALE レイヤー</th>
<th align="left">TCP パケット数</th>
<th align="left">UDP パケット</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>Bind (リソース割り当て)</p></td>
<td align="left"><p>該当なし</p></td>
<td align="left"><p>該当なし</p></td>
</tr>
<tr class="even">
<td align="left"><p>接続</p></td>
<td align="left"><p>パケットがありません</p></td>
<td align="left"><p>最初の UDP パケット (送信)</p></td>
</tr>
<tr class="odd">
<td align="left"><p>Receive/Accept</p></td>
<td align="left"><p>SYN (着信)</p></td>
<td align="left"><p>最初の UDP パケット (着信)</p></td>
</tr>
<tr class="even">
<td align="left"><p>確立されたフロー</p></td>
<td align="left"><p>最終確認 (着信 & 送信)</p></td>
<td align="left"><p>最初の UDP パケット (着信 & 送信)</p></td>
</tr>
</tbody>
</table>

 

 

 





