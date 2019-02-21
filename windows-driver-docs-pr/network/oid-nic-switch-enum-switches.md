---
title: OID_NIC_SWITCH_ENUM_SWITCHES
description: 上にあるドライバーまたはユーザー モード アプリケーションでは、配列を取得する OID_NIC_SWITCH_ENUM_SWITCHES のオブジェクト識別子 (OID) のクエリ要求を発行します。
ms.assetid: 706C3F1C-239F-4731-A38E-E150D26C79A5
ms.date: 08/08/2017
keywords: -OID_NIC_SWITCH_ENUM_SWITCHES ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 20213059153311ea49056c5b42b8b5f2855dd98e
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56550004"
---
# <a name="oidnicswitchenumswitches"></a>OID\_NIC\_スイッチ\_ENUM\_スイッチ


上にあるドライバーまたはユーザー モード アプリケーション OID のオブジェクト識別子 (OID) のクエリ要求を発行する\_NIC\_スイッチ\_ENUM\_スイッチ配列を取得します。 配列内の各要素には、ネットワーク アダプターで作成された NIC スイッチの属性を指定します。

この OID クエリ要求から正常に戻った後、 **InformationBuffer**のメンバー、 [ **NDIS\_OID\_要求**](https://msdn.microsoft.com/library/windows/hardware/ff566710)構造体以下を含むバッファーへのポインターが含まれます。

-   [ **NDIS\_NIC\_スイッチ\_情報\_配列**](https://msdn.microsoft.com/library/windows/hardware/hh451584)配列内の要素の数を定義する構造体。

-   配列の[ **NDIS\_NIC\_スイッチ\_情報**](https://msdn.microsoft.com/library/windows/hardware/hh451582)構造体。 各構造体には、ネットワーク アダプター上に作成する 1 つの NIC スイッチに関する情報が含まれています。

    **注**  NIC スイッチ、ネットワーク アダプターがない場合は、ドライバーの設定、 **NumElements**のメンバー、 [ **NDIS\_NIC\_スイッチ\_情報\_配列**](https://msdn.microsoft.com/library/windows/hardware/hh451584)構造体を 0、no [ **NDIS\_NIC\_スイッチ\_情報**](https://msdn.microsoft.com/library/windows/hardware/hh451582)構造体が返されます。

     

<a name="remarks"></a>注釈
-------

上にあるドライバーとユーザー モード アプリケーションは、OID の OID クエリ要求を発行\_NIC\_スイッチ\_ENUM\_ネットワーク アダプターで作成した NIC のスイッチを列挙するスイッチ。

**注**  以降 Windows Server 2012 では、シングル ルート I/O 仮想化 (SR-IOV) のインターフェイスに対してのみサポートして既定の NIC のスイッチ、ネットワーク アダプター。 そのため、返された[ **NDIS\_NIC\_スイッチ\_情報\_配列**](https://msdn.microsoft.com/library/windows/hardware/hh451584)構造体は、1 つを指定する必要があります[ **NDIS\_NIC\_切り替える\_情報**](https://msdn.microsoft.com/library/windows/hardware/hh451582) NDIS の識別子によって参照されている既定の NIC のスイッチの要素\_既定\_スイッチ\_ID。

 

### <a name="return-status-codes"></a>リターン状態コード

OID の OID のクエリ要求を処理する NDIS\_NIC\_スイッチ\_列挙\_ミニポート ドライバーのスイッチの要求。 ドライバーにはこの OID 要求が発行するされません。

NDIS が、OID を処理するときに\_NIC\_スイッチ\_ENUM\_スイッチ要求と、次のステータス コードの 1 つを返します。

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
<td><p>NDIS_STATUS_NOT_SUPPORTED</p></td>
<td><p>ミニポート ドライバーが SR-IOV 対応インターフェイスをサポートしないか、またはインターフェイスを使用して有効になっていません。</p></td>
</tr>
<tr class="odd">
<td><p>NDIS_STATUS_INVALID_PARAMETER</p></td>
<td><p>1 つ以上のメンバーの<a href="https://msdn.microsoft.com/library/windows/hardware/hh451577" data-raw-source="[&lt;strong&gt;NDIS_NIC_SWITCH_INFO_ARRAY&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/hh451577)"> <strong>NDIS_NIC_SWITCH_INFO_ARRAY</strong> </a>構造が無効な値を指定します。</p></td>
</tr>
<tr class="even">
<td><p>NDIS_STATUS_INVALID_LENGTH</p></td>
<td><p>情報バッファーが小さすぎます。 NDIS セット、<strong>データ。QUERY_INFORMATION します。BytesNeeded</strong>内のメンバー、 <a href="https://msdn.microsoft.com/library/windows/hardware/ff566710" data-raw-source="[&lt;strong&gt;NDIS_OID_REQUEST&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff566710)"> <strong>NDIS_OID_REQUEST</strong> </a>構造体に必要な最小バッファー サイズ。</p></td>
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
[**NDIS\_NIC\_スイッチ\_情報**](https://msdn.microsoft.com/library/windows/hardware/hh451582)

[**NDIS\_NIC\_スイッチ\_情報\_配列**](https://msdn.microsoft.com/library/windows/hardware/hh451584)

[**NDIS\_OID\_要求**](https://msdn.microsoft.com/library/windows/hardware/ff566710)

[OID\_NIC\_スイッチ\_作成\_スイッチ](oid-nic-switch-create-switch.md)

[OID\_NIC\_SWITCH\_PARAMETERS](oid-nic-switch-parameters.md)

 

 




