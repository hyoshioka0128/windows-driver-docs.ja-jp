---
title: OID_SWITCH_NIC_SAVE
description: オブジェクト識別子 (OID) のメソッドを要求 OID_SWITCH_NIC_SAVE の操作中に、拡張可能スイッチ ポートとそのネットワーク アダプター接続の実行時データを保存する HYPER-V 拡張可能スイッチに関する問題のプロトコルのエッジ。
ms.assetid: FE2F9767-7186-42FF-85C1-2A8203FEF629
ms.date: 08/08/2017
keywords: -OID_SWITCH_NIC_SAVE ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 23c2a7f8d71446b72d2b0dd8d7bc44aeed1b4ec6
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385497"
---
# <a name="oidswitchnicsave"></a>OID\_スイッチ\_NIC\_保存


HYPER-V 拡張可能スイッチのプロトコルのエッジの OID オブジェクト識別子 (OID) メソッド要求を発行する\_切り替える\_NIC\_拡張可能スイッチ ポートとそのネットワーク アダプターの実行時データを保存するための操作中に保存接続します。 拡張機能は、実行時のデータを保存して後で復元できるように、このデータを返します。 実行時のデータを保存すると後の OID のセット要求を通じた復元[OID\_スイッチ\_NIC\_復元](oid-switch-nic-restore.md)します。

**InformationBuffer**のメンバー、 [ **NDIS\_OID\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_oid_request)構造体にはへのポインターが含まれています、 [ **NDIS\_スイッチ\_NIC\_保存\_状態**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_switch_nic_save_state)構造体。 この構造体は、拡張可能スイッチのプロトコル edge によって割り当てられます。

<a name="remarks"></a>コメント
-------

OID の OID メソッド要求を受け取ったとき\_切り替える\_NIC\_保存、拡張可能スイッチ拡張機能で、次の手順に従って実行時データが保存されます。

-   拡張機能内のデータの保存、 [ **NDIS\_スイッチ\_NIC\_保存\_状態**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_switch_nic_save_state)構造から*SaveDataOffset*構造体の先頭からのバイト数。

-   場合、 *SaveDataSize*提供に必要なデータを保存する、拡張メソッドの構造体の設定を保持するのに十分な大きさでない*BytesNeeded*フィールド NDIS を\_SIZEOF\_NDIS\_スイッチ\_NIC\_保存\_状態\_リビジョン\_1 および保存を保持するために必要なバッファーのデータ、NDIS に OID が完了して\_ステータス\_バッファー\_すぎます\_短い。 必要なサイズの OID を再発行します。

-   拡張機能の設定、 *ExtensionId*と*ExtensionFriendlyName*の独自の識別子と名前、フィールドし、NDIS に OID メソッド要求が完了すると\_状態\_成功しました。 この原因のいずれかに拡張を許可するもう 1 つの OID メソッド要求を発行する拡張可能スイッチのプロトコルの端を返す複数のデータを保存または他の拡張機能を許可するには、独自のデータを保存するスタックがダウンします。

**注**  呼び出す必要がありますが、拡張機能では、実行時のデータを保存することはない場合、 [ **NdisFOidRequest** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisfoidrequest)拡張機能を基になるはこの OID メソッドの要求を転送するように、拡張可能スイッチ ドライバー スタックです。 この手順の詳細については、次を参照してください。 [NDIS フィルター ドライバーでの OID 要求のフィルタ リング](https://docs.microsoft.com/windows-hardware/drivers/network/filtering-oid-requests-in-an-ndis-filter-driver)します。

 

HYPER-V 拡張可能スイッチの設定、*ヘッダー*、 *PortId*、 *NicIdex*、 *SaveDataSize*と*SaveDataOffset* OID を発行する前に構造体のフィールド。 拡張機能は、これらのフィールドを変更できません。

OID の OID メソッド要求\_切り替える\_NIC\_保存は拡張可能スイッチの基になるミニポート edge によって最終的に処理されます。 NDIS に OID 要求が完了するこの OID メソッド要求は拡張可能スイッチのミニポート edge によって受信されると、\_状態\_成功します。 実行時のデータの拡張可能スイッチ ドライバー スタック内のすべての拡張機能をクエリが実行されている拡張可能スイッチのプロトコルの端に通知します。 拡張可能スイッチのプロトコルのエッジの OID セットの要求を発行し、 [OID\_切り替える\_NIC\_保存\_完了](oid-switch-nic-save-complete.md)保存を完了する操作。

拡張可能スイッチ ポートの実行時データを保存する方法の詳細については、次を参照してください。[保存 Hyper-v 拡張可能なスイッチ実行時データ](https://docs.microsoft.com/windows-hardware/drivers/network/saving-hyper-v-extensible-switch-run-time-data)します。

### <a name="return-status-codes"></a>リターン状態コード

拡張可能スイッチ拡張機能は、OID の OID メソッド要求の次のステータス コードのいずれかを返します\_切り替える\_NIC\_を保存します。

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
<td><p>情報バッファーの長さが小さすぎるため、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_switch_nic_save_state" data-raw-source="[&lt;strong&gt;NDIS_SWITCH_NIC_SAVE_STATE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_switch_nic_save_state)"> <strong>NDIS_SWITCH_NIC_SAVE_STATE</strong> </a>とその関連の実行時データ、拡張可能スイッチの拡張機能を設定する必要があります、<strong>データ。METHOD_INFORMATION します。BytesNeeded</strong>内のメンバー、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_oid_request" data-raw-source="[&lt;strong&gt;NDIS_OID_REQUEST&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_oid_request)"> <strong>NDIS_OID_REQUEST</strong> </a>構造体に必要な最小バッファー サイズ。</p></td>
</tr>
<tr class="even">
<td><p>NDIS_STATUS_SUCCESS</p></td>
<td><p>拡張機能は、保存する実行時データを返す場合、この状態を返します。</p></td>
</tr>
<tr class="odd">
<td><p>NDIS_STATUS_<em>Xxx</em></p></td>
<td><p>他の理由から、要求が失敗しました。</p></td>
</tr>
</tbody>
</table>

 

拡張可能スイッチの基になるミニポート edge OID の OID メソッド要求の次のステータス コードを返します\_切り替える\_NIC\_を保存します。

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

[**NDIS\_スイッチ\_NIC\_保存\_状態**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_switch_nic_save_state)

[**NdisFOidRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisfoidrequest)

[OID\_スイッチ\_NIC\_復元](oid-switch-nic-restore.md)

[OID\_スイッチ\_NIC\_保存\_完了](oid-switch-nic-save-complete.md)

 

 




