---
title: OID_WDI_TASK_START_AP
description: OID_WDI_TASK_START_AP は、IHV コンポーネントが、指定されたポートで Wi-fi ダイレクトグループ所有者を起動するようにポートを構成するように要求します。
ms.assetid: 647b039b-eb9a-43e7-9027-15a55df62c79
ms.date: 07/18/2017
keywords:
- Windows Vista 以降のネットワークドライバーの OID_WDI_TASK_START_AP
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: 573193bd4dab71428122a277da63bde07f88b2c6
ms.sourcegitcommit: ca5045a739eefd6ed14b9dbd9249b335e090c4e9
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/06/2020
ms.locfileid: "85968499"
---
# <a name="oid_wdi_task_start_ap"></a>OID \_ WDI \_ タスクの \_ 開始 \_ AP


OID \_ WDI \_ タスク \_ の開始 AP は、 \_ IHV コンポーネントが、指定されたポートで Wi-fi ダイレクトグループ所有者を起動するようにポートを構成するように要求します。

| Object | 中止対応                                     | 既定の優先順位 (ホストドライバーポリシー) | 通常の実行時間 (秒) |
|--------|---------------------------------------------------|---------------------------------------|---------------------------------|
| Port   | はい。 Abort の後に、dot11 をリセットする必要があります。 | 4                                     | 1                               |

 

