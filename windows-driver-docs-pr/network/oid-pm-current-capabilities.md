---
title: OID_PM_CURRENT_CAPABILITIES
description: クエリとして、それまでのドライバーは OID_PM_CURRENT_CAPABILITIES OID を使用して、ネットワークアダプターの現在使用可能な電源管理機能を照会できます。
ms.assetid: b35ce325-a1aa-43e0-bf68-cb2ab89dff76
ms.date: 08/08/2017
keywords: -Windows Vista 以降の OID_PM_CURRENT_CAPABILITIES ネットワークドライバー
ms.localizationpriority: medium
ms.openlocfilehash: c3230d7dc3de542da18d7948b3ad54ca716159ca
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844059"
---
# <a name="oid_pm_current_capabilities"></a>OID\_PM\_現在の\_機能


クエリとして、それまでのドライバーは、現在の\_機能 OID\_OID\_PM を使用して、ネットワークアダプターの現在使用可能な電源管理機能を照会できます。 OID クエリ要求から正常に戻った後、 [**ndis\_oid\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)構造の**informationbuffer**メンバーには、 [**ndis\_PM\_CAPABILITIES**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_pm_capabilities)構造体へのポインターが含まれています。

<a name="remarks"></a>注釈
-------

NDIS はミニポートドライバーのクエリを処理します。 NDIS 6.20 以降では、ミニポートドライバーは初期化中に電源管理のハードウェア機能を提供します。 ただし、NDIS では、一部の機能をプロトコルドライバーから非表示にすることができます。 たとえば、ユーザーが電源管理機能の一部またはすべてを無効にした場合、NDIS は異なる機能を報告する場合があります。

NDIS がプロトコルドライバーに報告する現在の電源管理機能は、ミニポートドライバーが NDIS に報告したハードウェア機能と必ずしも同じではないことに注意してください。

NDIS は、基盤となるネットワークアダプターの電源管理機能**を、** ndis\_バインド操作中に[**バインド\_PARAMETERS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_bind_parameters)構造内のプロトコルドライバーに報告します. したがって、プロトコルドライバーは OID に対してクエリを実行する必要はありません。

NDIS では、 [**ndis\_status\_PM\_機能**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-pm-capabilities-change)を発行し、その後のドライバーで使用可能な電源管理機能の変更を報告するように状態を変更\_ます。

基になるネットワークアダプターに NDIS 6.1 または古いミニポートドライバーがある場合、NDIS は、基盤となるネットワークアダプターの電源管理機能を[**ndis\_PM\_機能**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_pm_capabilities)の構造に変換します。

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


[**NDIS\_バインド\_パラメーター**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_bind_parameters)

[**NDIS\_OID\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)

[**NDIS\_PM\_機能**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_pm_capabilities)

[**NDIS\_STATUS\_PM\_機能\_変更**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-pm-capabilities-change)

 

 




