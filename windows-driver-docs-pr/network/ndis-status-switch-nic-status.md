---
title: NDIS_STATUS_SWITCH_NIC_STATUS
description: NDIS_STATUS_SWITCH_NIC_STATUS 状態の表示を使用して、HYPER-V 拡張可能スイッチの外部ネットワーク アダプターにバインドされている物理ネットワーク アダプターからの状態表示をカプセル化します。
ms.assetid: 51A3BE6A-35F1-4AF0-91C0-94681640BD64
ms.date: 07/18/2017
keywords:
- NDIS_STATUS_SWITCH_NIC_STATUS ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: cffe960cf89909e93c8cc1f6e8fcd81b1e2fb429
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56570594"
---
# <a name="ndisstatusswitchnicstatus"></a>NDIS\_状態\_スイッチ\_NIC\_状態


**NDIS\_状態\_スイッチ\_NIC\_ステータス**状態を示す値を使用して、外部ネットワークにバインドされている物理ネットワーク アダプターからの状態表示をカプセル化HYPER-V 拡張可能スイッチのアダプターです。 経由でこのカプセル化状態の表示は、拡張可能スイッチ ドライバー スタックに転送されます。

**StatusBuffer**のメンバー、 [ **NDIS\_状態\_INDICATION** ](https://msdn.microsoft.com/library/windows/hardware/ff567373)このを示す値をへのポインターが含まれている構造体[ **NDIS\_スイッチ\_NIC\_状態\_INDICATION** ](https://msdn.microsoft.com/library/windows/hardware/hh598217)構造体。

<a name="remarks"></a>コメント
-------

基になる物理ネットワーク アダプターでは、NDIS 状態を示す値を発行は、外部ネットワーク アダプターによって受信されます。 この場合、拡張可能スイッチのインターフェイスは、次の手順を実行します。

1.  インターフェイス内で、状態を示す値をカプセル化、 [ **NDIS\_スイッチ\_NIC\_状態\_INDICATION** ](https://msdn.microsoft.com/library/windows/hardware/hh598217)構造体。

2.  インターフェイスの問題、 **NDIS\_状態\_切り替える\_NIC\_状態**拡張可能スイッチのドライバー スタックをカプセル化された状態の表示を転送するように状態を示す値。 これにより、拡張可能スイッチの拡張機能をカプセル化された状態の表示を変更します。

    通常、拡張機能は、基になる外部ネットワーク アダプターにバインドされている物理アダプターのチームの現在のオフロード機能の変更をカプセル化された状態を示す値を変更します。

    外部ネットワーク アダプターを物理ネットワーク アダプターのバインドのさまざまな構成に関する詳細については、次を参照してください。[型の物理ネットワーク アダプターの構成](https://msdn.microsoft.com/library/windows/hardware/hh582274)します。

3.  ときに、 **NDIS\_状態\_切り替える\_NIC\_ステータス**状態を示す値がスタックの上にある、拡張可能スイッチ プロトコル ドライバーによって受信されると、インターフェイスの転送、関連プロトコルまたはフィルター ドライバーをカプセル化解除された状態を示す値。

拡張機能は、後続の拡張可能スイッチのドライバー スタックのドライバーをカプセル化されたハードウェア オフロード状態インジケーターも取得できます。 これにより、基になる外部ネットワーク アダプターに関連付けられている物理アダプターのチームの現在のオフロード機能を変更するドライバーもできます。 アダプターのチームが外部ネットワーク アダプターにバインドされると、チームの一般的な機能のみが NDIS または上位のプロトコルとフィルター ドライバーにアドバタイズされます。 拡張機能は、チーム内で一部のアダプターでサポートされている機能を提供するカプセル化された状態のインジケーターを送信して提供機能を拡張できます。

たとえば、拡張機能がカプセル化されたに発行できます[ **NDIS\_状態\_受信\_フィルター\_現在\_機能**](ndis-status-receive-filter-current-capabilities.md)チーム全体で現在有効になっている受信フィルター機能の変更を示す値。

転送したり、発生する方法の詳細についての**NDIS\_状態\_スイッチ\_NIC\_状態**、指示を参照してください[から NDIS 状態インジケーターを管理します。物理ネットワーク アダプター](https://msdn.microsoft.com/library/windows/hardware/hh598199)します。

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
<td><p>NDIS 6.30 以降をサポートします。</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Ndis.h (Ndis.h を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


****
[**NDIS\_状態\_を示す値**](https://msdn.microsoft.com/library/windows/hardware/ff567373)

[**NDIS\_状態\_受信\_フィルター\_現在\_機能**](ndis-status-receive-filter-current-capabilities.md)

 

 




