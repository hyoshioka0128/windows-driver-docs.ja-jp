---
title: OID_WWAN_PIN
description: OID_WWAN_PIN を設定または暗証番号 (Pin) に関連する情報を取得します。
ms.assetid: 5c93ffe0-8067-4022-ba8e-e528e44692e6
ms.date: 08/08/2017
keywords: -OID_WWAN_PIN ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 42e58929faa293234ef314b713186a3b3eea820a
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56571166"
---
# <a name="oidwwanpin"></a>OID\_WWAN\_暗証番号 (PIN)


OID\_WWAN\_暗証番号 (pin) が暗証番号 (Pin) に関連する情報を取得または設定します。

ミニポート ドライバー セットを処理する必要があり、クエリ要求が最初に、非同期に返す NDIS\_状態\_を示す値\_元の要求とそれ以降の送信に必要な[ **NDIS\_ステータス\_WWAN\_PIN\_情報**](ndis-status-wwan-pin-info.md)セットまたはクエリの要求が完了しているときに、状態の通知。

ミニポート ドライバーに送信する必要があります[ **NDIS\_状態\_WWAN\_PIN\_情報**](ndis-status-wwan-pin-info.md)を格納している状態の通知、 [ **NDIS\_WWAN\_PIN\_情報**](https://msdn.microsoft.com/library/windows/hardware/ff567911) MB デバイスまたはサブスクライバーのロックを解除する PIN が必要かどうかを示すために主に、暗証番号 (pin) 型と PIN の入力の状態情報を返す構造体Identity モジュール (SIM カード) クエリ要求を完了するとき。

呼び出し元がピンに関連する情報を設定する要求を提供、 [ **NDIS\_WWAN\_設定\_PIN** ](https://msdn.microsoft.com/library/windows/hardware/ff567922) MB のデバイスに PIN を送信するミニポート ドライバーに構造体有効にするか、PIN の設定を無効にする、SIM で PIN を変更したりします。

<a name="remarks"></a>コメント
-------

参照してください[WWAN ピン留め操作](https://msdn.microsoft.com/library/windows/hardware/ff559093)詳細については、この OID を使用します。

Windows 7 のミニポート ドライバーは、OID を使用する必要があります\_WWAN\_ピン留めします。 Windows 8 のミニポート ドライバーを使用する必要があります[OID\_WWAN\_PIN\_EX](oid-wwan-pin-ex.md)します。

ミニポート ドライバー Subscriber Identity Module (SIM カード) にアクセスできる処理がクエリ操作が、プロバイダーのネットワークにアクセスしないでください。

ミニポート ドライバーの初期化プロセス中に MB、サービスは続行されませんを登録する PIN1 が正常にロックされるまで有効になっている場合。

ミニポート ドライバーで、エンドユーザーが入力した暗証番号 (pin) 値を提供する、 **PinAction.Pin**の NDIS メンバー\_WWAN\_設定\_暗証番号 (pin) の構造を処理するときは、要求を設定します。 暗証番号 (pin) の値には、SIM カードに格納された値が一致する場合にのみ必要があります、要求を処理、ミニポート ドライバー。 ミニポート ドライバーが状態コード WWAN セットの要求を失敗するそれ以外の場合、\_状態\_失敗します。

CDMA ベースのデバイスでは、PIN1 として電源投入時のデバイスのロックを報告する必要があります。

ピンの種類、サポートされている、ミニポート ドライバーをサポートする必要があります、 *WwanPinOperationEnter*操作。 さらに、PIN1 がサポートされている場合のミニポート ドライバー サポートする必要が、 *WwanPinOperationEnable*、 *WwanPinOperationDisable*、および*WwanPinOperationChange*操作です。

ミニポート ドライバーできます WWAN で要求が失敗するか場合は、暗証番号 (pin) には、そのピンの型がロックされているとき、暗証番号 (pin) の種類が試されますの操作が無効にする、\_状態\_PIN\_も必要な作業を正常に完了要求。 ミニポート ドライバーでは、要求は正常に完了すると、無効にする操作、暗証番号 (pin) のロック解除もする必要があります。

複数の Pin を有効にし、一度に 1 つだけの暗証番号 (pin) を報告できるレポート作成、ミニポート ドライバーが PIN1 を最初にレポートで必要です。 たとえば、SubsidyLock と SIM PIN1 のレポートが有効な場合し SubsidyLock 暗証番号 (pin) に報告されます (後続のクエリ要求) PIN1 が正常に検証された後にのみ。

MB API には、PIN1 だけでなく他のピンがサポートされています。 ただし、サード パーティ製接続マネージャー/GUI は、Windows 接続マネージャー/GUI PIN1 のみをサポートするためにインストールする必要があります。

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


[**NDIS\_WWAN\_PIN\_情報**](https://msdn.microsoft.com/library/windows/hardware/ff567911)

[**NDIS\_WWAN\_設定\_暗証番号 (PIN)**](https://msdn.microsoft.com/library/windows/hardware/ff567922)

[**NDIS\_状態\_WWAN\_PIN\_情報**](ndis-status-wwan-pin-info.md)

[WWAN ピン留め操作](https://msdn.microsoft.com/library/windows/hardware/ff559093)

 

 




