---
title: スイッチ ポリシーの管理
description: スイッチ ポリシーの管理
ms.assetid: F2261CA6-2D7A-4499-82F9-7E2D7C9C908D
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ed25735cc1e83bbef24b1fcc8fd179de9a5d1ce4
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844112"
---
# <a name="managing-switch-policies"></a>スイッチ ポリシーの管理


Hyper-v 拡張可能スイッチのフィルターおよび転送拡張機能は、カスタムスイッチプロパティのプロパティを使用してプロビジョニングできます。 プロビジョニングが完了すると、拡張可能スイッチの受信データパスで取得されたパケットをフィルター処理するときに、これらの拡張機能によってポリシーが適用されます。 これらのポリシーの詳細については、「[ポリシーの切り替え](switch-policies.md)」を参照してください。

Hyper-v 拡張可能スイッチインターフェイスは、次のオブジェクト識別子 (Oid) を使用して、フィルターおよび転送拡張機能をカスタムスイッチポリシーのプロパティと共にプロビジョニングします。

<a href="" id="oid-switch-property-add"></a>[OID\_スイッチ\_プロパティ\_追加](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-property-add)  
この OID セット要求は、拡張可能なスイッチのプロトコルエッジによって発行され、WMI 管理レイヤーでプロパティの追加の基礎となる拡張機能に通知します。 [**Ndis\_OID\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)構造の**informationbuffer**には、ndis\_スイッチへのポインターが含まれています[ **\_プロパティ\_パラメーター**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_property_parameters)構造体。

カスタムスイッチのプロパティは、 **NdisSwitchPropertyTypeCustom**の型の列挙値[ **\_TYPE\_switch\_プロパティ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ne-ntddndis-_ndis_switch_property_type)によって指定さ**れ  ます**。

 

<a href="" id="oid-switch-property-update"></a>[OID\_スイッチ\_プロパティ\_更新](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-property-update)  
この OID セット要求は、拡張可能なスイッチのプロトコルエッジによって発行され、WMI 管理層でプロパティの更新の基になる拡張機能に通知します。 [**Ndis\_OID\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)構造の**informationbuffer**には、ndis\_スイッチへのポインターが含まれています[ **\_プロパティ\_パラメーター**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_property_parameters)構造体。

<a href="" id="oid-switch-property-delete"></a>[OID\_スイッチ\_プロパティ\_削除](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-property-delete)  
この OID セット要求は、拡張可能なスイッチのプロトコルエッジによって発行され、WMI 管理層でプロパティの削除の基になる拡張機能に通知します。 [**Ndis\_OID\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)構造の**informationbuffer**には、 [**ndis\_SWITCH\_プロパティ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_property_delete_parameters)へのポインターが含まれています\_パラメーター構造を削除\_ます。

<a href="" id="oid-switch-property-enum"></a>[OID\_SWITCH\_プロパティ\_列挙型](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-property-enum)  
この OID メソッド要求は拡張機能によって送信され、拡張可能スイッチで現在構成されているスイッチプロパティについて、拡張可能スイッチの基になるミニポートエッジに対してクエリを実行します。 [**NDIS\_OID\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)構造の**informationbuffer**には、バッファーへのポインターが含まれています。 このバッファーには、次のデータが含まれています。

-   スイッチポリシーのプロパティ列挙体のパラメーターを指定する、 [ **\_プロパティ\_列挙型\_パラメーター構造体\_NDIS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_property_enum_parameters) 。

-   [**ENUM\_INFO 構造体\_、NDIS\_SWITCH\_プロパティ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_property_enum_info)の配列。 これらの各構造体には、スイッチポリシーのプロパティに関する情報が含まれています。

    **注**  [**ndis\_switch\_プロパティ\_列挙型\_PARAMETERS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_property_enum_parameters)構造体の**numproperties**メンバーが0に設定されている場合は、 [**ndis\_SWITCH\_プロパティ\_enum\_INFO**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_property_enum_info)構造体が返されません。

     

拡張機能では、 [oid\_SWITCH\_プロパティ\_追加](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-property-add)の oid セット要求を行うことはできない  に**注意**してください。 [Oid\_\_プロパティ\_更新](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-property-update)、または[oid\_スイッチ\_プロパティ\_DELETE](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-property-delete)に切り替えます。

 

