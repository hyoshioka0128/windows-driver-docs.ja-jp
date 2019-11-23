---
title: NDIS_STATUS_NETWORK_CHANGE
description: NDIS_STATUS_NETWORK_CHANGE の状態は、ネットワークの変更によってネットワークアドレスの再ネゴシエーションが開始されることを示します。
ms.assetid: feb6bb71-7147-43dd-b09d-cb41404164eb
ms.date: 07/18/2017
keywords:
- Windows Vista 以降のネットワークドライバーの NDIS_STATUS_NETWORK_CHANGE
ms.localizationpriority: medium
ms.openlocfilehash: 89616ed87053ec21377793efa7dffa6ce1a4baf5
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842784"
---
# <a name="ndis_status_network_change"></a>NDIS\_の状態\_ネットワーク\_の変更


NDIS\_状態\_ネットワーク\_の状態の変更は、ネットワークが変更されたことを示します。これにより、その後のドライバーがネットワークアドレスの再ネゴシエーションを開始できるようになります。

<a name="remarks"></a>注釈
-------

NDIS ミニポートドライバーは、このステータス表示を生成して、レイヤー3のアドレスを再ネゴシエートするプロトコルドライバーを要求することができます。

NDIS では、802.3 をエミュレートする古い 802.1 X ワイヤレスミニポートドライバーの状態を\_ネットワーク\_NDIS\_状態が生成されます。 これらのミニポートドライバーは、メディアの種類として**NdisMedium802\_3** 、物理メディアの種類として**NdisPhysicalMediumWirelessLan**を報告します。 このようなミニポートドライバーによって、 [ **\_メディア\_接続**](ndis-status-media-connect.md)状態が表示され、関連するミニポートアダプターが接続状態になっている場合は、ndis によって NDIS\_ステータス\_ネットワーク\_、ミニポートアダプターの状態が変更されたことを示す\_状態が生成されます。

NDIS 6.0 以降のミニポートドライバーでは、ネットワークデータを処理する準備ができた後にのみ、NDIS\_の状態\_ネットワーク\_変更する必要があります。 たとえば、ネイティブ802.11 では、認証が正常に完了し、全レイヤーの2つの接続が確立した後に、この状態が生成されます。

**注**  メディア接続状態は正確に定義されていませんが、この状態は、ミニポートアダプターがネットワークデータを送受信できる状態として、大まかに定義できます。 メディア接続は、リンク認証ステータスに直接関連していません。 ネイティブ WiFi 802.3 インターフェイスは、リンクが認証されるまでパケットを送受信できません。 この場合、メディアに接続された状態は、ネイティブ802.11 でリンク認証された状態と一致します。

 

Ndis は、次のいずれかの NDIS\_ネットワーク\_、 [**ndis\_ステータス\_示さ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_status_indication)れる構造体の**statusbuffer**メンバーの\_型の値を変更します。

<a href="" id="ndispossiblenetworkchange"></a>**NdisPossibleNetworkChange**  
ミニポートドライバーによって、ネットワークの変更が検出されたことが検出されました。 この場合、それ以降のプロトコルはネットワークの変更を検出し、必要に応じてアドレスを再ネゴシエーションする必要があります。

また、NDIS では、802.3 をエミュレートする古い 802.1 X ワイヤレスミニポートドライバーの状態を\_ネットワーク\_NDIS\_状態を生成するときにもこの値が使用されます。 ただし、NDIS は、Windows Management Instrumentation (WMI) に対して同じイベントを変換するときに、 **NdisPossibleNetworkChange**ではなく**NdisNetworkChangeFromMediaConnect**を使用します。

<a href="" id="ndisdefinitelynetworkchange"></a>**NdisDefinitelyNetworkChange**  
ミニポートドライバーはネットワークが変更されていることを検出したため、それ以降のプロトコルはアドレスを再ネゴシエーションする必要があります。

<a href="" id="ndisnetworkchangefrommediaconnect"></a>**NdisNetworkChangeFromMediaConnect**  
802.3 をエミュレートする古い 802.1 X ワイヤレスミニポートドライバーは、 [**NDIS\_ステータス\_メディア\_接続**](ndis-status-media-connect.md)状態になったときに、接続状態が表示されたことを示します。 この値は、 [GUID\_NDIS\_状態\_ネットワーク\_の変更](https://docs.microsoft.com/windows-hardware/drivers/network/guid-ndis-status-network-change)に関する WMI イベント通知で使用されます。 **NdisNetworkChangeFromMediaConnect**は、NDIS\_状態\_ネットワーク\_の状態の表示を変更するためには使用されません。

[**Ndis\_ステータス\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_status_indication)表示構造体の**statusbuffersize**メンバーが SIZEOF (NDIS\_NETWORK\_CHANGE\_TYPE) に設定されています。

<a name="requirements"></a>要件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>バージョン</p></td>
<td><p>NDIS 6.0 以降でサポートされています。</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Ndis .h (Ndis .h を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**NDIS\_状態\_表示**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_status_indication)

[**NDIS\_状態\_メディア\_接続**](ndis-status-media-connect.md)

 

 




