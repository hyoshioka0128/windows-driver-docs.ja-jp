---
title: OID_SWITCH_PORT_PROPERTY_UPDATE
description: HYPER-V 拡張可能スイッチのプロトコルのエッジは、拡張可能スイッチのポート ポリシーのプロパティの更新プログラムの拡張可能スイッチの拡張機能を通知する OID_SWITCH_PORT_PROPERTY_UPDATE のオブジェクト識別子 (OID) セット要求を発行します。
ms.assetid: 674CA5EB-BF11-47E8-A2AC-6C789CA4FDB5
ms.date: 08/08/2017
keywords: -OID_SWITCH_PORT_PROPERTY_UPDATE ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: ce04afb1c726cefb28f6030ec61c2a68fe051fe1
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63343354"
---
# <a name="oidswitchportpropertyupdate"></a>OID\_スイッチ\_ポート\_プロパティ\_UPDATE


HYPER-V 拡張可能スイッチのプロトコルのエッジの OID オブジェクト識別子 (OID) セット要求を発行する\_切り替える\_ポート\_プロパティ\_に拡張可能スイッチの拡張機能の更新プログラムの詳細を通知する更新プログラムを拡張可能スイッチのポート ポリシーのプロパティ。

**InformationBuffer**のメンバー、 [ **NDIS\_OID\_要求**](https://msdn.microsoft.com/library/windows/hardware/ff566710)構造体には、バッファーへのポインターが含まれています。 このバッファーには、次のデータが含まれています。

-   [ **NDIS\_スイッチ\_ポート\_プロパティ\_パラメーター** ](https://msdn.microsoft.com/library/windows/hardware/hh598238)識別とポートのプロパティの型を指定します。

-   ポートのポリシーのパラメーターを含むプロパティのバッファー。 プロパティ バッファーに基づいている構造体が含まれています、 **PropertyType**のメンバー、 [ **NDIS\_スイッチ\_ポート\_プロパティ\_パラメーター** ](https://msdn.microsoft.com/library/windows/hardware/hh598238)構造体。 たとえば場合、 **PropertyType**に設定されているメンバー **NdisSwitchPortPropertyTypeVlan**、プロパティのバッファーが含まれています、 [ **NDIS\_スイッチ\_ポート\_プロパティ\_VLAN** ](https://msdn.microsoft.com/library/windows/hardware/hh598243)構造体。

<a name="remarks"></a>注釈
-------

転送拡張機能は、OID の OID のセット要求を処理できる\_スイッチ\_ポート\_プロパティ\_更新します。 その他のすべての種類の拡張機能を呼び出す必要があります[ **NdisFOidRequest** ](https://msdn.microsoft.com/library/windows/hardware/ff561830)拡張可能スイッチのドライバー スタックで、[次へ] の拡張機能に OID 要求を転送します。

NDIS を返すことによって、拡張機能がポートのプロパティの更新を拒否できます\_状態\_データ\_いない\_OID 要求に使用できます。 たとえば、拡張機能は、その更新されたポリシー、ポートを強制するリソースを割り当てることができない場合、更新要求を拒否する必要があります。

**注**  、拡張機能は、その他の NDIS を返す場合\_状態\_*Xxx*エラー状態コード、更新の通知も拒否されます。 ただし、NDIS を返すなどの一時的なシナリオに関する状態コードを返す\_状態\_リソースが作成の通知の再試行になる可能性があります。

 

場合は、拡張機能が、OID 要求を拒否しては、要求が完了したときに、状態を監視する必要があります。 拡張機能は、拡張可能スイッチ コントロール パスの拡張機能を基になるか、拡張可能スイッチのインターフェイスに OID 要求が拒否されたかどうかを決定するこれを行う必要があります。

OID を処理する方法に関するガイドラインの OID 要求のセットの\_スイッチ\_ポート\_プロパティ\_UPDATE を参照してください[ポート ポリシーの管理](https://msdn.microsoft.com/library/windows/hardware/hh598202)します。

### <a name="return-status-codes"></a>リターン状態コード

転送拡張機能の OID OID セットの要求が完了すると\_スイッチ\_ポート\_プロパティ\_更新プログラムは、1 つを返しますの次のステータス コード。

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
<td><p>情報バッファーの長さが小さすぎて処理を<a href="https://msdn.microsoft.com/library/windows/hardware/hh598238" data-raw-source="[&lt;strong&gt;NDIS_SWITCH_PORT_PROPERTY_PARAMETERS&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/hh598238)"> <strong>NDIS_SWITCH_PORT_PROPERTY_PARAMETERS</strong> </a>構造と構造体のプロパティのバッファー内のデータ。 拡張機能セット、<strong>データ。SET_INFORMATION します。BytesNeeded</strong>内のメンバー、 <a href="https://msdn.microsoft.com/library/windows/hardware/ff566710" data-raw-source="[&lt;strong&gt;NDIS_OID_REQUEST&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff566710)"> <strong>NDIS_OID_REQUEST</strong> </a>構造体に必要な最小バッファー サイズ。</p></td>
</tr>
<tr class="even">
<td><p>NDIS_STATUS_DATA_NOT_ACCEPTED</p></td>
<td><p>転送拡張機能は、ポートのポリシーの削除の通知を拒否しました。</p></td>
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

 

拡張機能は OID の OID のセット要求を完了しない場合\_切り替える\_ポート\_プロパティ\_拡張可能スイッチの基になるミニポート端で更新プログラム、要求が完了しました。 ミニポート edge では、次のステータス コードを返します。

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

 

 




