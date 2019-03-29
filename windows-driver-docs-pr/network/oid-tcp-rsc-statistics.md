---
title: OID_TCP_RSC_STATISTICS
description: クエリとして NDIS と関連付けたドライバーまたはユーザー モード アプリケーション使用 OID_TCP_RSC_STATISTICS OID ミニポート アダプターの受信セグメント coalescing (RSC) 統計情報を取得します。
ms.assetid: CD289868-1925-4222-8A4D-359118124325
ms.date: 08/08/2017
keywords: -OID_TCP_RSC_STATISTICS ネットワークのドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: fe48b97ade31b80a5e424b90d6358f3f1290f628
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56571620"
---
# <a name="oidtcprscstatistics"></a>OID\_TCP\_RSC\_統計情報


クエリとして NDIS と関連付けたドライバーまたはユーザー モード アプリケーション使用 OID\_TCP\_RSC\_統計 OID ミニポート アダプターの受信セグメント coalescing (RSC) 統計情報を取得します。

NDIS 6.30 および RSC サービスを提供する以降のミニポート ドライバーには、この OID をサポートする必要があります。 それ以外の場合、この OID は省略可能です。

<a name="remarks"></a>コメント
-------

**InformationBuffer**のメンバー [ **NDIS\_OID\_要求**](https://msdn.microsoft.com/library/windows/hardware/ff566710)構造に含まれる、 [ **NDIS\_RSC\_統計\_情報**](https://msdn.microsoft.com/library/windows/hardware/hh451657)構造体。

ミニポート ドライバーがのメンバーの統計情報を維持する必要があります、 [ **NDIS\_RSC\_統計\_情報**](https://msdn.microsoft.com/library/windows/hardware/hh451657)次のように構造体します。

-   ドライバーはで結合されたパケットの数を増やす必要があります、 **CoalescedPkts**パケットが 1 つのまとめられた単位 (SCU) に追加されるたびに 1 つのメンバー。
-   ドライバーでまとめられたオクテット数を増やす必要があります、 **CoalescedOctets** SCU にパケットが追加されるたびに、パケットの TCP ペイロードのサイズによってメンバー。
-   ドライバーは、結合されたイベント数を増やす必要があります**CoalesceEvents** SCU が完了するたびに 1 つのメンバー。 このようなすべての SCUs が 0 以外必要**CoalescedSegCount**値。
-   ドライバーで中止回数を増やす必要があります、**中止**メンバーを 1 つが見つかるたびに、例外以外の IP データグラムの長さを超えています。 この数は、パケットがハードウェア リソースにより統合しないケースを含める必要があります。

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
<td><p>NDIS 6.30 と Windows 8 以降のドライバーのサポートされています。</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Ntddndis.h (include Ndis.h)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**NDIS\_OID\_要求**](https://msdn.microsoft.com/library/windows/hardware/ff566710)

[**NDIS\_RSC\_統計\_情報**](https://msdn.microsoft.com/library/windows/hardware/hh451657)

 

 




