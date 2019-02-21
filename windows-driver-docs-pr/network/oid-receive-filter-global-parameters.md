---
title: OID_RECEIVE_FILTER_GLOBAL_PARAMETERS
description: 上にあるドライバーでは、グローバルを取得する OID_RECEIVE_FILTER_GLOBAL_PARAMETERS の要求がネットワーク アダプターのフィルターのパラメーターを受け取る OID クエリを発行します。
ms.assetid: be6f7210-d1f9-4490-838a-806488df41da
ms.date: 08/08/2017
keywords: -OID_RECEIVE_FILTER_GLOBAL_PARAMETERS ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 6e84ea157bbe706ea834a065ef594604595bde00
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56560866"
---
# <a name="oidreceivefilterglobalparameters"></a>OID\_受信\_フィルター\_GLOBAL\_パラメーター


上にあるドライバーは、OID の OID クエリ要求を発行\_受信\_フィルター\_GLOBAL\_グローバルを取得するパラメーターは、ネットワーク アダプターのフィルターのパラメーターを受信します。

OID のクエリ要求から正常に戻った後、 **InformationBuffer**のメンバー、 [ **NDIS\_OID\_要求**](https://msdn.microsoft.com/library/windows/hardware/ff566710)構造体ポインターが含まれています、 [ **NDIS\_受信\_フィルター\_GLOBAL\_パラメーター** ](https://msdn.microsoft.com/library/windows/hardware/ff567171)構造体。

<a name="remarks"></a>注釈
-------

NDIS フィルターが表示される次の NDIS インターフェイスで使用されます。

-   [NDIS パケット結合](https://msdn.microsoft.com/library/windows/hardware/hh451601)します。 使用する方法の詳細についてはこのインターフェイスでフィルターが表示されるを参照してください[管理パケット結合受信フィルター](https://msdn.microsoft.com/library/windows/hardware/hh464026)します。

-   [シングル ルート I/O 仮想化 (SR-IOV)](https://msdn.microsoft.com/library/windows/hardware/hh440235)します。 使用する方法の詳細についてはこのインターフェイスでフィルターが表示されるを参照してください[仮想ポートで受信フィルターを設定](https://msdn.microsoft.com/library/windows/hardware/hh440224)します。

-   [バーチャル マシン キュー (VMQ)](https://msdn.microsoft.com/library/windows/hardware/ff571035)。 使用する方法の詳細についてはこのインターフェイスでフィルターが表示されるを参照してください[設定および VMQ のフィルターをクリアする](https://msdn.microsoft.com/library/windows/hardware/ff570780)します。

プロトコル ドライバー以降 NDIS 6.20 が動作では、OID を使用\_受信\_フィルター\_GLOBAL\_パラメーターの現在のグローバル構成パラメーターをクエリには、ネットワーク アダプターでフィルター処理を受信します。 プロトコル ドライバーがこの OID を使用して、受信の種類をフィルター処理するかどうかを判断または受信するなど、キューを有効または無効にします。

### <a name="return-status-codes"></a>リターン状態コード

OID の OID のクエリ要求を処理する NDIS\_受信\_フィルター\_GLOBAL\_ミニポート ドライバー、および次のステータス コードを返します。 1 つのパラメーター。

<a href="" id="ndis-status-success"></a>NDIS\_状態\_成功  
要求は正常に完了しました。

<a href="" id="ndis-status-pending"></a>NDIS\_状態\_PENDING  
完了待ちになっています。 NDIS 渡します最終的な状態コードと結果を呼び出し元の OID 要求の完了ハンドラーに要求が完了した後。

<a href="" id="ndis-status-invalid-length"></a>NDIS\_状態\_無効な\_長さ  
情報バッファーが小さすぎます。 NDIS セット、**データ。クエリ\_情報。BytesNeeded**内のメンバー、 [ **NDIS\_OID\_要求**](https://msdn.microsoft.com/library/windows/hardware/ff566710)構造体に必要な最小バッファー サイズ。

<a href="" id="ndis-status-invalid-parameter"></a>NDIS\_状態\_無効な\_パラメーター  
基になるネットワーク アダプターがサポートされていない機能を有効にしようとした要求が失敗しました。

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

[**NDIS\_RECEIVE\_FILTER\_GLOBAL\_PARAMETERS**](https://msdn.microsoft.com/library/windows/hardware/ff567171)

 

 




