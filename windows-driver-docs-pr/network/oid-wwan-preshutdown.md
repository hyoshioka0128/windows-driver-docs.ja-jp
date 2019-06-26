---
title: OID_WWAN_PRESHUTDOWN
description: OID_WWAN_PRESHUTDOWN は、モデムを通知するシステムがシャット ダウン フェーズを入力して、モデムは、これは正しくシャット ダウンするため、その操作が完了に送信されます。
ms.assetid: B00A2D70-64E0-4686-92FC-D4095BDD713B
ms.date: 08/08/2017
keywords: -OID_WWAN_PRESHUTDOWN ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: b69613062c61a4fb24c7478fd5169e0ebd1d72b4
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67383209"
---
# <a name="oidwwanpreshutdown"></a>OID\_WWAN\_PRESHUTDOWN


OID\_WWAN\_PRESHUTDOWN はモデムに通知するシステムがシャット ダウン フェーズを入力して、モデムは、これは正しくシャット ダウンするため、その操作が完了に送信されます。 MBB の物理アダプターに対応するポート番号を持つのみ送信されます。 複数の PDP コンテキストをサポートする仮想アダプターには、この OID は受け取りません。

クエリ要求はサポートされていません。

ミニポート ドライバーが非同期的に、最初に返すセット要求を処理する必要があります**NDIS\_状態\_INDICATION\_REQUIRED**元の要求以降に送信する、 [**NDIS\_状態\_WWAN\_PRESHUTDOWN\_状態**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-preshutdown-state) MBB ドライバーには、すべてのモデムが必要な操作が完了したときの状態の通知シャット ダウンする前にします。 セットの要求が、 [ **NDIS\_WWAN\_設定\_PRESHUTDOWN\_状態**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_set_preshutdown_state)構造体。

ミニポート ドライバーに返す必要があります**NDIS\_状態\_いない\_サポートされている**この操作をサポートしていない場合。

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
<td><p>Windows 10、バージョン 1511 以降で利用できます。</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Ntddndis.h (include Ndis.h)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**NDIS\_状態\_WWAN\_PRESHUTDOWN\_状態**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-preshutdown-state)

[**NDIS\_WWAN\_設定\_PRESHUTDOWN\_状態**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_set_preshutdown_state)

 

 




