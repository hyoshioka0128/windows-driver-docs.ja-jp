---
title: OID_PM_PARAMETERS
description: クエリとしてプロトコル ドライバーは、ハードウェアの電源管理機能、ネットワーク アダプターの現在有効になっているクエリを実行するのに OID_PM_PARAMETERS OID を使用することができます。
ms.assetid: c3431724-1b5f-4634-8b1e-27fed9031f01
ms.date: 08/08/2017
keywords: -OID_PM_PARAMETERS ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 75fd60dbe2927ae0f0feb9518cfe7ffbb30df160
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67373898"
---
# <a name="oidpmparameters"></a>OID\_PM\_パラメーター


プロトコル ドライバーとして、クエリでは、OID を使用できる\_PM\_ハードウェアの電源管理機能、ネットワーク アダプターの現在有効になっているクエリを実行するパラメーターの OID。 OID のクエリ要求から正常に戻った後、 **InformationBuffer**のメンバー、 [ **NDIS\_OID\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_oid_request)構造体ポインターが含まれています、 [ **NDIS\_PM\_パラメーター** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_pm_parameters)構造体。

プロトコル ドライバーが、OID の使用時に、セットとして\_PM\_パラメーターの OID を有効にまたはネットワーク アダプターの現在のハードウェア機能を無効にします。 プロトコル ドライバーへのポインターを提供する、 [ **NDIS\_PM\_パラメーター** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_pm_parameters)構造体、 **InformationBuffer** のメンバー[**NDIS\_OID\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_oid_request)構造体。

<a name="remarks"></a>コメント
-------

以降では、NDIS 6.20 が動作は、上位のプロトコルとフィルター ドライバーは OID を使用\_PM\_クエリを実行し、電源管理を設定するには、現在有効になっているネットワーク アダプターのハードウェア機能へのパラメーター。

上位のドライバーが、OID をクエリした場合\_PM\_パラメーター OID、NDIS ミニポート ドライバーに転送することがなく、要求を完了します。 NDIS は、要求された設定を格納し、このような他の要求の設定ではそれらを結合します。 NDIS 低電力状態にネットワーク アダプターへの移行前に、NDIS は NDIS が格納されている要求のすべての設定の組み合わせを含むミニポート ドライバーにセットの要求を送信します。

現在有効になっている機能は、ハードウェアでサポートされる機能のサブセットであることができます。 ハードウェアでサポートされる機能の詳細については、次を参照してください。 [OID\_PM\_ハードウェア\_機能](oid-pm-hardware-capabilities.md)します。

**注**  場合 NDIS 設定、NDIS\_PM\_セレクティブ\_中断\_有効フラグ、 **WakeUpFlags**のメンバー [ **NDIS\_PM\_パラメーター** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_pm_parameters) OID の OID のセット要求を発行構造、\_PM\_ミニポート ドライバーに直接パラメーター。 これにより、NDIS フィルター ドライバー、ネットワーク ドライバー スタック内で処理をバイパスします。

 

NDIS またはミニポート ドライバーは、要求の状態コードの次のいずれかを返します。

<a href="" id="ndis-status-success"></a>NDIS\_状態\_成功  
要求は正常に完了しました。

<a href="" id="ndis-status-pending"></a>NDIS\_状態\_PENDING  
完了待ちになっています。 NDIS では、要求が完了した後、最終的な状態コードと結果を呼び出し元の OID 要求完了ハンドラーに渡すは。

<a href="" id="ndis-status-buffer-too-short"></a>NDIS\_状態\_バッファー\_すぎます\_短い  
情報バッファーが小さすぎます。 NDIS セット、**データ。クエリ\_情報。BytesNeeded** NDIS でメンバー\_OID\_構造体を最小バッファー サイズを要求が必要です。

<a href="" id="ndis-status-invalid-parameter"></a>NDIS\_状態\_無効な\_パラメーター  
基になるネットワーク アダプターがサポートされていない機能を有効にしようとした要求が失敗しました。

<a href="" id="ndis-status-failure"></a>NDIS\_状態\_エラー  
上記の理由以外の理由、要求が失敗しました。

<a name="requirements"></a>必要条件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>バージョン</p></td>
<td><p>以降では、NDIS 6.20 が動作をサポートします。</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Ntddndis.h (include Ndis.h)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**NDIS\_OID\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_oid_request)

[**NDIS\_PM\_パラメーター**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_pm_parameters)

[OID\_PM\_ハードウェア\_機能](oid-pm-hardware-capabilities.md)

 

 




