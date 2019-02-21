---
title: OID_WWAN_PRESHUTDOWN
description: OID_WWAN_PRESHUTDOWN は、モデムを通知するシステムがシャット ダウン フェーズを入力して、モデムは、これは正しくシャット ダウンするため、その操作が完了に送信されます。
ms.assetid: B00A2D70-64E0-4686-92FC-D4095BDD713B
ms.date: 08/08/2017
keywords: -OID_WWAN_PRESHUTDOWN ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 17f955d1179697ebdc8d8940b1abd0df293a703b
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56530399"
---
# <a name="oidwwanpreshutdown"></a>OID\_WWAN\_PRESHUTDOWN


OID\_WWAN\_PRESHUTDOWN はモデムに通知するシステムがシャット ダウン フェーズを入力して、モデムは、これは正しくシャット ダウンするため、その操作が完了に送信されます。 MBB の物理アダプターに対応するポート番号を持つのみ送信されます。 複数の PDP コンテキストをサポートする仮想アダプターには、この OID は受け取りません。

クエリ要求はサポートされていません。

ミニポート ドライバーが非同期的に、最初に返すセット要求を処理する必要があります**NDIS\_状態\_INDICATION\_REQUIRED**元の要求以降に送信する、 [**NDIS\_状態\_WWAN\_PRESHUTDOWN\_状態**](https://msdn.microsoft.com/library/windows/hardware/mt593233) MBB ドライバーには、すべてのモデムが必要な操作が完了したときの状態の通知シャット ダウンする前にします。 セットの要求が、 [ **NDIS\_WWAN\_設定\_PRESHUTDOWN\_状態**](https://msdn.microsoft.com/library/windows/hardware/mt593235)構造体。

ミニポート ドライバーに返す必要があります**NDIS\_状態\_いない\_サポートされている**この操作をサポートしていない場合。

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
<td><p>Windows 10、バージョン 1511 以降で利用できます。</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Ntddndis.h (include Ndis.h)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**NDIS\_状態\_WWAN\_PRESHUTDOWN\_状態**](https://msdn.microsoft.com/library/windows/hardware/mt593233)

[**NDIS\_WWAN\_設定\_PRESHUTDOWN\_状態**](https://msdn.microsoft.com/library/windows/hardware/mt593235)

 

 




