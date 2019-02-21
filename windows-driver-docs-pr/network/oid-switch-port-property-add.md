---
title: OID_SWITCH_PORT_PROPERTY_ADD
description: HYPER-V 拡張可能スイッチのプロトコルのエッジは、拡張可能スイッチ ポートのポリシーのプロパティの追加の拡張可能スイッチの拡張機能を通知する OID_SWITCH_PORT_PROPERTY_ADD のオブジェクト識別子 (OID) セット要求を発行します。
ms.assetid: 6F246E5A-A02A-4303-9DB0-51E2FD4DC9E7
ms.date: 08/08/2017
keywords: -OID_SWITCH_PORT_PROPERTY_ADD ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 88a0ab92b0ae6c63370c4680c822e2776df70acc
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56559969"
---
# <a name="oidswitchportpropertyadd"></a>OID\_スイッチ\_ポート\_プロパティ\_追加


HYPER-V 拡張可能スイッチのプロトコルのエッジの OID オブジェクト識別子 (OID) セット要求を発行する\_切り替える\_ポート\_プロパティ\_に拡張可能スイッチの拡張機能をポリシーの追加についての通知の追加拡張可能スイッチ ポートのプロパティです。

**InformationBuffer**のメンバー、 [ **NDIS\_OID\_要求**](https://msdn.microsoft.com/library/windows/hardware/ff566710)構造体には、バッファーへのポインターが含まれています。 このバッファーには、次のデータが含まれています。

-   [ **NDIS\_スイッチ\_ポート\_プロパティ\_パラメーター** ](https://msdn.microsoft.com/library/windows/hardware/hh598238)識別とポートのパラメーターの型を指定する構造体ポリシー。

-   ポートのポリシーのパラメーターを含むプロパティのバッファー。 プロパティ バッファーに基づいている構造体が含まれています、 **PropertyType**のメンバー、 [ **NDIS\_スイッチ\_ポート\_プロパティ\_パラメーター** ](https://msdn.microsoft.com/library/windows/hardware/hh598238)構造体。 たとえば場合、 **PropertyType**に設定されているメンバー **NdisSwitchPortPropertyTypeVlan**、プロパティのバッファーが含まれています、 [ **NDIS\_スイッチ\_ポート\_プロパティ\_VLAN** ](https://msdn.microsoft.com/library/windows/hardware/hh598243)構造体。

<a name="remarks"></a>注釈
-------

転送拡張機能は、OID の OID のセット要求を処理できる\_スイッチ\_ポート\_プロパティ\_を追加します。 その他のすべての種類の拡張機能を呼び出す必要があります[ **NdisFOidRequest** ](https://msdn.microsoft.com/library/windows/hardware/ff561830)拡張可能スイッチのドライバー スタックで、[次へ] の拡張機能に OID 要求を転送します。

NDIS を返すことによって、拡張機能がポートのプロパティの追加を拒否できます\_状態\_データ\_いない\_OID 要求に使用できます。 たとえば、拡張機能は、その構成済みポリシー、ポートを強制するリソースを割り当てることができない場合、追加要求を拒否する必要があります。

**注**  、拡張機能は、その他の NDIS を返す場合\_状態\_*Xxx*エラー ステータス コードを作成の通知も拒否されます。 ただし、NDIS を返すなどの一時的なシナリオに関する状態コードを返す\_状態\_リソースが作成の通知の再試行になる可能性があります。

 

場合は、拡張機能が、OID 要求を拒否しては、要求が完了したときに、状態を監視する必要があります。 拡張機能は、拡張可能スイッチ コントロール パスの拡張機能を基になるか、拡張可能スイッチのインターフェイスに OID 要求が拒否されたかどうかを決定するこれを行う必要があります。

OID を処理する方法に関するガイドラインの OID 要求のセットの\_スイッチ\_ポート\_プロパティ\_追加するを参照してください[ポート ポリシーの管理](https://msdn.microsoft.com/library/windows/hardware/hh598202)します。

### <a name="return-status-codes"></a>リターン状態コード

転送拡張機能の OID OID セットの要求が完了すると\_スイッチ\_ポート\_プロパティ\_を追加する次のステータス コードの 1 つを返します。

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
<td><p>NDIS_STATUS_INVALID_LENGTH</p></td>
<td><p>情報バッファーの長さが小さすぎて処理を<a href="https://msdn.microsoft.com/library/windows/hardware/hh598238" data-raw-source="[&lt;strong&gt;NDIS_SWITCH_PORT_PROPERTY_PARAMETERS&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/hh598238)"> <strong>NDIS_SWITCH_PORT_PROPERTY_PARAMETERS</strong> </a>構造とデータ構造を&#39;s プロパティ バッファー。 拡張機能セット、<strong>データ。SET_INFORMATION します。BytesNeeded</strong>内のメンバー、 <a href="https://msdn.microsoft.com/library/windows/hardware/ff566710" data-raw-source="[&lt;strong&gt;NDIS_OID_REQUEST&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff566710)"> <strong>NDIS_OID_REQUEST</strong> </a>構造体に必要な最小バッファー サイズ。</p></td>
</tr>
<tr class="even">
<td><p>NDIS_STATUS_DATA_NOT_ACCEPTED</p></td>
<td><p>転送拡張機能は、ポートのポリシーの追加の通知を拒否しました。</p></td>
</tr>
<tr class="odd">
<td><p>NDIS_STATUS_NOT_SUPPORTED</p></td>
<td><p>転送拡張機能は、ポート、ポリシーをサポートしていません。</p></td>
</tr>
<tr class="even">
<td><p>NDIS_STATUS_<em>Xxx</em></p></td>
<td><p>その他の理由の OID 要求が失敗しました。</p></td>
</tr>
</tbody>
</table>

 

拡張機能は OID の OID のセット要求を完了しない場合\_切り替える\_ポート\_プロパティ\_を追加する拡張可能スイッチの基になるミニポート端で要求を完了します。 ミニポート edge には、次のステータス コードが返されます。

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
[**NDIS\_OID\_要求**](https://msdn.microsoft.com/library/windows/hardware/ff566710)

[**NDIS\_スイッチ\_ポート\_プロパティ\_カスタム**](https://msdn.microsoft.com/library/windows/hardware/hh598230)

[**NDIS\_スイッチ\_ポート\_プロパティ\_パラメーター**](https://msdn.microsoft.com/library/windows/hardware/hh598238)

[**NDIS\_スイッチ\_ポート\_プロパティ\_VLAN**](https://msdn.microsoft.com/library/windows/hardware/hh598243)

[**NdisFOidRequest**](https://msdn.microsoft.com/library/windows/hardware/ff561830)

 

 




