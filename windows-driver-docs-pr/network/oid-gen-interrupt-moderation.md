---
title: OID_GEN_INTERRUPT_MODERATION
description: クエリとして、NDIS およびそれ以降のドライバーは、OID_GEN_INTERRUPT_MODERATION OID を使用して、ミニポートアダプターで割り込みモデレーションが有効になっているかどうかを判断します。
ms.assetid: 4d9d2bda-f0b3-42d5-bb49-93a9b256f5ad
ms.date: 08/08/2017
keywords: -Windows Vista 以降の OID_GEN_INTERRUPT_MODERATION ネットワークドライバー
ms.localizationpriority: medium
ms.openlocfilehash: ee23d7219250a5bbc78caaef3fd2415d298d299d
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843629"
---
# <a name="oid_gen_interrupt_moderation"></a>OID\_GEN\_割り込み\_モデレーション


クエリとして、NDIS およびそれ以降のドライバーは OID\_GEN\_割り込み\_モデレーション OID を使用して、ミニポートアダプターで割り込みのモデレートが有効になっているかどうかを判断します。 クエリが成功した場合、NDIS は、現在の割り込みモデレーションの設定を含む[**ndis\_interrupt\_モデレーション\_PARAMETERS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_interrupt_moderation_parameters)構造体を返します。

セットとして、NDIS およびそれ以降のドライバーは OID\_GEN\_割り込み\_モデレーション OID を使用して、ミニポートアダプターの割り込みのモデレーションを有効または無効にします。

**バージョン情報**

<a href="" id="windows-vista-and-later-versions-of-windows"></a>Windows Vista 以降のバージョンの Windows  
サポートされています。

<a href="" id="ndis-6-0-and-later-miniport-drivers"></a>NDIS 6.0 以降のミニポートドライバー  
必ず. を設定してクエリを実行します。

<a name="remarks"></a>注釈
-------

クエリの場合、ミニポートドライバーで割り込みモデレーションがサポートされていない場合、ドライバーは、NDIS\_INTERRUPT\_モデレーションの**InterruptModeration**メンバーで**NdisInterruptModerationNotSupported**を指定する必要があり\_PARAMETERS 構造体。

セットの場合、ドライバーが OID\_GEN\_INTERRUPT\_モデレーションクエリに応答して**NdisInterruptModerationNotSupported**を報告した場合、ドライバーは、に対する応答として無効な\_データ\_、NDIS の\_状態を返します。設定要求。 ミニポートドライバーは、 [**NDIS\_INTERRUPT\_モデレーション\_PARAMETERS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_interrupt_moderation_parameters)構造体を受け取ります。 NDIS\_INTERRUPT\_モデレーション\_PARAMETERS の**InterruptModeration**メンバーが**NdisInterruptModerationEnabled**に設定されている場合、ミニポートドライバーは割り込みモデレーションを有効にする必要があります。 それ以外の場合は、割り込みモデレーションを無効にする必要があります。

<a name="requirements"></a>要件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Header</p></td>
<td>Ntddndis (Ndis .h を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**NDIS\_INTERRUPT\_モデレーション\_パラメーター**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_interrupt_moderation_parameters)

 

 




