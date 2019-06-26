---
title: ポート ポリシーの概要
description: ポート ポリシーの概要
ms.assetid: 9FA63E67-F5CC-4508-A36F-7A5956568D0E
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a72707d1b3f75e30c7b6af48a14f5c6ad066cd11
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67372499"
---
# <a name="overview-of-port-policies"></a>ポート ポリシーの概要


NDIS 6.30 以降では、次の種類のポリシーは、HYPER-V 拡張可能スイッチ ポートのサポートされています。

<a href="" id="built-in-port-policies"></a>ポートの組み込みのポリシー  
組み込みのポートのポリシーは、拡張可能スイッチのインターフェイスによって適用されるプロパティを指定します。 拡張機能で拡張可能スイッチのドライバー スタックは、これらのポリシーのプロパティはプロビジョニングされません。

品質 (QoS) のプロパティのサービスおよびポートの組み込みポリシーにはアクセス制御リスト (Acl) が含まれます。 イングレス データ パス パケットの拡張可能スイッチのミニポート端が到着すると、スイッチは、パケットをフィルター処理し、これらのポリシーを適用します。 パケット フィルター処理が成功した場合、スイッチは、追加の処理と後続の拡張機能でフィルター処理のエグレス データ パスのパケットを転送します。

拡張可能スイッチのデータ パスの詳細については、次を参照してください。 [Hyper-v 拡張可能スイッチ データ パス](hyper-v-extensible-switch-data-path.md)します。

<a href="" id="standard-port-policies"></a>標準ポート ポリシー  
標準のポートのポリシーは、セキュリティ、プロファイル、または仮想 LAN (VLAN) のプロパティを指定します。 これらのプロパティは、拡張可能スイッチのプロトコルの端から発行されたオブジェクト識別子 (OID) 要求がプロビジョニングされます。 転送拡張機能がインストールおよび拡張可能スイッチのデータ パスで有効になっている、基になる拡張可能スイッチのミニポート edge によってこれらのポリシーが強制されます。 それ以外の場合、転送拡張機能は、プロビジョニングするポリシーを許可する場合、これらのポリシーを適用します。

標準のポートのプロパティがで指定された、 [ **NDIS\_スイッチ\_ポート\_プロパティ\_型**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ne-ntddndis-_ndis_switch_port_property_type)列挙値の**NdisSwitchPortPropertyTypeSecurity**、 **NdisSwitchPortPropertyTypeVlan**、および**NdisSwitchPortPropertyTypeProfile**します。

**注**  転送拡張機能を管理またはがない場合の VLAN のポートのプロパティの適用、状態を返す必要が\_データ\_いない\_の受け入れ、 [OID\_スイッチ\_ポート\_プロパティ\_追加](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-port-property-add)と[OID\_スイッチ\_ポート\_プロパティ\_更新](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-port-property-update)を追加または更新を要求しますプロパティ。 VLAN のポートのプロパティのプロパティの型がある**NdisSwitchPortPropertyTypeVlan**します。

 

<a href="" id="custom-port-policies"></a>カスタム ポート ポリシー  
ポートのカスタム ポリシーでは、独立系ソフトウェア ベンダー (ISV) によって定義されている専用のプロパティを指定します。 これらのプロパティは、拡張可能スイッチの拡張可能スイッチのプロトコルの edge によって発行され、ポートのカスタム ポリシーを管理する、基になる拡張機能によって適用される OID 要求でプロビジョニングされます。

カスタム ポートのプロパティは、管理オブジェクト フォーマット (MOF) クラス定義を介して定義されます。 ISV は、MOF クラスの定義でカスタム ポートのプロパティの形式を定義します。 MOF ファイルが、WMI 管理層に登録された後に、基になる拡張機能は、ポートのカスタム ポリシーでプロビジョニングされます。

カスタム ポートのプロパティが指定された[ **NDIS\_スイッチ\_ポート\_プロパティ\_型**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ne-ntddndis-_ndis_switch_port_property_type)列挙値の**NdisSwitchPortPropertyTypeCustom**します。 各カスタム ポートのプロパティは、GUID 値を使用して一意に定義されます。 拡張機能は、それらに構成されているプロパティの GUID 値を持つカスタムのポートのプロパティを管理します。

**注**  プロパティの GUID 値を拡張機能を構成するメソッドは、ISV 専用です。

 

ポートを標準とカスタム ポリシーは、次の OID 要求を介してプロビジョニングされています。

-   プロトコルのエッジの OID のセット要求を発行する[OID\_スイッチ\_ポート\_プロパティ\_追加](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-port-property-add)に標準またはカスタムのポートのプロパティの追加の基になる拡張機能を通知します。

-   プロトコルのエッジの OID のセット要求を発行する[OID\_スイッチ\_ポート\_プロパティ\_更新](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-port-property-update)に標準またはカスタムのポートのプロパティへの更新の基になる拡張機能を通知します。

-   プロトコルのエッジの OID のセット要求を発行する[OID\_スイッチ\_ポート\_プロパティ\_削除](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-port-property-delete)に標準またはカスタムのポートのプロパティの削除の基になる拡張機能を通知します。

ポートの新しいまたは更新されたポリシーのプロビジョニングは、OID 要求を拒否する転送拡張機能をブロックできます。 拡張機能は状態が、OID 要求の完了によって\_データ\_いない\_ACCEPTED です。 呼び出す必要がありますが、拡張機能は、OID 要求を拒否していない場合、 [ **NdisFOidRequest** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisfoidrequest)拡張可能スイッチ コントロール パス OID 要求を転送します。

**注**  要求が完了したときに状態が監視され、拡張機能が、OID 要求を拒否しては場合。 拡張機能は拡張可能スイッチ コントロール パスの拡張機能を基になるか、拡張可能スイッチのインターフェイスに OID 要求が拒否されたかどうかを判断します。

 

ポートのポリシーとプロパティを管理する方法の詳細については、次を参照してください。[ポート ポリシーの管理](managing-port-policies.md)します。

 

 





