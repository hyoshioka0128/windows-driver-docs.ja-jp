---
title: NDIS_STATUS_TCP_CONNECTION_OFFLOAD_HARDWARE_CAPABILITIES
description: MUX 中間ドライバー NDIS に通知する、NDIS_STATUS_TCP_CONNECTION_OFFLOAD_HARDWARE_CAPABILITIES 機能の状態を示す値を使用して、接続の変更があった上にあるドライバーは、基になるハードウェアの特性をオフロード.
ms.assetid: 694cc0c4-0987-4095-8490-14ddfc9eaedb
ms.date: 07/18/2017
keywords:
- NDIS_STATUS_TCP_CONNECTION_OFFLOAD_HARDWARE_CAPABILITIES ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 4a97a33ab6ca824dcf7045bc36b9edc902feb34d
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56535352"
---
# <a name="ndisstatustcpconnectionoffloadhardwarecapabilities"></a>NDIS\_状態\_TCP\_接続\_オフロード\_ハードウェア\_機能


MUX 中間ドライバーを使用して、NDIS\_状態\_TCP\_接続\_オフロード\_ハードウェア\_NDIS と関連付けたドライバーに通知する機能の機能の状態の表示基になるハードウェアの接続のオフロード特性の変更がありました。

<a name="remarks"></a>注釈
-------

基になる NIC を追加したり削除したり、MUX 中間ドライバーに関連付けられているハードウェア機能の全体的なセットを変更できます。

**StatusBuffer**のメンバー、 [ **NDIS\_状態\_INDICATION** ](https://msdn.microsoft.com/library/windows/hardware/ff567373)構造に含まれる、 [ **NDIS\_TCP\_接続\_オフロード**](https://msdn.microsoft.com/library/windows/hardware/ff567875)構造体。 NDIS\_TCP\_接続\_オフロードは、タスクのオフロード ハードウェア機能を指定します。

タスクのオフロード ハードウェア機能の詳細については、次を参照してください。 [OID\_TCP\_接続\_オフロード\_ハードウェア\_機能](https://msdn.microsoft.com/library/windows/hardware/ff569803)します。

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
<td><p>NDIS 6.0 以降をサポートします。</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Ndis.h (Ndis.h を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**NDIS\_状態\_を示す値**](https://msdn.microsoft.com/library/windows/hardware/ff567373)

[**NDIS\_TCP\_接続\_オフロード**](https://msdn.microsoft.com/library/windows/hardware/ff567875)

[OID\_TCP\_接続\_オフロード\_ハードウェア\_機能](https://msdn.microsoft.com/library/windows/hardware/ff569803)

 

 




