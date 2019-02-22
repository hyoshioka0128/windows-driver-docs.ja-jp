---
title: OID_SWITCH_NIC_ARRAY
description: HYPER-V 拡張可能なスイッチ、拡張機能の問題は、オブジェクト識別子 (OID) のクエリ要求を OID_SWITCH_NIC_ARRAY の配列を取得します。
ms.assetid: CA9958DF-4389-4B4F-B110-03F500E27A1B
ms.date: 08/08/2017
keywords: -OID_SWITCH_NIC_ARRAY ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 1e1e53c4320b7e77ae90f56e356aa0998428cc07
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56557683"
---
# <a name="oidswitchnicarray"></a>OID\_スイッチ\_NIC\_配列


HYPER-V 拡張可能スイッチの拡張機能の OID オブジェクト識別子 (OID) のクエリ要求を発行する\_切り替える\_NIC\_配列が配列を取得します。 配列内の各要素には、拡張可能スイッチ ポートに関連付けられている仮想ネットワーク アダプターの構成パラメーターを指定します。

OID のクエリ要求が正常に完了した場合、 **InformationBuffer**のメンバー、 [ **NDIS\_OID\_要求**](https://msdn.microsoft.com/library/windows/hardware/ff566710)構造体バッファーへのポインターが含まれています。 このバッファーには、次のデータが含まれています。

-   [ **NDIS\_スイッチ\_NIC\_配列**](https://msdn.microsoft.com/library/windows/hardware/hh598212)配列内の要素の数を定義する構造体。 この構造体には、配列内の最初の要素へのオフセットも指定します。

-   配列の[ **NDIS\_スイッチ\_NIC\_パラメーター** ](https://msdn.microsoft.com/library/windows/hardware/hh598215)構造体。 各構造体には、拡張可能スイッチ ポートに接続されているネットワーク アダプターに関する情報が含まれています。

    **注**  拡張可能スイッチ ポートにネットワーク アダプターが接続されていない場合、拡張可能スイッチの基になるミニポート edge の設定、 **NumElements**のメンバー、 [ **NDIS\_スイッチ\_NIC\_配列**](https://msdn.microsoft.com/library/windows/hardware/hh598212)構造体をゼロにします。 この場合、ありません[ **NDIS\_スイッチ\_NIC\_パラメーター** ](https://msdn.microsoft.com/library/windows/hardware/hh598215)構造体が返されます。

     

<a name="remarks"></a>注釈
-------

OID\_切り替える\_NIC\_配列 OID は、HYPER-V 拡張可能スイッチには、アクティブ化が完了したときにのみ発行する必要があります。 参照してください[HYPER-V 拡張可能スイッチの構成を照会](https://msdn.microsoft.com/library/windows/hardware/hh598293)の詳細。

拡張機能が、返された処理と[ **NDIS\_スイッチ\_NIC\_パラメーター** ](https://msdn.microsoft.com/library/windows/hardware/hh598215)構造にする必要がありますわけでは、のメンバーの文字列、さまざまなこと[**NDIS\_スイッチ\_ポート\_パラメーター** ](https://msdn.microsoft.com/library/windows/hardware/hh598229)構造体など**NicFriendlyName**NULL で終わるされます。 これらの文字列型のメンバーのデータ型は、型定義、 [**場合\_カウント済\_文字列**](https://msdn.microsoft.com/library/windows/hardware/hh451419)構造体。 ドライバーの値から文字列の長さを決定する必要があります、**長さ**この構造体のメンバー。

**注**  文字列が null で終わる場合、**長さ**メンバーは、終端の null 文字を含めることはできません。

 

### <a name="return-status-codes"></a>リターン状態コード

拡張可能スイッチの基になるミニポート edge OID の OID のクエリ要求が完了すると\_切り替える\_NIC\_配列と、次のステータス コードの 1 つを返します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>状態コード</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>NDIS_STATUS_SUCCESS</p></td>
<td><p>OID 要求は正常に完了しました。</p></td>
</tr>
<tr class="even">
<td><p>NDIS_STATUS_INVALID_LENGTH</p></td>
<td><p>返される情報バッファーの長さが小さすぎる、 <a href="https://msdn.microsoft.com/library/windows/hardware/hh598212" data-raw-source="[&lt;strong&gt;NDIS_SWITCH_NIC_ARRAY&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/hh598212)"> <strong>NDIS_SWITCH_NIC_ARRAY</strong> </a>とその配列の<a href="https://msdn.microsoft.com/library/windows/hardware/hh598215" data-raw-source="[&lt;strong&gt;NDIS_SWITCH_NIC_PARAMETERS&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/hh598215)"> <strong>NDIS_SWITCH_NIC_PARAMETERS</strong> </a>要素。 拡張可能スイッチのセットの基になるミニポート edge、<strong>データ。QUERY_INFORMATION します。BytesNeeded</strong>内のメンバー、 <a href="https://msdn.microsoft.com/library/windows/hardware/ff566710" data-raw-source="[&lt;strong&gt;NDIS_OID_REQUEST&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff566710)"> <strong>NDIS_OID_REQUEST</strong> </a>構造体に必要な最小バッファー サイズ。</p></td>
</tr>
<tr class="odd">
<td><p>NDIS_STATUS_FAILURE</p></td>
<td><p>他の理由から、要求が失敗しました。</p></td>
</tr>
</tbody>
</table>

 

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
<td><p>NDIS 6.30 以降をサポートします。</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Ntddndis.h (include Ndis.h)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


****
[**NDIS\_OID\_要求**](https://msdn.microsoft.com/library/windows/hardware/ff566710)

[**NDIS\_スイッチ\_NIC\_配列**](https://msdn.microsoft.com/library/windows/hardware/hh598212)

[**NDIS\_SWITCH\_NIC\_PARAMETERS**](https://msdn.microsoft.com/library/windows/hardware/hh598215)

[HYPER-V 拡張可能スイッチの構成のクエリを実行します。](https://msdn.microsoft.com/library/windows/hardware/hh598293)

 

 




