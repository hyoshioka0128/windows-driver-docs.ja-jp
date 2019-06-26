---
title: OID_WWAN_RADIO_STATE
description: OID_WWAN_RADIO_STATE を設定または MB デバイスの無線電源の状態に関する情報を返します。
ms.assetid: e6d09ae8-65c8-4544-9581-8937f61f0747
ms.date: 08/08/2017
keywords: -OID_WWAN_RADIO_STATE ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 0a3188587e7d1abfe7ceea6caf76fdab4e107c27
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67383192"
---
# <a name="oidwwanradiostate"></a>OID\_WWAN\_ラジオ\_状態


OID\_WWAN\_ラジオ\_状態が MB デバイスの無線電源の状態に関する情報を取得または設定します。

ミニポート ドライバー セットを処理する必要があり、クエリ要求が最初に、非同期に返す NDIS\_状態\_を示す値\_元の要求とそれ以降の送信に必要な[ **NDIS\_ステータス\_WWAN\_ラジオ\_状態**](ndis-status-wwan-radio-state.md)状態通知を含む、 [ **NDIS\_WWAN\_ラジオ\_状態**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_radio_state) MB デバイスの現在のオプションを示す構造が電源のセットの完了に関係なく状態または要求のクエリを実行します。

MB デバイスの無線電源の状態を設定するように要求して呼び出し元に提供する[ **NDIS\_WWAN\_設定\_ラジオ\_状態**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_set_radio_state)ミニポートに構造体適切な情報とドライバー。

<a name="remarks"></a>注釈
-------

詳細については、この OID を使用して、次を参照してください。 [WWAN ラジオの電源状態の操作](https://docs.microsoft.com/windows-hardware/drivers/network/mb-radio-power-state-operations)します。

ミニポート ドライバー アクセスしないでください、プロバイダーのネットワークまたは Subscriber Identity Module (SIM カード) とクエリの処理または操作を設定します。

ミニポート ドライバーでは、システムの再起動またはデバイスの削除と再挿入時の間で、ソフトウェア無線電源の状態を保持する必要があります。 ミニポート ドライバーは、デバイスのソフトウェア無線の情報を格納し、各再起動またはデバイスの再挿入時にすぐにデバイス ソフトウェア無線電源の状態を設定するためを使用する必要があります。 デバイスの電源状態の有効なオプションは表に従ってソフトウェアとハードウェア無線の電源状態の組み合わせに基づいて決定[ **WWAN\_ラジオ\_状態**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wwan/ns-wwan-_wwan_radio_state)します。

値が場合*WwanRadioOn*、ミニポート ドライバーがラジオの電源をオンにし、設定する必要があります、 **RadioState.SwRadioState** 、WWAN のメンバー\_ラジオ\_状態構造体*WwanRadioOn*します。 場合、 **RadioState.HwRadioState**メンバーが*WwanRadioOff*、ミニポート ドライバーの電源の状態情報をキャッシュし、物理的にラジオの電源をオンにすることを確認する必要があります状態**RadioState.HwRadioState**変更*WwanRadioOn*します。

値が場合*WwanRadioOff*、ミニポート ドライバーがラジオの電源状態をオフにする必要があり、設定、 **RadioState.SwRadioState**メンバー *WwanRadioOff*します。

ミニポート ドライバーによってプログラミング ラジオが予期される状態は次の表を参照してください。

**PIN モードや暗証番号 (pin) の状態の有効な組み合わせ**

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
<th>全体的なラジオ電源の状態</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>WwanRadioOff</p></td>
<td><p>WwanRadioOff</p></td>
<td><p>WwanRadioOff</p></td>
</tr>
<tr class="even">
<td><p>WwanRadioOff</p></td>
<td><p>WwanRadioOn</p></td>
<td><p>WwanRadioOff</p></td>
</tr>
<tr class="odd">
<td><p>WwanRadioOn</p></td>
<td><p>WwanRadioOff</p></td>
<td><p>WwanRadioOff</p></td>
</tr>
<tr class="even">
<td><p>WwanRadioOn</p></td>
<td><p>WwanRadioOn</p></td>
<td><p>WwanRadioOn</p></td>
</tr>
</tbody>
</table>

 

デバイス ハードウェア無線の電源スイッチを提供しないため、 **RadioState.HwRadioState** NDIS のメンバー\_WWAN\_ラジオ\_状態の構造は常に設定する必要があります*WwanRadioOn*します。

以降では、Windows 10 バージョン 1703、OID\_WWAN\_ラジオ\_状態のモデムが複数実行プログラムでどのようにサポートされるか、OS から無線状態の構成を処理するには、仕様を追加します。

Executor を複数サポートされているモデムの場合は、executor あたりの電源状態のオプションを構成する電源の利点があります。 エグゼキュータのオプションがオフの場合、OS でモデムがネットワークからの登録を解除する必要があり、スキャンまたは場所から更新を試行しません。 モデムは、各 executor にする必要があるハードウェアの電源状態を判断できるように、OS にアドバタイズするオプションの状態をサポートする必要があります。

例として場合は、モデムが 2 つの executor と executor のオプションのいずれかがオフに、他のときに、モデムに電源を RF フロント エンドを維持できますし、管理のオプションはスキャン/に対して ping を実行/場所を更新する必要はありません、executor の登録s またはオフになっている executor の携帯電話サービス。 両方の無線をオフの場合、モデムを RF、フロント エンドをオフにして、全体的なハードウェア低電力状態にします。 実装の詳細については、各 IHV に残されます。

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
<td><p>Windows 7 および Windows の以降のバージョンで使用できます。</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Ntddndis.h (include Ndis.h)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**NDIS\_WWAN\_ラジオ\_状態**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_radio_state)

[**NDIS\_WWAN\_設定\_ラジオ\_状態**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_set_radio_state)

[**NDIS\_状態\_WWAN\_ラジオ\_状態**](ndis-status-wwan-radio-state.md)

[WWAN ラジオの電源状態の操作](https://docs.microsoft.com/windows-hardware/drivers/network/mb-radio-power-state-operations)

[**WWAN\_ラジオ\_状態**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wwan/ns-wwan-_wwan_radio_state)

 

 




