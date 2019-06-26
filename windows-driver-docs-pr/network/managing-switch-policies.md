---
title: スイッチ ポリシーの管理
description: スイッチ ポリシーの管理
ms.assetid: F2261CA6-2D7A-4499-82F9-7E2D7C9C908D
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: fbc7257f64b01b06d706dd5d461fbbab0c6922f7
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67375232"
---
# <a name="managing-switch-policies"></a>スイッチ ポリシーの管理


HYPER-V 拡張可能スイッチのフィルター処理および転送拡張機能は、カスタムのスイッチのプロパティのプロパティをプロビジョニングできます。 プロビジョニング完了すると、これらの拡張機能は、拡張可能スイッチのイングレス データ パス取得したパケットをフィルター処理するときに、ポリシーを適用できます。 これらのポリシーの詳細については、次を参照してください。[スイッチ ポリシー](switch-policies.md)します。

HYPER-V 拡張可能スイッチのインターフェイスでは、次のオブジェクト識別子 (Oid) を使用して、フィルター処理と転送スイッチのカスタム ポリシーのプロパティを持つ拡張機能をプロビジョニングします。

<a href="" id="oid-switch-property-add"></a>[OID\_スイッチ\_プロパティ\_追加](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-property-add)  
WMI 管理層でのプロパティの追加の拡張機能を基になるに通知する拡張可能スイッチのプロトコルの端では、この OID セットの要求が発行されます。 **InformationBuffer**の[ **NDIS\_OID\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_oid_request)構造体にはへのポインターが含まれています、 [ **NDIS\_スイッチ\_プロパティ\_パラメーター** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_switch_property_parameters)構造体。

**注**  スイッチのカスタム プロパティがで指定された、 [ **NDIS\_切り替える\_プロパティ\_型**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ne-ntddndis-_ndis_switch_property_type) の列挙値**NdisSwitchPropertyTypeCustom**します。

 

<a href="" id="oid-switch-property-update"></a>[OID\_スイッチ\_プロパティ\_UPDATE](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-property-update)  
WMI 管理層でのプロパティの更新プログラムの拡張機能を基になるに通知する拡張可能スイッチのプロトコルの端では、この OID セットの要求が発行されます。 **InformationBuffer**の[ **NDIS\_OID\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_oid_request)構造体にはへのポインターが含まれています、 [ **NDIS\_スイッチ\_プロパティ\_パラメーター** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_switch_property_parameters)構造体。

<a href="" id="oid-switch-property-delete"></a>[OID\_スイッチ\_プロパティ\_削除](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-property-delete)  
WMI 管理層でのプロパティの削除の基になる拡張機能を通知する拡張可能スイッチのプロトコルの端では、この OID セットの要求が発行されます。 **InformationBuffer**の[ **NDIS\_OID\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_oid_request)構造体にはへのポインターが含まれています、 [ **NDIS\_スイッチ\_プロパティ\_削除\_パラメーター** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_switch_property_delete_parameters)構造体。

<a href="" id="oid-switch-property-enum"></a>[OID\_スイッチ\_プロパティ\_列挙型](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-property-enum)  
この OID メソッド要求は、拡張可能スイッチに現在構成されているスイッチのプロパティの拡張可能スイッチの基になるミニポート エッジをクエリに、拡張機能によって送信されます。 **InformationBuffer**の[ **NDIS\_OID\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_oid_request)構造体には、バッファーへのポインターが含まれています。 このバッファーには、次のデータが含まれています。

-   [ **NDIS\_切り替える\_プロパティ\_ENUM\_パラメーター** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_switch_property_enum_parameters)スイッチのプロパティの列挙型のパラメーターを指定する構造体ポリシー。

-   配列の[ **NDIS\_スイッチ\_プロパティ\_ENUM\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_switch_property_enum_info)構造体。 各構造体には、スイッチのポリシーのプロパティに関する情報が含まれています。

    **注**  場合、 **NumProperties**のメンバー、 [ **NDIS\_スイッチ\_プロパティ\_ENUM\_パラメーター**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_switch_property_enum_parameters)構造が 0、no に設定されている[ **NDIS\_スイッチ\_プロパティ\_ENUM\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_switch_property_enum_info)構造体が返されます。

     

**注**  の OID のセット要求を取得する必要があります、拡張機能[OID\_スイッチ\_プロパティ\_追加](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-property-add)します。 [OID\_スイッチ\_プロパティ\_UPDATE](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-property-update)、または[OID\_スイッチ\_プロパティ\_削除](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-property-delete)します。

 

