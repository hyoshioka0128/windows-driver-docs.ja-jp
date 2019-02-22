---
title: OID_SWITCH_PARAMETERS
description: HYPER-V 拡張可能スイッチの拡張機能は、拡張可能スイッチの構成データを取得する OID_SWITCH_PARAMETERS のオブジェクト識別子 (OID) のクエリ要求を発行します。
ms.assetid: F2CA0BE5-ED21-4ACF-B26A-4F512D4B15C7
ms.date: 08/08/2017
keywords: -OID_SWITCH_PARAMETERS ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: f18f4fd53d3d9fbe16ef9b289499acc31d859ff9
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56529938"
---
# <a name="oidswitchparameters"></a>OID\_スイッチ\_パラメーター


HYPER-V 拡張可能スイッチの拡張機能の OID オブジェクト識別子 (OID) のクエリ要求を発行する\_切り替える\_拡張可能スイッチの構成データを取得するパラメーター。

OID のクエリ要求が正常に完了した場合、 **InformationBuffer**のメンバー、 [ **NDIS\_OID\_要求**](https://msdn.microsoft.com/library/windows/hardware/ff566710)構造が含まれていますポインター、 [ **NDIS\_スイッチ\_パラメーター** ](https://msdn.microsoft.com/library/windows/hardware/hh598220)構造体。

<a name="remarks"></a>注釈
-------

拡張機能が、返された処理と[ **NDIS\_スイッチ\_パラメーター** ](https://msdn.microsoft.com/library/windows/hardware/hh598220)構造にする必要がありますを想定のメンバーの文字列、さまざまなこと、 **NDIS\_スイッチ\_パラメーター**構造体など**SwitchName**null で終わるされます。 これらの文字列型のメンバーのデータ型は、型定義、 [**場合\_カウント済\_文字列**](https://msdn.microsoft.com/library/windows/hardware/hh451419)構造体。 拡張機能の値から文字列の長さを決定する必要があります、**長さ**この構造体のメンバー。

**注**  文字列が null で終わる場合、**長さ**メンバーは、終端の null 文字を含めることはできません。

 

### <a name="return-status-codes"></a>リターン状態コード

拡張可能スイッチの基になるミニポート edge OID の OID のクエリ要求が完了すると\_切り替える\_パラメーターと、次のステータス コードの 1 つを返します。

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
<td><p>OID のクエリ要求 OID_SWITCH_PARAMETERS 構造を返し、情報バッファーの長さが小さすぎます。 拡張可能スイッチのセットの基になるミニポート edge、<strong>データ。QUERY_INFORMATION します。BytesNeeded</strong>内のメンバー、 <a href="https://msdn.microsoft.com/library/windows/hardware/ff566710" data-raw-source="[&lt;strong&gt;NDIS_OID_REQUEST&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff566710)"> <strong>NDIS_OID_REQUEST</strong> </a>構造体に必要な最小バッファー サイズ。</p></td>
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

[**NDIS\_スイッチ\_パラメーター**](https://msdn.microsoft.com/library/windows/hardware/hh598220)

[**NdisFOidRequest**](https://msdn.microsoft.com/library/windows/hardware/ff561830)

 

 




