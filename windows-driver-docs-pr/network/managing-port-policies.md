---
title: ポート ポリシーの管理
description: ポート ポリシーの管理
ms.assetid: 46394916-6558-4BDA-8920-E3C5378823BE
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 70c44e036cb0d0a7f4eea4a3039e6a8dc9272221
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844115"
---
# <a name="managing-port-policies"></a>ポート ポリシーの管理


Hyper-v 拡張可能スイッチのフィルターおよび転送拡張機能は、標準およびカスタムのポートプロパティのプロパティを使用してプロビジョニングできます。 プロビジョニングが完了すると、拡張可能スイッチの受信データパスで取得されたパケットをフィルター処理するときに、これらの拡張機能によってポリシーが適用されます。 これらのポリシーの詳細については、「[ポートポリシー](port-policies.md)」を参照してください。

Hyper-v 拡張可能スイッチインターフェイスは、次のオブジェクト識別子 (Oid) を使用して、フィルターおよび転送拡張機能を標準およびカスタムポートポリシーのプロパティと共にプロビジョニングします。

<a href="" id="oid-switch-port-property-add"></a>[OID\_スイッチ\_ポート\_プロパティ\_追加](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-port-property-add)  
この OID セット要求は、拡張可能なスイッチのプロトコルエッジによって発行され、WMI 管理レイヤーでプロパティの追加の基礎となる拡張機能に通知します。 [**Ndis\_OID\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)構造の**informationbuffer**には、 [**ndis\_SWITCH\_PORT\_プロパティ\_パラメーター**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_port_property_parameters)構造へのポインターが含まれています。

**注**  カスタムポートのプロパティは、 [**NDIS\_スイッチ\_ポート\_プロパティ\_TYPE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ne-ntddndis-_ndis_switch_port_property_type)列挙値**NdisSwitchPortPropertyTypeCustom**によって指定されます。 標準ポートのプロパティは、 **NDIS\_スイッチ\_ポート\_プロパティ\_TYPE**列挙値**NdisSwitchPortPropertyTypeSecurity**、 **NdisSwitchPortPropertyTypeVlan**、および**NdisSwitchPortPropertyTypeProfile**によって指定されます。

 

<a href="" id="oid-switch-port-property-update"></a>[OID\_スイッチ\_ポート\_プロパティ\_更新](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-port-property-update)  
この OID セット要求は、拡張可能なスイッチのプロトコルエッジによって発行され、WMI 管理層でプロパティの更新の基になる拡張を通知します。 [**Ndis\_OID\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)構造の**informationbuffer**には、 [**ndis\_SWITCH\_PORT\_プロパティ\_パラメーター**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_port_property_parameters)構造へのポインターが含まれています。

<a href="" id="oid-switch-port-property-delete"></a>[OID\_スイッチ\_ポート\_プロパティ\_削除](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-port-property-delete)  
この OID セット要求は、拡張可能なスイッチのプロトコルエッジによって発行され、WMI 管理層でプロパティの削除の基になる拡張を通知します。 [**Ndis\_OID\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)構造の**informationbuffer**には、 [**ndis\_SWITCH\_PORT\_プロパティ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_port_property_delete_parameters)へのポインターが含まれて\_パラメーター構造が削除されます。\_

<a href="" id="oid-switch-port-property-enum"></a>[OID\_スイッチ\_ポート\_プロパティ\_列挙型](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-port-property-enum)  
この OID メソッド要求は拡張機能によって送信され、拡張可能スイッチの指定されたポートに対して現在構成されているプロパティについて、拡張可能スイッチの基になるミニポートエッジに対してクエリを実行します。 [**NDIS\_OID\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)構造の**informationbuffer**には、バッファーへのポインターが含まれています。 このバッファーには、次のデータが含まれています。

-   指定されたポートのポリシー列挙のパラメーターを指定する[ **\_ポート\_プロパティ\_\_、NDIS\_スイッチ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_port_property_enum_parameters)。

-   [**NDIS\_スイッチの配列\_ポート\_プロパティ\_列挙型\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_port_property_enum_info)構造体です。 これらの各構造体には、拡張可能なスイッチポートポリシーのプロパティに関する情報が含まれています。

    **注**  Ndis の**numproperties**メンバー [ **\_switch\_PORT\_プロパティ\_enum\_PARAMETERS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_port_property_enum_parameters)構造体が0に設定されている場合は、 [**ndis\_switch\_PORT\_プロパティ\_enum\_INFO**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_port_property_enum_info)構造体が返されません。

     

拡張機能では、Oid の OID セット要求を[\_ポート\_プロパティ\_ADD\_](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-port-property-add)生成することはできない  に**注意**してください。 [Oid\_\_ポート\_プロパティ\_更新](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-port-property-update)、または[oid\_スイッチ\_ポート\_プロパティ\_削除](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-port-property-delete)を切り替えることができます。

 

