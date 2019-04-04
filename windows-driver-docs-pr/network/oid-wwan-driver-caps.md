---
title: OID_WWAN_DRIVER_CAPS
description: OID_WWAN_DRIVER_CAPS は、ミニポート ドライバーでサポートされている MB ドライバー モデルのバージョンを返します。
ms.assetid: 2310a341-6899-44ad-8dfb-a13fd0c42dcb
ms.date: 08/08/2017
keywords: -OID_WWAN_DRIVER_CAPS ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: fed4cfc9ac5595cacbe6ba3b145fc585a9b03c61
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56579884"
---
# <a name="oidwwandrivercaps"></a>OID\_WWAN\_ドライバー\_キャップ


OID\_WWAN\_ドライバー\_キャップは、ミニポート ドライバーでサポートされている MB ドライバー モデルのバージョンを返します。

要求のセットがサポートされていません。

ミニポート ドライバー処理 OID\_WWAN\_ドライバー\_同期的に上限を設定して、含まれた応答バッファーをすぐに完了する必要があります、 [ **NDIS\_WWAN\_ドライバー\_CAP** ](https://msdn.microsoft.com/library/windows/hardware/ff567908)クエリ要求を完了するときに、ミニポート ドライバーによって実装される MB ドライバー モデルのバージョンを記述する構造体。

<a name="remarks"></a>コメント
-------

詳細については、この OID を使用して、[MB ミニポート ドライバーの初期化](https://msdn.microsoft.com/library/windows/hardware/ff557186)を参照してください。

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


[MB ミニポート ドライバーの初期化](https://msdn.microsoft.com/library/windows/hardware/ff557186)

[**NDIS\_WWAN\_ドライバー\_キャップ**](https://msdn.microsoft.com/library/windows/hardware/ff567908)

 

 




