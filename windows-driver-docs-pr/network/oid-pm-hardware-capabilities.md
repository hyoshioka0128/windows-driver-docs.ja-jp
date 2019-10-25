---
title: OID_PM_HARDWARE_CAPABILITIES
description: クエリとして、これまでのドライバーは OID_PM_HARDWARE_CAPABILITIES OID を使用して、ネットワークアダプターの電源管理のハードウェア機能を照会できます。
ms.assetid: 52446584-bb73-4cf4-bda9-bf92ef2488e3
ms.date: 08/08/2017
keywords: -Windows Vista 以降の OID_PM_HARDWARE_CAPABILITIES ネットワークドライバー
ms.localizationpriority: medium
ms.openlocfilehash: ec73cd6c0a0d9e6227417e27ffa36e5269ac1cc8
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844055"
---
# <a name="oid_pm_hardware_capabilities"></a>OID\_PM\_ハードウェア\_機能


クエリとして、これまでのドライバーでは、OID\_PM\_ハードウェア\_機能 OID を使用して、ネットワークアダプターの電源管理のハードウェア機能を照会できます。 OID クエリ要求から正常に戻った後、 [**ndis\_oid\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)構造の**informationbuffer**メンバーには、 [**ndis\_PM\_CAPABILITIES**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_pm_capabilities)構造体へのポインターが含まれています。

<a name="remarks"></a>注釈
-------

NDIS はミニポートドライバーのクエリを処理します。 NDIS 6.20 以降では、ミニポートドライバーは、 [**NDIS\_ミニポート\_アダプターの PowerManagementCapabilitiesEx メンバーの初期化中に電源管理のハードウェア機能を提供\_全般\_ATTRIBUTES**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_miniport_adapter_general_attributes)構造体。

ミニポートドライバーは、 [**ndis\_status\_PM\_機能**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-pm-capabilities-change)を発行する必要があります。また、ネットワークアダプターの電源管理のハードウェア機能の変更を ndis およびそれ以降のドライバーに報告するように状態を変更\_ます。

NDIS は、要求に対して次のいずれかの状態コードを返します。

<a href="" id="ndis-status-success"></a>NDIS\_状態\_成功  
要求は正常に完了しました。 **Informationbuffer**は、 [**NDIS\_PM\_機能**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_pm_capabilities)の構造を指します。

<a href="" id="ndis-status-pending"></a>NDIS\_状態\_保留中  
要求は完了待ちです。 NDIS は、要求が完了した後に、最終的な状態コードと結果を呼び出し元の OID 要求完了ハンドラーに渡します。

<a href="" id="ndis-status-buffer-too-short"></a>NDIS\_ステータス\_バッファー\_短すぎる\_  
情報バッファーが短すぎます。 NDIS はデータを設定**します。クエリ\_情報。** 必要な最小バッファーサイズに対して、NDIS\_OID\_要求構造体のメンバーが必要です。

<a href="" id="ndis-status-failure"></a>NDIS\_状態\_エラー  
この要求は、上記の理由以外の理由で失敗しました。

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
<td><p>NDIS 6.20 以降でサポートされています。 ミニポートドライバーが要求されていません。 (「解説」を参照してください。)</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Ntddndis (Ndis .h を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**NDIS\_ミニポート\_アダプター\_全般\_属性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_miniport_adapter_general_attributes)

[**NDIS\_OID\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)

[**NDIS\_PM\_機能**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_pm_capabilities)

[**NDIS\_STATUS\_PM\_機能\_変更**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-pm-capabilities-change)

 

 




