---
title: OID_WWAN_DRIVER_CAPS
description: OID_WWAN_DRIVER_CAPS は、ミニポート ドライバーでサポートされている MB ドライバー モデルのバージョンを返します。
ms.assetid: 2310a341-6899-44ad-8dfb-a13fd0c42dcb
ms.date: 08/08/2017
keywords: -OID_WWAN_DRIVER_CAPS ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 14b378f5d8b4518b315bc865c826fe9bcc650d2e
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385495"
---
# <a name="oidwwandrivercaps"></a>OID\_WWAN\_ドライバー\_キャップ


OID\_WWAN\_ドライバー\_キャップは、ミニポート ドライバーでサポートされている MB ドライバー モデルのバージョンを返します。

要求のセットがサポートされていません。

ミニポート ドライバー処理 OID\_WWAN\_ドライバー\_同期的に上限を設定して、含まれた応答バッファーをすぐに完了する必要があります、 [ **NDIS\_WWAN\_ドライバー\_CAP** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_driver_caps)クエリ要求を完了するときに、ミニポート ドライバーによって実装される MB ドライバー モデルのバージョンを記述する構造体。

<a name="remarks"></a>コメント
-------

詳細については、この OID を使用して、次を参照してください。 [MB ミニポート ドライバーの初期化](https://docs.microsoft.com/windows-hardware/drivers/network/mb-miniport-driver-initialization)します。

ミニポート ドライバーが、プロバイダーのネットワークまたは Subscriber Identity Module (SIM カード) にアクセスしないでくださいクエリ操作を処理するときにします。

WWAN MB ドライバー モデルのバージョンの現在のバージョンが定義されている\_メジャー\_バージョンと WWAN\_マイナー\_バージョン\#トークンを定義します。 ミニポート ドライバーでは、MB、サービスがサポートされていない MB ドライバー モデルのバージョンを返します、MB、サービスは、デバイスを無視します。

MB サービスを初期化または再起動すると、ミニポート ドライバー既に読み込まれている可能性があります。 この場合は、MB サービスは、その他の任意の Oid を発行するために進む前に、ミニポート ドライバーによって MB ドライバー モデルの実装のバージョンを照会します。 これは、任意のセッションの開始時に発生します。

ミニポート ドライバーは、NDIS を返す必要があります\_状態\_いない\_任意の初期化エラーの場合はサポートされています。 ミニポート ドライバーは、NDIS を返す場合\_状態\_いない\_サポート、MB サービスでは、デバイスを無視しでその他の任意の Oid は続行されません。

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


[MB ミニポート ドライバーの初期化](https://docs.microsoft.com/windows-hardware/drivers/network/mb-miniport-driver-initialization)

[**NDIS\_WWAN\_ドライバー\_キャップ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_driver_caps)

 

 




