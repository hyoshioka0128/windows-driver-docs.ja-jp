---
title: OID_SWITCH_PORT_PROPERTY_ENUM
description: HYPER-V 拡張可能なスイッチ、拡張機能の問題は、オブジェクト識別子 (OID) メソッドへの要求を OID_SWITCH_PORT_PROPERTY_ENUM の配列を取得します。
ms.assetid: 5C391B82-FCA6-4A95-992F-EDB5DF6183C7
ms.date: 08/08/2017
keywords: -OID_SWITCH_PORT_PROPERTY_ENUM ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: e997fd31f419cd448813a8cb7ebdb15d7a7dc64c
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63343264"
---
# <a name="oidswitchportpropertyenum"></a>OID\_スイッチ\_ポート\_プロパティ\_列挙型


HYPER-V 拡張可能スイッチの拡張機能の OID オブジェクト識別子 (OID) メソッド要求の発行\_切り替える\_ポート\_プロパティ\_列挙型の配列を取得します。 この配列には、指定した条件に一致するポートがプロビジョニングされているポリシーが含まれます。 配列内の各要素には、指定した拡張可能スイッチ ポートのポリシーのプロパティを指定します。

**InformationBuffer**のメンバー、 [ **NDIS\_OID\_要求**](https://msdn.microsoft.com/library/windows/hardware/ff566710)構造体には、バッファーへのポインターが含まれています。 このバッファーには、次のデータが含まれています。

-   [ **NDIS\_スイッチ\_ポート\_プロパティ\_ENUM\_パラメーター** ](https://msdn.microsoft.com/library/windows/hardware/hh598236)ポリシーのパラメーターを指定する構造体指定したポートの列挙体。

-   配列の[ **NDIS\_スイッチ\_ポート\_プロパティ\_ENUM\_情報**](https://msdn.microsoft.com/library/windows/hardware/hh598233)構造体。 各構造体には、拡張可能スイッチ ポートのポリシーのプロパティに関する情報が含まれています。

    **注**  場合、 **NumProperties**のメンバー、 [ **NDIS\_スイッチ\_ポート\_プロパティ\_ENUM\_パラメーター** ](https://msdn.microsoft.com/library/windows/hardware/hh598236)構造が 0、no に設定されている[ **NDIS\_スイッチ\_ポート\_プロパティ\_ENUM\_情報** ](https://msdn.microsoft.com/library/windows/hardware/hh598233)構造体が返されます。

     

<a name="remarks"></a>注釈
-------

OID の OID メソッドの要求を発行する前に\_切り替える\_ポート\_プロパティ\_列挙型、拡張可能スイッチ拡張機能には、次のガイドラインが従う必要があります。

-   拡張機能では、OID を発行できるのみ\_切り替える\_ポート\_プロパティ\_拡張可能スイッチに関する問題のプロトコルのエッジの後の列挙要求、 [OID\_切り替える\_ポート\_作成](oid-switch-port-create.md)要求を発行する前に、 [OID\_スイッチ\_ポート\_破棄](oid-switch-port-teardown.md)要求。

-   拡張機能を呼び出す必要があります[ *ReferenceSwitchPort* ](https://msdn.microsoft.com/library/windows/hardware/hh598295)を呼び出す前に[ **NdisFOidRequest** ](https://msdn.microsoft.com/library/windows/hardware/ff561830) OID を発行する\_スイッチ\_ポート\_プロパティ\_列挙型の要求。 これにより、指定したポートが削除されないことまで、OID 要求が完了した後。

    拡張機能を呼び出す必要があります、OID 要求が完了すると、 [ *DereferenceSwitchPort*](https://msdn.microsoft.com/library/windows/hardware/hh598142)します。 拡張機能は、NDIS に OID 要求が完了したかどうかに関係なく、この関数を呼び出す必要があります\_状態\_成功します。

OID\_切り替える\_ポート\_プロパティ\_列挙型の OID は、HYPER-V 拡張可能スイッチには、アクティブ化が完了したときにのみ発行する必要があります。 参照してください[HYPER-V 拡張可能スイッチの構成を照会](https://msdn.microsoft.com/library/windows/hardware/hh598293)の詳細。

**注**  、拡張機能は OID の OID メソッド要求を受け取るかどうか\_スイッチ\_ポート\_プロパティ\_列挙型にする必要があります要求を完了できません、OID。 代わりに、呼び出す必要があります[ **NdisFOidRequest** ](https://msdn.microsoft.com/library/windows/hardware/ff561830)拡張可能スイッチのドライバー スタック ダウン OID 要求を転送します。

 

### <a name="return-status-codes"></a>リターン状態コード

拡張可能スイッチの基になるミニポート edge OID の OID のクエリ要求が完了すると\_切り替える\_ポート\_プロパティ\_列挙し、次のステータス コードを返します。

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
[*DereferenceSwitchPort*](https://msdn.microsoft.com/library/windows/hardware/hh598142)

[**NDIS\_OID\_要求**](https://msdn.microsoft.com/library/windows/hardware/ff566710)

[**NDIS\_スイッチ\_ポート\_プロパティ\_ENUM\_情報**](https://msdn.microsoft.com/library/windows/hardware/hh598233)

[**NDIS\_スイッチ\_ポート\_プロパティ\_ENUM\_パラメーター**](https://msdn.microsoft.com/library/windows/hardware/hh598236)

[**NdisFOidRequest**](https://msdn.microsoft.com/library/windows/hardware/ff561830)

[HYPER-V 拡張可能スイッチの構成のクエリを実行します。](https://msdn.microsoft.com/library/windows/hardware/hh598293)

[*ReferenceSwitchPort*](https://msdn.microsoft.com/library/windows/hardware/hh598295)

 

 




