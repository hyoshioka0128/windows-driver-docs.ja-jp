---
title: OID_WWAN_MODEM_CONFIG_INFO
description: OID_WWAN_MODEM_CONFIG_INFO は、モデムの構成情報に関する情報を取得します。
ms.assetid: 527B970C-09FC-4E49-A309-44D5C6A39778
ms.date: 08/08/2017
keywords:
- OID_WWAN_MODEM_CONFIG_INFO ネットワークドライバー (Windows Vista 以降)
ms.localizationpriority: medium
ms.openlocfilehash: f5551743122d0393efc0d8ce3f9c6e6857e0c074
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843836"
---
# <a name="oid_wwan_modem_config_info"></a>OID\_WWAN\_モデム\_構成\_情報


OID\_WWAN\_モデム\_構成\_情報モデムの構成情報に関する情報を取得します。

MBB ドライバーでは、クエリ要求を非同期的に処理し、最初に NDIS\_STATUS\_を返してから、後で[ndis\_ステータス\_WWAN\_MODEM を送信する前に、元の要求に対して必要な\_を示しています。構成\_情報](ndis-status-wwan-modem-config-info.md)の状態通知。 [**NDIS\_WWAN\_モデム\_CONFIG\_info**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_modem_config_info)構造体を含みます。これには、 [**WWAN\_MODEM\_config\_info**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wwan/ns-wwan-_wwan_modem_config_info)構造体が含まれています。モデムの構成に関する情報を提供します。

Set 要求は適用できません。

<a name="remarks"></a>注釈
-------

最初のクエリの実行中に、MBB ドライバーがモデムからまだ有効な情報を取得していない可能性があります。 無効な情報は0に設定されます。

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
<td><p>Windows 10 の次のメジャー更新</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Ntddndis (Ndis .h を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[NDIS\_ステータス\_WWAN\_モデム\_構成\_情報](ndis-status-wwan-modem-config-info.md)

[**NDIS\_WWAN\_モデム\_構成\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_modem_config_info)

[**WWAN\_モデム\_構成\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wwan/ns-wwan-_wwan_modem_config_info)



