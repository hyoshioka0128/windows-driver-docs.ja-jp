---
title: NDIS_STATUS_SWITCH_NIC_STATUS
description: NDIS_STATUS_SWITCH_NIC_STATUS の状態の表示は、Hyper-v 拡張可能スイッチの外部ネットワークアダプターにバインドされている物理ネットワークアダプターからの状態をカプセル化するために使用されます。
ms.assetid: 51A3BE6A-35F1-4AF0-91C0-94681640BD64
ms.date: 07/18/2017
keywords:
- NDIS_STATUS_SWITCH_NIC_STATUS ネットワークドライバー (Windows Vista 以降)
ms.localizationpriority: medium
ms.openlocfilehash: dda703d0ad7d4f9ac5680291bcea09ac29f38130
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843513"
---
# <a name="ndis_status_switch_nic_status"></a>NDIS\_状態\_スイッチ\_NIC\_の状態


**NDIS\_status\_スイッチ\_NIC\_状態**の状態の表示を使用して、hyper-v 拡張可能スイッチの外部ネットワークアダプターにバインドされている物理ネットワークアダプターからの状態をカプセル化します。 このカプセル化により、ステータス表示は拡張可能なスイッチドライバースタックに転送されます。

[**Ndis\_状態の\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_status_indication)表示構造体の**statusbuffer**メンバーには、ndis\_\_スイッチへのポインターが含まれています。これには、 [**NIC\_状態\_示さ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_switch_nic_status_indication)れる構造体が含まれます。

<a name="remarks"></a>注釈
-------

基になる物理ネットワークアダプターが NDIS ステータスを示すと、外部ネットワークアダプターによって受信されます。 これが発生すると、拡張可能なスイッチインターフェイスによって次の手順が実行されます。

1.  インターフェイスは、 [**NDIS\_スイッチ\_NIC\_状態\_示さ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_switch_nic_status_indication)れる構造体の状態を示します。

2.  インターフェイスは、NDIS\_の状態を発行し **\_スイッチ\_NIC\_状態**の状態を示します。これにより、カプセル化された状態が拡張可能なスイッチドライバースタックを示します。 これにより、拡張可能なスイッチ拡張機能によって、カプセル化された状態の表示を変更できます。

    通常、拡張機能は、外部ネットワークアダプターにバインドされている物理アダプターの基になるチームの現在のオフロード機能を変更するために、カプセル化された状態の表示を変更します。

    物理ネットワークアダプターを外部ネットワークアダプターにバインドできるさまざまな構成の詳細については、「[物理ネットワークアダプターの構成の種類](https://docs.microsoft.com/windows-hardware/drivers/network/types-of-physical-network-adapter-configurations)」を参照してください。

3.  NDIS の **\_状態\_切り替え\_NIC\_状態**の状態の表示は、スタック内の拡張可能なスイッチプロトコルドライバーによって受信されます。インターフェイスはカプセル化解除ステータスをプロトコルまたはフィルタードライバー。

拡張機能は、拡張可能なスイッチドライバースタックで、カプセル化されたハードウェアオフロードステータスの兆候を、それに関連するドライバーに送信することもできます。 これにより、ドライバーは、外部ネットワークアダプターに接続されている物理アダプターの基になるチームの現在のオフロード機能を変更することもできます。 アダプターのチームが外部ネットワークアダプターにバインドされている場合は、チームの共通機能だけが NDIS またはそれ以降のプロトコルとフィルタードライバーに提供されます。 拡張機能を使用すると、チーム内の一部のアダプターでサポートされている機能をアドバタイズすることで、アドバタイズされた機能を拡張できます。

たとえば、拡張機能は、カプセル化された NDIS\_の状態を発行して[ **\_フィルター\_現在の\_機能**](ndis-status-receive-filter-current-capabilities.md)についての情報を受け取り\_チーム全体の現在有効な受信フィルター機能を変更します。

Ndis\_の状態を転送または開始する方法の詳細については **\_\_\_** 「[物理ネットワークアダプターからの ndis ステータス](https://docs.microsoft.com/windows-hardware/drivers/network/managing-ndis-status-indications-from-physical-network-adapters)の表示の管理」を参照してください。

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
<td><p>NDIS 6.30 以降でサポートされています。</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Ndis .h (Ndis .h を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


****
[**NDIS\_状態\_表示**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_status_indication)

[**NDIS\_STATUS\_現在の\_の機能\_フィルターを受け取る\_** ](ndis-status-receive-filter-current-capabilities.md)

 

 




