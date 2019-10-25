---
title: OID_WWAN_SERVICE_ACTIVATION
description: OID_WWAN_SERVICE_ACTIVATION は、プロバイダーのネットワークへのアクセスを取得するために、サービスのアクティブ化を開始するようにミニポートドライバーに指示します。
ms.assetid: a70c087d-0650-4aab-b78e-0d5a7aa49eb6
ms.date: 08/08/2017
keywords: -Windows Vista 以降の OID_WWAN_SERVICE_ACTIVATION ネットワークドライバー
ms.localizationpriority: medium
ms.openlocfilehash: 97ec330be6aeeee3c0017fbd7d67f495e15ddc6f
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843793"
---
# <a name="oid_wwan_service_activation"></a>OID\_WWAN\_サービス\_アクティブ化


OID\_WWAN\_サービス\_アクティブ化は、プロバイダーのネットワークへのアクセスを取得するために、サービスのアクティブ化を開始するようにミニポートドライバーに指示します。

クエリ要求はサポートされていません。

ミニポートドライバーは、set 要求を非同期に処理し、最初に NDIS\_STATUS\_を返し、元の要求に必要な\_を示し、後で[**ndis\_ステータス\_WWAN\_サービスに送信する必要があり\_** ](ndis-status-wwan-service-activation.md)トランザクションの完了時にプロバイダーのネットワークにアクセスするためにサービスのアクティブ化を開始するための[**NDIS\_WWAN\_サービス\_アクティブ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_service_activation)化構造を含むアクティベーションステータス通知。

<a name="remarks"></a>注釈
-------

この OID の使用方法の詳細については、「 [MB サービスの検出とアクティブ化](https://docs.microsoft.com/windows-hardware/drivers/network/mb-service-detection-and-activation)」を参照してください。

ミニポートドライバーは、クエリまたは設定要求を処理するときに、サブスクライバー Id モジュール (SIM カード) またはプロバイダーネットワークにアクセスできます。

MB サービスは、サービスのアクティブ化プロセスでミニポートドライバーとユーザー操作が必要な場合に、OID\_WWAN\_サービス\_ライセンス認証を使用します。

これは、ミニポートドライバーが開始した、またはサービスプロバイダーのヘルプデスクへの呼び出しなど、帯域外の手動サービスのアクティブ化には必要ありません。 上記のシナリオのようにデバイスをアクティブ化した後、現在のミニポートドライバー **ReadyState**が*WwanReadyStateNotActivated*の場合、ミニポートドライバーは、mb の初期化に進み、mb サービスに対して準備完了の状態の変化を通知します。NDIS\_ステータス\_WWAN\_準備ができている\_情報を示します。

ミニポートドライバーは、ミニポートドライバーベースのサービスのアクティブ化をサポートしていない場合、NDIS\_の状態\_返す必要があり\_サポートされていません。

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


[OID\_WWAN\_準備完了\_情報](oid-wwan-ready-info.md)

[**NDIS\_WWAN\_サービス\_アクティブ化**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_service_activation)

[**NDIS\_ステータス\_WWAN\_サービス\_アクティブ化**](ndis-status-wwan-service-activation.md)

[MB サービスの検出とアクティブ化](https://docs.microsoft.com/windows-hardware/drivers/network/mb-service-detection-and-activation)

 

 




