---
title: WIA\_IPA\_バッファー\_サイズ
description: WIA\_IPA\_バッファー\_サイズ プロパティには、(バイト単位)、データ転送中に使用されるバッファーのサイズが含まれています。 WIA ミニドライバーは、作成し、このプロパティを保持します。
ms.assetid: 2feb26fa-674d-4dc2-b8bb-51942cb48737
keywords:
- WIA_IPA_BUFFER_SIZE イメージング デバイス
topic_type:
- apiref
api_name:
- WIA_IPA_BUFFER_SIZE
api_location:
- Wiadef.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1e7b26b1ecbfaf9266b2b593ae6343371f6470c4
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56574533"
---
# <a name="wiaipabuffersize"></a>WIA\_IPA\_バッファー\_サイズ


WIA\_IPA\_バッファー\_サイズ プロパティには、(バイト単位)、データ転送中に使用されるバッファーのサイズが含まれています。 WIA ミニドライバーは、作成し、このプロパティを保持します。

## <span id="ddk_wia_ipa_buffer_size_si"></span><span id="DDK_WIA_IPA_BUFFER_SIZE_SI"></span>


プロパティの種類:VT\_I4

有効な値 :WIA\_PROP\_NONE

アクセス権:読み取り専用です。

<a name="remarks"></a>コメント
-------

WIA\_IPA\_バッファー\_サイズ プロパティのと同じですが、 [ **WIA\_IPA\_MIN\_バッファー\_サイズ**](wia-ipa-min-buffer-size.md)プロパティ。

アプリケーションは、WIA を読み取ることができます\_IPA\_バッファー\_サイズのデータ転送のドライバーが指定したバッファー サイズを確認します。 WIA サービスも、ミニドライバーのデータ転送中にメモリを割り当てるには、このプロパティを読み取ります。

**注**  値を WIA\_IPA\_バッファー\_サイズ プロパティが含まれていますが、特定の時点で、アプリケーションが要求できるデータ量の最小。 バッファーのサイズは大きくデバイス要求が大きくなります。 このより大きなバッファー サイズと、デバイス、低速で応答するいないと思われる、コンピューター全体のパフォーマンスが低下し、過剰なリソースを消費することができます。 小さすぎてバッファー サイズは、多数の小さい要求を要求することによってデータ転送のパフォーマンスを低下することができます。 一般的なデバイス、要求の数とそれらの要求のサイズには、データ要求のサイズを考慮して適切なバッファー サイズを選択します。

 

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
<td><p>すべての転送が有効な項目の Windows Vista のドライバーの省略可能。 また、Windows Server 2003、Windows XP、および Windows の以前のバージョン用に設計されたアプリケーションは、転送のバッファー サイズを見積もることができますをこのプロパティを実装する場合は、そのため、転送速度が最適でいます。</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Wiadef.h (Wiadef.h を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**WIA\_IPA\_MIN\_バッファー\_サイズ**](wia-ipa-min-buffer-size.md)

 

 






