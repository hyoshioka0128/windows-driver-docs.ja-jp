---
title: NDIS_STATUS_WWAN_SIGNAL_STATE
description: ミニポートドライバーは、測定されたシグナルの強さが事前に定義された間隔でしきい値を超えたときに、NDIS_STATUS_WWAN_SIGNAL_STATE 通知を使用して信号強度の通知を送信します。
ms.assetid: b5d6b2a6-ed19-45d9-85ca-ac66e38f41fd
ms.date: 08/08/2017
keywords: -Windows Vista 以降の NDIS_STATUS_WWAN_SIGNAL_STATE ネットワークドライバー
ms.localizationpriority: medium
ms.openlocfilehash: 23cf8ec2788e7965f2641e1bd36560086d40d340
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844642"
---
# <a name="ndis_status_wwan_signal_state"></a>NDIS\_ステータス\_WWAN\_シグナル\_状態


ミニポートドライバーは、NDIS\_ステータス\_WWAN\_SIGNAL\_状態通知を使用して、測定されたシグナルの強さが事前に定義された間隔でしきい値を超えたときに信号強度の通知を送信します。

ミニポートドライバーは、この通知を使用して、要請されていないイベントも送信できます。

この通知では、 [**NDIS\_WWAN\_SIGNAL\_状態**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_signal_state)構造体を使用します。

<a name="remarks"></a>注釈
-------

既定では、Rssi 値が最後に報告された値から少なくとも +/-5 デシベルで変更された場合、または5秒ごとに1回表示される場合、ミニポートドライバーは MB サービスに通知する必要があります。 しきい値は、Signalstate に指定されて**います。 RssiThreshold**メンバーは、NDIS\_WWAN\_シグナル\_状態構造体です。最大 frequency 値は、 **Signalstate. RssiInterval**メンバーで指定されます。

NDIS\_WWAN\_DEVICE\_CAPS 構造体の**DeviceCaps**メンバーは、MB サービスによって Rssi 値がどのように解釈されるかを制御します。 **WwanCellularClass**が**WwanCellularClassGSM**の場合、Rssi はデバイスの感度ノイズフロアを上回るデシベルとして報告されます。 **WwanCellularClass**が**WwanCellularClassCDMA**の場合、Rssi は補正 Rssi (ノイズ用のアカウント) として報告されます。

アプリケーションはシグナルの強さをポーリングしないようにする必要があります。 スタートアップなどの特殊な状況でのみ、アプリケーションは*クエリ*要求を使用してシグナルの強さを取得することがあります。

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
<td>Ndis. h</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**NDIS\_WWAN\_シグナル\_状態**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_signal_state)

[OID\_WWAN\_シグナル\_状態](oid-wwan-signal-state.md)

 

 




