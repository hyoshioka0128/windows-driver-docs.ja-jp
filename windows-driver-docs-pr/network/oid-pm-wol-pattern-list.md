---
title: OID_PM_WOL_PATTERN_LIST
description: クエリとしてドライバーを重なって使用 OID_PM_WOL_PATTERN_LIST OID を列挙できます wake on LAN のパターンを基になるネットワーク アダプターに設定されています。
ms.assetid: 7e5a65d8-39ec-4624-aede-97df945ef5e5
ms.date: 08/08/2017
keywords: -OID_PM_WOL_PATTERN_LIST ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 7e3d635835d2a18d79b702371a91bdcbd3cf2c43
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63359160"
---
# <a name="oidpmwolpatternlist"></a>OID\_PM\_WOL\_パターン\_一覧


クエリとしてドライバーを重なってできます OID を使用\_PM\_WOL\_パターン\_wake on LAN のパターンを基になるネットワーク アダプターに設定されているを列挙するリストの OID。 で、クエリから正常に戻った後、 **InformationBuffer**のメンバー、 [ **NDIS\_OID\_要求**](https://msdn.microsoft.com/library/windows/hardware/ff566710)構造に含まれる、一覧へのポインター [ **NDIS\_PM\_WOL\_パターン**](https://msdn.microsoft.com/library/windows/hardware/ff566768)現在追加 WOL パターンを記述する構造体。

<a name="remarks"></a>注釈
-------

NDIS は、ミニポート ドライバーにクエリを処理します。 NDIS ドライバーは、OID を使用できる\_PM\_WOL\_パターン\_基になるネットワーク アダプターに設定されているパターンに LAN でウェイク アップの一覧を取得する OID をリストします。

各[ **NDIS\_PM\_WOL\_パターン**](https://msdn.microsoft.com/library/windows/hardware/ff566768) NDIS セットの一覧で構造体、 **NextWoLPatternOffset**メンバーをOID 情報バッファーの先頭からのオフセット (つまり、バッファーの先頭を**InformationBuffer**のメンバー、 [ **NDIS\_OID\_要求**](https://msdn.microsoft.com/library/windows/hardware/ff566710)へのポインターを構造体) を次の先頭に**NDIS\_PM\_WOL\_パターン**リスト内の構造。 内のオフセット、 **NextWoLPatternOffset**一覧の最後の構造体のメンバーは 0 になります。

内のオフセットを[ **NDIS\_PM\_WOL\_パターン**](https://msdn.microsoft.com/library/windows/hardware/ff566768)以外の構造体**NextWoLPatternOffset** (たとえば、 **NameBufferOffset**)、NDIS は、それぞれの先頭に相対的なオフセット**NDIS\_PM\_WOL\_パターン**構造体。

ネットワーク アダプターに設定されている WOL パターンがない場合は、NDIS の設定、**データ。クエリ\_情報。BytesWritten**のメンバー、 [ **NDIS\_OID\_要求**](https://msdn.microsoft.com/library/windows/hardware/ff566710)構造体をゼロを返す**NDIS\_の状態\_成功**要求。 内のデータ、**データ。クエリ\_INFORMATION.InformationBuffer** NDIS によってメンバーが変更されていません。

NDIS は、要求の次のステータス コードのいずれかを返します。

<a href="" id="ndis-status-success"></a>NDIS\_状態\_成功  
要求は正常に完了しました。 **InformationBuffer**存在する場合、WOL パターンの一覧へのポインターが含まれています。

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


[**NDIS\_OID\_要求**](https://msdn.microsoft.com/library/windows/hardware/ff566710)

[**NDIS\_PM\_WOL\_パターン**](https://msdn.microsoft.com/library/windows/hardware/ff566768)

[OID\_PM\_追加\_WOL\_パターン](oid-pm-add-wol-pattern.md)

[OID\_PM\_削除\_WOL\_パターン](oid-pm-remove-wol-pattern.md)

[OID\_PNP\_WAKE\_を\_パターン\_一覧](oid-pnp-wake-up-pattern-list.md)

 

 




