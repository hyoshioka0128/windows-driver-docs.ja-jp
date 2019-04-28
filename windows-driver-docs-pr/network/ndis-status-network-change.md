---
title: NDIS_STATUS_NETWORK_CHANGE
description: NDIS_STATUS_NETWORK_CHANGE 状態では、後続のネットワーク アドレスの再ネゴシエーションを開始するドライバーを許可するネットワークの変更を示します。
ms.assetid: feb6bb71-7147-43dd-b09d-cb41404164eb
ms.date: 07/18/2017
keywords:
- NDIS_STATUS_NETWORK_CHANGE ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 93867577d2a2ec73afe379040c4f05334103bff3
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63380148"
---
# <a name="ndisstatusnetworkchange"></a>NDIS\_状態\_ネットワーク\_変更


NDIS\_状態\_ネットワーク\_状態の変更が後続のネットワーク アドレスの再ネゴシエーションを開始するドライバーを許可するネットワークの変更を示します。

<a name="remarks"></a>注釈
-------

NDIS ミニポート ドライバーでは、レイヤー 3 つのアドレスを再ネゴシエートする上位のプロトコルのドライバーを入手するには、この状態表示を生成できます。

NDIS 生成 NDIS\_状態\_ネットワーク\_古い 802.1 X の変更状態インジケーターのワイヤレス 802.3 をエミュレートするミニポート ドライバー。 これらのミニポート ドライバーがメディアの種類を報告**NdisMedium802\_3**の物理メディア タイプと**NdisPhysicalMediumWirelessLan**します。 このようなミニポート ドライバーが生成するとき、 [ **NDIS\_状態\_メディア\_CONNECT** ](ndis-status-media-connect.md)に接続された状態を示す値と関連付けられているミニポート アダプターが状態では、NDIS 生成、NDIS\_状態\_ネットワーク\_ミニポート アダプターの状態表示を変更します。

NDIS 6.0 とそれ以降のミニポート ドライバーは、NDIS を生成する必要があります\_状態\_ネットワーク\_ネットワーク データを処理する準備ができた後にのみ変更状態を示す値。 たとえば、ネイティブの 802.11 でこの状態を示す値が生成されます認証が正常に完了し、完全なレイヤー 2 接続が実現されます。

**注**  - ミニポート アダプターがネットワークのデータを送受信することが状態としてこの状態を疎定義メディアが接続された状態は正確に定義されていません。 メディア接続は直接関係ありません認証の状態をリンクします。 ネイティブ WiFi 802.3 インターフェイスは、リンクが認証された後、までパケットを送受信できません。 この場合は、メディアが接続された状態はネイティブの 802.11 のリンクで認証された状態と一致します。

 

NDIS が次のいずれかを提供する NDIS\_ネットワーク\_変更\_で値型、 **StatusBuffer**のメンバー、 [ **NDIS\_の状態\_INDICATION** ](https://msdn.microsoft.com/library/windows/hardware/ff567373)構造体。

<a href="" id="ndispossiblenetworkchange"></a>**NdisPossibleNetworkChange**  
ミニポート ドライバーでは、ネットワークの変更が存在する可能性が検出されました。 ここでは、上にあるプロトコルは、存在する場合は、ネットワークの変更を検出し、必要に応じて、アドレスの再ネゴシエーションする必要があります。

NDIS は、NDIS を生成するときもこの値を使って\_状態\_ネットワーク\_変更の状態インジケーターの古い 802.1 X ワイヤレス 802.3 をエミュレートするミニポート ドライバー。 ただし、NDIS 使用**NdisNetworkChangeFromMediaConnect**の代わりに**NdisPossibleNetworkChange**同じイベントを変換、ときに Windows Management Instrumentation (WMI)。

<a href="" id="ndisdefinitelynetworkchange"></a>**NdisDefinitelyNetworkChange**  
上にあるプロトコルは、アドレスを再ネゴシエートする必要がありますのでネットワークの変更が認識されているミニポート ドライバーが検出されました。

<a href="" id="ndisnetworkchangefrommediaconnect"></a>**NdisNetworkChangeFromMediaConnect**  
古い 802.1 X ワイヤレスのミニポート ドライバー生成 802.3 をエミュレートする、 [ **NDIS\_状態\_メディア\_CONNECT** ](ndis-status-media-connect.md)状態表示になっていた、接続の状態。 WMI イベント通知では、この値が使用される[GUID\_NDIS\_状態\_ネットワーク\_変更](https://msdn.microsoft.com/library/windows/hardware/ff553595)します。 **NdisNetworkChangeFromMediaConnect** NDIS で使用されていない\_状態\_ネットワーク\_変更状態を示す値。

**StatusBufferSize**のメンバー、 [ **NDIS\_状態\_INDICATION** ](https://msdn.microsoft.com/library/windows/hardware/ff567373) sizeof に構造体が設定されている (NDIS\_ネットワーク\_変更\_型)。

<a name="requirements"></a>必要条件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>バージョン</p></td>
<td><p>NDIS 6.0 以降をサポートします。</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Ndis.h (Ndis.h を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**NDIS\_状態\_を示す値**](https://msdn.microsoft.com/library/windows/hardware/ff567373)

[**NDIS\_状態\_メディア\_接続**](ndis-status-media-connect.md)

 

 