拡張可能スイッチ拡張機能は、の OID セット要求を処理する場合これらのガイドラインに従う必要があります[OID\_切り替える\_プロパティ\_追加](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-property-add)、 [OID\_スイッチ\_プロパティ\_UPDATE](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-property-update)、または[OID\_スイッチ\_プロパティ\_削除](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-property-delete):

-   拡張機能は変更しないで、 [ **NDIS\_スイッチ\_プロパティ\_パラメーター** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_switch_property_parameters)または[ **NDIS\_スイッチ\_プロパティ\_削除\_パラメーター** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_switch_property_delete_parameters) OID 要求に関連付けられている構造体。

-   拡張機能を処理する必要があります、 [OID\_スイッチ\_プロパティ\_UPDATE](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-property-update)または[OID\_スイッチ\_プロパティ\_DELETE](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-property-delete)セットの要求、拡張機能は以前の次のメンバーに一致するスイッチのプロパティを使用してプロビジョニングされている場合、 [ **NDIS\_切り替える\_プロパティ\_パラメーター** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_switch_port_property_parameters)または[ **NDIS\_スイッチ\_プロパティ\_削除\_パラメーター** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_switch_property_delete_parameters)構造体。

    -   **PropertyType**メンバー スイッチのプロパティの型を指定します。

        **注**  NDIS 6.30 以降、のみのプロパティを切り替える**NdisSwitchPropertyTypeCustom**で指定された、 [ **NDIS\_切り替える\_プロパティ\_パラメーター** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_switch_port_property_parameters)または[ **NDIS\_スイッチ\_プロパティ\_削除\_パラメーター**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_switch_property_delete_parameters)構造体。

         

    -   **PropertyId**拡張機能を認識する独自の GUID 値を指定するメンバー。 この GUID 値も拡張可能スイッチのカスタム ポリシーのプロパティの形式を定義した独立系ソフトウェア ベンダー (ISV) によって作成されます。

        **注**  拡張可能スイッチのカスタム ポリシーのプロパティに含まれる、 [ **NDIS\_切り替える\_プロパティ\_カスタム**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_switch_property_custom)構造体。

         

-   拡張機能が更新する必要があるかどうか、またはスイッチ ポリシー一致の次のメンバーを削除、拡張機能は、これらの OID セット要求を処理する場合、 [ **NDIS\_切り替える\_プロパティ\_パラメーター**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_switch_property_parameters)構造体。

    -   **PropertyVersion**拡張可能スイッチのポリシーのバージョンを指定するメンバー。

    -   **PropertyInstanceId**メンバーの拡張可能スイッチ ポリシー インスタンスを指定します。

    これらのメンバーの値を拡張機能が以前にプロビジョニングされてスイッチ ポリシーのプロパティが一致しない場合、拡張機能は、NDIS に OID セット要求を失敗する必要があります\_状態\_無効な\_パラメーター。 それ以外の場合、拡張機能が、OID セット要求を完了し、NDIS を返す必要があります\_状態\_成功します。

-   フィルター処理、または転送拡張機能は、追加、削除、またはスイッチのポリシーの更新プログラムを拒否できます。 拡張機能は状態が、OID 要求の完了によって\_データ\_いない\_ACCEPTED です。

    **注**  取得拡張機能の追加またはスイッチのポリシーの変更しない拒否する必要があります。 代わりに、拡張可能スイッチ コントロール パスに OID 要求に転送する必要があります。

     

-   キャプチャまたは拡張機能を正常にフィルター処理は、スイッチのカスタム ポリシーの OID のセット要求を処理する場合は OID 要求を完了する必要があり、拡張可能スイッチ コントロール パスに転送する必要があります。

    転送拡張機能は、スイッチのカスタム ポリシーの OID のセット要求を正常に処理する場合は、OID 要求を完了し、適切な NDIS を返すにする必要があります\_状態\_*Xxx*値。

-   呼び出す必要がありますが、拡張機能が、OID セット要求を完了しない場合[ **NdisFOidRequest** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisfoidrequest)拡張可能スイッチのドライバー スタック ダウン OID 要求を転送します。 この場合、拡張機能は、基になる拡張機能の OID 要求が失敗したかどうかを検出する OID の完了状態を監視する必要があります。

 

 





