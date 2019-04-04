---
title: OID_WWAN_READY_INFO
description: OID_WWAN_READY_INFO では、デバイスの準備完了の状態、その Subscriber Identity Module (SIM カード) を含むを返します。
ms.assetid: 3e6f6cb7-14fc-4eee-b5d6-d5e0cad46ea2
ms.date: 08/08/2017
keywords: -OID_WWAN_READY_INFO ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 4b34a8b706684b9b3871f6ae1f71d3ed20b4132a
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56573136"
---
# <a name="oidwwanreadyinfo"></a>OID\_WWAN\_準備\_情報


OID\_WWAN\_準備\_情報がデバイスの準備完了の状態、その Subscriber Identity Module (SIM カード) を含むを返します。 これは、任意のセッションの先頭に通常発生します。

要求のセットがサポートされていません。

ミニポート ドライバーは、最初に、非同期的には、NDIS を返すクエリ要求を処理する必要があります\_状態\_INDICATION\_元の要求とそれ以降の送信に必要な[ **NDIS\_状態\_WWAN\_準備\_情報**](ndis-status-wwan-ready-info.md)状態通知を含む、 [ **NDIS\_WWAN\_準備完了\_情報**](https://msdn.microsoft.com/library/windows/hardware/ff567916)クエリ要求を完了したときに、構造体を示す MB デバイスの準備完了状態。

<a name="remarks"></a>コメント
-------

詳細については、この OID を使用して、[MB デバイスの準備](https://msdn.microsoft.com/library/windows/hardware/ff557164)を参照してください。

ミニポート ドライバーがデバイスのメモリをアクセスまたは SIM カードの処理時にクエリ操作が、プロバイダーのネットワークにアクセスしないでください。

ミニポート ドライバーが (必要な) 場合、PIN がクリアされるまで待機する必要がありますと、サブスクライバーの id と電話番号 (TNs) を読み取るし、NDIS の ReadyInfo.ReadyState メンバーを設定し、\_WWAN\_準備\_情報WwanReadyStateInitialized 構造体。

ミニポート ドライバーは OID に失敗することは決して\_WWAN\_準備\_必要があり、情報は常に正しいデバイスの準備完了状態を返します。

デバイスの準備完了状態が変更されるたびに、ミニポート ドライバーは MB サービスを常に通知する必要があります。

ミニポート ドライバーには、次の手順で、優れたユーザー エクスペリエンスを提供する必要がありますに従います。

-   PIN1 がロックされている場合のミニポート ドライバーが準備完了の状態のイベント通知を送信する必要が最初**ReadyInfo.ReadyState**設定*WwanReadyStateDeviceLocked*します。 MB サービス要求を送信、ミニポート ドライバー、OID セット OID の\_WWAN\_ピン留めします。 デバイスのロックを解除し、ミニポート ドライバーを別の準備完了の状態のイベント通知を送信する必要があります後**ReadyInfo.ReadyState**に設定*WwanReadyStateInitialized*します。 ミニポート ドライバーにデバイスの準備完了状態を変更する必要があります PIN1 が正常にロックするまで*WwanReadyStateInitialized*します。

-   ミニポート ドライバーでイベント通知の送信する必要がありますまず**ReadyInfo.ReadyState**設定*WwanReadyStateSimNotInserted* MB サービスが SIM カードが月として、存在しない場合、ミニポート ドライバーを読み込むときにSIM カードが挿入または削除を許可するデバイスの場合があります。 ミニポート ドライバーと別のイベント通知を送信する必要があります、デバイスに SIM カードのホットな挿入を検出する機能がある場合は、 **ReadyInfo.ReadyState**設定*WwanReadyStateInitialized*ときに、ユーザーは、SIM を挿入します。

-   サービス アクティブ化の状態を検出する機能を搭載するデバイスを設定する必要があります**ReadyInfo.ReadyState**に*WwanReadyStateNotActivated*します。 さらに、ミニポート ドライバーでは、サービスのアクティブ化をサポートする場合、ミニポート ドライバーが要求を受信 OID セット OID の\_WWAN\_サービス\_アクティブ化します。 サービスのアクティブ化が正常に完了、ミニポート ドライバーと別のイベント通知を送信する必要があります**ReadyInfo.ReadyState**設定*WwanReadyStateInitialized*します。

-   ミニポート ドライバーを特定のファームウェアのリビジョンを必要とする必要があります、適切なファームウェアのリビジョンが使用できることを確認します。 ミニポート ドライバーが設定してイベント通知のトランザクションを完了する必要があります、ファームウェアのリビジョンが利用できない場合**ReadyInfo.ReadyState**に*WwanReadyStateFailure*します。

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


[**NDIS\_WWAN\_準備\_情報**](https://msdn.microsoft.com/library/windows/hardware/ff567916)

[**NDIS\_状態\_WWAN\_準備\_情報**](ndis-status-wwan-ready-info.md)

[MB デバイスの準備](https://msdn.microsoft.com/library/windows/hardware/ff557164)

 

 




