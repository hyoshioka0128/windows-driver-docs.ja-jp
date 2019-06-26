---
title: OID_WWAN_MODEM_CONFIG_INFO
description: OID_WWAN_MODEM_CONFIG_INFO では、モデムの構成情報に関する情報を取得します。
ms.assetid: 527B970C-09FC-4E49-A309-44D5C6A39778
ms.date: 08/08/2017
keywords:
- OID_WWAN_MODEM_CONFIG_INFO ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 9771208aa2f23f2fd8920b8c38521668c1c3e4c6
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67376758"
---
# <a name="oidwwanmodemconfiginfo"></a>OID\_WWAN\_モデム\_CONFIG\_情報


OID\_WWAN\_モデム\_CONFIG\_情報は、モデムの構成情報に関する情報を取得します。

MBB ドライバーは、最初に、非同期的には、NDIS を返すクエリ要求を処理する必要があります\_状態\_INDICATION\_後で送信する前に、元の要求に必要な[NDIS\_の状態\_WWAN\_モデム\_CONFIG\_情報](ndis-status-wwan-modem-config-info.md)状態通知を含む、 [ **NDIS\_WWAN\_モデム\_構成\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_modem_config_info)を格納する構造体、 [ **WWAN\_モデム\_CONFIG\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wwan/ns-wwan-_wwan_modem_config_info)モデムの構成に関する情報を提供する構造体。

要求のセットには適用されません。

<a name="remarks"></a>注釈
-------

MBB ドライバーは、初期のクエリ中にモデムからまだ有効な情報を指定できません。 有効でない情報は、0 に設定されます。

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
<td><p>Windows 10 への次のメジャー アップデート</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Ntddndis.h (include Ndis.h)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[NDIS\_状態\_WWAN\_モデム\_CONFIG\_情報](ndis-status-wwan-modem-config-info.md)

[**NDIS\_WWAN\_モデム\_CONFIG\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_modem_config_info)

[**WWAN\_モデム\_CONFIG\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wwan/ns-wwan-_wwan_modem_config_info)



