---
title: カスタム ポート機能の状態情報を管理します。
description: カスタム ポート機能の状態情報を管理します。
ms.assetid: C989888B-1636-488A-80BF-13D136312417
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 372388340c148149f2f49d03150fa969abae1bd0
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56538338"
---
# <a name="managing-custom-port-feature-status-information"></a>カスタム ポート機能の状態情報を管理します。


HYPER-V 拡張可能スイッチのインターフェイスは、拡張可能スイッチ ポートのカスタム状態情報を照会する次のオブジェクト識別子 (OID) を使用します。 この状態情報と呼ばれる*機能の状態をポート*情報。

<a href="" id="oid-switch-port-feature-status-query"></a>[OID\_スイッチ\_ポート\_機能\_状態\_クエリ](https://msdn.microsoft.com/library/windows/hardware/hh598274)  
指定したポートのプロパティのカスタム機能の状態情報を取得する拡張可能スイッチのプロトコルの端では、この OID メソッド要求が発行されます。

この OID メソッド要求から正常に戻った後、 **InformationBuffer**のメンバー、 [ **NDIS\_OID\_要求**](https://msdn.microsoft.com/library/windows/hardware/ff566710)構造体バッファーへのポインターが含まれています。 このバッファーには、次のデータが含まれています。

-   [ **NDIS\_スイッチ\_ポート\_機能\_状態\_パラメーター** ](https://msdn.microsoft.com/library/windows/hardware/hh598227)カスタム機能の状態を指定する構造体返される情報。

    **注**  カスタム機能のステータスには、 **FeatureStatusType**に設定されているメンバー **NdisSwitchPortPropertyTypeCustom**。

     

-   [ **NDIS\_スイッチ\_ポート\_機能\_状態\_カスタム**](https://msdn.microsoft.com/library/windows/hardware/hh598226)に関する状態情報を格納する構造体、拡張可能スイッチ ポートに割り当てられているカスタム プロパティです。

    拡張可能スイッチのプロトコルの端を発行したとき、 [OID\_切り替える\_ポート\_機能\_状態\_クエリ](https://msdn.microsoft.com/library/windows/hardware/hh598274)要求と、設定、 **FeatureStatusCustomBufferLength**と**FeatureStatusCustomBufferOffset**メンバー内の場所に、 **InformationBuffer**拡張機能の使用時に使用できるメンバー機能の状態情報を返します。

拡張可能スイッチ拡張機能は、の OID メソッド要求を受け取ったときにこれらのガイドラインに従う必要があります[OID\_切り替える\_ポート\_機能\_状態\_クエリ](https://msdn.microsoft.com/library/windows/hardware/hh598274):

-   一致するカスタムの拡張可能なスイッチ ポートのプロパティを管理する場合、拡張機能は、OID 要求を処理する必要があります、 **FeatureStatusId**のメンバー、 [ **NDIS\_切り替える\_ポート\_機能\_状態\_パラメーター** ](https://msdn.microsoft.com/library/windows/hardware/hh598227)構造体。

-   によって指定されたパラメーターに一致する機能の状態情報を返す必要があります、拡張機能は、OID メソッド要求を処理する場合、 [ **NDIS\_スイッチ\_ポート\_機能\_状態\_パラメーター** ](https://msdn.microsoft.com/library/windows/hardware/hh598227)構造体。

    拡張機能で NDIS OID 要求は失敗する必要があります機能の状態のバッファーが小さすぎる場合\_状態\_無効な\_長さ。 拡張機能を設定する必要があります、**データ。設定\_情報。BytesNeeded**内のメンバー、 [ **NDIS\_OID\_要求**](https://msdn.microsoft.com/library/windows/hardware/ff566710)構造体に必要な最小バッファー サイズ。

    それ以外の場合、拡張機能が機能の状態情報を取得し、NDIS に OID 要求を完了する必要があります\_状態\_成功します。

-   呼び出す必要がありますが、拡張機能が拡張可能スイッチのカスタム プロパティを管理しない場合は[ **NdisFOidRequest** ](https://msdn.microsoft.com/library/windows/hardware/ff561830)拡張可能スイッチのドライバー スタック ダウン OID 要求を転送します。

    OID 要求を転送する方法の詳細については、[NDIS フィルター ドライバーでの OID 要求のフィルタ リング](filtering-oid-requests-in-an-ndis-filter-driver.md)を参照してください。

詳細を定義し、ポート機能の状態情報を登録する方法については、[カスタム ポート機能の状態](custom-port-feature-status.md)を参照してください。

 

 





