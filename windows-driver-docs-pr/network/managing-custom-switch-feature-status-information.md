---
title: カスタム スイッチ機能の状態情報の管理
description: カスタム スイッチ機能の状態情報の管理
ms.assetid: A1D561CC-22D8-47B6-9D95-6294B2998F3E
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 665f433a29206b461048183c8a4bc685632c3091
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844121"
---
# <a name="managing-custom-switch-feature-status-information"></a>カスタム スイッチ機能の状態情報の管理


Hyper-v 拡張可能スイッチインターフェイスは、次のオブジェクト識別子 (OID) を使用して、拡張可能なスイッチのカスタムステータス情報を照会します。 この状態情報は、*スイッチ機能の状態*情報として知られています。

<a href="" id="oid-switch-feature-status-query"></a>[OID\_スイッチ\_機能\_状態\_クエリ](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-feature-status-query)  
この OID メソッド要求は、指定されたスイッチプロパティのカスタム機能状態情報を取得するために、拡張可能スイッチのプロトコルエッジによって発行されます。

この OID メソッド要求から正常に戻った後、 [**NDIS\_OID\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)構造の**informationbuffer**メンバーには、バッファーへのポインターが含まれています。 このバッファーには、次のデータが含まれています。

-   取得するカスタム機能の状態情報を指定する、 [ **\_機能\_状態\_パラメーター**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_feature_status_parameters)の構造を示す NDIS\_スイッチ。

    **メモ**  カスタム機能の状態の場合は、 **featurestatustype**メンバーが [] に設定されています。

     

-   拡張可能なスイッチポートに割り当てられているカスタムプロパティに関するステータス情報を格納する、 [ **\_の機能\_\_状態の NDIS\_スイッチ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_feature_status_custom)。

    拡張可能スイッチのプロトコルエッジが[\_機能\_状態\_クエリ要求の OID\_切り替える](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-feature-status-query)と、 **Featurestatuscustombufferlength**メンバーと**featurestatuscustombufferlength**メンバーが、機能の状態情報を返すために使用できる**informationbuffer**メンバー内の場所に設定されます。

拡張可能なスイッチ拡張機能で oid メソッドの要求を受け取ったときに、次のガイドラインに従う必要があります[\_スイッチ\_機能\_状態\_クエリ](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-feature-status-query):

-   拡張機能は、NDIS\_スイッチの**Featurestatusid**メンバーと一致する拡張可能なカスタムスイッチ機能の状態を管理する必要があります。この機能は、 [ **\_状態\_パラメーター構造\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_feature_status_parameters)ます。

-   拡張機能が OID メソッド要求を処理する場合は、NDIS\_スイッチによって指定されたパラメーターに一致する機能の状態情報を返す必要があります[ **\_機能\_status\_parameters**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_feature_status_parameters)構造体です。

    機能の状態バッファーが小さすぎる場合、拡張機能は、NDIS\_の状態\_無効な\_の長さの OID 要求を失敗させる必要があります。 拡張機能はデータを設定する必要があり**ます。\_情報を設定します。** 必要な最小バッファーサイズに対して、 [**NDIS\_OID\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)構造体のメンバーが必要です。

    それ以外の場合、拡張機能は機能の状態情報を返し、NDIS\_STATUS\_SUCCESS による OID 要求を完了する必要があります。

-   拡張機能がカスタム拡張スイッチの機能の状態を管理していない場合は、 [**NdisFOidRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfoidrequest)を呼び出して、拡張可能なスイッチドライバースタックから OID 要求を転送する必要があります。

    OID 要求を転送する方法の詳細については、「 [NDIS フィルタードライバーでの Oid 要求のフィルター処理](filtering-oid-requests-in-an-ndis-filter-driver.md)」を参照してください。

スイッチ機能の状態情報を定義および登録する方法の詳細については、「[カスタムスイッチの機能の状態](custom-switch-feature-status.md)」を参照してください。

 

 





