---
title: スイッチ ポリシーの概要
description: スイッチ ポリシーの概要
ms.assetid: DB9368CE-96D4-48C9-AE18-601EE4A09001
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 39c9643db76bd69175dd137e10fac7941f931e57
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843722"
---
# <a name="overview-of-switch-policies"></a>スイッチ ポリシーの概要


NDIS 6.30 以降では、Hyper-v 拡張可能スイッチで次の種類のポリシーがサポートされています。

<a href="" id="built-in-switch-policies"></a>組み込みのスイッチポリシー  
組み込みのスイッチポリシーでは、拡張可能スイッチインターフェイスによって適用されるプロパティを指定します。 拡張可能なスイッチドライバースタック内の拡張機能は、これらのポリシーのプロパティを使用してプロビジョニングされません。

組み込みのスイッチポリシーには、一般的なスイッチ構成に影響を与えるプロパティが含まれますが、個々のスイッチポートのトラフィックフローには影響しません。 たとえば、このような組み込みポリシーの1つは、ハードウェアのオフロードをシングルルート i/o 仮想化 (SR-IOV) インターフェイスをサポートする物理アダプターに許可するようにスイッチを構成することです。 このインターフェイスの詳細については、「[シングルルート I/o 仮想化 (sr-iov)](overview-of-single-root-i-o-virtualization--sr-iov-.md)」を参照してください。

<a href="" id="custom-switch-policies"></a>カスタムスイッチポリシー  
カスタムスイッチポリシーでは、独立系ソフトウェアベンダー (ISV) によって定義された独自のプロパティを指定します。 これらのプロパティは拡張可能なスイッチのプロトコルエッジによってプロビジョニングされ、カスタムスイッチポリシーを管理する基になる拡張機能によって適用されます。

ISV はカスタムスイッチプロパティの形式を定義します。 カスタムスイッチプロパティの形式は、ISV 専用です。

カスタムスイッチプロパティは、管理オブジェクトフォーマット (MOF) のクラス定義によって定義されます。 MOF ファイルが WMI 管理層に登録されると、基になる拡張機能がカスタムスイッチポリシーを使用してプロビジョニングされます。

カスタムスイッチプロパティは、 [**NDIS\_スイッチ\_プロパティ\_TYPE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ne-ntddndis-_ndis_switch_property_type)列挙値**NdisSwitchPropertyTypeCustom**によって指定されます。 各カスタムスイッチプロパティは、GUID 値によって一意に定義されます。 拡張機能は、プロパティの GUID 値を使用して構成されているカスタムスイッチプロパティを管理します。

プロパティの GUID 値を使用して拡張機能が構成されているメソッドは、ISV 専用の  に**注意**してください。

 

カスタムスイッチポリシーは、次の OID 要求によってプロビジョニングされます。

-   プロトコルエッジは、Oid セット要求[oid\_スイッチ\_プロパティ\_](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-property-add)を発行して、カスタムスイッチプロパティの追加の基になる拡張機能に通知します。

-   プロトコルエッジは、Oid の OID セット要求を[\_し\_プロパティ\_更新](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-property-update)を発行して、更新の基になる拡張機能をカスタムスイッチプロパティに通知します。

-   プロトコルエッジは、Oid の OID セット要求を[\_し\_プロパティ\_削除](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-property-delete)して、カスタムスイッチプロパティの削除の基になる拡張機能に通知します。

転送拡張機能は、OID 要求を vetoing ことによって、新しいまたは更新されたスイッチポリシーのプロビジョニングをブロックできます。 この拡張機能では、状態が\_の OID 要求を完了することによってこれを実行します。データ\_\_は受け入れられません。 拡張機能が OID 要求を拒否しない場合は、 [**NdisFOidRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfoidrequest)を呼び出して、拡張可能なスイッチコントロールパスで oid 要求を転送する必要があります。

**  、** 拡張機能が OID 要求を拒否しない場合、要求が完了したときに状態を監視します。 拡張機能は、拡張可能なスイッチコントロールパスまたは拡張可能なスイッチインターフェイスで、基になる拡張機能によって OID 要求が拒否されたかどうかを判断します。

 

スイッチポリシーとプロパティを管理する方法の詳細については、「[スイッチポリシーの管理](managing-switch-policies.md)」を参照してください。

 

 





