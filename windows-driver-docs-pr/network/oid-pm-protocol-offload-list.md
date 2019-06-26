---
title: OID_PM_PROTOCOL_OFFLOAD_LIST
description: クエリとしてドライバー関連使用 OID_PM_PROTOCOL_OFFLOAD_LIST OID を列挙できます、基になるネットワーク アダプターに設定されているプロトコルのオフロードします。
ms.assetid: 95ace77b-e583-4611-8460-af67b4d4805d
ms.date: 08/08/2017
keywords: -OID_PM_PROTOCOL_OFFLOAD_LIST ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 5f563ebb18f062c69796277d468aa611a4cc33cd
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67377064"
---
# <a name="oidpmprotocoloffloadlist"></a>OID\_PM\_プロトコル\_オフロード\_一覧


クエリとしてドライバーを重なってできます OID を使用\_PM\_プロトコル\_オフロード\_一覧の OID を基になるネットワーク アダプターに設定されているプロトコルのオフロードを列挙します。 OID のクエリ要求から正常に戻った後、 **InformationBuffer**のメンバー、 [ **NDIS\_OID\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_oid_request)構造体一覧へのポインターを含む[ **NDIS\_PM\_プロトコル\_オフロード**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_pm_protocol_offload)現在アクティブなプロトコルを記述する構造体の負荷を軽減します。

<a name="remarks"></a>注釈
-------

NDIS は、ミニポート ドライバーにクエリを処理します。 NDIS ドライバーは、OID を使用できる\_PM\_プロトコル\_オフロード\_基になるネットワーク アダプターに設定されているプロトコルのオフロードの一覧を取得する一覧の OID。

各[ **NDIS\_PM\_プロトコル\_オフロード**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_pm_protocol_offload) NDIS セットの一覧で構造体、 **NextProtocolOffloadOffset**OID 情報バッファーの先頭からのオフセットにメンバー (つまり、バッファーの先頭を**InformationBuffer**のメンバー、 [ **NDIS\_OID\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_oid_request)へのポインターを構造体) [次へ] の NDIS の先頭に\_PM\_プロトコル\_の一覧でオフロード構造体。 内のオフセット、 **NextProtocolOffloadOffset**一覧の最後の構造体のメンバーは 0 になります。

ネットワーク アダプターに設定されているプロトコルのオフロードがない場合は、NDIS の設定、**データ。クエリ\_情報。BytesWritten** NDIS のメンバー\_OID\_要求の構造が 0 を返します。 NDIS\_状態\_成功します。 内のデータ、**データ。クエリ\_INFORMATION.InformationBuffer** NDIS によってメンバーが変更されていません。

NDIS は、要求の次のステータス コードのいずれかを返します。

<a href="" id="ndis-status-success"></a>NDIS\_状態\_成功  
要求は正常に完了しました。 **InformationBuffer**存在する場合は、プロトコルのオフロードの一覧へのポインターを格納します。

<a href="" id="ndis-status-pending"></a>NDIS\_状態\_PENDING  
完了待ちになっています。 最終的な状態コードと結果は、呼び出し元の OID 要求完了ハンドラーに渡されるされます。

<a href="" id="ndis-status-buffer-too-short"></a>NDIS\_状態\_バッファー\_すぎます\_短い  
情報バッファーが小さすぎます。 NDIS セット、**データ。クエリ\_情報。BytesNeeded** NDIS でメンバー\_OID\_構造体を最小バッファー サイズを要求が必要です。

<a href="" id="ndis-status-failure"></a>NDIS\_状態\_エラー  
上記の理由以外の理由、要求が失敗しました。

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
<td><p>以降では、NDIS 6.20 が動作をサポートします。 ミニポート ドライバーには要求されません。 (「解説」の「」を参照).</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Ntddndis.h (include Ndis.h)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**NDIS\_OID\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_oid_request)

[**NDIS\_PM\_プロトコル\_オフロード**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_pm_protocol_offload)

 

 




