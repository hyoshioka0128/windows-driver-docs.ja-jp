---
title: ポート ポリシーの概要
description: ポート ポリシーの概要
ms.assetid: 9FA63E67-F5CC-4508-A36F-7A5956568D0E
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: efb0e8968ef4fe2e8f174721d814e44400047e27
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843725"
---
# <a name="overview-of-port-policies"></a>ポート ポリシーの概要


NDIS 6.30 以降では、Hyper-v 拡張可能スイッチポートで次の種類のポリシーがサポートされています。

<a href="" id="built-in-port-policies"></a>組み込みのポートポリシー  
組み込みのポートポリシーでは、拡張可能なスイッチインターフェイスによって適用されるプロパティを指定します。 拡張可能なスイッチドライバースタック内の拡張機能は、これらのポリシーのプロパティを使用してプロビジョニングされません。

組み込みのポートポリシーには、アクセス制御リスト (Acl) およびサービスの品質 (QoS) プロパティが含まれます。 パケットが受信データパスの拡張可能スイッチのミニポートエッジに到着すると、スイッチはパケットをフィルター処理して、これらのポリシーを適用します。 パケットがフィルター処理に合格すると、スイッチはパケットを送信データパスの上に転送し、追加の処理や拡張によるフィルター処理を行います。

拡張可能なスイッチのデータパスの詳細については、「 [Hyper-v 拡張可能スイッチのデータパス](hyper-v-extensible-switch-data-path.md)」を参照してください。

<a href="" id="standard-port-policies"></a>標準ポートポリシー  
標準ポートポリシーでは、セキュリティ、プロファイル、または仮想 LAN (VLAN) のプロパティを指定します。 これらのプロパティは、拡張可能スイッチのプロトコルエッジによって発行されたオブジェクト識別子 (OID) 要求によってプロビジョニングされます。 拡張可能なスイッチのデータパスに転送拡張機能がインストールされていない場合、これらのポリシーは、基になる拡張可能スイッチのミニポートエッジによって適用されます。 そうしないと、ポリシーをプロビジョニングできる場合、転送拡張機能によってこれらのポリシーが適用されます。

標準ポートのプロパティは、 [**NDIS\_スイッチ\_ポート\_プロパティ\_TYPE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ne-ntddndis-_ndis_switch_port_property_type)列挙値**NdisSwitchPortPropertyTypeSecurity**、 **NdisSwitchPortPropertyTypeVlan**、および**NdisSwitchPortPropertyTypeProfile**によって指定されます。

**注**  転送拡張機能が VLAN ポートのプロパティを管理または適用しない場合は、 [oid\_スイッチ\_ポート\_プロパティ\_add](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-port-property-add)および[oid\_switch\_port](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-port-property-update)\_プロパティ\_プロパティを追加または更新する更新要求に対して\_\_\_データを返す必要があります。 VLAN ポートのプロパティには、 **NdisSwitchPortPropertyTypeVlan**のプロパティの種類があります。

 

<a href="" id="custom-port-policies"></a>カスタムポートポリシー  
カスタムポートポリシーでは、独立系ソフトウェアベンダー (ISV) によって定義された独自のプロパティを指定します。 これらのプロパティは、拡張可能なスイッチのプロトコルエッジによって発行され、カスタムポートポリシーを管理する基になる拡張機能によって適用される OID 要求によってプロビジョニングされます。

カスタムポートプロパティは、管理オブジェクトフォーマット (MOF) のクラス定義によって定義されます。 ISV は、MOF クラス定義を使用してカスタムポートプロパティの形式を定義します。 MOF ファイルが WMI 管理層に登録されると、基になる拡張機能がカスタムポートポリシーを使用してプロビジョニングされます。

カスタムポートプロパティは、 [**NDIS\_スイッチ\_ポート\_プロパティ\_TYPE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ne-ntddndis-_ndis_switch_port_property_type)列挙値**NdisSwitchPortPropertyTypeCustom**によって指定されます。 各カスタムポートプロパティは、GUID 値によって一意に定義されます。 拡張機能は、プロパティの GUID 値を使用して構成されているカスタムポートプロパティを管理します。

プロパティの GUID 値を使用して拡張機能が構成されているメソッドは、ISV 専用の  に**注意**してください。

 

標準およびカスタムポートポリシーは、次の OID 要求によってプロビジョニングされます。

-   プロトコルエッジは、Oid の OID セット要求を[\_ポート\_プロパティ\_\_](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-port-property-add)して、標準またはカスタムポートプロパティの追加を基になる拡張機能に通知します。

-   プロトコルエッジは、Oid の OID セット要求を[\_し\_ポート\_プロパティ\_更新](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-port-property-update)を発行して、更新の基になる拡張機能を標準またはカスタムポートプロパティに通知します。

-   プロトコルエッジは、Oid の OID セット要求を[\_し\_ポート\_プロパティ\_削除](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-port-property-delete)を発行して、標準またはカスタムポートプロパティの削除の基になる拡張機能に通知します。

転送拡張機能は、OID 要求を vetoing ことによって、新しいまたは更新されたポートポリシーのプロビジョニングをブロックできます。 この拡張機能では、状態が\_の OID 要求を完了することによってこれを実行します。データ\_\_は受け入れられません。 拡張機能が OID 要求を拒否しない場合は、 [**NdisFOidRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfoidrequest)を呼び出して、拡張可能なスイッチコントロールパスで oid 要求を転送する必要があります。

**  、** 拡張機能が OID 要求を拒否しない場合、要求が完了したときに状態を監視します。 拡張機能は、拡張可能なスイッチコントロールパスまたは拡張可能なスイッチインターフェイスで、基になる拡張機能によって OID 要求が拒否されたかどうかを判断します。

 

ポートポリシーとプロパティを管理する方法の詳細については、「[ポートポリシーの管理](managing-port-policies.md)」を参照してください。

 

 





