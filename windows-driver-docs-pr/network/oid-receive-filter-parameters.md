---
title: OID_RECEIVE_FILTER_PARAMETERS
description: 上にある、ドライバーは、ネットワーク アダプターでのフィルターの現在の構成パラメーターを取得する OID_RECEIVE_FILTER_PARAMETERS の OID メソッド要求を発行します。
ms.assetid: 1bb12945-0dad-47b9-9f44-e05efe292979
ms.date: 08/08/2017
keywords: -OID_RECEIVE_FILTER_PARAMETERS ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 17503b1d9edc9b54073ddf6c2032b01e129b0bdb
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63362566"
---
# <a name="oidreceivefilterparameters"></a>OID\_受信\_フィルター\_パラメーター


OID の OID メソッド要求を発行する上位のドライバー\_受信\_フィルター\_ネットワーク アダプターでのフィルターの現在の構成パラメーターを取得するパラメーター。

**InformationBuffer**のメンバー、 [ **NDIS\_OID\_要求**](https://msdn.microsoft.com/library/windows/hardware/ff566710)構造体にはへのポインターが含まれています、 [ **NDIS\_受信\_フィルター\_パラメーター** ](https://msdn.microsoft.com/library/windows/hardware/ff567181)構造体。 NDIS を使用して、 **FilterId**入力構造で、フィルターを特定のメンバー。

OID メソッドの要求から正常に戻った後、 **InformationBuffer**のメンバー、 [ **NDIS\_OID\_要求**](https://msdn.microsoft.com/library/windows/hardware/ff566710)構造体バッファーへのポインターが含まれています。 このバッファーは、以下を格納する形式です。

-   [ **NDIS\_受信\_フィルター\_パラメーター** ](https://msdn.microsoft.com/library/windows/hardware/ff567181) NDIS のパラメーターを指定する構造体は、フィルターを受信します。

-   配列の[ **NDIS\_受信\_フィルター\_フィールド\_パラメーター** ](https://msdn.microsoft.com/library/windows/hardware/ff567169)フィルターを指定する構造体のフィールドの条件をテストします。ネットワーク パケットのヘッダー。

<a name="remarks"></a>注釈
-------

NDIS フィルターが表示される次の NDIS インターフェイスで使用されます。

-   [NDIS パケット結合](https://msdn.microsoft.com/library/windows/hardware/hh451601)します。 使用する方法の詳細についてはこのインターフェイスでフィルターが表示されるを参照してください[管理パケット結合受信フィルター](https://msdn.microsoft.com/library/windows/hardware/hh464026)します。

-   [シングル ルート I/O 仮想化 (SR-IOV)](https://msdn.microsoft.com/library/windows/hardware/hh440235)します。 使用する方法の詳細についてはこのインターフェイスでフィルターが表示されるを参照してください[仮想ポートで受信フィルターを設定](https://msdn.microsoft.com/library/windows/hardware/hh440224)します。

-   [バーチャル マシン キュー (VMQ)](https://msdn.microsoft.com/library/windows/hardware/ff571035)。 使用する方法の詳細についてはこのインターフェイスでフィルターが表示されるを参照してください[設定および VMQ のフィルターをクリアする](https://msdn.microsoft.com/library/windows/hardware/ff570780)します。

上にあるドライバーは、OID の OID メソッド要求を発行\_受信\_フィルター\_パラメーターをネットワーク アダプターに設定された受信フィルターの構成パラメーターを取得します。 これには、VMQ の受信キューまたは SR-IOV 仮想ポート (VPort) に設定された受信フィルターとミニポート ドライバーにダウンロードされたパケットの結合フィルターが含まれます。

上にあるドライバーから以前の OID メソッド要求のフィルターの識別子を取得した[OID\_受信\_フィルター\_設定\_フィルター](oid-receive-filter-set-filter.md)またはの OID 要求から[OID\_受信\_フィルター\_ENUM\_フィルター](oid-receive-filter-enum-filters.md)します。

### <a name="return-status-codes"></a>リターン状態コード

OID の OID 要求を処理する NDIS\_受信\_フィルター\_ミニポート ドライバー、および次のステータス コードを返します。 1 つのパラメーター。

<a href="" id="ndis-status-success"></a>NDIS\_状態\_成功  
要求は正常に完了しました。 **InformationBuffer**を指す、 [ **NDIS\_受信\_フィルター\_パラメーター** ](https://msdn.microsoft.com/library/windows/hardware/ff567181)構造体。

<a href="" id="ndis-status-pending"></a>NDIS\_状態\_PENDING  
完了待ちになっています。 NDIS 渡します最終的な状態コードと結果を呼び出し元の OID 要求の完了ハンドラーに要求が完了した後。

<a href="" id="ndis-status-invalid-parameter"></a>NDIS\_状態\_無効な\_パラメーター  
上にあるドライバーやアプリケーションには、無効なフィルターの識別子が用意されています。 未定義のフィルターを指定する場合または 0 の場合は、フィルター id が無効です。

<a href="" id="ndis-status-invalid-length"></a>NDIS\_状態\_無効な\_長さ  
情報バッファーが小さすぎます。 NDIS セット、**データ。クエリ\_情報。BytesNeeded**内のメンバー、 [ **NDIS\_OID\_要求**](https://msdn.microsoft.com/library/windows/hardware/ff566710)構造体に必要な最小バッファー サイズ。

<a href="" id="ndis-status-failure"></a>NDIS\_状態\_エラー  
他の理由から、要求が失敗しました。

<a name="requirements"></a>要件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>バージョン</p></td>
<td><p>以降では、NDIS 6.20 が動作をサポートします。</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Ntddndis.h (include Ndis.h)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**NDIS\_OID\_要求**](https://msdn.microsoft.com/library/windows/hardware/ff566710)

[OID\_受信\_フィルター\_ENUM\_フィルター](oid-receive-filter-enum-filters.md)

[**NDIS\_受信\_フィルター\_パラメーター**](https://msdn.microsoft.com/library/windows/hardware/ff567181)

[OID\_受信\_フィルター\_設定\_フィルター](oid-receive-filter-set-filter.md)

 

 




