---
title: スイッチ ポリシーの概要
description: スイッチ ポリシーの概要
ms.assetid: DB9368CE-96D4-48C9-AE18-601EE4A09001
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: de8a6e03b8b3b9607ec440675ac56e009267d4ef
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63372850"
---
# <a name="overview-of-switch-policies"></a>スイッチ ポリシーの概要


NDIS 6.30 以降では、次の種類のポリシーは、HYPER-V 拡張可能スイッチのサポートされています。

<a href="" id="built-in-switch-policies"></a>スイッチの組み込みのポリシー  
スイッチの組み込みポリシーでは、拡張可能スイッチのインターフェイスによって適用されるプロパティを指定します。 拡張機能で拡張可能スイッチのドライバー スタックは、これらのポリシーのプロパティはプロビジョニングされません。

スイッチの組み込みポリシーでは、一般に、スイッチの構成に影響が、個々 のスイッチ ポート経由でトラフィック フローは影響しませんプロパティを含めます。 たとえば、このような 1 つの組み込みのポリシーは、シングル ルート I/O 仮想化 (SR-IOV) インターフェイスをサポートする物理アダプターにハードウェア オフロードを許可するスイッチを構成します。 このインターフェイスの詳細については、次を参照してください。 [Single Root I/O Virtualization (SR-IOV)](overview-of-single-root-i-o-virtualization--sr-iov-.md)します。

<a href="" id="custom-switch-policies"></a>スイッチのカスタム ポリシー  
スイッチのカスタム ポリシーでは、独立系ソフトウェア ベンダー (ISV) によって定義されている専用のプロパティを指定します。 これらのプロパティは、拡張可能スイッチのプロトコルの端でプロビジョニングされ、スイッチのカスタム ポリシーを管理する、基になる拡張機能によって適用されます。

ISV は、カスタムのスイッチのプロパティの書式を定義します。 スイッチのカスタム プロパティの形式は、ISV 専用。

スイッチのカスタム プロパティは、管理オブジェクト フォーマット (MOF) クラス定義を通じて定義されます。 MOF ファイルが、WMI 管理層に登録された後に、基になる拡張機能は、スイッチのカスタム ポリシーでプロビジョニングされます。

スイッチのカスタム プロパティがで指定された、 [ **NDIS\_切り替える\_プロパティ\_型**](https://msdn.microsoft.com/library/windows/hardware/hh598257)列挙値の**NdisSwitchPropertyTypeCustom**します。 各スイッチのカスタム プロパティは、GUID 値を使用して一意に定義されます。 拡張機能は、対象に構成されているプロパティの GUID 値を持つこれらのスイッチのカスタム プロパティを管理します。

**注**  プロパティの GUID 値を拡張機能を構成するメソッドは、ISV 専用です。

 

スイッチのカスタム ポリシーは、次の OID 要求を介してプロビジョニングされています。

-   プロトコルのエッジの OID のセット要求を発行する[OID\_切り替える\_プロパティ\_追加](https://msdn.microsoft.com/library/windows/hardware/hh598280)スイッチのカスタム プロパティの追加の拡張機能を基になるに通知します。

-   プロトコルのエッジの OID のセット要求を発行する[OID\_切り替える\_プロパティ\_更新](https://msdn.microsoft.com/library/windows/hardware/hh598283)スイッチのカスタム プロパティへの更新の基になる拡張機能を通知します。

-   プロトコルのエッジの OID のセット要求を発行する[OID\_切り替える\_プロパティ\_削除](https://msdn.microsoft.com/library/windows/hardware/hh598281)スイッチのカスタム プロパティの削除の基になる拡張機能を通知します。

新しいまたは更新されたスイッチ ポリシーのプロビジョニングは、OID 要求を拒否する転送拡張機能をブロックできます。 拡張機能は状態が、OID 要求の完了によって\_データ\_いない\_ACCEPTED です。 呼び出す必要がありますが、拡張機能は、OID 要求を拒否していない場合、 [ **NdisFOidRequest** ](https://msdn.microsoft.com/library/windows/hardware/ff561830)拡張可能スイッチ コントロール パス OID 要求を転送します。

**注**  要求が完了したときに状態が監視され、拡張機能が、OID 要求を拒否しては場合。 拡張機能は拡張可能スイッチ コントロール パスの拡張機能を基になるか、拡張可能スイッチのインターフェイスに OID 要求が拒否されたかどうかを判断します。

 

スイッチのポリシーとプロパティを管理する方法の詳細については、次を参照してください。[スイッチ ポリシーの管理](managing-switch-policies.md)します。

 

 





