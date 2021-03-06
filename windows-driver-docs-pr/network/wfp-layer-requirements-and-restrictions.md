---
title: WFP レイヤーの要件と制限
description: WFP レイヤーの要件と制限
ms.assetid: 3677cc12-3242-4fbd-809d-303b9d324139
keywords:
- WDK Windows フィルタ リング プラットフォーム パケットの処理
- パケット WDK Windows フィルタ リング プラットフォームの処理
- 処理の WDK Windows フィルタ リング プラットフォーム パケットのレイヤー
ms.date: 01/22/2019
ms.localizationpriority: medium
ms.openlocfilehash: 65af57fd54cedef4acb03ea27c2a6fbbd563d503
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67356986"
---
# <a name="wfp-layer-requirements-and-restrictions"></a>WFP レイヤーの要件と制限


WFP レイヤーには、次の要件と制限が適用されます。

<a href="" id="forwarding-layer-------"></a>**転送層**   
IP パケットは、発生元であるコンピューターに割り当てられているアドレスの送信先となるパケットの IP 転送が有効になっていると、パケットが送信またはインターフェイスよりもさまざまなインターフェイスで受信した場合、転送層に配信されます、lローカル アドレスが割り当てられます。 既定では、IP 転送は無効になりを使用して有効にすることができます、 **netsh interface ipv4 インターフェイスを設定する**IPv4 転送のコマンドまたは**netsh interface ipv6 インターフェイスを設定する**IPv6 用コマンド転送します。

転送層が到着すると、受信した各フラグメントを転送したり、すべてのフラグメントが到着し、それらを転送するまでは、IP ペイロードのフラグメントを保持することができます。 これと呼ばれます*フラグメント化*します。 フラグメントのグループ化が無効な場合 (これは既定で無効)、によってフラグメントが示された IP パケットが 1 回 WFP に転送されます。 フラグメントのグループ化を有効にすると、フラグメントと示されます WFP を 2 回--自体には、フラグメントとして最初にもう一度によって定義されたフラグメント グループ内で、 [ **NET\_バッファー\_一覧**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_net_buffer_list)チェーン。 WFP セット、 **FWP\_条件\_フラグ\_IS\_フラグメント\_グループ**フラグメント レイヤー コールアウトを転送するグループのフラグが示されている場合。 使用してフラグメントのグループ化を有効にすることができます、 **netsh インターフェイス {ipv4 | ipv6} 設定グローバル groupforwardedfragments = 有効になっている**コマンド。 フラグメントのグループ化は、再構築、移動先ホストにある元の IP パケットの再構築したものであると異なります。

[ **NET\_バッファー\_一覧**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_net_buffer_list)転送層で示される構造体は、完全な IP パケットや IP パケットのフラグメントを IP パケットのフラグメント グループを記述できます。 2 回に示す吹き出しにする、IP パケットのフラグメントでは、転送レイヤーは走査、中に: フラグメントとして最初、もう一度、フラグメント グループ内のフラグメントとして。

フラグメントのグループは、指定したときに、 **FWP\_条件\_フラグ\_IS\_フラグメント\_グループ**コールアウト ドライバーの入力方向の値としてフラグが渡されます[*classifyFn* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fwpsk/nc-fwpsk-fwps_callout_classify_fn0)コールアウト関数。 ここで、 [ **NET\_バッファー\_一覧**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_net_buffer_list)によって示される構造体、 *NetBufferList*パラメーターは、の最初のノード**NET\_バッファー\_一覧**チェーンでそれぞれ**NET\_バッファー\_一覧**パケットのフラグメントを記述します。

前方挿入されたパケットは、WFP レイヤーには表示されません。 挿入されたパケットは、もう一度コールアウト ドライバーに指示できます。 無限ループを防ぐためには、まず、ドライバーを呼び出して、 [ **FwpsQueryPacketInjectionState0** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fwpsk/nf-fwpsk-fwpsquerypacketinjectionstate0)関数への呼び出しを続行する前に、 *classifyFn*コールアウト関数、およびドライバーの挿入の状態を持つパケットを許可するように[ **FWPS\_パケット\_インジェクション\_状態**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fwpsk/ne-fwpsk-fwps_packet_injection_state_) に設定**FWPS\_パケット\_INJECTED\_BY\_セルフ**または**FWPS\_パケット\_以前\_INJECTED\_BY\_セルフ**変更されていないを通過します。

