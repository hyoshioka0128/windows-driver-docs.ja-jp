---
title: OID_SWITCH_PROPERTY_ENUM
description: HYPER-V 拡張可能なスイッチ、拡張機能の問題は、オブジェクト識別子 (OID) メソッドへの要求を OID_SWITCH_PROPERTY_ENUM の配列を取得します。
ms.assetid: 45277355-4486-4CE0-ACBF-68D6BC6B79E7
ms.date: 08/08/2017
keywords: -OID_SWITCH_PROPERTY_ENUM ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 6fbaa6e59eb4629788d1618762573ab6392a1bcb
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63327662"
---
# <a name="oidswitchpropertyenum"></a>OID\_スイッチ\_プロパティ\_列挙型


HYPER-V 拡張可能スイッチの拡張機能の OID オブジェクト識別子 (OID) メソッド要求の発行\_切り替える\_プロパティ\_列挙型の配列を取得します。 この配列には、指定した条件に一致するプロビジョニングされたスイッチ ポリシーが含まれます。 配列内の各要素には、拡張可能スイッチのポリシーのプロパティを指定します。

**InformationBuffer**のメンバー、 [ **NDIS\_OID\_要求**](https://msdn.microsoft.com/library/windows/hardware/ff566710)構造体には、バッファーへのポインターが含まれています。 このバッファーには、次のデータが含まれています。

-   [ **NDIS\_切り替える\_プロパティ\_ENUM\_パラメーター** ](https://msdn.microsoft.com/library/windows/hardware/hh598253)拡張可能スイッチのポリシーのパラメーターを指定する構造体列挙体です。

-   配列の[ **NDIS\_スイッチ\_プロパティ\_ENUM\_情報**](https://msdn.microsoft.com/library/windows/hardware/hh598250)構造体。 各構造体には、ポリシーを拡張可能スイッチに関する情報が含まれています。

    **注**  、拡張機能の設定、拡張機能が拡張可能スイッチを指定したポリシーのインスタンスにプロビジョニングされていない場合、 **NumProperties**のメンバー、 [ **NDIS\_スイッチ\_プロパティ\_ENUM\_パラメーター** ](https://msdn.microsoft.com/library/windows/hardware/hh598253)構造体を 0、no [ **NDIS\_スイッチ\_プロパティ\_ENUM\_情報**](https://msdn.microsoft.com/library/windows/hardware/hh598250)構造体が返されます。

     

<a name="remarks"></a>注釈
-------

OID\_切り替える\_プロパティ\_列挙型の OID は、HYPER-V 拡張可能スイッチには、アクティブ化が完了したときにのみ発行する必要があります。 参照してください[HYPER-V 拡張可能スイッチの構成を照会](https://msdn.microsoft.com/library/windows/hardware/hh598293)の詳細。

OID とは異なりは、クエリの要求[OID\_スイッチ\_ポート\_プロパティ\_ENUM](oid-switch-port-property-enum.md)、拡張機能をいずれかを呼び出す必要はありません*ReferenceSwitchXxx*または*DereferenceSwitchXxx* OID を発行するときに関数\_切り替える\_プロパティ\_拡張可能スイッチのドライバー スタック ダウン要求を列挙します。

**注**  、拡張機能は OID の OID メソッド要求を受け取るかどうか\_スイッチ\_プロパティ\_列挙型にする必要があります要求を完了できません、OID。 代わりに、呼び出す必要があります[ **NdisFOidRequest** ](https://msdn.microsoft.com/library/windows/hardware/ff561830)拡張可能スイッチのドライバー スタック ダウン OID 要求を転送します。

 

### <a name="return-status-codes"></a>リターン状態コード

拡張可能スイッチの基になるミニポート edge OID の OID のクエリ要求が完了すると\_切り替える\_プロパティ\_列挙し、次のステータス コードのいずれかを返します。

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
<td><p>返される情報バッファーの長さが小さすぎる、 <a href="https://msdn.microsoft.com/library/windows/hardware/hh598253" data-raw-source="[&lt;strong&gt;NDIS_SWITCH_PROPERTY_ENUM_PARAMETERS&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/hh598253)"> <strong>NDIS_SWITCH_PROPERTY_ENUM_PARAMETERS</strong> </a>構造とその配列の<a href="https://msdn.microsoft.com/library/windows/hardware/hh598250" data-raw-source="[&lt;strong&gt;NDIS_SWITCH_PROPERTY_ENUM_INFO&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/hh598250)"> <strong>NDIS_SWITCH_PROPERTY_ENUM_情報</strong></a>要素。 拡張可能スイッチのセットの基になるミニポート edge、<strong>データ。METHOD_INFORMATION します。BytesNeeded</strong>内のメンバー、 <a href="https://msdn.microsoft.com/library/windows/hardware/ff566710" data-raw-source="[&lt;strong&gt;NDIS_OID_REQUEST&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff566710)"> <strong>NDIS_OID_REQUEST</strong> </a>構造体に必要な最小バッファー サイズ。</p></td>
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

[**NDIS\_スイッチ\_プロパティ\_ENUM\_情報**](https://msdn.microsoft.com/library/windows/hardware/hh598250)

[**NDIS\_スイッチ\_プロパティ\_ENUM\_パラメーター**](https://msdn.microsoft.com/library/windows/hardware/hh598253)

[HYPER-V 拡張可能スイッチの構成のクエリを実行します。](https://msdn.microsoft.com/library/windows/hardware/hh598293)

 

 




