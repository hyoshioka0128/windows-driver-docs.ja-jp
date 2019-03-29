---
title: OID_GEN_INTERRUPT_MODERATION
description: クエリとして NDIS および上にあるドライバーはミニポート アダプターの割り込み節度が有効になっているかを判断する OID_GEN_INTERRUPT_MODERATION OID を使用します。
ms.assetid: 4d9d2bda-f0b3-42d5-bb49-93a9b256f5ad
ms.date: 08/08/2017
keywords: -OID_GEN_INTERRUPT_MODERATION ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: e80cad2d81817bf4ad523d1900a26dd471f65fca
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56581646"
---
# <a name="oidgeninterruptmoderation"></a>OID\_GEN\_INTERRUPT\_モデレート


クエリ、NDIS と関連付けたドライバーを使用、OID\_GEN\_割り込み\_モデレート OID ミニポート アダプターの割り込み節度が有効になっているかどうかを判断します。 NDIS を返します、クエリが成功したかどうか、 [ **NDIS\_割り込み\_モデレート\_パラメーター** ](https://msdn.microsoft.com/library/windows/hardware/ff565793)現在割り込み節度を含む構造体設定。

セットとして NDIS と関連付けたドライバー OID を使用\_GEN\_割り込み\_モデレート OID を有効またはミニポート アダプターの割り込み節度を無効にします。

**バージョン情報**

<a href="" id="windows-vista-and-later-versions-of-windows"></a>Windows Vista および Windows の以降のバージョン  
サポートされています。

<a href="" id="ndis-6-0-and-later-miniport-drivers"></a>NDIS 6.0 とそれ以降のミニポート ドライバー  
必須。 設定し、クエリを実行します。

<a name="remarks"></a>コメント
-------

クエリの場合、ミニポート ドライバーが割り込み節度をサポートしていない場合、ドライバーする必要があります指定**NdisInterruptModerationNotSupported**で、 **InterruptModeration**の NDIS メンバー\_割り込み\_モデレート\_パラメーター構造体。

ドライバーによって報告された場合、セットに対して**NdisInterruptModerationNotSupported** OID への応答で\_GEN\_INTERRUPT\_モデレート クエリでは、ドライバーは、NDIS を返す必要があります\_ステータス\_無効な\_データ セットの要求に応答します。 ミニポート ドライバーが、受信、 [ **NDIS\_INTERRUPT\_モデレート\_パラメーター** ](https://msdn.microsoft.com/library/windows/hardware/ff565793)構造体。 場合、 **InterruptModeration**の NDIS メンバー\_INTERRUPT\_モデレート\_にパラメーターが設定されている**NdisInterruptModerationEnabled**、ミニポート ドライバー割り込み節度を有効にする必要があります。 それ以外の場合、割り込み節度を無効にしてする必要があります。

<a name="requirements"></a>必要条件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Header</p></td>
<td>Ntddndis.h (include Ndis.h)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**NDIS\_INTERRUPT\_モデレート\_パラメーター**](https://msdn.microsoft.com/library/windows/hardware/ff565793)

 

 




