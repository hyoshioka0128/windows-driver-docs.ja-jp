---
title: NDIS_STATUS_PD_CURRENT_CONFIG
description: この状態表示では、NDIS_PD_CONFIG 構造が変更されたことを示す通知です。
ms.assetid: 0B63E85E-36A8-4DC4-A060-C40DCB6BE454
ms.date: 07/18/2017
keywords:
- NDIS_STATUS_PD_CURRENT_CONFIG ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 4a4151d69824add438e64b1f853479d5cb6da00f
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56535348"
---
# <a name="ndisstatuspdcurrentconfig"></a>NDIS\_状態\_PD\_現在\_構成


この状態の表示は、通知を[ **NDIS\_PD\_CONFIG** ](https://msdn.microsoft.com/library/windows/hardware/dn931835)構造が変更されました。

PacketDirect 対応ミニポート ドライバーは、NDIS を行う必要があります\_状態\_PD\_現在\_後の構成状態の表示、 [OID\_PD\_閉じる\_プロバイダー](https://msdn.microsoft.com/library/windows/hardware/dn931851)または[OID\_PD\_オープン\_プロバイダー](https://msdn.microsoft.com/library/windows/hardware/dn931852)要求。

ミニポート ドライバー呼び出し[ **NdisMIndicateStatusEx** ](https://msdn.microsoft.com/library/windows/hardware/ff563600)ステータスの表示にしてへのポインターを渡す必要があります、 [ **NDIS\_状態\_INDICATION** ](https://msdn.microsoft.com/library/windows/hardware/ff567373)を通じて構造体、 *StatusIndication*パラメーター。 この通知を行うときに、ミニポート ドライバーがの次のメンバーを設定する必要があります、 **NDIS\_状態\_INDICATION**構造体。

-   **SourceHandle**ミニポートで受信したハンドルに設定する必要があります、 *MiniportAdapterHandle*のパラメーター、 [ *MiniportInitializeEx* ](https://msdn.microsoft.com/library/windows/hardware/ff559389)関数。

-   **StatusCode** NDIS に設定する必要があります\_状態\_PD\_現在\_構成します。

-   **StatusBuffer** 、適切な NDIS を格納する ULONG 変数のアドレスを設定する必要があります\_状態\_xxxx コード スキャン操作の結果。

-   **StatusBufferSize**に設定する必要があります**sizeof**(ULONG)。

<a name="requirements"></a>要件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>サポートされている最小のクライアント</p></td>
<td><p>Windows 10</p></td>
</tr>
<tr class="even">
<td><p>サポートされている最小のサーバー</p></td>
<td><p>Windows Server 2016</p></td>
</tr>
<tr class="odd">
<td><p>Header</p></td>
<td>Ndis.h (Ndis.h を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**NDIS\_状態\_を示す値**](https://msdn.microsoft.com/library/windows/hardware/ff567373)

[**NdisMIndicateStatusEx**](https://msdn.microsoft.com/library/windows/hardware/ff563600)

[OID\_PD\_閉じる\_プロバイダー](https://msdn.microsoft.com/library/windows/hardware/dn931851)

[OID\_PD\_オープン\_プロバイダー](https://msdn.microsoft.com/library/windows/hardware/dn931852)

 

 




