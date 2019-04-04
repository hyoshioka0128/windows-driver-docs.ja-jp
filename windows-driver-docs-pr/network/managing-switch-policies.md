---
title: スイッチ ポリシーの管理
description: スイッチ ポリシーの管理
ms.assetid: F2261CA6-2D7A-4499-82F9-7E2D7C9C908D
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3645f6da02e6d0d1db8a939ea616b452d4531b0d
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56578332"
---
# <a name="managing-switch-policies"></a>スイッチ ポリシーの管理


HYPER-V 拡張可能スイッチのフィルター処理および転送拡張機能は、カスタムのスイッチのプロパティのプロパティをプロビジョニングできます。 プロビジョニング完了すると、これらの拡張機能は、拡張可能スイッチのイングレス データ パス取得したパケットをフィルター処理するときに、ポリシーを適用できます。 これらのポリシーの詳細については、[スイッチ ポリシー](switch-policies.md)を参照してください。

HYPER-V 拡張可能スイッチのインターフェイスでは、次のオブジェクト識別子 (Oid) を使用して、フィルター処理と転送スイッチのカスタム ポリシーのプロパティを持つ拡張機能をプロビジョニングします。

<a href="" id="oid-switch-property-add"></a>[OID\_スイッチ\_プロパティ\_追加](https://msdn.microsoft.com/library/windows/hardware/hh598280)  
WMI 管理層でのプロパティの追加の拡張機能を基になるに通知する拡張可能スイッチのプロトコルの端では、この OID セットの要求が発行されます。 **InformationBuffer**の[ **NDIS\_OID\_要求**](https://msdn.microsoft.com/library/windows/hardware/ff566710)構造体にはへのポインターが含まれています、 [ **NDIS\_スイッチ\_プロパティ\_パラメーター** ](https://msdn.microsoft.com/library/windows/hardware/hh598255)構造体。

**注**  スイッチのカスタム プロパティがで指定された、 [ **NDIS\_切り替える\_プロパティ\_型**](https://msdn.microsoft.com/library/windows/hardware/hh598257) の列挙値**NdisSwitchPropertyTypeCustom**します。

 

<a href="" id="oid-switch-property-update"></a>[OID\_スイッチ\_プロパティ\_UPDATE](https://msdn.microsoft.com/library/windows/hardware/hh598283)  
WMI 管理層でのプロパティの更新プログラムの拡張機能を基になるに通知する拡張可能スイッチのプロトコルの端では、この OID セットの要求が発行されます。 **InformationBuffer**の[ **NDIS\_OID\_要求**](https://msdn.microsoft.com/library/windows/hardware/ff566710)構造体にはへのポインターが含まれています、 [ **NDIS\_スイッチ\_プロパティ\_パラメーター** ](https://msdn.microsoft.com/library/windows/hardware/hh598255)構造体。

<a href="" id="oid-switch-property-delete"></a>[OID\_スイッチ\_プロパティ\_削除](https://msdn.microsoft.com/library/windows/hardware/hh598281)  
WMI 管理層でのプロパティの削除の基になる拡張機能を通知する拡張可能スイッチのプロトコルの端では、この OID セットの要求が発行されます。 **InformationBuffer**の[ **NDIS\_OID\_要求**](https://msdn.microsoft.com/library/windows/hardware/ff566710)構造体にはへのポインターが含まれています、 [ **NDIS\_スイッチ\_プロパティ\_削除\_パラメーター** ](https://msdn.microsoft.com/library/windows/hardware/hh598249)構造体。

<a href="" id="oid-switch-property-enum"></a>[OID\_スイッチ\_プロパティ\_列挙型](https://msdn.microsoft.com/library/windows/hardware/hh598282)  
この OID メソッド要求は、拡張可能スイッチに現在構成されているスイッチのプロパティの拡張可能スイッチの基になるミニポート エッジをクエリに、拡張機能によって送信されます。 **InformationBuffer**の[ **NDIS\_OID\_要求**](https://msdn.microsoft.com/library/windows/hardware/ff566710)構造体には、バッファーへのポインターが含まれています。 このバッファーには、次のデータが含まれています。

-   [ **NDIS\_切り替える\_プロパティ\_ENUM\_パラメーター** ](https://msdn.microsoft.com/library/windows/hardware/hh598253)スイッチのプロパティの列挙型のパラメーターを指定する構造体ポリシー。

-   配列の[ **NDIS\_スイッチ\_プロパティ\_ENUM\_情報**](https://msdn.microsoft.com/library/windows/hardware/hh598250)構造体。 各構造体には、スイッチのポリシーのプロパティに関する情報が含まれています。

    **注**  場合、 **NumProperties**のメンバー、 [ **NDIS\_スイッチ\_プロパティ\_ENUM\_パラメーター**](https://msdn.microsoft.com/library/windows/hardware/hh598253)構造が 0、no に設定されている[ **NDIS\_スイッチ\_プロパティ\_ENUM\_情報**](https://msdn.microsoft.com/library/windows/hardware/hh598250)構造体が返されます。

     

**注**  の OID のセット要求を取得する必要があります、拡張機能[OID\_スイッチ\_プロパティ\_追加](https://msdn.microsoft.com/library/windows/hardware/hh598280)します。 [OID\_スイッチ\_プロパティ\_UPDATE](https://msdn.microsoft.com/library/windows/hardware/hh598283)、または[OID\_スイッチ\_プロパティ\_削除](https://msdn.microsoft.com/library/windows/hardware/hh598281)します。

 

拡張可能スイッチ拡張機能は、の OID セット要求を処理する場合これらのガイドラインに従う必要があります[OID\_切り替える\_プロパティ\_追加](https://msdn.microsoft.com/library/windows/hardware/hh598280)、 [OID\_スイッチ\_プロパティ\_UPDATE](https://msdn.microsoft.com/library/windows/hardware/hh598283)、または[OID\_スイッチ\_プロパティ\_削除](https://msdn.microsoft.com/library/windows/hardware/hh598281):

-   拡張機能は変更しないで、 [ **NDIS\_スイッチ\_プロパティ\_パラメーター** ](https://msdn.microsoft.com/library/windows/hardware/hh598255)または[ **NDIS\_スイッチ\_プロパティ\_削除\_パラメーター** ](https://msdn.microsoft.com/library/windows/hardware/hh598249) OID 要求に関連付けられている構造体。

-   拡張機能を処理する必要があります、 [OID\_スイッチ\_プロパティ\_UPDATE](https://msdn.microsoft.com/library/windows/hardware/hh598283)または[OID\_スイッチ\_プロパティ\_DELETE](https://msdn.microsoft.com/library/windows/hardware/hh598281)セットの要求、拡張機能は以前の次のメンバーに一致するスイッチのプロパティを使用してプロビジョニングされている場合、 [ **NDIS\_切り替える\_プロパティ\_パラメーター** ](https://msdn.microsoft.com/library/windows/hardware/hh598238)または[ **NDIS\_スイッチ\_プロパティ\_削除\_パラメーター** ](https://msdn.microsoft.com/library/windows/hardware/hh598249)構造体。

    -   **PropertyType**メンバー スイッチのプロパティの型を指定します。

        **注**  NDIS 6.30 以降、のみのプロパティを切り替える**NdisSwitchPropertyTypeCustom**で指定された、 [ **NDIS\_切り替える\_プロパティ\_パラメーター** ](https://msdn.microsoft.com/library/windows/hardware/hh598238)または[ **NDIS\_スイッチ\_プロパティ\_削除\_パラメーター**](https://msdn.microsoft.com/library/windows/hardware/hh598249)構造体。

         

    -   **PropertyId**拡張機能を認識する独自の GUID 値を指定するメンバー。 この GUID 値も拡張可能スイッチのカスタム ポリシーのプロパティの形式を定義した独立系ソフトウェア ベンダー (ISV) によって作成されます。

        **注**  拡張可能スイッチのカスタム ポリシーのプロパティに含まれる、 [ **NDIS\_切り替える\_プロパティ\_カスタム**](https://msdn.microsoft.com/library/windows/hardware/hh598247)構造体。

         

-   拡張機能が更新する必要があるかどうか、またはスイッチ ポリシー一致の次のメンバーを削除、拡張機能は、これらの OID セット要求を処理する場合、 [ **NDIS\_切り替える\_プロパティ\_パラメーター**](https://msdn.microsoft.com/library/windows/hardware/hh598255)構造体。

    -   **PropertyVersion**拡張可能スイッチのポリシーのバージョンを指定するメンバー。

    -   **PropertyInstanceId**メンバーの拡張可能スイッチ ポリシー インスタンスを指定します。

    これらのメンバーの値を拡張機能が以前にプロビジョニングされてスイッチ ポリシーのプロパティが一致しない場合、拡張機能は、NDIS に OID セット要求を失敗する必要があります\_状態\_無効な\_パラメーター。 それ以外の場合、拡張機能が、OID セット要求を完了し、NDIS を返す必要があります\_状態\_成功します。

-   フィルター処理、または転送拡張機能は、追加、削除、またはスイッチのポリシーの更新プログラムを拒否できます。 拡張機能は状態が、OID 要求の完了によって\_データ\_いない\_ACCEPTED です。

    **注**  取得拡張機能の追加またはスイッチのポリシーの変更しない拒否する必要があります。 代わりに、拡張可能スイッチ コントロール パスに OID 要求に転送する必要があります。

     

-   キャプチャまたは拡張機能を正常にフィルター処理は、スイッチのカスタム ポリシーの OID のセット要求を処理する場合は OID 要求を完了する必要があり、拡張可能スイッチ コントロール パスに転送する必要があります。

    転送拡張機能は、スイッチのカスタム ポリシーの OID のセット要求を正常に処理する場合は、OID 要求を完了し、適切な NDIS を返すにする必要があります\_状態\_*Xxx*値。

-   呼び出す必要がありますが、拡張機能が、OID セット要求を完了しない場合[ **NdisFOidRequest** ](https://msdn.microsoft.com/library/windows/hardware/ff561830)拡張可能スイッチのドライバー スタック ダウン OID 要求を転送します。 この場合、拡張機能は、基になる拡張機能の OID 要求が失敗したかどうかを検出する OID の完了状態を監視する必要があります。

 

 





