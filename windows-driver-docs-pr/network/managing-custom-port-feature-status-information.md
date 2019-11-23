---
title: カスタム ポート機能の状態情報の管理
description: カスタム ポート機能の状態情報の管理
ms.assetid: C989888B-1636-488A-80BF-13D136312417
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4e6f116340e593dd33816e71109f3ccfd6c3ac43
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844126"
---
# <a name="managing-custom-port-feature-status-information"></a>カスタム ポート機能の状態情報の管理


Hyper-v 拡張可能スイッチインターフェイスは、次のオブジェクト識別子 (OID) を使用して、拡張可能なスイッチポートのカスタムステータス情報を照会します。 この状態情報は、*ポート機能の状態*情報として知られています。

<a href="" id="oid-switch-port-feature-status-query"></a>[OID\_スイッチ\_ポート\_機能\_状態\_クエリ](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-port-feature-status-query)  
この OID メソッド要求は、指定されたポートプロパティのカスタム機能状態情報を取得するために、拡張可能スイッチのプロトコルエッジによって発行されます。

この OID メソッド要求から正常に戻った後、 [**NDIS\_OID\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)構造の**informationbuffer**メンバーには、バッファーへのポインターが含まれています。 このバッファーには、次のデータが含まれています。

-   [**NDIS\_スイッチ\_ポート\_機能\_ステータス\_パラメーター**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_port_feature_status_parameters)構造で、返されるカスタム機能の状態情報を指定します。

    **メモ**  カスタム機能の状態の場合は、 **featurestatustype**メンバーが [] に設定されています。

     

-   [**NDIS\_スイッチ\_ポート\_機能\_状態\_カスタム**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_port_feature_status_custom)構造には、拡張可能なスイッチポートに割り当てられているカスタムプロパティに関するステータス情報が含まれています。

    拡張可能スイッチのプロトコルエッジが[OID\_スイッチ\_ポート\_機能\_状態\_クエリ](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-port-feature-status-query)要求を発行すると、 **Featurestatuscustombufferlength**メンバーと**featurestatuscustombufferlength**メンバーが、機能の状態情報を返すために拡張で使用できる**informationbuffer**メンバー内の場所に設定されます。

拡張可能なスイッチ拡張機能は、oid の OID メソッド要求を受信するときに、次のガイドラインに従う必要があります。 [\_スイッチ\_ポート\_機能\_状態\_クエリ](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-port-feature-status-query):

-   拡張機能は、NDIS\_スイッチの**Featurestatusid**メンバーと一致するカスタム拡張可能スイッチポートプロパティを管理する必要があります。このプロパティは、 [ **\_ポート\_機能\_状態\_PARAMETERS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_port_feature_status_parameters)構造体です。

-   拡張機能が OID メソッド要求を処理する場合は、NDIS\_スイッチで指定されたパラメーターに一致する機能の状態情報を返す必要があります[ **\_ポート\_機能\_状態\_パラメーター**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_port_feature_status_parameters)構造です。

    機能の状態バッファーが小さすぎる場合、拡張機能は、NDIS\_の状態\_無効な\_の長さの OID 要求を失敗させる必要があります。 拡張機能はデータを設定する必要があり**ます。\_情報を設定します。** 必要な最小バッファーサイズに対して、 [**NDIS\_OID\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)構造体のメンバーが必要です。

    それ以外の場合、拡張機能は機能の状態情報を返し、NDIS\_STATUS\_SUCCESS による OID 要求を完了する必要があります。

-   拡張機能がカスタム拡張可能スイッチのプロパティを管理していない場合は、 [**NdisFOidRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfoidrequest)を呼び出して、拡張可能なスイッチドライバースタックで OID 要求を転送する必要があります。

    OID 要求を転送する方法の詳細については、「 [NDIS フィルタードライバーでの Oid 要求のフィルター処理](filtering-oid-requests-in-an-ndis-filter-driver.md)」を参照してください。

ポート機能の状態情報を定義および登録する方法の詳細については、「[カスタムポート機能の状態](custom-port-feature-status.md)」を参照してください。

 

 





