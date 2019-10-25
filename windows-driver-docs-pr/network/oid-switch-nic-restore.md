---
title: OID_SWITCH_NIC_RESTORE
description: Hyper-v 拡張可能スイッチのプロトコルエッジは、拡張可能なスイッチポートとそのネットワークアダプターに対して復元できるランタイムデータを拡張可能なスイッチ拡張機能に通知するために、オブジェクト識別子 (OID) セット要求を OID_SWITCH_NIC_RESTORE に発行します。接続.
ms.assetid: 252FB1D2-932F-4FB8-83D6-2690171D746D
ms.date: 08/08/2017
keywords: -Windows Vista 以降の OID_SWITCH_NIC_RESTORE ネットワークドライバー
ms.localizationpriority: medium
ms.openlocfilehash: 224a73a8433f4dbc84b34d9ed499678e429438e2
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843949"
---
# <a name="oid_switch_nic_restore"></a>OID\_スイッチ\_NIC\_復元


Hyper-v 拡張可能スイッチのプロトコルエッジは、オブジェクト識別子 (OID) セットの OID\_の要求を発行します。これにより、拡張可能なスイッチポートに対して復元できる実行時のデータについて、拡張可能なスイッチ拡張機能に通知\_\_ます。とそのネットワークアダプター接続があります。

[**Ndis\_OID\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)構造の**informationbuffer**メンバーには、ndis\_\_スイッチへのポインターが含まれています。これには、 [**NIC\_\_状態**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_nic_save_state)構造が保存されます。 この構造体は、拡張可能スイッチのプロトコルエッジによって割り当てられます。

<a name="remarks"></a>注釈
-------

Oid の OID セット要求を受信すると\_スイッチ\_NIC\_復元し、拡張可能なスイッチ拡張機能が実行時データを所有しているかどうかを最初に決定する必要があります。 この拡張機能では、NDIS\_スイッチの**Extensionid**メンバーの値を比較することによって、 [ **\_NIC\_保存\_状態**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_nic_save_state)構造を、拡張機能が自身を識別するために使用する GUID 値に比較します。

拡張可能なスイッチポートのランタイムデータが拡張機能によって所有されている場合は、次の方法でこのデータが復元されます。

1.  拡張機能は、 **SaveData**メンバーの実行時データを拡張割り当てストレージにコピーします。

    **  ** NDIS\_スイッチの**ポート id**メンバーの値[ **\_NIC\_保存\_状態**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_nic_save_state)構造は、実行時データが保存された時点の**ポート id**値とは異なる場合があります。 これは、あるホストから別のホストへのライブマイグレーション中に実行時データが保存された場合に発生する可能性があります。 ただし、拡張可能なスイッチポートの構成は、ライブマイグレーション中も保持されます。 これにより、拡張機能は、新しい**ポート id**値を使用して、拡張可能なスイッチポートにランタイムデータを復元できます。

     

2.  拡張機能は、NDIS\_STATUS\_SUCCESS の OID set 要求を完了します。

拡張機能が指定されたランタイムデータを所有していない場合、拡張機能は[**NdisFOidRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfoidrequest)を呼び出して、この OID セット要求を拡張可能なスイッチドライバースタック内の基になる拡張機能に転送します。 この場合、拡張機能では、OID 要求に関連付けられている\_状態の構造を[**保存\_\_NIC\_スイッチ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_nic_save_state)を変更することはできません。

OID\_スイッチ\_NIC に切り替えると、拡張可能なスイッチのミニポートエッジによって\_セットの要求が受信されると、NDIS\_STATUS\_SUCCESS で OID 要求が完了します。 これにより、拡張可能スイッチのプロトコルエッジに、ランタイムデータを所有している拡張機能がないことが通知されます。

実行時データを復元する方法の詳細については、「 [Hyper-v 拡張可能スイッチのランタイムデータの復元](https://docs.microsoft.com/windows-hardware/drivers/network/restoring-hyper-v-extensible-switch-run-time-data)」を参照してください。

**注**  拡張機能によって OID セット要求が失敗した場合は、拡張可能なスイッチによって復元操作全体が失敗します。 そのため、可能な場合、拡張機能は OID 要求の失敗を回避する必要があります。 たとえば、ランタイムデータを復元するために必要なリソースを拡張機能が割り当てられない場合、実行時データを復元せずに正常に機能しないと、OID 要求は失敗します。 ただし、拡張機能がエラー状態から回復できる場合、OID セット要求は失敗しません。

 

### <a name="return-status-codes"></a>ステータスコードを返す

拡張機能によって oid の OID セット要求が完了し\_\_NIC\_復元されると、次のステータスコードのいずれかが返されます。

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
<tr class="even">
<td><p>NDIS_STATUS_<em>Xxx</em></p></td>
<td><p>他の理由で要求が失敗しました。</p></td>
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

[**NDIS\_スイッチ\_NIC\_\_の状態を保存する**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_nic_save_state)

[**NdisFOidRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfoidrequest)

 

 