拡張可能なスイッチ拡張機能は、oid の OID セット要求を処理するときに、次のガイドラインに従う必要があります。 [\_スイッチ\_ポート\_プロパティ\_追加](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-port-property-add)、 [oid\_スイッチ\_ポート\_プロパティ\_更新](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-port-property-update)、または[oid\_スイッチ\_ポート\_プロパティ\_削除](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-port-property-delete)します。

-   この拡張機能では、OID 要求に関連付けられている\_パラメーター構造を削除\_には、 [**ndis\_スイッチ\_ポート\_プロパティ\_パラメーター**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_port_property_parameters)または[**ndis\_スイッチ\_プロパティ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_port_property_delete_parameters)を変更することはできません。\_

-   拡張機能がプロパティを管理する場合、拡張機能はこれらの OID 要求を処理する必要があります。 OID 要求によっては、拡張機能は、NDIS\_スイッチの次のメンバーを検査する必要があります[ **\_ポート\_プロパティ\_パラメーター**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_port_property_parameters)または[**ndis\_スイッチ\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_port_property_delete_parameters)ポートのプロパティを削除\_パラメーター構造を削除して、ポートのプロパティを管理するかどうかを判断します。\_\_

    -   **PropertyType**メンバーです。 このメンバーは、ポートプロパティの種類を指定します。 カスタムポートプロパティには、 **NdisSwitchPortPropertyTypeCustom**の**PropertyType**メンバー値があります。 標準ポートのプロパティには、その他のプロパティ型の値があります。 たとえば、標準 VLAN ポートポリシーのプロパティの type 値は**NdisSwitchPortPropertyTypeVlan**です。

    -   **PropertyId**メンバーです。 このメンバーは、カスタムポートプロパティの専用の GUID 値を指定します。 この GUID 値は、独立系ソフトウェアベンダー (ISV) によって作成され、カスタム拡張可能スイッチプロパティの形式も定義します。

        拡張機能では、標準ポートポリシーのこのメンバーを無視する必要がある  に**注意**してください。

         

-   拡張機能が以前にプロビジョニングされているポートプロパティで、NDIS\_スイッチの次のメンバー ([**プロパティ\_パラメーター**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_property_parameters)構造) に一致するポートプロパティを使用して、拡張機能が以前にプロビジョニングされている場合は、 [OID\_スイッチ\_ポート\_プロパティ\_](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-port-property-update)処理する必要があります。\_

    -   **PropertyType**メンバーです。

    -   **PropertyId**メンバーです。

        拡張機能では、標準ポートポリシーのこのメンバーを無視する必要がある  に**注意**してください。

         

    -   **Propertyversion**メンバー。 このメンバーは、拡張機能がプロビジョニングされたポートプロパティのバージョンを指定します。

    -   **Propertyinstanceid**メンバー。 このメンバーは、拡張機能がプロビジョニングされたポートプロパティのインスタンスを指定します。

-   フィルター処理または転送拡張機能は、管理するポートポリシーの追加または更新を拒否することができます。 この拡張機能では、状態が\_の OID 要求を完了することによってこれを実行します。データ\_\_は受け入れられません。

    拡張機能をキャプチャする  、ポートポリシーの追加または更新を拒否**することは**できません。 代わりに、OID 要求を拡張可能なスイッチ制御パスに転送する必要があります。

     

-   転送拡張機能は、サポートしていない標準ポートプロパティに対する OID 要求を失敗させたり、プロパティが独自のポリシー構成と競合したりする可能性があります。 この場合、拡張機能は OID 要求を完了し、エラーを報告するための適切な NDIS 状態コードを返す必要があります。

-   拡張機能が標準ポートポリシーの OID セット要求を正常に処理した場合、OID 要求を完了しないようにし、拡張可能なスイッチ制御パスに転送する必要があります。

-   キャプチャまたはフィルター拡張によってカスタムポートポリシーの OID セット要求が正常に処理された場合、OID 要求を完了しないようにし、拡張可能なスイッチ制御パスに転送する必要があります。

    転送拡張機能によってカスタムポートポリシーの OID セット要求が正常に処理された場合、OID 要求を完了し、適切な NDIS\_STATUS\_*Xxx*値を返す必要があります。

-   拡張機能が OID セット要求を完了しない場合は、 [**NdisFOidRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfoidrequest)を呼び出して、拡張可能なスイッチドライバースタックから oid 要求を転送する必要があります。 この場合、拡張機能は、基になる拡張機能が OID 要求に失敗したかどうかを検出するために、OID の完了状態を監視する必要があります。

 

 





