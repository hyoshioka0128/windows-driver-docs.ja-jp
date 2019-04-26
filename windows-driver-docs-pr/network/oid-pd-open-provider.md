---
title: OID_PD_OPEN_PROVIDER
description: NDIS プロトコルまたはフィルター ドライバーは、ミニポート ドライバーのおプロバイダー オブジェクトで PD 機能にアクセスする PD 対応ミニポート ドライバーに OID_PD_OPEN_PROVIDER のオブジェクト識別子 (OID) メソッド要求を送信します。
ms.assetid: B13E0FAC-A179-4785-9B39-CB498064947B
ms.date: 08/08/2017
keywords: -OID_PD_OPEN_PROVIDER ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: aeb4fb1808bde918932b081e456df3254aa4718f
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63346788"
---
# <a name="oidpdopenprovider"></a>OID\_PD\_オープン\_プロバイダー


OID のオブジェクト識別子 (OID) メソッド要求を送信する NDIS プロトコルまたはフィルター ドライバー\_PD\_オープン\_PD 対応ミニポート ドライバーにプロバイダーをミニポート ドライバーのおプロバイダー オブジェクトで PD 機能にアクセスするには. PD 対応のすべてのミニポート ドライバーでは、この OID 要求を処理する必要があります。

**InformationBuffer**のメンバー、 [ **NDIS\_OID\_要求**](https://msdn.microsoft.com/library/windows/hardware/ff566710)構造体には、バッファーへのポインターが含まれています。 このバッファーには、次のデータが含まれています。

-   [ **NDIS\_PD\_オープン\_プロバイダー\_パラメーター** ](https://msdn.microsoft.com/library/windows/hardware/dn931842)構造体

<a name="remarks"></a>注釈
-------

<a name="requirements"></a>必要条件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>サポートされている最小のクライアント</p></td>
<td><p>Windows 10</p></td>
</tr>
<tr class="even">
<td><p>サポートされている最小のサーバー</p></td>
<td><p>Windows Server 2016</p></td>
</tr>
<tr class="odd">
<td><p>Header</p></td>
<td>Ntddndis.h (include Ndis.h)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[*MiniportOidRequest*](https://msdn.microsoft.com/library/windows/hardware/ff559416)

[**NDIS\_PD\_オープン\_プロバイダー\_パラメーター**](https://msdn.microsoft.com/library/windows/hardware/dn931842)

[NDIS\_状態\_PD\_現在\_構成](https://msdn.microsoft.com/library/windows/hardware/dn931850)

[OID\_PD\_閉じる\_プロバイダー](oid-pd-close-provider.md)

 

 




