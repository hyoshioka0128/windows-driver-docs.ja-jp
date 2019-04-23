---
title: OID_WDI_TASK_START_AP
description: OID_WDI_TASK_START_AP は、IHV コンポーネントが Wi-Fi Direct グループの所有者を指定したポートを開始するポートを構成することを要求します。
ms.assetid: 647b039b-eb9a-43e7-9027-15a55df62c79
ms.date: 07/18/2017
keywords:
- OID_WDI_TASK_START_AP ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: 1631e42945f5e4e73177003dbcbe45b50cc764fe
ms.sourcegitcommit: d17b4c61af620694ffa1c70a2dc9d308fd7e5b2e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/22/2019
ms.locfileid: "59903362"
---
# <a name="oidwditaskstartap"></a>OID\_WDI\_タスク\_開始\_アジア太平洋


OID\_WDI\_タスク\_開始\_AP 要求 IHV コンポーネントが、Wi-Fi Direct グループの所有者を指定したポートを開始するポートを構成します。

| オブジェクト | 中止できます。                                     | 既定の優先順位 (ホスト ドライバー ポリシー) | 通常の実行時間 (秒) |
|--------|---------------------------------------------------|---------------------------------------|---------------------------------|
| ポート   | [はい]。 Abort は、dot11 リセット後にする必要があります。 | 4                                     | 1                               |

 

初期化中に、ドライバーは 5 GHz 帯域の機能の移動を設定[ **WDI\_TLV\_P2P\_機能**](https://msdn.microsoft.com/library/windows/hardware/dn897865)アクセスを開始できるかどうかを示す5 GHz 帯域のポイントします。

アダプターが、運用提供チャネルの AP を開始する必要があります 5 GHz 帯域のサポートでの GO が設定されている場合と、AP バンド チャネル リスト パラメーターで指定されたリストを試す必要があります、失敗した場合。 オペレーティング システムでこの AP が設定してインターネット接続を提供がかどうかについて、ドライバーにヒントを提供すること、 **DOT11\_WFD\_グループ\_機能\_クロス\_接続\_サポートされている**フラグ[ **WDI\_TLV\_P2P\_グループ\_所有者\_機能**](https://msdn.microsoft.com/library/windows/hardware/dn897954).

場合**MustUseSpecifiedChannel**で[ **WDI\_TLV\_開始\_AP\_パラメーター** ](https://msdn.microsoft.com/library/windows/hardware/dn898065)を指定すると、AP 可能性があります指定のバンドの AP を開始できることがない場合は、次のエラーのいずれかを返す/チャネル。

|                                                                 |                                                                                                         |
|-----------------------------------------------------------------|---------------------------------------------------------------------------------------------------------|
| **NDIS\_状態\_DOT11\_AP\_チャネル\_現在\_いない\_利用可能** | 指定したチャネルの AP を今すぐ開始できません。 後で、指定されたチャネルで再試行してください。 |
| **NDIS\_状態\_DOT11\_AP\_バンド\_現在\_いない\_利用可能**    | 指定のバンドの AP を今すぐ開始できません。 後で、指定のバンドで再試行してください。        |
| **NDIS\_状態\_DOT11\_AP\_チャネル\_いない\_許可**              | 規制上の理由により、指定したチャネルの AP を開始できません。                           |
| **NDIS\_状態\_DOT11\_AP\_バンド\_いない\_許可**                 | 規制上の理由により、指定のバンドの AP を開始できません。                              |

 

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
<th>許可されている複数の TLV インスタンス</th>
<th>省略可能</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><a href="https://msdn.microsoft.com/library/windows/hardware/dn898062" data-raw-source="[&lt;strong&gt;WDI_TLV_SSID&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/dn898062)"><strong>WDI_TLV_SSID</strong></a></td>
<td></td>
<td></td>
<td>AP で使用する SSID です。</td>
</tr>
<tr class="even">
<td><a href="https://msdn.microsoft.com/library/windows/hardware/dn898065" data-raw-source="[&lt;strong&gt;WDI_TLV_START_AP_PARAMETERS&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/dn898065)"><strong>WDI_TLV_START_AP_PARAMETERS</strong></a></td>
<td></td>
<td></td>
<td>このタスクのパラメーターです。</td>
</tr>
<tr class="odd">
<td><a href="https://msdn.microsoft.com/library/windows/hardware/dn926141" data-raw-source="[&lt;strong&gt;WDI_TLV_AUTH_ALGO_LIST&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/dn926141)"><strong>WDI_TLV_AUTH_ALGO_LIST</strong></a></td>
<td></td>
<td></td>
<td>接続に使用できる認証アルゴリズムの一覧。</td>
</tr>
<tr class="even">
<td><a href="https://msdn.microsoft.com/library/windows/hardware/dn897847" data-raw-source="[&lt;strong&gt;WDI_TLV_MULTICAST_CIPHER_ALGO_LIST&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/dn897847)"><strong>WDI_TLV_MULTICAST_CIPHER_ALGO_LIST</strong></a></td>
<td></td>
<td></td>
<td>接続を使用するマルチキャストの暗号アルゴリズムの一覧。</td>
</tr>
<tr class="odd">
<td><a href="https://msdn.microsoft.com/library/windows/hardware/dn898074" data-raw-source="[&lt;strong&gt;WDI_TLV_UNICAST_CIPHER_ALGO_LIST&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/dn898074)"><strong>WDI_TLV_UNICAST_CIPHER_ALGO_LIST</strong></a></td>
<td></td>
<td></td>
<td>接続を使用するマルチキャストの暗号アルゴリズムの一覧。</td>
</tr>
<tr class="even">
<td><a href="https://msdn.microsoft.com/library/windows/hardware/dn897869" data-raw-source="[&lt;strong&gt;WDI_TLV_P2P_CHANNEL_NUMBER&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/dn897869)"><strong>WDI_TLV_P2P_CHANNEL_NUMBER</strong></a></td>
<td></td>
<td>x</td>
<td>指定すると、これとグループの構成で決定された運用チャネルを定義します。 これはのみ、動作モードが Wi-Fi Direct の移動時に指定可能性があります。</td>
</tr>
<tr class="odd">
<td><a href="https://msdn.microsoft.com/library/windows/hardware/mt593242" data-raw-source="[&lt;strong&gt;WDI_TLV_AP_BAND_CHANNEL&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/mt593242)"><strong>WDI_TLV_AP_BAND_CHANNEL</strong></a></td>
<td>x</td>
<td>x</td>
<td>Windows 10 バージョン 1511、WDI バージョン 1.0.10 に追加されます。
<p>バンドとアクセス ポイントを開始するチャネルの省略可能なリスト。 MustUseSpecifiedChannels が 1 に設定されている場合、アジア太平洋はこの一覧からのみ開始できます。 設定されていない場合は、この一覧は、ファームウェアを選択するチャネルの推奨設定をするものでし、場合は、指定したチャネルのいずれかの AP を開始することはできません、別のチャネルを選択こと可能性があります。</p></td>
</tr>
</tbody>
</table>

 

## <a name="task-completion-indication"></a>タスクの完了を示す値


[NDIS\_STATUS\_WDI\_INDICATION\_START\_AP\_COMPLETE](ndis-status-wdi-indication-start-ap-complete.md)

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
<td>Dot11wdi.h</td>
</tr>
</tbody>
</table>

 

 




