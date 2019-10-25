---
title: OID_PM_WOL_PATTERN_LIST
description: クエリとして、これまでのドライバーは OID_PM_WOL_PATTERN_LIST OID を使用して、基になるネットワークアダプターに設定されている wake on LAN パターンを列挙できます。
ms.assetid: 7e5a65d8-39ec-4624-aede-97df945ef5e5
ms.date: 08/08/2017
keywords: -Windows Vista 以降の OID_PM_WOL_PATTERN_LIST ネットワークドライバー
ms.localizationpriority: medium
ms.openlocfilehash: 83d61dbd692327cc649b3af3326cfb20e6687d5e
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844046"
---
# <a name="oid_pm_wol_pattern_list"></a>OID\_PM\_WOL\_パターン\_リスト


クエリとして、これまでのドライバーは OID\_PM\_WOL\_PATTERN\_LIST OID を使用して、基になるネットワークアダプターに設定されている wake on LAN パターンを列挙できます。 クエリから正常に戻った後、 [**ndis\_OID\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)構造の**informationbuffer**メンバーには、 [**NDIS\_PM\_\_WOL**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_pm_wol_pattern)のリストへのポインターが含まれています。現在追加されている WOL パターン。

<a name="remarks"></a>注釈
-------

NDIS はミニポートドライバーのクエリを処理します。 NDIS ドライバーでは、OID\_PM\_WOL\_PATTERN\_LIST OID を使用して、基になるネットワークアダプターに設定されている wake on LAN パターンの一覧を取得できます。

Ndis では、各[**ndis\_PM\_WOL\_パターン**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_pm_wol_pattern)構造について、 OID 情報バッファーの先頭からのオフセット (つまり、 **NextWoLPatternOffset メンバー) を設定します。** リスト内の次の**NDIS\_PM\_WOL\_パターン**構造の先頭に、 [**NDIS\_OID\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)構造を指す) の informationbuffer メンバー。 リスト内の最後の構造体の**NextWoLPatternOffset**メンバーのオフセットが0です。

Ndis\_PM のオフセットの場合、 **NextWoLPatternOffset**以外の[ **\_WOL\_パターン**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_pm_wol_pattern)構造 ( **namebufferoffset**など) では、ndis は各**ndis\_PM の先頭を基準とするオフセットを提供します。\_WOL\_パターン**構造です。

ネットワークアダプターに WOL パターンが設定されていない場合、NDIS はデータを設定し**ます。クエリ\_情報。BytesWritten** OID のメンバーが[ **\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)構造体を0に指定し、要求の **\_成功を示す ndis\_ステータス**を返します。 データ内のデータ **。クエリ\_情報。 InformationBuffer**メンバーは、NDIS によって変更されていません。

NDIS は、要求に対して次のいずれかの状態コードを返します。

<a href="" id="ndis-status-success"></a>NDIS\_状態\_成功  
要求は正常に完了しました。 **Informationbuffer**には、WOL パターン (存在する場合) のリストへのポインターが含まれています。

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

[**NDIS\_PM\_WOL\_パターン**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_pm_wol_pattern)

[OID\_PM\_\_WOL\_パターンの追加](oid-pm-add-wol-pattern.md)

[OID\_PM\_\_WOL\_パターンの削除](oid-pm-remove-wol-pattern.md)

[OID\_PNP\_ウェイクアップ\_\_パターン\_一覧](oid-pnp-wake-up-pattern-list.md)

 

 




