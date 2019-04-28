---
title: OID_WWAN_SERVICE_ACTIVATION
description: OID_WWAN_SERVICE_ACTIVATION では、ミニポート ドライバー プロバイダーのネットワークにアクセスするためにサービスのアクティブ化を開始するように指示します。
ms.assetid: a70c087d-0650-4aab-b78e-0d5a7aa49eb6
ms.date: 08/08/2017
keywords: -OID_WWAN_SERVICE_ACTIVATION ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 15574dd8a63a321b7c0e07e3dfbeba068eab3a1b
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63368452"
---
# <a name="oidwwanserviceactivation"></a>OID\_WWAN\_サービス\_アクティブ化


OID\_WWAN\_サービス\_ライセンス認証プロバイダーのネットワークにアクセスするためにサービスのアクティブ化を開始するミニポート ドライバーに指示します。

クエリ要求はサポートされていません。

ミニポート ドライバーが非同期的に、最初に返す NDIS セット要求を処理する必要があります\_状態\_INDICATION\_元の要求とそれ以降の送信に必要な[ **NDIS\_状態\_WWAN\_サービス\_アクティベーション**](ndis-status-wwan-service-activation.md)状態通知を含む、 [ **NDIS\_WWAN\_サービス\_アクティベーション**](https://msdn.microsoft.com/library/windows/hardware/ff567918)構造体をトランザクションが完了しているときに、プロバイダーのネットワークにアクセスするためにサービスのアクティブ化を開始します。

<a name="remarks"></a>注釈
-------

詳細については、この OID を使用して、次を参照してください。 [MB サービスの検出とアクティブ化](https://msdn.microsoft.com/library/windows/hardware/ff559122)します。

処理するときに、プロバイダーのネットワークは、クエリまたは要求を設定またはミニポート ドライバーが Subscriber Identity Module (SIM カード) にアクセスできます。

MB サービス OID を使用して\_WWAN\_サービス\_ライセンス認証の場合は、サービスのアクティブ化プロセスがミニポート ドライバーとユーザーの相互作用が必要です。

これは開始ミニポート ドライバーまたはサービス プロバイダーのヘルプ デスクを呼び出すなどの帯域外の手動のサービスのアクティブ化は必要ありません。 場合に、上記のシナリオと同様に、デバイスをアクティブ化した後、現在のミニポート ドライバー **ReadyState**は*WwanReadyStateNotActivated*、ミニポート ドライバーが MB の初期化で続行され、NDIS を使用して準備完了状態の変更の MB サービスに通知\_状態\_WWAN\_準備\_情報を示す値。

ミニポート ドライバーは、NDIS を返す必要があります\_状態\_いない\_ミニポート ドライバー ベースのサービスのアクティブ化をサポートしていない場合にサポートされています。

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
<td>Ntddndis.h (include Ndis.h)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[OID\_WWAN\_準備\_情報](oid-wwan-ready-info.md)

[**NDIS\_WWAN\_サービス\_アクティブ化**](https://msdn.microsoft.com/library/windows/hardware/ff567918)

[**NDIS\_状態\_WWAN\_サービス\_アクティブ化**](ndis-status-wwan-service-activation.md)

[MB サービスの検出とアクティブ化](https://msdn.microsoft.com/library/windows/hardware/ff559122)

 

 




