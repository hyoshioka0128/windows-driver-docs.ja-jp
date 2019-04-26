---
title: ポート ポリシーの管理
description: ポート ポリシーの管理
ms.assetid: 46394916-6558-4BDA-8920-E3C5378823BE
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 916a50af47ca454e754ab8d32d52c5ddbca53d09
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63343540"
---
# <a name="managing-port-policies"></a>ポート ポリシーの管理


HYPER-V 拡張可能スイッチのフィルター処理および転送拡張機能は、標準とカスタム ポートのプロパティのプロパティでプロビジョニングできます。 プロビジョニング完了すると、これらの拡張機能は、拡張可能スイッチのイングレス データ パス取得したパケットをフィルター処理するときに、ポリシーを適用できます。 これらのポリシーの詳細については、次を参照してください。[ポート ポリシー](port-policies.md)します。

HYPER-V 拡張可能スイッチのインターフェイスは、ポートを標準とカスタム ポリシーのプロパティをフィルター処理と転送拡張機能をプロビジョニングするのに次のオブジェクト識別子 (Oid) を使用します。

<a href="" id="oid-switch-port-property-add"></a>[OID\_スイッチ\_ポート\_プロパティ\_追加](https://msdn.microsoft.com/library/windows/hardware/hh598275)  
WMI 管理層でのプロパティの追加の拡張機能を基になるに通知する拡張可能スイッチのプロトコルの端では、この OID セットの要求が発行されます。 **InformationBuffer**の[ **NDIS\_OID\_要求**](https://msdn.microsoft.com/library/windows/hardware/ff566710)構造体にはへのポインターが含まれています、 [ **NDIS\_スイッチ\_ポート\_プロパティ\_パラメーター** ](https://msdn.microsoft.com/library/windows/hardware/hh598238)構造体。

**注**  でカスタム ポートのプロパティが指定された、 [ **NDIS\_スイッチ\_ポート\_プロパティ\_型**](https://msdn.microsoft.com/library/windows/hardware/hh598242)列挙値の**NdisSwitchPortPropertyTypeCustom**します。 標準のポートのプロパティがで指定された、 **NDIS\_スイッチ\_ポート\_プロパティ\_型**列挙値の**NdisSwitchPortPropertyTypeSecurity**、 **NdisSwitchPortPropertyTypeVlan**、および**NdisSwitchPortPropertyTypeProfile**します。

 

<a href="" id="oid-switch-port-property-update"></a>[OID\_スイッチ\_ポート\_プロパティ\_UPDATE](https://msdn.microsoft.com/library/windows/hardware/hh598278)  
WMI 管理層でのプロパティの更新プログラムの基になる拡張機能を通知するために拡張可能スイッチのプロトコルの端では、この OID セットの要求が発行されます。 **InformationBuffer**の[ **NDIS\_OID\_要求**](https://msdn.microsoft.com/library/windows/hardware/ff566710)構造体にはへのポインターが含まれています、 [ **NDIS\_スイッチ\_ポート\_プロパティ\_パラメーター** ](https://msdn.microsoft.com/library/windows/hardware/hh598238)構造体。

<a href="" id="oid-switch-port-property-delete"></a>[OID\_スイッチ\_ポート\_プロパティ\_削除](https://msdn.microsoft.com/library/windows/hardware/hh598276)  
WMI 管理層でのプロパティの削除の基になる拡張機能を通知するために拡張可能スイッチのプロトコルの端では、この OID セットの要求が発行されます。 **InformationBuffer**の[ **NDIS\_OID\_要求**](https://msdn.microsoft.com/library/windows/hardware/ff566710)構造体にはへのポインターが含まれています、 [ **NDIS\_スイッチ\_ポート\_プロパティ\_削除\_パラメーター** ](https://msdn.microsoft.com/library/windows/hardware/hh598232)構造体。

<a href="" id="oid-switch-port-property-enum"></a>[OID\_スイッチ\_ポート\_プロパティ\_列挙型](https://msdn.microsoft.com/library/windows/hardware/hh598277)  
この OID メソッド要求は、クエリの指定したポート拡張可能スイッチに現在構成されているプロパティの拡張可能スイッチの基になるミニポート エッジに拡張機能によって送信されます。 **InformationBuffer**の[ **NDIS\_OID\_要求**](https://msdn.microsoft.com/library/windows/hardware/ff566710)構造体には、バッファーへのポインターが含まれています。 このバッファーには、次のデータが含まれています。

-   [ **NDIS\_スイッチ\_ポート\_プロパティ\_ENUM\_パラメーター** ](https://msdn.microsoft.com/library/windows/hardware/hh598236)ポリシーのパラメーターを指定する構造体指定したポートの列挙体。

-   配列の[ **NDIS\_スイッチ\_ポート\_プロパティ\_ENUM\_情報**](https://msdn.microsoft.com/library/windows/hardware/hh598233)構造体。 各構造体には、拡張可能スイッチ ポートのポリシーのプロパティに関する情報が含まれています。

    **注**  場合、 **NumProperties**のメンバー、 [ **NDIS\_スイッチ\_ポート\_プロパティ\_ENUM\_パラメーター** ](https://msdn.microsoft.com/library/windows/hardware/hh598236)構造が 0、no に設定されている[ **NDIS\_スイッチ\_ポート\_プロパティ\_ENUM\_情報** ](https://msdn.microsoft.com/library/windows/hardware/hh598233)構造体が返されます。

     

**注**  の OID のセット要求を取得する必要があります、拡張機能[OID\_スイッチ\_ポート\_プロパティ\_追加](https://msdn.microsoft.com/library/windows/hardware/hh598275)します。 [OID\_スイッチ\_ポート\_プロパティ\_UPDATE](https://msdn.microsoft.com/library/windows/hardware/hh598278)、または[OID\_スイッチ\_ポート\_プロパティ\_DELETE](https://msdn.microsoft.com/library/windows/hardware/hh598276).

 

拡張可能スイッチ拡張機能は、の OID セット要求を処理する場合これらのガイドラインに従う必要があります[OID\_切り替える\_ポート\_プロパティ\_追加](https://msdn.microsoft.com/library/windows/hardware/hh598275)、 [OID\_スイッチ\_ポート\_プロパティ\_UPDATE](https://msdn.microsoft.com/library/windows/hardware/hh598278)、または[OID\_スイッチ\_ポート\_プロパティ\_削除](https://msdn.microsoft.com/library/windows/hardware/hh598276):

-   拡張機能は変更しないで、 [ **NDIS\_スイッチ\_ポート\_プロパティ\_パラメーター** ](https://msdn.microsoft.com/library/windows/hardware/hh598238)または[ **NDIS\_スイッチ\_ポート\_プロパティ\_削除\_パラメーター** ](https://msdn.microsoft.com/library/windows/hardware/hh598232) OID 要求に関連付けられている構造体。

-   拡張機能は、拡張機能が、プロパティを管理する場合、これらの OID 要求を処理する必要があります。 拡張機能によっては、OID 要求の次のメンバーを調べる必要がある、 [ **NDIS\_スイッチ\_ポート\_プロパティ\_パラメーター** ](https://msdn.microsoft.com/library/windows/hardware/hh598238)または[ **NDIS\_スイッチ\_ポート\_プロパティ\_削除\_パラメーター** ](https://msdn.microsoft.com/library/windows/hardware/hh598232)を決定する構造体かどうか、ポートのプロパティを管理します。

    -   **PropertyType**メンバー。 このメンバーは、ポートのプロパティの型を指定します。 カスタム ポートのプロパティが、 **PropertyType**のメンバー値**NdisSwitchPortPropertyTypeCustom**します。 標準のポートのプロパティでは、その他のプロパティ型の値があります。 たとえば、標準的な VLAN ポート ポリシー プロパティ値を持つ型の**NdisSwitchPortPropertyTypeVlan**します。

    -   **PropertyId**メンバー。 このメンバーは、カスタム ポートのプロパティの独自の GUID 値を指定します。 この GUID 値は、また、カスタムの拡張可能スイッチのプロパティの形式を定義した独立系ソフトウェア ベンダー (ISV) によって作成されます。

        **注**  拡張機能は、標準のポートのポリシーは、このメンバーを無視する必要があります。

         

-   拡張機能を処理する必要があります、 [OID\_スイッチ\_ポート\_プロパティ\_UPDATE](https://msdn.microsoft.com/library/windows/hardware/hh598278)セットの要求と一致するポートのプロパティを使用して、拡張機能を以前にプロビジョニングする場合、次のメンバー、 [ **NDIS\_スイッチ\_プロパティ\_パラメーター** ](https://msdn.microsoft.com/library/windows/hardware/hh598255)構造体。

    -   **PropertyType**メンバー。

    -   **PropertyId**メンバー。

        **注**  拡張機能は、標準のポートのポリシーは、このメンバーを無視する必要があります。

         

    -   **PropertyVersion**メンバー。 このメンバーは、ポート プロパティで、拡張機能がプロビジョニングされているのバージョンを指定します。

    -   **PropertyInstanceId**メンバー。 このメンバーには、拡張機能でプロビジョニングされているポートのプロパティのインスタンスを指定します。

-   フィルター処理、または転送拡張機能は、追加や、管理しているポート ポリシーの更新を拒否できます。 拡張機能は状態が、OID 要求の完了によって\_データ\_いない\_ACCEPTED です。

    **注**  取得拡張機能の追加またはポートのポリシーの変更しない拒否する必要があります。 代わりに、拡張可能スイッチ コントロール パスに OID 要求に転送する必要があります。

     

-   転送拡張機能には、標準のポートのプロパティがサポートされていないか、またはプロパティ、独自のポリシー構成の競合の OID 要求が失敗します。 この場合、拡張機能は、OID 要求を完了し、エラーを報告して適切な NDIS 状態コードを返す必要があります。

-   拡張機能は、標準ポート ポリシー OID セットの要求を正常に処理する場合は OID 要求を完了する必要があり、拡張可能スイッチ コントロール パスに転送する必要があります。

-   キャプチャまたは拡張機能を正常にフィルター処理は、カスタム ポート ポリシー OID セットの要求を処理する場合は OID 要求を完了する必要があり、拡張可能スイッチ コントロール パスに転送する必要があります。

    転送拡張機能では、カスタム ポート ポリシー OID セットの要求が正常に処理する場合は、OID 要求を完了し、適切な NDIS を返すにする必要があります\_状態\_*Xxx*値。

-   呼び出す必要がありますが、拡張機能が、OID セット要求を完了しない場合[ **NdisFOidRequest** ](https://msdn.microsoft.com/library/windows/hardware/ff561830)拡張可能スイッチのドライバー スタック ダウン OID 要求を転送します。 この場合、拡張機能は、基になる拡張機能の OID 要求が失敗したかどうかを検出する OID の完了状態を監視する必要があります。

 

 





