---
title: NDIS_STATUS_WWAN_PREFERRED_MULTICARRIER_PROVIDERS
description: ミニポート ドライバーでは、前の OID_WWAN_PREFERRED_MULTICARRIER_PROVIDERSquery 要求に応答する NDIS_STATUS_WWAN_PREFERRED_MULTICARRIER_PROVIDERS 通知を使用します。ミニポート ドライバーは、この通知を使用して、MB サービスから OID_WWAN_PREFERRED_MULTICARRIER_PROVIDERS 設定要求の結果として更新プログラムに関する MB サービスに通知することがあります。 OID_WWAN_PREFERRED_MULTICARRIER_PROVIDERS セット要求への応答には、PreferredListHeader メンバー内の 0 個の要素を含める必要があります。 ミニポート ドライバーには、MB サービス マルチ キャリア プロバイダーの優先一覧 (PMCPL) が変更されたことを通知するためには、この通知が不要なイベントを送信できます。この通知は、NDIS_WWAN_PREFERRED_MULTICARRIER_PROVIDERS 構造体を使用します。
ms.assetid: DBE8911D-1A92-40BC-94EB-BED3B8B82CB0
ms.date: 07/18/2017
keywords:
- NDIS_STATUS_WWAN_PREFERRED_MULTICARRIER_PROVIDERS ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 06b3a214854dc4f5c15410f8acbf35e11c97ec03
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56549000"
---
# <a name="ndisstatuswwanpreferredmulticarrierproviders"></a>NDIS\_状態\_WWAN\_優先\_マルチ\_プロバイダー


ミニポート ドライバーを使用して、NDIS\_状態\_WWAN\_優先\_マルチ\_プロバイダーの通知を前に応答する[OID\_WWAN\_優先\_マルチ\_プロバイダー](https://msdn.microsoft.com/library/windows/hardware/hh831868)*クエリ*要求。

ミニポート ドライバーは可能性がありますもこの通知を使用して、OID の結果として更新プログラムに関する MB サービスに通知する\_WWAN\_優先\_マルチ\_プロバイダー*設定*からの要求MB サービスです。 OID への応答を\_WWAN\_優先\_マルチ\_プロバイダー*設定*要求内の 0 個の要素を含める必要があります、 **PreferredListHeader**メンバー。 ミニポート ドライバーには、MB サービス マルチ キャリア プロバイダーの優先一覧 (PMCPL) が変更されたことを通知するためには、この通知が不要なイベントを送信できます。

この通知を使用して、 [ **NDIS\_WWAN\_優先\_マルチ\_プロバイダー** ](https://msdn.microsoft.com/library/windows/hardware/hh831864)構造体。

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
<td><p>Windows 8 以降でサポートされています。</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Ndis.h</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**NDIS\_WWAN\_優先\_マルチ\_プロバイダー**](https://msdn.microsoft.com/library/windows/hardware/hh831864)

 

 




