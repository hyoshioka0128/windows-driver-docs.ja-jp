---
title: Hyper-V 拡張可能スイッチ構成のクエリ
description: Hyper-V 拡張可能スイッチ構成のクエリ
ms.assetid: AF646860-01AB-4F4B-84F8-B570054B10FC
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1f52dd8578dd8f3f2a3d09317c3584b2d218c721
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67379212"
---
# <a name="querying-the-hyper-v-extensible-switch-configuration"></a>Hyper-V 拡張可能スイッチ構成のクエリ


HYPER-V 拡張可能スイッチのインターフェイスには、拡張可能スイッチ、ポート、およびそのネットワーク アダプターの接続の現在の構成を照会する拡張可能スイッチ拡張機能によって発行されるオブジェクト識別子 (OID) 要求が含まれています。 これらの要求には、次の Oid が含まれます。

<a href="" id="oid-switch-nic-array"></a>[OID\_スイッチ\_NIC\_配列](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-nic-array)  
この OID クエリ要求では、配列を返します。 配列内の各要素には、拡張可能スイッチ ポートに関連付けられているネットワーク アダプターの構成パラメーターを指定します。

<a href="" id="oid-switch-parameters"></a>[OID\_スイッチ\_パラメーター](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-parameters)  
この OID クエリ要求は、拡張可能スイッチの現在の構成を返します。

<a href="" id="oid-switch-port-array"></a>[OID\_スイッチ\_ポート\_配列](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-port-array)  
この OID クエリ要求では、配列を返します。 配列内の各要素には、拡張可能スイッチ ポートの構成パラメーターを指定します。

<a href="" id="oid-switch-port-property-enum"></a>[OID\_スイッチ\_ポート\_プロパティ\_列挙型](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-port-property-enum)  
この OID メソッド要求は、配列を返します。 配列内の各要素には、指定した拡張可能スイッチ ポートのポリシーのプロパティを指定します。

<a href="" id="oid-switch-property-enum"></a>[OID\_スイッチ\_プロパティ\_列挙型](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-property-enum)  
この OID メソッド要求は、配列を返します。 配列内の各要素には、拡張可能スイッチのポリシーのプロパティを指定します。

**注**  最初に発行する必要がありますが、スイッチ拡張機能は、の hyper-v 拡張可能スイッチのバインド、ときに、 [OID\_切り替える\_パラメーター](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-parameters)スイッチの基本的な情報を取得する OID。 場合、 **IsActive**のメンバー、 [ **NDIS\_スイッチ\_パラメーター** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_switch_parameters)構造が FALSE で、拡張機能は、その他のクエリの Oid を発行する必要がありますまで、スイッチには、アクティブ化が完了しました。 ここで、 **NetEventSwitchActivate** [ **NET\_PNP\_イベント**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_net_pnp_event)通知スイッチのアクティブ化イベントを指定します。 場合、 **IsActive**メンバーは、TRUE をバインドで、拡張機能は安全に他のクエリの Oid を発行します。 Hyper-v 拡張可能なスイッチが完了していないアクティブ化中に、構成のクエリを実行すると、スイッチの構成の不完全な初期ビューを持つ拡張機能が発生します。

 

**注**  拡張機能は、独自の OID 要求を生成するときでは、この同じと同様の NDIS フィルター ドライバー。 これを行う方法の詳細については、次を参照してください。 [NDIS フィルター ドライバーから OID の要求を生成する](generating-oid-requests-from-an-ndis-filter-driver.md)します。

 

拡張可能スイッチ OID 要求の管理パスの詳細については、次を参照してください。 [Hyper-v 拡張可能スイッチ コントロール パスの OID 要求](hyper-v-extensible-switch-control-path-for-oid-requests.md)します。

 

 





