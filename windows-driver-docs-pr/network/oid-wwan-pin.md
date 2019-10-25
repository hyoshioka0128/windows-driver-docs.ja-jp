---
title: OID_WWAN_PIN
description: OID_WWAN_PIN は、暗証番号 (Pin) に関連する情報を設定または返します。
ms.assetid: 5c93ffe0-8067-4022-ba8e-e528e44692e6
ms.date: 08/08/2017
keywords: -Windows Vista 以降の OID_WWAN_PIN ネットワークドライバー
ms.localizationpriority: medium
ms.openlocfilehash: d2dfc86d22a39a70a7dff7431cda9307c421f975
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843813"
---
# <a name="oid_wwan_pin"></a>OID\_WWAN\_PIN


OID\_WWAN\_PIN は、暗証番号 (pin) に関連する情報を設定または返します。

ミニポートドライバーは、セットおよびクエリ要求を非同期的に処理し、最初に NDIS\_\_STATUS を返し、元の要求に対して必要な\_を示し、後で[**ndis\_ステータス\_WWAN\_PIN を送信する必要があり @no__t**](ndis-status-wwan-pin-info.md)設定要求またはクエリ要求を完了したときの情報状態通知 (_s)

ミニポートドライバーは、 [**ndis\_ステータス\_wwan\_pin\_情報**](ndis-status-wwan-pin-info.md)の状態通知を送信する必要があります。これには、pin の種類と pin を返すための[ **\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_pin_info)構造が含まれます。情報は、主に、クエリ要求の完了時に、MB デバイスまたはサブスクライバー Id モジュール (SIM カード) のロックを解除するために PIN が必要かどうかを示すために指定します。

Pin に関連する情報を設定するように要求している呼び出し元は、 [**NDIS\_WWAN\_設定\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_set_pin)ピン留めをミニポートドライバーに設定して、MB デバイスに pin を送信したり、pin の設定を有効または無効にしたり、SIM の pin を変更したりします。

<a name="remarks"></a>注釈
-------

この OID の使用方法の詳細については、「 [WWAN Pin 操作](https://docs.microsoft.com/windows-hardware/drivers/network/mb-pin-operations)」を参照してください。

Windows 7 ミニポートドライバーは、OID\_WWAN\_PIN を使用する必要があります。 Windows 8 ミニポートドライバーでは、 [\_EX\_PIN\_](oid-wwan-pin-ex.md)使用する必要があります。

ミニポートドライバーは、クエリ操作を処理するときにサブスクライバー Id モジュール (SIM カード) にアクセスできますが、プロバイダーネットワークにはアクセスできません。

ミニポートドライバーの初期化プロセスでは、PIN1 が正常にロック解除されるまで、MB サービスは登録に進みません。

ミニポートドライバーは、set 要求を処理するときに、エンドユーザーによって入力された PIN 値を、NDIS\_WWAN の**Pinaction. pin**メンバー\_設定\_ピン留めします。 PIN 値が SIM カードに格納されている値と一致する場合にのみ、要求をミニポートドライバーで処理する必要があります。 それ以外の場合、ミニポートドライバーは、ステータスコード WWAN\_ステータス\_失敗したセット要求を失敗させる必要があります。

CDMA ベースのデバイスは、電源オンデバイスのロックを PIN1 として報告する必要があります。

サポートされているすべての PIN の種類について、ミニポートドライバーは、 *Wwanpinoperationenter*操作をサポートする必要があります。 さらに、PIN1 がサポートされている場合、ミニポートドライバーは、 *Wwanpinoperationenable*、 *wwanpinoperationenable*、および*wwanpinoperationenable*操作をサポートする必要があります。

Pin の種類がロックされているときに pin の無効化操作が試行された場合、ミニポートドライバーは、WWAN\_ステータス\_の要求を失敗させるか、PIN\_必要があります。または、要求を正常に完了できます。 ミニポートドライバーが要求を正常に完了した場合、無効化操作でも PIN のロックが解除されます。

複数の Pin の報告が有効になっていて、一度に1つのピンだけを報告できる場合、ミニポートドライバーは最初に PIN1 を報告する必要があります。 たとえば、SubsidyLock と SIM PIN1 のレポートが有効になっている場合、PIN1 が正常に検証された後にのみ、(後続のクエリ要求で) SubsidyLock PIN を報告する必要があります。

MB API は、PIN1 に加えて他のピンもサポートしています。 ただし、Windows 接続マネージャー/GUI は PIN1 のみをサポートしているため、サードパーティの接続マネージャー/GUI をインストールする必要があります。

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


[**NDIS\_WWAN\_PIN\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_pin_info)

[**NDIS\_WWAN\_設定\_PIN**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_set_pin)

[**NDIS\_ステータス\_WWAN\_PIN\_情報**](ndis-status-wwan-pin-info.md)

[WWAN Pin の操作](https://docs.microsoft.com/windows-hardware/drivers/network/mb-pin-operations)

 

 




