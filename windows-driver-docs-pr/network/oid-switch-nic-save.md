---
title: OID_SWITCH_NIC_SAVE
description: Hyper-v 拡張可能スイッチのプロトコルエッジは、拡張可能なスイッチポートとそのネットワークアダプター接続の実行時データを保存する操作中に、OID_SWITCH_NIC_SAVE のオブジェクト識別子 (OID) メソッド要求を発行します。
ms.assetid: FE2F9767-7186-42FF-85C1-2A8203FEF629
ms.date: 08/08/2017
keywords: -Windows Vista 以降のネットワークドライバーの OID_SWITCH_NIC_SAVE
ms.localizationpriority: medium
ms.openlocfilehash: 124188f6bf80e4de7c10462789d4db71b583bfef
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843946"
---
# <a name="oid_switch_nic_save"></a>OID\_スイッチ\_NIC\_保存


Hyper-v 拡張可能スイッチのプロトコルエッジは、オブジェクト識別子 (OID) のメソッド要求を OID\_します。これは、拡張可能なスイッチポートとそのネットワークアダプター接続の実行時データを保存するための操作中に保存\_\_NIC です。 この拡張機能は、実行時データを保存して後で復元できるように、このデータを返します。 実行時のデータが保存されると、 [oid\_スイッチ\_\_NIC](oid-switch-nic-restore.md)の設定要求によって復元されます。

[**Ndis\_OID\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)構造の**informationbuffer**メンバーには、ndis\_\_スイッチへのポインターが含まれています。これには、 [**NIC\_\_状態**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_nic_save_state)構造が保存されます。 この構造体は、拡張可能スイッチのプロトコルエッジによって割り当てられます。

<a name="remarks"></a>注釈
-------

Oid の OID メソッド要求を受信すると\_スイッチ\_NIC\_保存すると、拡張可能なスイッチ拡張機能によって次のように実行時データが保存されます。

-   拡張機能は、 [**NDIS\_スイッチ\_\_NIC**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_nic_save_state)内のデータを保存します。これにより、構造体の先頭から*SaveDataOffset*バイトを開始位置として\_状態構造が保存されます。

-   指定された*Savedatasize*が、必要な保存データを保持するのに十分な大きさでない場合は、拡張機能によって、メソッド構造体の*BYTESNEEDED*フィールドが NDIS\_SIZEOF\_NDIS\_スイッチ\_NIC\_\_状態\_リビジョン\_1 に保存し、保存データを保持するために必要なバッファーの量を加算して、ndis\_STATUS\_\_\_ OID は必要なサイズで再発行されます。

-   拡張機能は、 *Extensionid*および*extensionid*フィールドに独自の識別子と名前を設定し、NDIS\_STATUS\_SUCCESS による OID メソッド要求を完了します。 これにより、拡張可能なスイッチのプロトコルエッジで別の OID メソッド要求が発行され、拡張機能によってより多くの保存データが返されるか、他の拡張機能によって独自のデータが保存されます。

**注**  保存するランタイムデータが拡張機能にない場合は、 [**NdisFOidRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfoidrequest)を呼び出して、この OID メソッド要求を拡張可能なスイッチドライバースタック内の基になる拡張機能に転送する必要があります。 この手順の詳細については、「 [NDIS フィルタードライバーでの OID 要求のフィルター処理](https://docs.microsoft.com/windows-hardware/drivers/network/filtering-oid-requests-in-an-ndis-filter-driver)」を参照してください。

 

Hyper-v 拡張可能スイッチは、OID を発行する前に、構造体の*Header*、*ポート id*、 *NicIdex*、 *savedatasize* 、および*SaveDataOffset*の各フィールドを設定します。 拡張機能はこれらのフィールドを変更できません。

OID\_スイッチ\_\_NIC の OID メソッド要求は、最終的に、拡張可能スイッチの基になるミニポートエッジによって処理されます。 この OID メソッド要求は、拡張可能スイッチのミニポートエッジによって受信された後、NDIS\_STATUS\_SUCCESS による OID 要求を完了します。 これにより、拡張可能スイッチのプロトコルエッジに、拡張スイッチドライバースタックのすべての拡張機能が実行時データを照会したことが通知されます。 拡張可能なスイッチのプロトコルエッジは oid セットの要求を発行して、 [\_\_NIC\_スイッチ](oid-switch-nic-save-complete.md)を設定し、保存\_完了して保存操作を完了します。

拡張可能なスイッチポートのランタイムデータを保存する方法の詳細については、「 [Hyper-v 拡張可能スイッチの実行時データの保存](https://docs.microsoft.com/windows-hardware/drivers/network/saving-hyper-v-extensible-switch-run-time-data)」を参照してください。

### <a name="return-status-codes"></a>ステータスコードを返す

拡張可能なスイッチ拡張機能は、oid\_スイッチ\_\_NIC の OID メソッド要求について、次のいずれかの状態コードを返します。

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
<td><p>NDIS_STATUS_BUFFER_TOO_SHORT</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_nic_save_state" data-raw-source="[&lt;strong&gt;NDIS_SWITCH_NIC_SAVE_STATE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_nic_save_state)"><strong>NDIS_SWITCH_NIC_SAVE_STATE</strong></a>には、情報バッファーの長さが小さすぎるため、拡張可能なスイッチ拡張機能でデータを設定する必要があり<strong>ます。METHOD_INFORMATION。BytesNeeded</strong>必要な最小バッファーサイズに<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request" data-raw-source="[&lt;strong&gt;NDIS_OID_REQUEST&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)"><strong>NDIS_OID_REQUEST</strong></a>構造体のメンバーが必要です。</p></td>
</tr>
<tr class="even">
<td><p>NDIS_STATUS_SUCCESS</p></td>
<td><p>拡張機能は、保存する実行時データを返す場合に、この状態を返します。</p></td>
</tr>
<tr class="odd">
<td><p>NDIS_STATUS_<em>Xxx</em></p></td>
<td><p>他の理由で要求が失敗しました。</p></td>
</tr>
</tbody>
</table>

 

拡張可能スイッチの基になるミニポートエッジは、oid\_スイッチ\_\_NIC の OID メソッド要求について、次のステータスコードを返します。

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

[**NDIS\_スイッチ\_NIC\_\_の状態を保存する**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_nic_save_state)

[**NdisFOidRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfoidrequest)

[OID\_スイッチ\_NIC\_復元](oid-switch-nic-restore.md)

[OID\_\_NIC の切り替え\_保存\_完了](oid-switch-nic-save-complete.md)

 

 




