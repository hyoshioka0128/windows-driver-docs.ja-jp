---
title: OID_WWAN_SIGNAL_STATE
description: OID_WWAN_SIGNAL_STATE 返します。 または現在のシグナルの状態を設定します。
ms.assetid: 6f5d8fd6-b4cf-4058-a27e-d4f7cea19f47
ms.date: 08/08/2017
keywords: -OID_WWAN_SIGNAL_STATE ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 0669db51a498d02b31d57d58eab82b552c8e0e21
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56578350"
---
# <a name="oidwwansignalstate"></a>OID\_WWAN\_信号\_状態


OID\_WWAN\_信号\_状態を返すか、現在のシグナルの状態を設定します。

ミニポート ドライバー セットを処理する必要があり、クエリ要求が最初に、非同期に返す NDIS\_状態\_を示す値\_元の要求とそれ以降の送信に必要な[ **NDIS\_ステータス\_WWAN\_信号\_状態**](ndis-status-wwan-signal-state.md)状態通知を含む、 [ **NDIS\_WWAN\_信号\_状態**](https://msdn.microsoft.com/library/windows/hardware/ff567931)設定の完了に関係なく、エンドユーザーに示すように現在シグナル状態の表示に関する情報を提供または要求をクエリする構造体。

呼び出し元をユーザーが現在シグナル状態の表示を設定する要求を提供、 [ **NDIS\_WWAN\_設定\_信号\_INDICATION** ](https://msdn.microsoft.com/library/windows/hardware/ff567928)適切な情報、ミニポート ドライバー構造体。

<a name="remarks"></a>コメント
-------

詳細については、この OID を使用して、次を参照してください。 [WWAN 信号強度操作](https://msdn.microsoft.com/library/windows/hardware/ff559125)します。

ミニポート ドライバー アクセスしないでください、プロバイダーのネットワークまたは Subscriber Identity Module (SIM カード) とクエリの処理または操作を設定します。

一般に、シグナルの状態が示されますのではなくにポーリングされます。 ただし、現在シグナルの状態が MB サービスによって決定する必要がある場合に、この OID は使用されます。

クエリ要求に応答して、ミニポート ドライバーは、NDIS を送信する必要があります\_状態\_WWAN\_信号\_状態通知します。

MB サービスからセットの要求のミニポート ドライバーが必要です。

-   現在の値を返す**Rssi**と**ErrorRate** NDIS で\_WWAN\_信号\_の絶対値のレポートに加えて、状態の構造体**RssiInterval**と**RssiThreshold**ミニポート ドライバーで設定されています。

-   内部的にキャッシュ、 **RssiInterval**や**RssiThreshold**値の場合でも、デバイスが任意の演算子と共に現在登録されていないと、その制限パラメーターの設定でデバイスによって課されることができます登録後の考えられる状態になります。 ミニポート ドライバーは、[次へ] の即時使用可能な状況ではこれらの設定を適用するようにしてください。

-   ハードウェアやソフトウェア無線スイッチの状態が OFF が現在の場合は、要求を正常に完了します。 ミニポート ドライバーでは、要求データをキャッシュし、信号強度、スイッチがオンにするとレポート作成を開始します。

-   適切なこの要求が失敗する可能性が**uStatus**エラー コードを設定します。

MB サービスからのクエリ要求を処理するときに、ミニポート ドライバーでは、次を実行できます。

-   現在の値を返す**Rssi**と**ErrorRate** NDIS で\_WWAN\_信号\_の絶対値のレポートに加えて、状態の構造体**RssiInterval**と**RssiThreshold**ミニポート ドライバーで設定されています。

-   適切なこの要求は失敗**uStatus**エラー コードを設定します。

戻り値。

NDIS\_状態\_いない\_サポートされています。

ミニポート ドライバーでは、信号の強さをサポートしていないデバイスの機能を認識している特定のデバイスのこれには、このエラー コードで要求を失敗を返すことができます。

**推奨される実装**

1.  デバイスは、信号強度のインジケーターをサポートする必要があります。

2.  ドライバーの少なくとも 50% の信号強度指標を報告する必要があります、 **RssiInterval** 5 分の期間を設定します。

3.  デバイスは、次の状態で信号の強さを報告を避ける必要があります。
    1.  デバイスがない登録または登録解除およびは GSM デバイスのみに適用されます。
    2.  オプションの有効な状態には OFF です。
    3.  上記の状態を信号の強さをクエリを次のデータ ミニポート ドライバーで返される必要があります。

        Rssi = WWAN\_RSSI\_不明

        ErrorRate = WWAN\_ERROR\_RATE\_UNKNOWN;

        RssiInterval = &lt; WWAN\_RSSI\_無効、WWAN\_RSSI\_既定値またはセットの最後の値&gt;

        RssiThreshold = &lt; WWAN\_RSSI\_無効、WWAN\_RSSI\_既定値またはセットの最後の値&gt;

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
<td><p>Windows 7 および Windows の以降のバージョンで使用できます。</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Ntddndis.h (include Ndis.h)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**NDIS\_WWAN\_設定\_信号\_を示す値**](https://msdn.microsoft.com/library/windows/hardware/ff567928)

[WWAN 信号強度の操作](https://msdn.microsoft.com/library/windows/hardware/ff559125)

 

 




