---
title: OID_PM_PARAMETERS
description: クエリとして、プロトコルドライバーは OID_PM_PARAMETERS OID を使用して、現在有効になっているネットワークアダプターの電源管理ハードウェア機能を照会できます。
ms.assetid: c3431724-1b5f-4634-8b1e-27fed9031f01
ms.date: 08/08/2017
keywords: -Windows Vista 以降の OID_PM_PARAMETERS ネットワークドライバー
ms.localizationpriority: medium
ms.openlocfilehash: 8ecb2b2704a3e8c92f8b5d6882b3eda2fb3c3169
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844053"
---
# <a name="oid_pm_parameters"></a>OID\_PM\_パラメーター


クエリとして、プロトコルドライバーは、OID\_PM\_PARAMETERS OID を使用して、現在有効になっているネットワークアダプターの電源管理ハードウェア機能を照会できます。 OID クエリ要求から正常に戻った後、 [**ndis\_oid\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)構造の**informationbuffer**メンバーには、 [**ndis\_PM\_PARAMETERS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_pm_parameters)構造体へのポインターが含まれています。

セットとして、プロトコルドライバーは、OID\_PM\_PARAMETERS OID を使用して、ネットワークアダプターの現在のハードウェア機能を有効または無効にすることができます。 プロトコルドライバーは、ndis [ **\_OID\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)構造の**informationbuffer**メンバー内にある[**ndis\_PM\_PARAMETERS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_pm_parameters)構造体へのポインターを提供します。

<a name="remarks"></a>注釈
-------

NDIS 6.20 以降では、プロトコルおよびフィルタードライバーは OID\_PM\_パラメーターを使用して、現在有効になっているネットワークアダプターの電源管理のハードウェア機能を照会および設定します。

その後のドライバーが OID\_PM\_PARAMETERS OID に対してクエリを実行すると、NDIS はミニポートドライバーに転送せずに要求を完了します。 NDIS は、要求された設定を格納し、その他の要求の設定と組み合わせます。 Ndis は、ネットワークアダプターを低電力状態に移行する前に、ndis が格納したすべての要求の組み合わせた設定を含むミニポートドライバーにセット要求を送信します。

現在有効になっている機能は、ハードウェアがサポートする機能のサブセットにすることができます。 ハードウェアがサポートする機能の詳細については、「 [OID\_PM\_ハードウェア\_機能](oid-pm-hardware-capabilities.md)」を参照してください。

**  ndis** [ **\_pm\_PARAMETERS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_pm_parameters)構造体の**WakeUpFlags**メンバーで、NDIS\_PM\_選択的\_SUSPEND\_ENABLED フラグが設定されている場合、oid の oid セット要求が発行され\_PM は、パラメーターをミニポートドライバーに直接\_します。 これにより、NDIS はネットワークドライバースタック内のドライバーをフィルター処理することによって処理をバイパスできます。

 

NDIS またはミニポートドライバーは、要求に対して次のいずれかの状態コードを返します。

<a href="" id="ndis-status-success"></a>NDIS\_状態\_成功  
要求は正常に完了しました。

<a href="" id="ndis-status-pending"></a>NDIS\_状態\_保留中  
要求は完了待ちです。 NDIS は、要求が完了した後に、最終的な状態コードと結果を呼び出し元の OID 要求完了ハンドラーに渡します。

<a href="" id="ndis-status-buffer-too-short"></a>NDIS\_ステータス\_バッファー\_短すぎる\_  
情報バッファーが短すぎます。 NDIS はデータを設定**します。クエリ\_情報。** 必要な最小バッファーサイズに対して、NDIS\_OID\_要求構造体のメンバーが必要です。

<a href="" id="ndis-status-invalid-parameter"></a>NDIS\_の状態\_無効な\_パラメーターです  
基になるネットワークアダプターでサポートされていない機能を有効にしようとしたため、要求は失敗しました。

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
<td><p>NDIS 6.20 以降でサポートされています。</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Ntddndis (Ndis .h を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**NDIS\_OID\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)

[**NDIS\_PM\_パラメーター**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_pm_parameters)

[OID\_PM\_ハードウェア\_機能](oid-pm-hardware-capabilities.md)

 

 




