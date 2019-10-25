---
title: OID_PM_GET_PROTOCOL_OFFLOAD
description: ネットワークアダプターからの低電力プロトコルオフロードのパラメーター設定を取得するために、OID_PM_GET_PROTOCOL_OFFLOAD の OID メソッド要求が、後続のドライバーによって発行されます。
ms.assetid: c14b9278-6f24-41a1-bc2e-536a75460ecd
ms.date: 08/08/2017
keywords: -Windows Vista 以降の OID_PM_GET_PROTOCOL_OFFLOAD ネットワークドライバー
ms.localizationpriority: medium
ms.openlocfilehash: f3b6b3325b789bd23437c94af80df3fe1f8a9e01
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844057"
---
# <a name="oid_pm_get_protocol_offload"></a>OID\_PM\_\_プロトコル\_オフロードを取得します。


それより後のドライバーは oid\_PM の oid メソッド要求を発行し、ネットワークアダプターから低電力プロトコルオフロードのパラメーター設定を取得するために\_プロトコル\_オフロード\_取得します。

[**NDIS\_OID\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)構造体の**informationbuffer**メンバーには、最初に ULONG プロトコルオフロード識別子へのポインターが含まれています。 OID メソッド要求から正常に戻った後、 **ndis\_oid\_要求**構造の**informationbuffer**メンバーには、 [**ndis\_PM\_プロトコル\_オフロード**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_pm_protocol_offload)構造へのポインターが含まれています。

<a name="remarks"></a>注釈
-------

NDIS 6.20 以降のプロトコルドライバーでは、OID\_PM\_使用して\_プロトコル\_オフロード方式の OID を取得し、ネットワークアダプターから低電力プロトコルオフロードのパラメーター設定を取得します。

情報バッファーは、ULONG 型プロトコルオフロード識別子をポイントする必要があります。 Ndis は、ndis [ **\_pm\_\_プロトコル**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_pm_protocol_offload)の**ProtocolOffloadId**メンバーで、 [\_プロトコルの追加\_前の OID\_pm が送信されたときに、このプロトコルオフロード識別子を set\_](oid-pm-add-protocol-offload.md)基になるネットワークアダプターに対して OID 要求をオフロードします。

ミニポートドライバーは、要求に対して次のいずれかの状態コードを返します。

<a href="" id="ndis-status-success"></a>NDIS\_状態\_成功  
要求されたデータが正常に取得されました。 情報バッファーには、対応する NDIS\_PM\_プロトコル\_オフロード構造が含まれています。

<a href="" id="ndis-status-pending"></a>NDIS\_状態\_保留中  
要求は完了待ちです。 最終的な状態コードと結果は、呼び出し元の OID 要求完了ハンドラーに渡されます。

<a href="" id="ndis-status-invalid-parameter"></a>NDIS\_の状態\_無効な\_パラメーターです  
指定されたプロトコルオフロード識別子は無効です。

<a href="" id="ndis-status-buffer-too-short"></a>NDIS\_ステータス\_バッファー\_短すぎる\_  
情報バッファーが短すぎます。 NDIS はデータを設定**します。クエリ\_情報。** 必要な最小バッファーサイズに対して、NDIS\_OID\_要求構造体のメンバーが必要です。

<a href="" id="ndis-status-not-supported"></a>NDIS\_の状態\_\_サポートされていません  
ミニポートドライバーの NDIS バージョンが6.20 を下回っています。

<a href="" id="ndis-status-failure"></a>NDIS\_状態\_エラー  
この要求は、上記の理由以外の理由で失敗しました。

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
<td><p>NDIS 6.20 以降でサポートされています。 ミニポートドライバーの場合は必須です。 (「解説」を参照してください。)</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Ntddndis (Ndis .h を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**NDIS\_PM\_プロトコル\_オフロード**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_pm_protocol_offload)

[OID\_PM\_\_プロトコル\_オフロードの追加](oid-pm-add-protocol-offload.md)

 

 




