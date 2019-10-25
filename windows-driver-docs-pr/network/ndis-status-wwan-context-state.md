---
title: NDIS_STATUS_WWAN_CONTEXT_STATE
description: ミニポートドライバーは、特定のコンテキストのアクティブ化状態が変化したときに、NDIS_STATUS_WWAN_CONTEXT_STATE 通知を使用してイベント通知を送信します。
ms.assetid: 6713f6a3-d1b7-49d0-83e1-50a33e9fff32
ms.date: 08/08/2017
keywords: -Windows Vista 以降の NDIS_STATUS_WWAN_CONTEXT_STATE ネットワークドライバー
ms.localizationpriority: medium
ms.openlocfilehash: 3b55732d4c213fbe96c303b05febb9d750a62ad7
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842634"
---
# <a name="ndis_status_wwan_context_state"></a>NDIS\_ステータス\_WWAN\_コンテキスト\_状態


ミニポートドライバーは、特定のコンテキストのアクティベーション状態が変更されたときにイベント通知を送信するために、NDIS\_ステータス\_WWAN\_コンテキスト\_状態通知を使用します。

ミニポートドライバーは、この通知を使用して、要請されていないイベントも送信できます。

この通知では、 [**NDIS\_WWAN\_コンテキスト\_状態**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_context_state)構造を使用します。

<a name="remarks"></a>注釈
-------

また、MB サービスからの*set*要求の結果としてコンテキスト状態の変更が発生しない場合、ミニポートドライバーは mb サービスに通知する必要があります。 たとえば、ネットワークがコンテキストを非アクティブにした場合、ミニポートドライバーは MB サービスに通知する必要があります。 ミニポートドライバーでは、ネットワークで開始されたコンテキストのアクティブ化を実装しないでください。

ミニポートドライバーは、適用されるすべてのコンテキスト状態の変更について、Windows に直接通知する必要があります。たとえば、NDIS\_ステータス\_WWAN\_パケット\_サービスまたは NDIS\_状態\_WWAN\_REGISTER\_状態の通知。

個別の音声接続とデータ接続をサポートする、MB のミニポートドライバーは、次のガイドラインに従う必要があります。

-   初期化時には、VoiceCallState を WwanVoiceCallStateNone に設定する必要があります。

-   音声通話の開始時に、VoiceCallState を WwanVoiceCallStateInProgress に設定してイベント通知を送信します。 他のすべてのメンバーは、現在の状態を反映している必要があります。 音声通話中にアクティブな接続がない場合は、ConnectionId を "0" に設定する必要があります。

-   音声通話が完了したら、VoiceCallState を WwanVoiceCallStateHangUp に設定してイベント通知を送信します。 他のすべてのメンバーは、現在の状態を反映している必要があります。 音声通話の切断中にアクティブな接続がない場合は、ConnectionId を "0" に設定する必要があります。 このイベントの後に、ミニポートドライバーで VoiceCallState を**WwanVoiceCallStateNone**に設定する必要があります。

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


[**NDIS\_WWAN\_コンテキスト\_の状態**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_context_state)

[OID\_WWAN\_プロビジョニングされた\_コンテキスト](oid-wwan-provisioned-contexts.md)

 

 