次のコマンドを使用するには、システムの現在の「グループ転送されたフラグメント」設定を表示する: **netsh インターフェイス {ipv4 | ipv6} グローバル**します。

<a href="" id="network-layer-------"></a>**ネットワーク層**   
受信パスに対してのみ指示は、IP パケットのフラグメントは、このレイヤーで 3 つの点で示されています。 最初に、IP パケットとして IP としてもう一度フラグメント、および 3 回目の再構築された IP パケットの一部として。 WFP セット、 **FWP\_条件\_フラグ\_IS\_フラグメント**ネットワーク レイヤーの吹き出しにフラグメントが示されている場合にフラグを設定します。 

たとえば、1 つの IP パケットが 4 つのフラグメントに分割されている場合このパケットがないように行われます。

1. 各「元」IP パケットを (4 つの分類、または引き出し線の分類関数の呼び出し) の 1 つを示す値
2. 各「元フラグメント」の 1 つを示す値 (4 つの分類)
3. 最後の再構築された IP パケット (1 分類) の 1 つを示す値

条件のフィルター処理を追加するときに**FWP\_一致\_フラグ\_NONE\_設定**と組み合わせて使用することができます、 **FWP\_条件\_フラグ\_IS\_フラグメント**を 2 つ目の indication(s) を回避するフラグ。 これらの条件のフラグは、分類コールアウト ドライバーは気にしないようにするものです。 引き出し線 (を断片化し、再構築されていないもの) だけ完全なパケットを検査する場合は、IP パケットとして示されている処理のフラグメントを回避するために IP ヘッダーを解析する必要があります。 コールアウトは、これを実現するために、次の手順を実行します。

1. チェックよりフラグメント (MF) フラグが設定やフラグメントのオフセット フィールドがない場合は、最初の indication(s) をスキップ 0。
2. すべての分類を許可するフィルターを記述、 **FWP_CONDITION_FLAG_IS_FRAGMENT**設定されます。
3. 再構築されたパケットに必要な処理を実行します。

 または、引き出し線は、トランスポート層でパケットを検査できます。

<a href="" id="transport-layer-and-ale-------"></a>**トランスポート層と ALE**   
IPsec の処理と共存できるようにするには、コールアウト受信トランスポート層でパケットを検査する必要がありますも ALE で登録が表示され、レイヤーをそのまま使用します。 このような吹き出し検査/は変更できますがトランスポート層でトラフィックのほとんどが ALE 受信受け入れるレイヤーに割り当てられているパケットも許可する必要があります。 このような吹き出しを検査または ALE レイヤーからのパケットを変更もする必要があります。 WFP セット、 **FWPS\_メタデータ\_フィールド\_ALE\_分類\_REQUIRED**トランスポートことを示すことと、メタデータ フラグを ALE を必要とするこれらのパケットのレイヤー検査します。 IPsec の処理は、ALE レイヤーに最初の「接続」との接続を再度承認する必要があるものを作成するこれらのパケットが到達するまで遅延されます。

トランスポート層と ALE レイヤー コールアウトする必要がありますに登録ユニバーサル副層よりも負荷の低いは副層にします。 組み込みの IPsec/ALE 強制コールアウトは、ユニバーサル副層に存在します。

次の表では、ALE レイヤーで示すことができますが、パケットの種類を示します。 一部の ALE レイヤーがないこと常に自分を示す値に関連付けられているパケットに注意します。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">ALE レイヤー</th>
<th align="left">TCP パケット</th>
<th align="left">UDP パケット</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>バインド (リソースの割り当て)</p></td>
<td align="left"><p>該当なし</p></td>
<td align="left"><p>該当なし</p></td>
</tr>
<tr class="even">
<td align="left"><p>接続</p></td>
<td align="left"><p>パケットがありません。</p></td>
<td align="left"><p>最初の UDP パケット (発信)</p></td>
</tr>
<tr class="odd">
<td align="left"><p>表示される同意</p></td>
<td align="left"><p>SYN (受信)</p></td>
<td align="left"><p>最初の UDP パケット (受信)</p></td>
</tr>
<tr class="even">
<td align="left"><p>フローが確立されています。</p></td>
<td align="left"><p>最後の確認 (受信および送信)</p></td>
<td align="left"><p>最初の UDP パケット (受信および送信)</p></td>
</tr>
</tbody>
</table>

 

 

 





