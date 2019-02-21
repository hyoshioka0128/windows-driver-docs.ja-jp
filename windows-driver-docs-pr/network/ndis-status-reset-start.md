---
title: NDIS_STATUS_RESET_START
description: NDIS_STATUS_RESET_START 状態では、ミニポート アダプターがリセットされていることを示します。
ms.assetid: 8758652b-137b-43e3-a896-8360f2b5051c
ms.date: 07/18/2017
keywords:
- NDIS_STATUS_RESET_START ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 2a026c9c371f27ba3aeaf068b42daa279b0715bd
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56535763"
---
# <a name="ndisstatusresetstart"></a>NDIS\_状態\_リセット\_開始


NDIS\_状態\_リセット\_開始状態では、ミニポート アダプターがリセットされていることを示します。

<a name="remarks"></a>注釈
-------

ミニポート ドライバーは呼び出さないでください、 [ **NdisMIndicateStatusEx** ](https://msdn.microsoft.com/library/windows/hardware/ff563600)関数開始を通知し、リセット操作の開始時に、NDIS が上にあるドライバーを通知するために各リセット操作の完了と終了します。

NDIS ミニポート ドライバーを呼び出すときに、ミニポート ドライバーがミニポート アダプターをリセット[ *MiniportResetEx* ](https://msdn.microsoft.com/library/windows/hardware/ff559432)関数。 NDIS 呼び出し、 [ *ProtocolStatusEx* ](https://msdn.microsoft.com/library/windows/hardware/ff570270)の各関数には、プロトコルと中間ドライバーがバインドされていると、 [ *FilterStatus* ](https://msdn.microsoft.com/library/windows/hardware/ff549973)の関数NDIS の状態の上にあるフィルター モジュールが、\_状態\_リセット\_を開始します。 NDIS ミニポート ドライバーには、リセットが完了すると、通知状態の上にあるドライバー [ **NDIS\_状態\_リセット\_エンド**](ndis-status-reset-end.md)します。

プロトコル ドライバーが、NDIS を受信すると\_状態\_リセット\_は開始状態の表示。

-   まで送信可能な状態である、データを保持、 *ProtocolStatusEx*関数が受け取った、NDIS\_状態\_リセット\_終了ステータスを示す値。

-   などのリソースを返すへの呼び出しでのデータ バッファーを受信した点を除いては、基になるミニポート ドライバーが送信されるすべての NDIS 呼び出しをしないように、 [ **NdisReturnNetBufferLists** ](https://msdn.microsoft.com/library/windows/hardware/ff564534)関数。

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
<td><p>NDIS 6.0 および NDIS 5.1 のドライバーを Windows Vista でサポートされています。 Windows XP で 5.1 の NDIS ドライバーのサポートされています。</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Ndis.h (Ndis.h を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[*FilterStatus*](https://msdn.microsoft.com/library/windows/hardware/ff549973)

[*MiniportResetEx*](https://msdn.microsoft.com/library/windows/hardware/ff559432)

[**NDIS\_状態\_リセット\_終了**](ndis-status-reset-end.md)

[**NdisMIndicateStatusEx**](https://msdn.microsoft.com/library/windows/hardware/ff563600)

[**NdisReturnNetBufferLists**](https://msdn.microsoft.com/library/windows/hardware/ff564534)

[*ProtocolStatusEx*](https://msdn.microsoft.com/library/windows/hardware/ff570270)

 

 




