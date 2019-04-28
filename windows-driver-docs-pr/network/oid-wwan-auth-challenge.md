---
title: OID_WWAN_AUTH_CHALLENGE
description: OID_WWAN_AUTH_CHALLENGE MB デバイスの場合は、または、NDIS_WWAN_ を含む SIM.n NDIS_STATUS_WWAN_AUTHENTICATION_RESPONSE 状態通知から応答を取得する、サブスクライバー Identity モジュール (SIM) カードに認証チャレンジを送信します。認証キーを提供する AUTHENTICATION_RESPONSE 構造は、クエリ要求を完了したときに、呼び出し元によってに基づいて課題を要求しました。
ms.assetid: C39300F2-DF14-4DA8-9BD2-83593CC29837
ms.date: 08/08/2017
keywords: -OID_WWAN_AUTH_CHALLENGE ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: d760f90c006b80835d53ad4f52ebac535448e840
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63372864"
---
# <a name="oidwwanauthchallenge"></a>OID\_WWAN\_AUTH\_チャレンジ


OID\_WWAN\_AUTH\_チャレンジ MB デバイスの場合は、または、SIM から応答を取得する、サブスクライバー Identity モジュール (SIM) カードに認証チャレンジを送信します。

要求のセットがサポートされていません。

これは、省略可能な OID です。 クエリ要求を非同期的に、最初に返す NDIS ミニポート ドライバーでは、これを実装するときに処理する必要があります\_状態\_INDICATION\_元の要求と後で、NDIS を送信するには、必要な作業\_状態\_WWAN\_認証\_、NDIS を含む応答のステータス通知\_WWAN\_認証\_認証キーを提供する応答の構造クエリ要求を完了するときは、呼び出し元によってに基づいて課題を要求しました。

<a name="remarks"></a>注釈
-------

この OID を処理するときに、ミニポート ドライバーは、SIM カードにアクセスできますが、プロバイダーのネットワークにアクセスしないでください。 この OID は、機内モード無線オフでも動作する必要があります。

OID\_WWAN\_AUTH\_チャレンジは、第 2 世代と第 3 世代のモバイル ネットワークをサポートしています。 SIM には、標準的な第 2 世代モバイル ネットワークである GSM 認証とキー アグリーメント プリミティブに基づいている認証機構を指定します。 別名とも呼ばれる ' の Universal Mobile Telecommunications システム UMTS () で指定された、第 3 世代認証とキーの承諾メカニズムを使用して\[TS33.102\]とで CDMA2000 \[S.S0055 A\]デバイスの機能によって異なります。

ミニポート ドライバーは、NDIS を返す必要があります\_状態\_いない\_返す 1 つまたはすべての認証メソッドをサポートしていない場合にサポートされます。

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
<td>Ntddndis.h (include Ndis.h)</td>
</tr>
</tbody>
</table>

 

 




