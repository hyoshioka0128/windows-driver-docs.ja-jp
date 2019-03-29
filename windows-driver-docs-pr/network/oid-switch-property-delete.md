---
title: OID_SWITCH_PROPERTY_DELETE
description: HYPER-V 拡張可能スイッチのプロトコルのエッジは、スイッチのポリシーのプロパティの削除についての拡張可能スイッチの拡張機能を通知する OID_SWITCH_PROPERTY_DELETE のオブジェクト識別子 (OID) セット要求を発行します。
ms.assetid: 55291392-C018-4578-9767-DC5621F75D44
ms.date: 08/08/2017
keywords: -OID_SWITCH_PROPERTY_DELETE ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: a4226e27db36186919dbd6afd7c4e14c1b5e55e4
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56579869"
---
# <a name="oidswitchpropertydelete"></a>OID\_スイッチ\_プロパティ\_削除


HYPER-V 拡張可能スイッチのプロトコルのエッジの OID オブジェクト識別子 (OID) セット要求を発行する\_切り替える\_プロパティ\_スイッチ ポリシーのプロパティの削除に関する拡張機能を拡張可能スイッチに通知を削除します。

**InformationBuffer**のメンバー、 [ **NDIS\_OID\_要求**](https://msdn.microsoft.com/library/windows/hardware/ff566710)構造には、を格納しているバッファーへのポインターが含まれる[ **NDIS\_スイッチ\_プロパティ\_削除\_パラメーター** ](https://msdn.microsoft.com/library/windows/hardware/hh598249)構造体。

<a name="remarks"></a>コメント
-------

転送拡張機能は、OID の OID のセット要求を処理できる\_スイッチ\_プロパティ\_を削除します。 その他のすべての種類の拡張機能を呼び出す必要があります[ **NdisFOidRequest** ](https://msdn.microsoft.com/library/windows/hardware/ff561830)拡張可能スイッチのドライバー スタックで、[次へ] の拡張機能に OID 要求を転送します。

OID を処理する方法に関するガイドラインの OID 要求のセットの\_スイッチ\_プロパティ\_を削除しを参照してください[スイッチ ポリシーの管理](https://msdn.microsoft.com/library/windows/hardware/hh598203)します。

### <a name="return-status-codes"></a>リターン状態コード

転送拡張機能の OID OID セットの要求が完了すると\_スイッチ\_プロパティ\_DELETE、1 つを返しますの次のステータス コード。

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
<td><p>転送拡張機能は、スイッチのポリシーをサポートしていません。</p></td>
</tr>
<tr class="odd">
<td><p>NDIS_STATUS_<em>Xxx</em></p></td>
<td><p>その他の理由の OID 要求が失敗しました。</p></td>
</tr>
</tbody>
</table>

 

転送拡張機能は OID の OID のセット要求を完了しない場合\_切り替える\_プロパティ\_拡張可能スイッチの基になるミニポート端で DELETE、要求が完了しました。 ミニポート edge では、次のステータス コードを返します。

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

 

<a name="requirements"></a>必要条件
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

[**NDIS\_スイッチ\_プロパティ\_カスタム**](https://msdn.microsoft.com/library/windows/hardware/hh598247)

[**NDIS\_スイッチ\_プロパティ\_パラメーター**](https://msdn.microsoft.com/library/windows/hardware/hh598255)

[**NdisFOidRequest**](https://msdn.microsoft.com/library/windows/hardware/ff561830)

 

 




