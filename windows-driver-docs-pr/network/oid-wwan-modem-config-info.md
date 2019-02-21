---
title: OID_WWAN_MODEM_CONFIG_INFO
description: OID_WWAN_MODEM_CONFIG_INFO では、モデムの構成情報に関する情報を取得します。
ms.assetid: 527B970C-09FC-4E49-A309-44D5C6A39778
ms.date: 08/08/2017
keywords:
- OID_WWAN_MODEM_CONFIG_INFO ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 1ee6dbf13c9a69f5a19b50463464ae22e26024df
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56552425"
---
# <a name="oidwwanmodemconfiginfo"></a>OID\_WWAN\_モデム\_CONFIG\_情報


OID\_WWAN\_モデム\_CONFIG\_情報は、モデムの構成情報に関する情報を取得します。

MBB ドライバーは、最初に、非同期的には、NDIS を返すクエリ要求を処理する必要があります\_状態\_INDICATION\_後で送信する前に、元の要求に必要な[NDIS\_の状態\_WWAN\_モデム\_CONFIG\_情報](ndis-status-wwan-modem-config-info.md)状態通知を含む、 [ **NDIS\_WWAN\_モデム\_構成\_情報**](https://msdn.microsoft.com/library/windows/hardware/07C2BAED-157A-459C-B558-115C0091ECE5)を格納する構造体、 [ **WWAN\_モデム\_CONFIG\_情報**](https://msdn.microsoft.com/library/windows/hardware/14FBFA51-F4A5-417A-8905-241CEA543774)モデムの構成に関する情報を提供する構造体。

要求のセットには適用されません。

<a name="remarks"></a>注釈
-------

MBB ドライバーは、初期のクエリ中にモデムからまだ有効な情報を指定できません。 有効でない情報は、0 に設定されます。

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

[**NDIS\_WWAN\_モデム\_CONFIG\_情報**](https://msdn.microsoft.com/library/windows/hardware/07C2BAED-157A-459C-B558-115C0091ECE5)

[**WWAN\_モデム\_CONFIG\_情報**](https://msdn.microsoft.com/library/windows/hardware/14FBFA51-F4A5-417A-8905-241CEA543774)



