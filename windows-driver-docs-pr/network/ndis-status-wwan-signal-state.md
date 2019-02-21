---
title: NDIS_STATUS_WWAN_SIGNAL_STATE
description: ミニポート ドライバーは、信号強度を測定すると通知を送信する NDIS_STATUS_WWAN_SIGNAL_STATE 通知を使用して、事前定義された間隔内で、しきい値の範囲外の強度の移動を通知します。
ms.assetid: b5d6b2a6-ed19-45d9-85ca-ac66e38f41fd
ms.date: 08/08/2017
keywords: -NDIS_STATUS_WWAN_SIGNAL_STATE ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: dfd6fd10142ae4457849732c50876103fc9a89f1
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56537941"
---
# <a name="ndisstatuswwansignalstate"></a>NDIS\_状態\_WWAN\_信号\_状態


ミニポート ドライバーを使用して、NDIS\_状態\_WWAN\_信号\_信号強度を測定すると通知を送信する状態の通知、事前定義された間隔内で、しきい値の範囲外の強度の移動の通知.

ミニポート ドライバーには、この通知が不要なイベントを送信できます。

この通知を使用して、 [ **NDIS\_WWAN\_信号\_状態**](https://msdn.microsoft.com/library/windows/hardware/ff567931)構造体。

<a name="remarks"></a>注釈
-------

既定では、ミニポート ドライバーは Rssi 値の変更によって、少なくとも過去 5 デシベル単位 +/-報告された値、または 1 つを示す値 5 秒ごとの最大の頻度でサービスに MB を通知する必要があります。 しきい値の値が指定された、 **SignalState.RssiThreshold**の NDIS メンバー\_WWAN\_信号\_状態構造体、で最大の頻度の値が指定されて**SignalState.RssiInterval**メンバー。

**DeviceCaps.WwanCellularClass**の NDIS メンバー\_WWAN\_デバイス\_CAPS 構造体が MB サービスによって Rssi 値を解釈する方法を制御します。 場合**WwanCellularClass**は**WwanCellularClassGSM**Rssi がデバイスの秘密度ノイズ フロア上デシベル単位として報告されます。 場合**WwanCellularClass**は**WwanCellularClassCDMA**Rssi がレベル RSSI (ノイズのアカウント) として報告されます。

信号の強度には、アプリケーションはポーリングする必要があることはありません。 起動時などの特殊な状況でのみ、アプリケーションを使用して、*クエリ*信号の強さを取得する要求。

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
<td>Ndis.h</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**NDIS\_WWAN\_信号\_状態**](https://msdn.microsoft.com/library/windows/hardware/ff567931)

[OID\_WWAN\_信号\_状態](oid-wwan-signal-state.md)

 

 




