---
title: Hyper-V 拡張可能スイッチ構成のクエリ
description: Hyper-V 拡張可能スイッチ構成のクエリ
ms.assetid: AF646860-01AB-4F4B-84F8-B570054B10FC
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 21a8115003c16d79c0c40807eda5f9224062ad5b
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844880"
---
# <a name="querying-the-hyper-v-extensible-switch-configuration"></a>Hyper-V 拡張可能スイッチ構成のクエリ


Hyper-v 拡張可能スイッチインターフェイスには、拡張可能なスイッチ拡張機能によって発行されたオブジェクト識別子 (OID) 要求が含まれており、拡張スイッチ、そのポート、およびネットワークアダプター接続の現在の構成を照会できます。 これらの要求には、次の Oid が含まれます。

<a href="" id="oid-switch-nic-array"></a>[OID\_スイッチ\_NIC\_配列](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-nic-array)  
この OID クエリ要求では、配列が返されます。 配列の各要素は、拡張可能なスイッチポートに関連付けられているネットワークアダプターの構成パラメーターを指定します。

<a href="" id="oid-switch-parameters"></a>[OID\_スイッチ\_パラメーター](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-parameters)  
この OID クエリ要求では、拡張可能スイッチの現在の構成が返されます。

<a href="" id="oid-switch-port-array"></a>[OID\_スイッチ\_ポート\_配列](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-port-array)  
この OID クエリ要求では、配列が返されます。 配列の各要素は、拡張可能なスイッチポートの構成パラメーターを指定します。

<a href="" id="oid-switch-port-property-enum"></a>[OID\_スイッチ\_ポート\_プロパティ\_列挙型](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-port-property-enum)  
この OID メソッド要求は、配列を返します。 配列の各要素は、指定された拡張可能なスイッチポートのポリシーのプロパティを指定します。

<a href="" id="oid-switch-property-enum"></a>[OID\_SWITCH\_プロパティ\_列挙型](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-property-enum)  
この OID メソッド要求は、配列を返します。 配列の各要素は、拡張可能なスイッチポリシーのプロパティを指定します。

**注**  スイッチ拡張機能が Hyper-v 拡張可能スイッチにバインドされている場合、基本的なスイッチ情報を取得するには、まず[oid\_スイッチ\_パラメーター](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-parameters) oid を発行する必要があります。 [**NDIS\_switch\_PARAMETERS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_parameters)構造体の**ISACTIVE**メンバーが FALSE の場合、スイッチがアクティブ化を完了するまで、他のクエリ oid は拡張機能によって発行されません。 この場合、 **NetEventSwitchActivate** [**NET\_PNP\_イベント**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_pnp_event)通知は、スイッチアクティブ化イベントを指定します。 **IsActive**メンバーが BIND で TRUE の場合、拡張機能は他のクエリ oid を安全に発行できます。 Hyper-v 拡張可能スイッチのアクティブ化が完了していないときに構成を照会すると、拡張機能によってスイッチ構成の初期ビューが不完全になります。

 

拡張機能によって独自の OID 要求が生成された場合、この処理は、NDIS フィルタードライバーと同じ方法で行われ**ます  。** この方法の詳細については、「 [NDIS フィルタードライバーからの OID 要求の生成](generating-oid-requests-from-an-ndis-filter-driver.md)」を参照してください。

 

拡張可能なスイッチ OID 要求の制御パスの詳細については、「 [OID 要求の Hyper-v 拡張可能スイッチ制御パス](hyper-v-extensible-switch-control-path-for-oid-requests.md)」を参照してください。

 

 





