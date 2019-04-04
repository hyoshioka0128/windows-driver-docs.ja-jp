---
title: カスタム スイッチ機能の状態情報の管理
description: カスタム スイッチ機能の状態情報の管理
ms.assetid: A1D561CC-22D8-47B6-9D95-6294B2998F3E
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 228382aab92f39c7b72a618ec782ffc5bb9365c5
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56571128"
---
# <a name="managing-custom-switch-feature-status-information"></a>カスタム スイッチ機能の状態情報の管理


HYPER-V 拡張可能スイッチのインターフェイスは、拡張可能スイッチのカスタム状態情報を照会する次のオブジェクト識別子 (OID) を使用します。 この状態情報と呼ばれる*機能の状態を切り替える*情報。

<a href="" id="oid-switch-feature-status-query"></a>[OID\_スイッチ\_機能\_状態\_クエリ](https://msdn.microsoft.com/library/windows/hardware/hh598260)  
指定されたスイッチのプロパティのカスタム機能の状態情報を取得する拡張可能スイッチのプロトコルの端でこの OID メソッド要求が発行されます。

この OID メソッド要求から正常に戻った後、 **InformationBuffer**のメンバー、 [ **NDIS\_OID\_要求**](https://msdn.microsoft.com/library/windows/hardware/ff566710)構造体バッファーへのポインターが含まれています。 このバッファーには、次のデータが含まれています。

-   [ **NDIS\_スイッチ\_機能\_状態\_パラメーター** ](https://msdn.microsoft.com/library/windows/hardware/hh598208)されるカスタム機能の状態情報を指定する構造体返されます。

    **注**  カスタム機能のステータスには、 **FeatureStatusType**に設定されているメンバー **NdisSwitchPropertyTypeCustom**。

     

-   [ **NDIS\_スイッチ\_機能\_状態\_カスタム**](https://msdn.microsoft.com/library/windows/hardware/hh598207)構造に割り当てられているカスタム プロパティに関する状態情報を含む、拡張可能スイッチ ポート。

    拡張可能スイッチのプロトコルの端を発行したとき、 [OID\_切り替える\_機能\_状態\_クエリ](https://msdn.microsoft.com/library/windows/hardware/hh598260)要求と、設定、 **FeatureStatusCustomBufferLength**と**FeatureStatusCustomBufferOffset**メンバー内の場所に、 **InformationBuffer**拡張機能の使用時に使用できるメンバー機能の状態情報を返します。

拡張可能スイッチ拡張機能は、の OID メソッド要求を受け取ったときにこれらのガイドラインに従う必要があります[OID\_切り替える\_機能\_状態\_クエリ](https://msdn.microsoft.com/library/windows/hardware/hh598260):

-   一致するカスタムの拡張可能スイッチ機能の状態を管理する場合、拡張機能は、OID 要求を処理する必要があります、 **FeatureStatusId**のメンバー、 [ **NDIS\_切り替える\_機能\_状態\_パラメーター** ](https://msdn.microsoft.com/library/windows/hardware/hh598208)構造体。

-   によって指定されたパラメーターに一致する機能の状態情報を返す必要があります、拡張機能は、OID メソッド要求を処理する場合、 [ **NDIS\_スイッチ\_機能\_状態\_パラメーター** ](https://msdn.microsoft.com/library/windows/hardware/hh598208)構造体。

    拡張機能で NDIS OID 要求は失敗する必要があります機能の状態のバッファーが小さすぎる場合\_状態\_無効な\_長さ。 拡張機能を設定する必要があります、**データ。設定\_情報。BytesNeeded**内のメンバー、 [ **NDIS\_OID\_要求**](https://msdn.microsoft.com/library/windows/hardware/ff566710)構造体に必要な最小バッファー サイズ。

    それ以外の場合、拡張機能が機能の状態情報を取得し、NDIS に OID 要求を完了する必要があります\_状態\_成功します。

-   呼び出す必要がありますが、拡張機能が拡張可能スイッチのカスタム機能の状態を管理しない場合は[ **NdisFOidRequest** ](https://msdn.microsoft.com/library/windows/hardware/ff561830)拡張可能スイッチのドライバー スタック ダウン OID 要求を転送します。

    OID 要求を転送する方法の詳細については、[NDIS フィルター ドライバーでの OID 要求のフィルタ リング](filtering-oid-requests-in-an-ndis-filter-driver.md)を参照してください。

詳細を定義し、スイッチ機能の状態情報を登録する方法については、[スイッチ機能の状態のカスタム](custom-switch-feature-status.md)を参照してください。

 

 





