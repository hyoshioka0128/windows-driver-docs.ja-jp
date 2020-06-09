---
title: バグチェック 0x4A IRQL_GT_ZERO_AT_SYSTEM_SERVICE
description: IRQL_GT_ZERO_AT_SYSTEM_SERVICE バグチェックの値は0x0000004A です。 これは、スレッドが、その IRQL がまだ PASSIVE_LEVEL 上にあるときに、システム呼び出しからユーザーモードに戻ることを示します。
ms.assetid: 0da64630-d446-426a-a51f-34117fe9daa7
keywords:
- バグチェック 0x4A IRQL_GT_ZERO_AT_SYSTEM_SERVICE
- IRQL_GT_ZERO_AT_SYSTEM_SERVICE
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- IRQL_GT_ZERO_AT_SYSTEM_SERVICE
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 4984386f54ee4fd3e6cf3378ac2bf611327840e6
ms.sourcegitcommit: dadc9ced1670d667e31eb0cb58d6a622f0f09c46
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/09/2020
ms.locfileid: "84534627"
---
# <a name="bug-check-0x4a-irql_gt_zero_at_system_service"></a>\_ \_ \_ \_ システム \_ サービスでのバグチェック 0x4a: IRQL GT ゼロ


\_ \_ \_ システムサービスのバグチェックの IRQL GT ゼロには、 \_ \_ 値0x0000004a があります。 これは、その IRQL がまだパッシブレベルを超えている場合に、スレッドがシステム呼び出しからユーザーモードに戻ることを示し \_ ます。

> [!IMPORTANT]
> このトピックはプログラマーを対象としています。 コンピューターの使用中にブルースクリーンのエラーコードが表示された顧客の場合は、「[ブルースクリーンエラーのトラブルシューティング](https://www.windows.com/stopcode)」を参照してください。


## <a name="irql_gt_zero_at_system_service-parameters"></a>\_ \_ \_ \_ システムサービスパラメーターでの \_ IRQL GT ゼロ


<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">パラメーター</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>1</p></td>
<td align="left"><p>システム関数のアドレス (システム呼び出しルーチン)</p></td>
</tr>
<tr class="even">
<td align="left"><p>2</p></td>
<td align="left"><p>現在の IRQL</p></td>
</tr>
<tr class="odd">
<td align="left"><p>3</p></td>
<td align="left"><p>0</p></td>
</tr>
<tr class="even">
<td align="left"><p>4</p></td>
<td align="left"><p>0</p></td>
</tr>
</tbody>
</table>


## <a name="resolution"></a>解像度 
! [デバッグ拡張機能の[**分析**](-analyze.md)] には、バグチェックに関する情報が表示され、根本原因を特定するのに役立ちます。
 

 




