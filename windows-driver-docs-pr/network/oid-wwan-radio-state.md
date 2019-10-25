---
title: OID_WWAN_RADIO_STATE
description: OID_WWAN_RADIO_STATE は、MB デバイスのラジオ電源状態に関する情報を設定または返します。
ms.assetid: e6d09ae8-65c8-4544-9581-8937f61f0747
ms.date: 08/08/2017
keywords: -Windows Vista 以降の OID_WWAN_RADIO_STATE ネットワークドライバー
ms.localizationpriority: medium
ms.openlocfilehash: 7e12e3aaee5a7bba80355036d6b7c59c809f75db
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843803"
---
# <a name="oid_wwan_radio_state"></a>OID\_WWAN\_無線\_の状態


OID\_WWAN\_ラジオ\_状態セットまたは MB デバイスのラジオ電源状態に関する情報を返します。

ミニポートドライバーは、セットおよびクエリ要求を非同期的に処理し、最初に NDIS\_\_状態を返し、元の要求に必要な\_を示し、その後、 [**ndis\_ステータス\_WWAN\_RADIO @no_ を送信する必要があり**](ndis-status-wwan-radio-state.md)set 要求またはクエリ要求の完了に関係なく、MB デバイスの現在の無線電源状態を示す[**NDIS\_WWAN\_無線\_状態**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_radio_state)構造を含む _t_8_ state 状態通知。

MB デバイスのラジオ電源状態を設定するように要求している呼び出し元は、NDIS\_WWAN を提供し、適切な情報を使用して[ **\_ラジオ\_状態**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_set_radio_state)構造をミニポートドライバーに設定\_ます。

<a name="remarks"></a>注釈
-------

この OID の使用方法の詳細については、「 [WWAN ラジオの電源状態操作](https://docs.microsoft.com/windows-hardware/drivers/network/mb-radio-power-state-operations)」を参照してください。

クエリまたはセット操作を処理するときに、ミニポートドライバーがプロバイダーネットワークまたはサブスクライバー Id モジュール (SIM カード) にアクセスすることはできません。

ミニポートドライバーは、システムの再起動またはデバイスの削除と再挿入時の間でソフトウェア無線電源状態を保持する必要があります。 ミニポートドライバは、デバイスのソフトウェア無線情報を格納し、デバイスの再起動または再挿入時のたびにデバイスソフトウェアラジオの電源状態をすぐに設定するために使用します。 デバイスの有効なラジオの電源状態は、 [**WWAN\_ラジオ\_状態**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wwan/ns-wwan-_wwan_radio_state)の表に従って、ソフトウェアとハードウェアの無線電源の状態の組み合わせに基づいて決定されます。

値が*WwanRadioOn*の場合、ミニポートドライバーは、無線電源をオンにして、 **RadioState**\_\_の SwRadioState メンバーをに設定する必要*があります*。 HwRadioState メンバーが*WwanRadioState Ooff*の場合、ミニポートドライバーはこの電源状態情報をキャッシュする必要があり、 **RadioState HwRadioState**が *WwanRadioOn に変更されると、無線電源状態を物理的にオンにします。* .

値が*Wwan放射 Ooff*の場合、ミニポートドライバーは、オプションの電源状態をオフにし、 **RadioState**メンバーを*wwan放射 ooff*に設定する必要があります。

ミニポートドライバーによる想定される無線状態プログラミングについては、次の表を参照してください。

**PIN モードと PIN の状態の有効な組み合わせ**

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th>HwRadioState 値</th>
<th>SwRadioState 値</th>
<th>全体的な無線電源状態</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Wwan放射 Ooff</p></td>
<td><p>Wwan放射 Ooff</p></td>
<td><p>Wwan放射 Ooff</p></td>
</tr>
<tr class="even">
<td><p>Wwan放射 Ooff</p></td>
<td><p>WwanRadioOn</p></td>
<td><p>Wwan放射 Ooff</p></td>
</tr>
<tr class="odd">
<td><p>WwanRadioOn</p></td>
<td><p>Wwan放射 Ooff</p></td>
<td><p>Wwan放射 Ooff</p></td>
</tr>
<tr class="even">
<td><p>WwanRadioOn</p></td>
<td><p>WwanRadioOn</p></td>
<td><p>WwanRadioOn</p></td>
</tr>
</tbody>
</table>

 

ハードウェアオプションの電源スイッチを搭載していないデバイスの場合、NDIS\_WWAN\_RADIO\_STATE 構造体の**RadioState**メンバーは、常に*WwanRadioOn*に設定する必要があります。

Windows 10 以降のバージョン1703、OID\_WWAN\_RADIO\_の状態では、マルチ実行プログラムでサポートされているモデムが OS から無線状態の構成を処理する方法について、追加の仕様があります。

マルチ実行プログラムでサポートされているモデムを使用すると、実行プログラムごとにオプションの電源状態を構成する利点があります。 実行プログラムのラジオがオフになっている場合、OS はモデムにネットワークからの登録解除を要求し、スキャンや場所の更新を試行しません。 モデムは、OS にアドバタイズする各実行プログラムに対してオプションの状態をサポートする必要があります。これにより、ハードウェアの電源状態を判断できます。

たとえば、モデムに2つの実行プログラムがあり、一方の実行プログラムがオンになっているときに、いずれかのオプションがオフになっている場合、モデムは RF フロントエンドの電源がオンになっている状態で、スキャン/ping/場所の更新を行う必要がない実行プログラムに登録を維持することができます。オフになっている実行プログラムの、またはその他の携帯電話サービス。 両方の無線がオフになっている場合、モデムは RF フロントエンドをオフにして、ハードウェア全体を低電力状態にすることができます。 実装の詳細は、各 IHV に残されています。

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
<td><p>Windows 7 以降のバージョンの Windows で使用できます。</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Ntddndis (Ndis .h を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**NDIS\_WWAN\_無線\_の状態**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_radio_state)

[**NDIS\_WWAN\_\_ラジオ\_状態の設定**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_set_radio_state)

[**NDIS\_ステータス\_WWAN\_ラジオ\_状態**](ndis-status-wwan-radio-state.md)

[WWAN 無線電源状態操作](https://docs.microsoft.com/windows-hardware/drivers/network/mb-radio-power-state-operations)

[**WWAN\_ラジオ\_の状態**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wwan/ns-wwan-_wwan_radio_state)

 

 




