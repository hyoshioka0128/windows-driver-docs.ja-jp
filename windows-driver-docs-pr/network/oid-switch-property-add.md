---
title: OID_SWITCH_PROPERTY_ADD
description: HYPER-V 拡張可能スイッチのプロトコルのエッジは、ポリシー プロパティのスイッチの拡張可能スイッチの拡張機能を通知する OID_SWITCH_PROPERTY_ADD のオブジェクト識別子 (OID) セット要求を発行します。
ms.assetid: 63A6D2BE-81F4-4D27-B5DF-68466EFF306E
ms.date: 08/08/2017
keywords: -OID_SWITCH_PROPERTY_ADD ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 8676b5fad8bc48f710bd5f8277a735fe342350c2
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67386981"
---
# <a name="oidswitchpropertyadd"></a>OID\_スイッチ\_プロパティ\_追加


HYPER-V 拡張可能スイッチのプロトコルのエッジの OID オブジェクト識別子 (OID) セット要求を発行する\_切り替える\_プロパティ\_ポリシー プロパティのスイッチの拡張可能スイッチの拡張機能を通知に追加

**InformationBuffer**のメンバー、 [ **NDIS\_OID\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_oid_request)構造体には、バッファーへのポインターが含まれています。 このバッファーには、次のデータが含まれています。

-   [ **NDIS\_切り替える\_プロパティ\_パラメーター** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_switch_property_parameters)識別と拡張可能スイッチのポリシーの種類を指定します。

-   拡張可能スイッチ ポリシーのパラメーターを含むプロパティのバッファー。 プロパティ バッファーに基づいている構造体が含まれています、 **PropertyType**のメンバー、 [ **NDIS\_スイッチ\_プロパティ\_パラメーター**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_switch_property_parameters)構造体。

    **注**  以降、Windows Server 2012 では、 **PropertyType**にメンバーを設定する必要があります**NdisSwitchPropertyTypeCustom**プロパティ バッファーは、を含める必要があります[ **NDIS\_スイッチ\_プロパティ\_カスタム**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_switch_property_custom)構造体。

     

<a name="remarks"></a>注釈
-------

転送拡張機能は、OID の OID のセット要求を処理できる\_スイッチ\_プロパティ\_を追加します。 その他のすべての種類の拡張機能を呼び出す必要があります[ **NdisFOidRequest** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisfoidrequest)拡張可能スイッチのドライバー スタックで、[次へ] の拡張機能に OID 要求を転送します。

拡張機能は、NDIS を返すことによってプロパティのスイッチを拒否することができます\_状態\_データ\_いない\_OID 要求に使用できます。 たとえば、拡張機能は、その更新されたポリシー、スイッチを強制するリソースを割り当てることができない場合、追加要求を拒否する必要があります。

**注**  、拡張機能は、その他の NDIS を返す場合\_状態\_*Xxx*エラー ステータス コードを作成の通知も拒否されます。 ただし、NDIS を返すなどの一時的なシナリオに関する状態コードを返す\_状態\_リソースが作成の通知の再試行になる可能性があります。

 

場合は、拡張機能が、OID 要求を拒否しては、要求が完了したときに、状態を監視する必要があります。 拡張機能は、拡張可能スイッチ コントロール パスの拡張機能を基になるか、拡張可能スイッチのインターフェイスに OID 要求が拒否されたかどうかを決定するこれを行う必要があります。

OID を処理する方法に関するガイドラインの OID 要求のセットの\_スイッチ\_プロパティ\_追加するを参照してください[スイッチ ポリシーの管理](https://docs.microsoft.com/windows-hardware/drivers/network/managing-switch-policies)します。

### <a name="return-status-codes"></a>リターン状態コード

転送拡張機能の OID OID セットの要求が完了すると\_スイッチ\_プロパティ\_を追加する次のステータス コードの 1 つを返します。

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
<td><p>NDIS_STATUS_DATA_NOT_ACCEPTED</p></td>
<td><p>拡張機能は、スイッチのポリシーの追加の通知を拒否しました。</p></td>
</tr>
<tr class="even">
<td><p>NDIS_STATUS_FAILURE</p></td>
<td><p>その他の理由の OID 要求が失敗しました。</p></td>
</tr>
</tbody>
</table>

 

拡張機能は OID の OID のセット要求を完了しない場合\_切り替える\_プロパティ\_を追加する拡張可能スイッチの基になるミニポート端で要求を完了します。 ミニポート edge では、次のステータス コードを返します。

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
[**NDIS\_OID\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_oid_request)

[**NDIS\_スイッチ\_プロパティ\_カスタム**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_switch_property_custom)

[**NDIS\_スイッチ\_プロパティ\_パラメーター**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_switch_property_parameters)

[**NdisFOidRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisfoidrequest)

 

 




