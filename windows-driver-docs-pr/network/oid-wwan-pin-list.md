---
title: OID_WWAN_PIN_LIST
description: OID_WWAN_PIN_LIST MB デバイスでサポートされている個人の Id 番号 (Pin) のすべてのさまざまな種類の一覧を取得し、(最小値と最大の長さ)、暗証番号 (pin) 形式では、PIN の入力モードの PIN の長さなど、各ピンの追加の詳細を入力(有効/無効/が使用不可)。 この OID には、デバイスでサポートされている各ピンの現在のモードも指定します。 要求のセットがサポートされていません。 ミニポート ドライバーする必要がありますクエリ要求を処理、非同期的に NDIS_STATUS_INDICATION_REQUIRED を元の要求を最初に返すと、後で NDIS_WWAN_PIN_LIST の構造体を格納している NDIS_STATUS_WWAN_PIN_LIST 状態通知の送信クエリ要求を完了するときは、対応する説明を伴うピンの一覧を返します。
ms.assetid: 76a1181c-974e-472d-ad15-d9c6208aa2b4
ms.date: 08/08/2017
keywords: -OID_WWAN_PIN_LIST ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 4ff9595dfb399a370d3c976febb8440cc20c9a45
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67360766"
---
# <a name="oidwwanpinlist"></a>OID\_WWAN\_PIN\_一覧


OID\_WWAN\_PIN\_リストが MB デバイスでサポートされている個人の Id 番号 (Pin) のすべてのさまざまな種類の一覧を返し、PIN の長さなど、各ピンの追加の詳細を入力 (最小値と最大長)、PIN の形式、PIN の入力モード (有効/無効/が使用不可)。 この OID には、デバイスでサポートされている各ピンの現在のモードも指定します。

要求のセットがサポートされていません。

ミニポート ドライバーは、最初に、非同期的には、NDIS を返すクエリ要求を処理する必要があります\_状態\_INDICATION\_元の要求とそれ以降の送信に必要な[ **NDIS\_状態\_WWAN\_PIN\_一覧**](ndis-status-wwan-pin-list.md)状態通知を含む、 [ **NDIS\_WWAN\_暗証番号(pin)\_リスト**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_pin_list)構造体をクエリ要求を完了したときに、対応する説明を伴うピンの一覧を返します。

<a name="remarks"></a>コメント
-------

詳細については、この OID を使用して、次を参照してください。 [WWAN ピン留め操作](https://docs.microsoft.com/windows-hardware/drivers/network/mb-pin-operations)します。

ミニポート ドライバー Subscriber Identity Module (SIM カード) にアクセスできる処理がクエリ操作が、プロバイダーのネットワークにアクセスしないでください。

ミニポート ドライバーでは、自分のデバイスでサポートされているすべてのピンを報告する必要があります。 デバイスが Pin を一覧表示をサポートしていない場合、ミニポート ドライバーがサポートされるすべてのデバイスのミニポート ドライバー自体に保持される静的な (ハード コードされた) の一覧には、この一覧をレポートする必要があります。

デバイス電源投入時の検証または id の機能を提供する、暗証番号 (pin) は、PIN1 として報告する必要があり、PIN1 ガイドラインに準拠している必要があります。

デバイスの準備完了状態を変更するときに、ミニポート ドライバーはこの情報を返す必要があります*WwanReadyStateInitialized*またはデバイスの準備完了状態が*WwanReadyStateDeviceLocked* (ピンがロックされています)。 ミニポート ドライバーが可能な限り、この情報を他のデバイスの準備完了の状態で返すもする必要があります。

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


[**NDIS\_WWAN\_PIN\_一覧**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_pin_list)

[**NDIS\_状態\_WWAN\_PIN\_一覧**](ndis-status-wwan-pin-list.md)

[WWAN ピン留め操作](https://docs.microsoft.com/windows-hardware/drivers/network/mb-pin-operations)

 

 




