---
title: OID_WWAN_DRIVER_CAPS
description: OID_WWAN_DRIVER_CAPS は、ミニポートドライバーでサポートされている MB ドライバーモデルのバージョンを返します。
ms.assetid: 2310a341-6899-44ad-8dfb-a13fd0c42dcb
ms.date: 08/08/2017
keywords: -Windows Vista 以降の OID_WWAN_DRIVER_CAPS ネットワークドライバー
ms.localizationpriority: medium
ms.openlocfilehash: 6ea5310a837756060d4f3237d1acc24a412e1685
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843847"
---
# <a name="oid_wwan_driver_caps"></a>OID\_WWAN\_ドライバー\_CAP


OID\_WWAN\_ドライバー\_CAP は、ミニポートドライバーでサポートされている MB ドライバーモデルのバージョンを返します。

Set 要求はサポートされていません。

ミニポートドライバーは、OID\_WWAN\_ドライバー\_CAP を同期的に処理します。また、バージョンを示す[**NDIS\_WWAN\_DRIVER\_CAPS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_driver_caps)構造を含む応答バッファーと共に直ちに戻る必要があります。クエリ要求の完了時にミニポートドライバーによって実装された MB ドライバーモデルの。

<a name="remarks"></a>注釈
-------

この OID の使用方法の詳細については、「 [MB ミニポートドライバーの初期化](https://docs.microsoft.com/windows-hardware/drivers/network/mb-miniport-driver-initialization)」を参照してください。

クエリ操作を処理するときに、ミニポートドライバーはプロバイダーネットワークまたはサブスクライバー Id モジュール (SIM カード) にアクセスしないようにする必要があります。

現在のバージョンの MB ドライバーモデルのバージョンは、WWAN\_メジャー\_バージョンおよび WWAN\_マイナー\_バージョンによって定義され \#トークンを定義します。 ミニポートドライバーが、mb サービスでサポートされていない MB ドライバーモデルのバージョンを返した場合、そのデバイスは MB サービスによって無視されます。

MB サービスが初期化または再起動されると、ミニポートドライバーが既に読み込まれている可能性があります。 この場合、MB サービスは、ミニポートドライバーによって実装されている MB ドライバーモデルのバージョンを照会してから、他の Oid の発行を続行します。 これは、セッションの開始時に発生します。

すべての初期化エラーが発生した場合、ミニポートドライバーは NDIS\_の状態\_返す必要があり\_サポートされていません。 ミニポートドライバーが NDIS\_STATUS を返し\_\_サポートされていない場合、MB サービスはデバイスを無視し、他の Oid は続行されません。

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


[MB ミニポートドライバーの初期化](https://docs.microsoft.com/windows-hardware/drivers/network/mb-miniport-driver-initialization)

[**NDIS\_WWAN\_ドライバー\_CAP**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_driver_caps)

 

 




