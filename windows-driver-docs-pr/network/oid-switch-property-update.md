---
title: OID_SWITCH_PROPERTY_UPDATE
description: Hyper-v 拡張可能スイッチのプロトコルエッジは、拡張可能なスイッチポリシープロパティのパラメーターの更新について拡張可能なスイッチ拡張機能に通知するために、オブジェクト識別子 (OID) セット要求を OID_SWITCH_PROPERTY_UPDATE に発行します。
ms.assetid: AEC32AD8-B353-4D58-9111-D70C2FFA9F66
ms.date: 08/08/2017
keywords: -Windows Vista 以降の OID_SWITCH_PROPERTY_UPDATE ネットワークドライバー
ms.localizationpriority: medium
ms.openlocfilehash: e589054fa32875e03584576fe66f0316c9a80f45
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843913"
---
# <a name="oid_switch_property_update"></a>OID\_スイッチ\_プロパティ\_更新


Hyper-v 拡張可能スイッチのプロトコルエッジは、オブジェクト識別子 (OID) セットの OID\_スイッチ\_プロパティ\_更新を発行して拡張可能スイッチの拡張機能に、拡張可能なスイッチポリシーのパラメーターの更新について通知します。".

[**NDIS\_OID\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)構造体の**informationbuffer**メンバーには、バッファーへのポインターが含まれています。 このバッファーには、次のデータが含まれています。

-   拡張可能なスイッチポリシーの識別と種類を指定する[**NDIS\_スイッチ\_プロパティ\_パラメーター**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_property_parameters)構造。

-   拡張可能なスイッチポリシーのパラメーターを格納しているプロパティバッファー。 プロパティバッファーには、NDIS\_スイッチの**PropertyType**メンバーに基づく構造体が含まれています[ **\_プロパティ\_PARAMETERS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_property_parameters)構造体です。

    **注**  Windows Server 2012 以降では、 **PropertyType**メンバーを**NdisSwitchPropertyTypeCustom**に設定し、プロパティバッファーに[**NDIS\_SWITCH\_プロパティ\_カスタム**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_property_custom)を含める必要があることに注意してください。データ.

     

<a name="remarks"></a>注釈
-------

転送拡張機能では、OID の OID set 要求を処理できます。\_スイッチ\_プロパティ\_更新を設定します。 その他のすべての種類の拡張機能は、 [**NdisFOidRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfoidrequest)を呼び出して、拡張可能なスイッチドライバースタックの次の拡張機能に OID 要求を転送する必要があります。

拡張機能は、OID 要求に対して\_受け入れられない\_データ\_NDIS\_状態を返すことによって、switch プロパティの更新を拒否することができます。 たとえば、スイッチで更新されたポリシーを適用するために、拡張機能がリソースを割り当てられない場合、更新要求を拒否する必要があります。

**注**  拡張機能から他の NDIS\_ステータス\_*Xxx*エラー状態コードが返された場合は、作成通知も拒否されます。 ただし、NDIS\_STATUS\_リソースを返すなど、一時的なシナリオのステータスコードを返すと、作成通知の再試行が発生する可能性があります。

 

拡張機能が OID 要求を拒否しない場合は、要求が完了したときに状態を監視する必要があります。 拡張機能は、拡張可能なスイッチコントロールパスまたは拡張可能なスイッチインターフェイスで、基になる拡張機能によって OID 要求が拒否されたかどうかを判断するために、この処理を実行します。

Oid の OID セット要求を処理する方法に関するガイドラインについては\_スイッチ\_プロパティ\_更新については、「[スイッチポリシーの管理](https://docs.microsoft.com/windows-hardware/drivers/network/managing-switch-policies)」を参照してください。

### <a name="return-status-codes"></a>ステータスコードを返す

拡張機能によって oid の OID セット要求が完了し\_\_プロパティ\_更新されると、次のステータスコードのいずれかが返されます。

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
<td><p>拡張機能によって、スイッチポリシーの更新通知が拒否されました。</p></td>
</tr>
<tr class="even">
<td><p>NDIS_STATUS_FAILURE</p></td>
<td><p>OID 要求は、他の理由で失敗しました。</p></td>
</tr>
</tbody>
</table>

 

拡張機能が oid の OID 設定要求を完了していない場合は\_\_プロパティ\_更新されますが、要求は、拡張可能スイッチの基になるミニポートエッジによって完了します。 ミニポートエッジは、次の状態コードを返します。

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
<td><p>OID 要求が正常に完了しました。</p></td>
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
<td><p>NDIS 6.30 以降でサポートされています。</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Ntddndis (Ndis .h を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


****
[**NDIS\_OID\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)

[**NDIS\_スイッチ\_プロパティ\_カスタム**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_property_custom)

[**NDIS\_スイッチ\_プロパティ\_パラメーター**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_property_parameters)

[**NdisFOidRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfoidrequest)

 

 




