---
title: RSC 状態のクエリと変更
description: このセクションでは、クエリまたは coalescing (RSC) 状態 RSC 対応のミニポート ドライバーの現在の受信セグメントを変更する方法について説明します。
ms.assetid: 5455FBB2-3603-44EF-B1C6-494D31DD820D
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9e2757cf1740bcd118e679d4fffa04394930f319
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56582063"
---
# <a name="querying-and-changing-rsc-state"></a>RSC 状態のクエリと変更


このセクションでは、クエリまたは coalescing (RSC) 状態 RSC 対応のミニポート ドライバーの現在の受信セグメントを変更する方法について説明します。

## <a name="querying-rsc-state"></a>RSC の状態のクエリを実行します。


発行することにより、RSC の現在の状態を問い合わせることができます、 [OID\_TCP\_オフロード\_現在\_CONFIG](https://msdn.microsoft.com/library/windows/hardware/ff569805) OID 要求。 NDIS は、この OID を処理し、ミニポートに渡しません。

## <a name="changing-rsc-state"></a>RSC の状態を変更します。


RSC を有効になっているか、発行することによって無効になっている、 [OID\_TCP\_オフロード\_パラメーター](https://msdn.microsoft.com/library/windows/hardware/ff569807) OID 要求。 この OID を使用して、 [ **NDIS\_オフロード\_パラメーター** ](https://msdn.microsoft.com/library/windows/hardware/ff566706)構造体。 この構造で、 **RscIPv4**と**RscIPv6**メンバーは、次の値を持つことができます。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">項目</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>NDIS_OFFLOAD_PARAMETERS_NO_CHANGE</strong></p></td>
<td align="left"><p>RSC の状態は変更されません。</p></td>
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

 

ミニポート ドライバーのプロセスの後、 [OID\_TCP\_オフロード\_パラメーター](https://msdn.microsoft.com/library/windows/hardware/ff569807) OID 要求を渡す必要があります、 [ **NDIS\_状態\_タスク\_オフロード\_現在\_CONFIG** ](https://msdn.microsoft.com/library/windows/hardware/ff567424)で更新された状態の表示状態の負荷を軽減します。

ミニポート ドライバーが受信すると、 [OID\_TCP\_オフロード\_現在\_CONFIG](https://msdn.microsoft.com/library/windows/hardware/ff569805) OID 要求を**NDIS\_オフロード\_パラメーター\_RSC\_無効**フラグを指定すると、OID 要求を完了する前に、スタック上のセグメントを結合する既存のすべてのドライバーを示す必要があります。

 

 





