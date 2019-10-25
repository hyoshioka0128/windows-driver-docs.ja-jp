---
title: OID_PM_ADD_WOL_PATTERN
description: セットとして、NDIS プロトコルドライバーは OID_PM_ADD_WOL_PATTERN OID を使用して、電源管理 wake on LAN パターンをネットワークアダプターに追加します。 NDIS_OID_REQUEST 構造体の InformationBuffer メンバーには、NDIS_PM_WOL_PATTERN 構造体へのポインターが含まれています。
ms.assetid: 1005cebb-8ead-4d16-b3ea-5a74da0b054f
ms.date: 08/08/2017
keywords: -Windows Vista 以降の OID_PM_ADD_WOL_PATTERN ネットワークドライバー
ms.localizationpriority: medium
ms.openlocfilehash: 6b3b9c374da2a89a2260fb72f6b766afdbecf935
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844062"
---
# <a name="oid_pm_add_wol_pattern"></a>OID\_PM\_\_WOL\_パターンの追加


セットとして、NDIS プロトコルドライバーでは、OID\_PM\_\_WOL\_PATTERN OID を追加して、ネットワークアダプターに電源管理 wake on LAN パターンを追加します。 [**Ndis\_OID\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)構造体の**informationbuffer**メンバーには、 [**ndis\_PM\_WOL\_パターン**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_pm_wol_pattern)構造へのポインターが含まれています。

<a name="remarks"></a>注釈
-------

NDIS 6.20 以降のプロトコルドライバーでは、OID\_PM\_使用して\_WOL\_パターンを追加して、ネットワークアダプターに Wake on LAN (WOL) パターンを追加します。 OID 要求には、ネットワークアダプターが低電力状態のときに、受信パケットと比較する必要がある条件が含まれています。 ネットワークアダプターは、パターンの条件に一致するパケットを受信すると、ウェイクアップイベントを生成する必要があります。

プロトコルドライバーは、基になるネットワークアダプターに正常にバインドされた後に、wol パターンを設定するために必要なデータ (インターフェイスの IP アドレスなど) があるとすぐに、WOL パターンを追加できます。 プロトコルドライバーは、以前に追加された WOL パターンやオフロードプロトコルの拒否など、他の電源管理イベント通知に応答して WOL パターンを追加することもできます。

NDIS および同じミニポートアダプターにバインドされているその他のプロトコルドライバーの競合状態を回避するために、NDIS がネットワークアダプターを低電力状態に設定しようとすると、そのネットワークアダプターに新しいウェイクアップパターンを追加しようとすると失敗します。 たとえば、NDIS プロトコルドライバーが、そのネットワークアダプターの**NetEventSetPower**イベント通知を処理するコンテキストで新しい WOL パターンを追加しようとすると、ndis は要求に失敗します。

NDIS がこの OID 要求を基になる NDIS ドライバーに送信するか、またはそれ以降のドライバーへの要求を完了する前に、 [**ndis\_PM\_WOL\_パターン**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_pm_wol_pattern)構造の ULONG **PatternId**メンバーを一意の値に設定します。 プロトコルドライバーと NDIS は、このパターン識別子を OID\_PM と共に使用して、基になるネットワークアダプターから WOL パターンを削除する[\_wol\_pattern oid 要求\_削除](oid-pm-remove-wol-pattern.md)します。

**  パターン**識別子は、ネットワークアダプターに設定されている各パターンに対して一意の値です。 ただし、パターン識別子は、すべてのミニポートアダプターでグローバルに一意ではありません。

 

NDIS または基になるネットワークアダプターが WOL パターンを削除すると、 [**ndis\_ステータス\_PM\_wol\_パターン\_拒否**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-pm-wol-pattern-rejected)状態が示されます。 [**NDIS\_ステータス\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_status_indication)表示構造体の**statusbuffer**メンバーは、拒否された WOL パターンの ULONG WOL パターン識別子を含みます。

ミニポートドライバーは、要求に対して次のいずれかの状態コードを返します。

<a href="" id="ndis-status-success"></a>NDIS\_状態\_成功  
要求されたパターンが正常に追加されました。 NDIS\_PM\_WOL\_PATTERN 構造体の**PatternId**メンバーには、パターン識別子が含まれています。

<a href="" id="ndis-status-pending"></a>NDIS\_状態\_保留中  
要求は完了待ちです。 NDIS は、要求が完了した後に、最終的な状態コードと結果を呼び出し元の OID 要求完了ハンドラーに渡します。

<a href="" id="ndis-status-pm-wol-pattern-list-full"></a>NDIS\_STATUS\_PM\_WOL\_パターン\_リスト\_完全  
パターン一覧がいっぱいで、ネットワークアダプターが別のパターンを追加できないため、要求は失敗しました。

<a href="" id="ndis-status-resources"></a>NDIS\_状態\_リソース  
リソースが不足しているため、NDIS または基になるネットワークアダプターで新しいパターンを追加できませんでした。

<a href="" id="ndis-status-invalid-parameter"></a>NDIS\_の状態\_無効な\_パラメーターです  
NDIS\_PM\_WOL\_パターン構造の1つ以上のパラメーターが無効です。

<a href="" id="ndis-status-buffer-too-short"></a>NDIS\_ステータス\_バッファー\_短すぎる\_  
情報バッファーが短すぎます。 NDIS はデータを設定**します。\_情報を設定します。** 必要な最小バッファーサイズに対して、NDIS\_OID\_要求構造体のメンバーが必要です。

<a href="" id="ndis-status-not-supported"></a>NDIS\_の状態\_\_サポートされていません  
ネットワークアダプターは、要求された WOL パターンをサポートしていません。

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
<td><p>NDIS 6.20 以降でサポートされています。 ミニポートドライバーの場合は必須です。</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Ntddndis (Ndis .h を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**NDIS\_OID\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)

[**NDIS\_PM\_WOL\_パターン**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_pm_wol_pattern)

[**NDIS\_状態\_表示**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_status_indication)

[**NDIS\_状態\_PM\_WOL\_パターン\_拒否されました**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-pm-wol-pattern-rejected)

[OID\_PM\_\_WOL\_パターンの削除](oid-pm-remove-wol-pattern.md)

[OID\_PNP\_追加\_ウェイクアップ\_上\_パターン](oid-pnp-add-wake-up-pattern.md)

 

 