拡張可能なスイッチ拡張機能は、oid\_スイッチの OID セット要求を処理するときに、次のガイドラインに従う必要があります。これは、プロパティ[\_追加](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-property-add)、OID [\_スイッチ\_プロパティ\_更新](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-property-update)、または[oid\_スイッチ\_プロパティ\_削除](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-property-delete)\_ます。

-   拡張機能では、OID 要求に関連付けられている\_パラメーター構造を削除\_プロパティ\_パラメーターまたは[**ndis\_スイッチ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_property_delete_parameters) [ **\_プロパティ、ndis\_スイッチ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_property_parameters)を変更することはできません。\_

-   拡張機能では、 [oid\_スイッチ\_プロパティ\_更新](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-property-update)または[oid\_スイッチ](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-property-delete)を処理する必要があります。この拡張機能が以前にプロビジョニングされている場合は、次のような[**ndis\_スイッチ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_port_property_parameters)のメンバーに一致するスイッチプロパティ\_プロパティ\_パラメーターまたは[**NDIS\_スイッチ\_プロパティ\_\_パラメーター**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_property_delete_parameters)構造を削除します。\_\_

    -   スイッチプロパティの型を指定する**PropertyType**メンバー。

        **注**  Ndis 6.30 以降では、 **NdisSwitchPropertyTypeCustom**のスイッチプロパティのみが指定されています。これは、 [**ndis\_スイッチ\_プロパティ\_パラメーター**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_port_property_parameters)または[**ndis\_スイッチ\_プロパティ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_property_delete_parameters)によって指定されます。\_パラメーター構造は削除\_ます。

         

    -   拡張によって認識される専用の GUID 値を指定する**PropertyId**メンバー。 この GUID 値は、独立系ソフトウェアベンダー (ISV) によって作成され、カスタム拡張可能スイッチポリシープロパティの形式も定義します。

        カスタム拡張可能なスイッチポリシープロパティが[**NDIS\_スイッチ\_プロパティ\_カスタム**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_property_custom)構造に含まれて  **ことに注意**してください。

         

-   拡張機能がこれらの OID セット要求を処理する場合、拡張機能は、NDIS\_スイッチの次のメンバーと一致するスイッチポリシーを更新または削除する必要があります[ **\_プロパティ\_PARAMETERS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_property_parameters)構造体です。

    -   拡張可能なスイッチポリシーのバージョンを指定する**Propertyversion**メンバー。

    -   拡張可能なスイッチポリシーのインスタンスを指定する**Propertyinstanceid**メンバー。

    これらのメンバーの値が、拡張機能が既にプロビジョニングされているスイッチポリシープロパティと一致しない場合、拡張機能は NDIS\_STATUS の OID set 要求を失敗させ、\_パラメーター\_無効にする必要があります。 それ以外の場合、拡張機能は OID セット要求を完了し、NDIS\_STATUS\_SUCCESS を返す必要があります。

-   フィルターまたは転送拡張機能は、スイッチポリシーの追加、削除、または更新を拒否することができます。 この拡張機能では、状態が\_の OID 要求を完了することによってこれを実行します。データ\_\_は受け入れられません。

    **注**  拡張機能をキャプチャする場合は、スイッチポリシーの追加または更新を拒否することはできません。 代わりに、OID 要求を拡張可能なスイッチ制御パスに転送する必要があります。

     

-   キャプチャまたはフィルター拡張によってカスタムスイッチポリシーの OID セット要求が正常に処理された場合、OID 要求を完了しないようにし、拡張可能なスイッチコントロールパスの下位に転送する必要があります。

    転送拡張機能によってカスタムスイッチポリシーの OID セット要求が正常に処理された場合、OID 要求を完了し、適切な NDIS\_STATUS\_*Xxx*値を返す必要があります。

-   拡張機能が OID セット要求を完了しない場合は、 [**NdisFOidRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfoidrequest)を呼び出して、拡張可能なスイッチドライバースタックから oid 要求を転送する必要があります。 この場合、拡張機能は、基になる拡張機能が OID 要求に失敗したかどうかを検出するために、OID の完了状態を監視する必要があります。

 

 





