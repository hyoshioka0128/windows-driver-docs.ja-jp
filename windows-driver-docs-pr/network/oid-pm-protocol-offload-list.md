---
title: OID_PM_PROTOCOL_OFFLOAD_LIST
description: クエリとして、それまでのドライバーは OID_PM_PROTOCOL_OFFLOAD_LIST OID を使用して、基になるネットワークアダプターに設定されているプロトコルオフロードを列挙できます。
ms.assetid: 95ace77b-e583-4611-8460-af67b4d4805d
ms.date: 08/08/2017
keywords: -Windows Vista 以降の OID_PM_PROTOCOL_OFFLOAD_LIST ネットワークドライバー
ms.localizationpriority: medium
ms.openlocfilehash: 2b56a7e7dab666171abca749c408a610033162fd
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844052"
---
# <a name="oid_pm_protocol_offload_list"></a>OID\_PM\_プロトコル\_オフロード\_一覧


クエリとして、それより前のドライバーは OID\_PM\_プロトコル\_オフロード\_リスト OID を使用して、基になるネットワークアダプターに設定されているプロトコルオフロードを列挙できます。 OID クエリ要求から正常に戻った後、 [**ndis\_oid\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)構造の**informationbuffer**メンバーには、 [**ndis\_PM\_プロトコル\_オフロード**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_pm_protocol_offload)のリストへのポインターが含まれています。現在アクティブなプロトコルのオフロードを記述する構造体。

<a name="remarks"></a>注釈
-------

NDIS はミニポートドライバーのクエリを処理します。 NDIS ドライバーでは、OID\_PM\_プロトコル\_オフロード\_リスト OID を使用して、基になるネットワークアダプターに設定されているプロトコルオフロードの一覧を取得できます。

Ndis では、各[**ndis\_PM\_プロトコル\_オフロード**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_pm_protocol_offload)構造を一覧で使用して、 **NEXTPROTOCOLOFFLOADOFFSET**メンバーを OID 情報バッファーの先頭からのオフセット (つまり、リスト内の次の NDIS\_PM\_プロトコル\_オフロード構造の開始位置を示す[**ndis\_OID\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)構造体を指す) の**informationbuffer**メンバー。 リスト内の最後の構造体の**NextProtocolOffloadOffset**メンバーのオフセットが0です。

ネットワークアダプターに設定されているプロトコルオフロードがない場合、NDIS はデータを設定し**ます。クエリ\_情報。BytesWritten** OID のメンバーが\_要求構造体を0に指定し、ndis\_STATUS\_SUCCESS を返しました。 データ内のデータ **。クエリ\_情報。 InformationBuffer**メンバーは、NDIS によって変更されていません。

NDIS は、要求に対して次のいずれかの状態コードを返します。

<a href="" id="ndis-status-success"></a>NDIS\_状態\_成功  
要求は正常に完了しました。 **Informationbuffer**には、プロトコルのオフロードのリストへのポインターが含まれています (存在する場合)。

<a href="" id="ndis-status-pending"></a>NDIS\_状態\_保留中  
要求は完了待ちです。 最終的な状態コードと結果は、呼び出し元の OID 要求完了ハンドラーに渡されます。

<a href="" id="ndis-status-buffer-too-short"></a>NDIS\_ステータス\_バッファー\_短すぎる\_  
情報バッファーが短すぎます。 NDIS はデータを設定**します。クエリ\_情報。** 必要な最小バッファーサイズに対して、NDIS\_OID\_要求構造体のメンバーが必要です。

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
<td><p>NDIS 6.20 以降でサポートされています。 ミニポートドライバーが要求されていません。 (「解説」を参照してください。)</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Ntddndis (Ndis .h を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**NDIS\_OID\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)

[**NDIS\_PM\_プロトコル\_オフロード**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_pm_protocol_offload)

 

 




