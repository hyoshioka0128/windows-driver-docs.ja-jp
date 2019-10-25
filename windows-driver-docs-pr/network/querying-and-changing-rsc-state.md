---
title: RSC 状態のクエリと変更
description: このセクションでは、RSC 対応ミニポートドライバーの現在の受信セグメント合体 (RSC) 状態を照会または変更する方法について説明します。
ms.assetid: 5455FBB2-3603-44EF-B1C6-494D31DD820D
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5b35a3494657abfd6a58b492872902539a17f993
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844885"
---
# <a name="querying-and-changing-rsc-state"></a>RSC 状態のクエリと変更


このセクションでは、RSC 対応ミニポートドライバーの現在の受信セグメント合体 (RSC) 状態を照会または変更する方法について説明します。

## <a name="querying-rsc-state"></a>RSC 状態のクエリ


現在の RSC の状態を照会するには、 [oid\_TCP\_オフロード\_現在の\_CONFIG](https://docs.microsoft.com/windows-hardware/drivers/network/oid-tcp-offload-current-config) oid 要求を発行します。 NDIS はこの OID を処理し、ミニポートには渡しません。

## <a name="changing-rsc-state"></a>RSC 状態の変更


RSC を有効または無効にするには、 [oid\_TCP\_オフロード\_PARAMETERS](https://docs.microsoft.com/windows-hardware/drivers/network/oid-tcp-offload-parameters) oid 要求を発行します。 この OID では、 [**NDIS\_OFFLOAD\_PARAMETERS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_offload_parameters)構造体を使用します。 この構造体では、 **RscIPv4**メンバーと**RscIPv6**メンバーは次の値を持つことができます。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">用語</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>NDIS_OFFLOAD_PARAMETERS_NO_CHANGE</strong></p></td>
<td align="left"><p>RSC の状態は変更されていません。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>NDIS_OFFLOAD_PARAMETERS_RSC_DISABLED</strong></p></td>
<td align="left"><p>RSC を無効にするには、このフラグを指定します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>NDIS_OFFLOAD_PARAMETERS_RSC_ENABLED</strong></p></td>
<td align="left"><p>RSC を有効にするには、このフラグを指定します。</p></td>
</tr>
</tbody>
</table>

 

ミニポートドライバーは、 [\_TCP\_オフロード\_パラメーター](https://docs.microsoft.com/windows-hardware/drivers/network/oid-tcp-offload-parameters) oid 要求の oid を処理した後で、 [**NDIS\_ステータス\_タスク\_オフロード\_現在の\_構成**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-task-offload-current-config)状態を示します。更新されたオフロード状態。

ミニポートドライバーが OID を受け取ると[\_TCP\_オフロード\_現在の\_構成](https://docs.microsoft.com/windows-hardware/drivers/network/oid-tcp-offload-current-config)OID 要求では、 **NDIS\_** \_\_RSC\_DISABLED フラグが指定されています。では、OID 要求を完了する前に、ドライバーはスタック上にある既存の結合されたセグメントを示す必要があります。

 

 





