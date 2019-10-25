---
title: OID_WWAN_READY_INFO
description: OID_WWAN_READY_INFO は、デバイスの準備完了状態を返します。これには、そのサブスクライバー Id モジュール (SIM カード) が含まれます。
ms.assetid: 3e6f6cb7-14fc-4eee-b5d6-d5e0cad46ea2
ms.date: 08/08/2017
keywords: -Windows Vista 以降の OID_WWAN_READY_INFO ネットワークドライバー
ms.localizationpriority: medium
ms.openlocfilehash: f9b442eb56e0d1577ef8cd3dd27c030e636c3eff
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843799"
---
# <a name="oid_wwan_ready_info"></a>OID\_WWAN\_準備完了\_情報


OID\_WWAN\_準備完了\_情報は、デバイスの準備完了状態を返します。これには、そのサブスクライバー Id モジュール (SIM カード) が含まれます。 これは、通常、セッションの開始時に発生します。

Set 要求はサポートされていません。

ミニポートドライバーは、クエリ要求を非同期的に処理し、最初に NDIS\_\_STATUS を返し、元の要求に対して必要な\_を示し、その後、 [**ndis\_ステータス\_WWAN\_準備完了\_に送信する必要があり**](ndis-status-wwan-ready-info.md)クエリ要求の完了時に、MB デバイスの準備完了状態を示す、 [**NDIS\_WWAN\_READY\_info**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_ready_info)構造体を含む情報ステータス通知。

<a name="remarks"></a>注釈
-------

この OID の使用方法の詳細については、「 [MB デバイスの準備](https://docs.microsoft.com/windows-hardware/drivers/network/mb-device-readiness)」を参照してください。

ミニポートドライバーは、クエリ操作の処理時にデバイスメモリまたは SIM カードにアクセスできますが、プロバイダーネットワークにはアクセスできません。

ミニポートドライバーは、PIN がクリアされる (必要な場合) まで待機してから、サブスクライバーの id と電話番号 (TNs) を読み取り、次に、NDIS\_\_\_の ReadyInfo の ReadyState メンバーをに設定します。WwanReadyStateInitialized.

ミニポートドライバーは、\_の OID\_の準備ができている\_情報ではなく、常に正しいデバイスの準備完了状態を返す必要があります。

ミニポートドライバーは、デバイスの準備ができているときに常に MB サービスに通知する必要があります。

優れたユーザーエクスペリエンスを提供するには、ミニポートドライバーが次の手順に従う必要があります。

-   PIN1 がロックされている場合、ミニポートドライバーは、 **ReadyInfo**を*WwanReadyStateDeviceLocked*に設定した状態のイベント通知を最初に送信する必要があります。 次に、MB サービスは、WWAN\_PIN\_oid セット要求の OID を送信します。 デバイスのロックが解除された後、ミニポートドライバーは、 **ReadyInfo**を*WwanReadyStateInitialized*に設定した状態で、別の準備完了イベント通知を送信する必要があります。 PIN1 が正常にロック解除されるまで、ミニポートドライバーでは、デバイスの準備完了状態を*WwanReadyStateInitialized*に変更することはできません。

-   ミニポートドライバーは、まず、ReadyInfo を使用してイベント通知を送信する必要があります。*この場合、* MB サービスが sim カードが存在しない場合はミニポートドライバーを読み込む場合は、sim カードを使用できるデバイスの場合もあり**ます。** 挿入または削除されます。 デバイスに SIM カードのホット挿入を検出する機能がある場合、ミニポートドライバーは、ユーザーが SIM を挿入するときに、ReadyState を*WwanReadyStateInitialized*に設定**し**て、別のイベント通知を送信する必要があります。

-   サービスのアクティブ化の状態を検出する機能を持つデバイスは、 **ReadyInfo**を*WwanReadyStateNotActivated*に設定する必要があります。 さらに、ミニポートドライバーがサービスのアクティブ化をサポートしている場合、ミニポートドライバーは oid\_WWAN\_サービス\_アクティブ化の OID セット要求を受け取ります。 サービスのアクティブ化が正常に完了した場合、ミニポートドライバーは、ReadyInfo を*WwanReadyStateInitialized*に設定**し**て別のイベント通知を送信する必要があります。

-   特定のファームウェアのリビジョンを必要とするミニポートドライバーは、正しいファームウェアのリビジョンが使用可能であることを確認する必要があります。 ファームウェアのリビジョンが使用できない場合は、 **ReadyInfo**を*WwanReadyStateFailure*に設定して、ミニポートドライバーがイベント通知トランザクションを完了する必要があります。

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


[**NDIS\_WWAN\_準備完了\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_ready_info)

[**NDIS\_ステータス\_WWAN\_準備完了\_情報**](ndis-status-wwan-ready-info.md)

[デバイスの準備 (MB)](https://docs.microsoft.com/windows-hardware/drivers/network/mb-device-readiness)

 

 




