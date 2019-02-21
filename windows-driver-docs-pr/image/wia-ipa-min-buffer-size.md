---
title: WIA\_IPA\_MIN\_バッファー\_サイズ
description: WIA\_IPA\_MIN\_バッファー\_サイズ プロパティは、データ転送で使用される最小バッファー サイズを指定します。
ms.assetid: 0d289645-666c-4b67-8971-cdeff3caef3e
keywords:
- WIA_IPA_MIN_BUFFER_SIZE イメージング デバイス
topic_type:
- apiref
api_name:
- WIA_IPA_MIN_BUFFER_SIZE
api_location:
- Wiadef.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: a038ca873179974a9d2f4958bc3d129fce867c0a
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56549636"
---
# <a name="wiaipaminbuffersize"></a>WIA\_IPA\_MIN\_バッファー\_サイズ


WIA\_IPA\_MIN\_バッファー\_サイズ プロパティは、データ転送で使用される最小バッファー サイズを指定します。

## <span id="ddk_wia_ipa_min_buffer_size_si"></span><span id="DDK_WIA_IPA_MIN_BUFFER_SIZE_SI"></span>


プロパティの種類:VT\_I4

有効な値 :WIA\_PROP\_NONE

アクセス権:読み取り専用かどうか

<a name="remarks"></a>注釈
-------

データ転送のコールバックのメカニズム、WIA は行います\_IPA\_MIN\_バッファー\_サイズ プロパティの値を 64 KB のような小さいことができます。 ただし、転送のファイル、プロパティの場合は、一度に 1 つのページのデータを転送するために必要なバイト数。 WIA ミニドライバーは、作成し、この WIA プロパティを保持します。

WIA\_IPA\_MIN\_バッファー\_サイズのと同じですが、 [ **WIA\_IPA\_バッファー\_サイズ**](wia-ipa-buffer-size.md)プロパティ。

アプリケーションは、WIA を読み取ることができます\_IPA\_MIN\_バッファー\_サイズのデータ転送のドライバーが指定したバッファー サイズを確認します。 WIA サービスも、ミニドライバーのデータ転送中にメモリを割り当てるには、このプロパティを読み取ります。

**注**  値を WIA\_IPA\_MIN\_バッファー\_サイズ プロパティが含まれていますは任意の時点で、アプリケーションが要求できるデータの最小量。 バッファーのサイズは大きくデバイス要求が大きくなります。 このより大きなバッファー サイズと、デバイス、低速で応答を表示、コンピューター全体のパフォーマンスが低下し、過剰なリソースを消費することができます。 小さすぎてバッファー サイズは、多数の小さい要求を要求することによってデータ転送のパフォーマンスを低下することができます。 一般的なデバイス、要求の数とそれらの要求のサイズには、データ要求のサイズを考慮して適切なバッファー サイズを選択します。

 

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
<td><p>すべての転送が有効な項目の Windows Vista のドライバーの省略可能。 また、Windows Server 2003、Windows XP、および以前の Windows バージョン用に記述されたアプリケーションは、転送のバッファー サイズを見積もることができますをこのプロパティが実装されている場合は、そのため、転送速度が最適でいます。</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Wiadef.h (Wiadef.h を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**WIA\_IPA\_バッファー\_サイズ**](wia-ipa-buffer-size.md)

 

 