初期化中に、ドライバーは[**WDI \_ TLV \_ P2P \_ 機能**](https://docs.microsoft.com/windows-hardware/drivers/network/wdi-tlv-p2p-capabilities)の5GHz バンドの on を設定して、5 GHz の帯域でアクセスポイントを開始できるかどうかを示します。

[5 GHz の帯域幅で実行する] が設定されている場合、アダプターは、提供されたオペレーティングチャネルで AP を開始する必要があり、失敗した場合は、[AP バンドチャネル] の一覧のパラメーターで指定したリストを試す必要があります。 オペレーティングシステムは、 [**WDI \_ TLV \_ P2P \_ グループ \_ 所有者 \_ 機能**](https://docs.microsoft.com/windows-hardware/drivers/network/wdi-tlv-p2p-group-owner-capability)で、 **DOT11 \_ WFD \_ group \_ 機能の \_ 交差 \_ 接続が \_ サポートさ**れているフラグを設定することによって、この AP がインターネット接続を提供するかどうかについてのヒントをドライバーに提供します。

**MustUseSpecifiedChannel** in [**WDI \_ TLV \_ start \_ ap \_ パラメーター**](https://docs.microsoft.com/windows-hardware/drivers/network/wdi-tlv-start-ap-parameters)が指定されている場合、ap は、指定されたバンド/チャネルで ap を開始できない場合、次のいずれかのエラーを返すことがあります。

NDIS \_ ステータス \_ DOT11 \_ \_ の ap チャネルは \_ 現在 \_ \_ 使用できません * * * *: 現在、指定されたチャネルで ap を開始することはできません。 指定されたチャネルで後で再試行してください。

NDIS \_ ステータス \_ DOT11 \_ \_ の ap バンドは \_ 現在 \_ \_ 使用できません * * * *: 現在、指定されたバンドで ap を開始することはできません。 指定されたバンドで後で再試行してください。

NDIS \_ ステータス \_ DOT11 \_ の ap チャネルは許可され \_ \_ ていません \_ * * * *: 規制上の理由により、指定されたチャネルで ap を開始できません。

NDIS \_ ステータス \_ DOT11 \_ の ap バンドは許可され \_ \_ ていません \_ * * * *: 規制上の理由により、指定されたバンドで ap を開始できません。


 

## <a name="task-parameters"></a>タスク パラメーター


<table>
<colgroup>
<col width="25%" />
<col width="25%" />
<col width="25%" />
<col width="25%" />
</colgroup>
<thead>
<tr class="header">
<th>TLV</th>
<th>複数の TLV インスタンスを使用できます</th>
<th>省略可能</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><a href="https://docs.microsoft.com/windows-hardware/drivers/network/wdi-tlv-ssid-list" data-raw-source="[&lt;strong&gt;WDI_TLV_SSID&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/network/wdi-tlv-ssid-list)"><strong>WDI_TLV_SSID</strong></a></td>
<td></td>
<td></td>
<td>AP によって使用される SSID。</td>
</tr>
<tr class="even">
<td><a href="https://docs.microsoft.com/windows-hardware/drivers/network/wdi-tlv-start-ap-parameters" data-raw-source="[&lt;strong&gt;WDI_TLV_START_AP_PARAMETERS&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/network/wdi-tlv-start-ap-parameters)"><strong>WDI_TLV_START_AP_PARAMETERS</strong></a></td>
<td></td>
<td></td>
<td>このタスクの追加パラメーター。</td>
</tr>
<tr class="odd">
<td><a href="https://docs.microsoft.com/windows-hardware/drivers/network/wdi-tlv-auth-algo-list" data-raw-source="[&lt;strong&gt;WDI_TLV_AUTH_ALGO_LIST&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/network/wdi-tlv-auth-algo-list)"><strong>WDI_TLV_AUTH_ALGO_LIST</strong></a></td>
<td></td>
<td></td>
<td>接続が使用できる認証アルゴリズムの一覧。</td>
</tr>
<tr class="even">
<td><a href="https://docs.microsoft.com/windows-hardware/drivers/network/wdi-tlv-multicast-cipher-algo-list" data-raw-source="[&lt;strong&gt;WDI_TLV_MULTICAST_CIPHER_ALGO_LIST&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/network/wdi-tlv-multicast-cipher-algo-list)"><strong>WDI_TLV_MULTICAST_CIPHER_ALGO_LIST</strong></a></td>
<td></td>
<td></td>
<td>接続が使用できるマルチキャスト暗号アルゴリズムの一覧。</td>
</tr>
<tr class="odd">
<td><a href="https://docs.microsoft.com/windows-hardware/drivers/network/wdi-tlv-unicast-cipher-algo-list" data-raw-source="[&lt;strong&gt;WDI_TLV_UNICAST_CIPHER_ALGO_LIST&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/network/wdi-tlv-unicast-cipher-algo-list)"><strong>WDI_TLV_UNICAST_CIPHER_ALGO_LIST</strong></a></td>
<td></td>
<td></td>
<td>接続が使用できるマルチキャスト暗号アルゴリズムの一覧。</td>
</tr>
<tr class="even">
<td><a href="https://docs.microsoft.com/windows-hardware/drivers/network/wdi-tlv-p2p-channel-number" data-raw-source="[&lt;strong&gt;WDI_TLV_P2P_CHANNEL_NUMBER&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/network/wdi-tlv-p2p-channel-number)"><strong>WDI_TLV_P2P_CHANNEL_NUMBER</strong></a></td>
<td></td>
<td>X</td>
<td>指定した場合、これにより、グループフォーメーションで決定されるオペレーティングチャネルが定義されます。 これは、動作モードが Wi-fi ダイレクト移動の場合にのみ指定できます。</td>
</tr>
<tr class="odd">
<td><a href="https://docs.microsoft.com/windows-hardware/drivers/network/wdi-tlv-ap-band-channel" data-raw-source="[&lt;strong&gt;WDI_TLV_AP_BAND_CHANNEL&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/network/wdi-tlv-ap-band-channel)"><strong>WDI_TLV_AP_BAND_CHANNEL</strong></a></td>
<td>X</td>
<td>X</td>
<td>Windows 10 バージョン1511、WDI version 1.0.10 に追加されました。
<p>アクセスポイントを開始するバンドとチャネルのオプションの一覧。 MustUseSpecifiedChannels が1に設定されている場合、AP はこの一覧からのみ開始できます。 設定されていない場合、この一覧は、ファームウェアが選択できるチャネルの推奨事項として使用されます。指定されたチャネルで AP を開始できない場合は、別のチャネルを選択する可能性があります。</p></td>
</tr>
</tbody>
</table>

 

## <a name="task-completion-indication"></a>タスクの完了を示す


[NDIS \_ ステータス \_ WDI \_ 表示 \_ 開始 \_ AP \_ 完了](ndis-status-wdi-indication-start-ap-complete.md)

<a name="requirements"></a>要件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>サポートされている最小のクライアント</p></td>
<td><p>Windows 10</p></td>
</tr>
<tr class="even">
<td><p>サポートされている最小のサーバー</p></td>
<td><p>Windows Server 2016</p></td>
</tr>
<tr class="odd">
<td><p>Header</p></td>
<td>Dot11wdi</td>
</tr>
</tbody>
</table>

 

 




