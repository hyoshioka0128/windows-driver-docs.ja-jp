---
title: OID_WWAN_PIN_LIST
description: OID_WWAN_PIN_LIST は、MB デバイスでサポートされているすべての種類の個人識別番号 (Pin) と、pin の長さ (最小長と最大長)、PIN の形式、PIN-入力モードなどの追加の詳細情報の一覧を返します。(有効/無効/不可)。 この OID は、デバイスでサポートされている各 PIN の現在のモードも指定します。 Set 要求はサポートされていません。 ミニポートドライバーは、クエリ要求を非同期的に処理し、最初に NDIS_STATUS_INDICATION_REQUIRED を元の要求に戻してから、NDIS_WWAN_PIN_LIST 構造体を含む NDIS_STATUS_WWAN_PIN_LIST ステータス通知をに送信する必要があります。クエリ要求の完了時に、対応する説明と共にピンの一覧を返します。
ms.assetid: 76a1181c-974e-472d-ad15-d9c6208aa2b4
ms.date: 08/08/2017
keywords: -Windows Vista 以降の OID_WWAN_PIN_LIST ネットワークドライバー
ms.localizationpriority: medium
ms.openlocfilehash: 5f4c28923eee706ea830ac1e2f65ceed667255d5
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843815"
---
# <a name="oid_wwan_pin_list"></a>OID\_WWAN\_PIN\_リスト


OID\_WWAN\_PIN\_一覧には、MB デバイスでサポートされているさまざまな種類の暗証番号 (pin) と、pin の長さ (最小値と最大長) などの追加の詳細情報の一覧が表示されます。、PIN の形式、PIN-入力モード (有効/無効/使用不可)。 この OID は、デバイスでサポートされている各 PIN の現在のモードも指定します。

Set 要求はサポートされていません。

ミニポートドライバーは、クエリ要求を非同期的に処理し、最初に NDIS\_\_STATUS を返し、元の要求に必要な\_を示し、その後、 [**ndis\_ステータス\_WWAN\_PIN を送信する必要があり\_** ](ndis-status-wwan-pin-list.md) [**NDIS\_WWAN\_PIN\_リスト**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_pin_list)構造を含む状態通知を一覧表示して、クエリ要求の完了時に、対応する説明と共に pin の一覧を返します。

<a name="remarks"></a>注釈
-------

この OID の使用方法の詳細については、「 [WWAN Pin の操作](https://docs.microsoft.com/windows-hardware/drivers/network/mb-pin-operations)」を参照してください。

ミニポートドライバーは、クエリ操作を処理するときにサブスクライバー Id モジュール (SIM カード) にアクセスできますが、プロバイダーネットワークにはアクセスできません。

ミニポートドライバーは、デバイスでサポートされているすべての Pin を報告する必要があります。 デバイスが一覧のピンをサポートしていない場合、ミニポートドライバーは、サポートしているすべてのデバイスについて、ミニポートドライバー自体に保持されている静的 (ハードコーディングされた) リストからこのリストを報告する必要があります。

デバイスの電源検証機能または識別機能を提供する PIN は、PIN1 として報告され、PIN1 ガイドラインに準拠している必要があります。

ミニポートドライバーは、デバイスの準備完了状態が*WwanReadyStateInitialized*に変わるか、デバイスの準備ができている *(PIN*がロックされている) ときに、この情報を返す必要があります。 ミニポートドライバーは、可能な限り、他のデバイスの準備完了状態でこの情報を返す必要もあります。

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


[**NDIS\_WWAN\_PIN\_一覧**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_pin_list)

[**NDIS\_ステータス\_WWAN\_PIN\_一覧**](ndis-status-wwan-pin-list.md)

[WWAN Pin の操作](https://docs.microsoft.com/windows-hardware/drivers/network/mb-pin-operations)

 

 




