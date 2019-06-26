---
title: OID_WDI_TASK_CREATE_PORT
description: OID_WDI_TASK_CREATE_PORT は、IHV コンポーネントによって新しい 802.11 エンティティが作成されたことを要求します。
ms.assetid: e1a03a97-608f-42af-bd39-37a7eb9ad5b7
ms.date: 07/18/2017
keywords:
- OID_WDI_TASK_CREATE_PORT ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: 487bd64619ee9b771ddc76999d35473e1bb6a2ef
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67387242"
---
# <a name="oidwditaskcreateport"></a>OID\_WDI\_タスク\_作成\_ポート


OID\_WDI\_タスク\_作成\_ポートは IHV コンポーネントによって新しい 802.11 エンティティが作成されたことを要求します。

| オブジェクト  | 中止できます。 | 既定の優先順位 (ホスト ドライバー ポリシー) | 通常の実行時間 (秒) |
|---------|---------------|---------------------------------------|---------------------------------|
| [アダプター] | X            | 6                                     | 1                               |

 

作成したポートの操作モードに設定されて**WDI\_操作\_モード\_STA**タスク パラメーターで指定されている場合を除き、します。

Wi-Fi Direct デバイスのポートでは、として機能する場合は、MAC **uOpmodeMask**を含む**WDI\_操作\_モード\_P2P\_デバイス**します。 この場合、IHV コンポーネント ドライバーは Wi-Fi Direct デバイスにこのポートの予約済みの MAC アドレスを割り当てるし、要求完了の表示で返すことにする必要があります。

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
<td><a href="https://docs.microsoft.com/windows-hardware/drivers/network/wdi-tlv-create-port-parameters" data-raw-source="[&lt;strong&gt;WDI_TLV_CREATE_PORT_PARAMETERS&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/network/wdi-tlv-create-port-parameters)"><strong>WDI_TLV_CREATE_PORT_PARAMETERS</strong></a></td>
<td></td>
<td></td>
<td>ポートの作成のパラメーターです。</td>
</tr>
<tr class="even">
<td><a href="https://docs.microsoft.com/windows-hardware/drivers/network/wdi-tlv-create-port-mac-address" data-raw-source="[&lt;strong&gt;WDI_TLV_CREATE_PORT_MAC_ADDRESS&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/network/wdi-tlv-create-port-mac-address)"><strong>WDI_TLV_CREATE_PORT_MAC_ADDRESS</strong></a></td>
<td></td>
<td>x</td>
<td><p>この TLV は、UE は休止状態から再開中に、プライマリ以外のポートを再作成するときに使用されます。 この TLV が存在する場合は、ファームウェアは、ポートを作成するこの MAC アドレスを使用する必要があります。 この MAC アドレス、ファームウェアが休止状態の前に、ポートの種類を作成する MAC アドレスにすることが保証されます。</p>
<p>目標では、上位層の状態を一致させるために、同じ NDIS ポート番号と MAC アドレスを使用します。 WFC_PORT_ID を娯楽などのさまざまなことはできますが、ポート ID が既存のポートの任意のポート ID と競合する必要がありますしないことに注意してください。 この情報は、UE と LE/ファームウェアの間のみ使用されます。</p></td>
</tr>
</tbody>
</table>

 

## <a name="task-completion-indication"></a>タスクの完了を示す値


[NDIS\_STATUS\_WDI\_INDICATION\_CREATE\_PORT\_COMPLETE](ndis-status-wdi-indication-create-port-complete.md)

<a name="requirements"></a>必要条件
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

 

 




