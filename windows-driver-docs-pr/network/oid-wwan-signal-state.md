---
title: OID_WWAN_SIGNAL_STATE
description: OID_WWAN_SIGNAL_STATE は、現在のシグナルの状態を返します。値の設定も行います。
ms.assetid: 6f5d8fd6-b4cf-4058-a27e-d4f7cea19f47
ms.date: 04/05/2019
keywords: -Windows Vista 以降の OID_WWAN_SIGNAL_STATE ネットワークドライバー
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: c3ef17d56b2dc7e15d01ad33b2fb22825bbd4156
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843792"
---
# <a name="oid_wwan_signal_state"></a>OID\_WWAN\_シグナル\_状態


OID\_WWAN\_シグナル\_状態は、現在のシグナル状態を返します。値の設定も行います。

ミニポートドライバーは、セットおよびクエリ要求を非同期的に処理し、最初に NDIS\_の\_状態を返し、元の要求に対して必要な\_を示し、その後、 [**ndis\_ステータス\_WWAN\_SIGNAL を送信する必要があり @no**](ndis-status-wwan-signal-state.md)set または query の完了に関係なく、エンドユーザーに表示される現在のシグナル状態の通知に関する情報を提供するために、 [**NDIS\_WWAN\_シグナル\_状態**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_signal_state)構造を含んだ状態の通知を表示します。要求.

現在のシグナル状態の通知をエンドユーザーに設定するように要求している呼び出し元は、NDIS\_WWAN を提供し、適切な情報を使用して[ **\_シグナル\_示す\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_set_signal_indication)をミニポートドライバーに設定します。

<a name="remarks"></a>注釈
-------

この OID の使用方法の詳細については、「 [WWAN 信号強度の操作](https://docs.microsoft.com/windows-hardware/drivers/network/mb-signal-strength-operations)」を参照してください。

クエリまたはセット操作を処理するときに、ミニポートドライバーがプロバイダーネットワークまたはサブスクライバー Id モジュール (SIM カード) にアクセスすることはできません。

一般に、シグナル状態はポーリングではなく示す必要があります。 ただし、この OID は、現在のシグナル状態を MB サービスによって決定する必要がある場合に使用できます。

クエリ要求への応答として、ミニポートドライバーは、\_WWAN\_シグナル\_状態通知の NDIS\_状態を送信する必要があります。

MB サービスからのセット要求では、ミニポートドライバーは次のことを行う必要があります。

-   「」に設定されている**Rssiinterval**と**rssiinterval**の絶対値を報告するだけでなく、NDIS\_WWAN\_SIGNAL\_STATE 構造**体の現在の値** **を返し**ます。ミニポートドライバー。

-   デバイスが現在のオペレーターに登録されていない場合でも、パラメーターの設定時にデバイスによって課される制限を適用できる場合にのみ、 **Rssiinterval**と**rssiinterval**の値を内部でキャッシュします。 ミニポートドライバーは、次の直ちに使用可能な状況でこれらの設定を適用しようとします。

-   ハードウェアまたはソフトウェアのラジオスイッチの状態が現在オフになっている場合は、要求を正常に完了します。 ミニポートドライバーは、要求データをキャッシュし、スイッチがオンになった後のシグナルの強さの報告を開始します。

-   は、適切な**uStatus**エラーコードセットでこの要求を失敗させることができます。

ミニポートドライバーは、MB サービスからのクエリ要求を処理するときに、次の操作を実行できます。

-   「」に設定されている**Rssiinterval**と**rssiinterval**の絶対値を報告するだけでなく、NDIS\_WWAN\_SIGNAL\_STATE 構造**体の現在の値** **を返し**ます。ミニポートドライバー。

-   適切な**uStatus**エラーコードセットでこの要求を失敗させます。

戻り値:

NDIS\_の状態\_\_サポートされていません

信号の強さをサポートしていないデバイスの機能を認識している特定のデバイスでは、ミニポートドライバーはこのエラーを返すことがあります。このエラーコードでは、要求が失敗する可能性があります。

**推奨される実装**

1.  デバイスは、信号強度のインジケーターをサポートする必要があります。

2.  ドライバーは、5分間にわたって、 **Rssiinterval**設定の少なくとも50% の信号強度を報告する必要があります。

3.  デバイスは、次の状態でシグナルの強さを報告しないようにする必要があります。
    1.  デバイスが登録されていないか登録解除されているため、GSM デバイスにのみ適用されます。
    2.  無線の有効な状態がオフです。
    3.  上記の状態では、信号強度に対するクエリが、ミニポートドライバーによって次のデータと共に返される必要があります。

        Rssi = WWAN\_RSSI\_不明

        ErrorRate = WWAN\_エラー\_率\_不明です。

        RssiInterval = &lt; WWAN\_RSSI\_DISABLE、WWAN\_RSSI\_DEFAULT または last set 値&gt;

        RssiThreshold = &lt; WWAN\_RSSI\_DISABLE、WWAN\_RSSI\_DEFAULT または last set 値&gt;

### <a name="windows-10-version-1903"></a>Windows 10 バージョン 1903

Windows 10 バージョン1903以降では、OID_WWAN_SIGNAL_STATE はリビジョン3にアップグレードされました。 このリビジョンにより、ホストは、ミニポートドライバーから新しい reference signal received power (RSRP) 値と Signal to 騒音 (SNR) 値を照会できるようになります。 ドライバーで5G がサポートされている場合、ミニポートドライバーは、この OID のリビジョン3とそのデータ構造を使用する必要があります。

5G data クラスのサポートの詳細については、「 [MB 5G データクラスのサポート](mb-5g-data-class-support.md)」を参照してください。

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


[**NDIS\_WWAN\_\_シグナル\_示す設定**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_set_signal_indication)

[WWAN の信号強度の操作](https://docs.microsoft.com/windows-hardware/drivers/network/mb-signal-strength-operations)

 

 




