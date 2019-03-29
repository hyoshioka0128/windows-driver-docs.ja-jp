---
title: ACE
description: ACE
ms.assetid: efdf43ae-d4d4-4950-9435-e10bf5b75cf2
keywords:
- アクセス制御エントリの WDK ファイル システム
- ACE の WDK ファイル システム
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: c09852728fe16ca66bf2b8aaa4306f602e0d0861
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56579105"
---
# <a name="ace"></a>ACE





ACE は、アクセス制御リスト (ACL) でアクセス制御エントリ (ACE) です。

現在定義されている ACE 型を次に示します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">属性</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>ACCESS_ALLOWED_ACE</p></td>
<td align="left"><p>許可は、ユーザーまたはグループに権限を指定します。 この ACE は、随意 ACL (DACL) 内に格納されます。</p></td>
</tr>
<tr class="even">
<td align="left"><p>ACCESS_DENIED_ACE</p></td>
<td align="left"><p>ユーザーまたはグループに指定された権限を拒否します。 この ACE は、DACL で格納されます。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>SYSTEM_AUDIT_ACE</p></td>
<td align="left"><p>どのような種類のアクセスが発生するシステム レベルの監査を指定します。 この ACE は、システムの ACL (SACL) に格納されます。</p></td>
</tr>
</tbody>
</table>

 

4 つ目の ACE の構造、システム\_アラーム\_ACE、現在サポートされていません。

ACL には、Ace のリストが含まれています。 ACE は、特定のユーザーまたはグループのオブジェクトへのアクセスを定義またはシステム管理メッセージまたは特定のユーザーまたはグループのアラームを生成するアクセスの種類を定義します。 ユーザーまたはグループは、セキュリティ識別子 (SID) によって識別されます。

各 ACE の ACE が始まる\_ヘッダー構造体。 ヘッダーの後のデータの形式は、ヘッダーで指定された ACE 型によって異なります。

この構造体は、32 ビットの境界に合わせて調整する必要があります。

要件: ntifs.h (ntifs.h を含む)

## <a name="related-topics"></a>関連トピック


[**アクセス\_許可\_ACE**](https://msdn.microsoft.com/library/windows/hardware/ff538796)

[**アクセス\_DENIED\_ACE**](https://msdn.microsoft.com/library/windows/hardware/ff538831)

[**ACE\_ヘッダー**](https://msdn.microsoft.com/library/windows/hardware/ff538847)

[**ACL**](https://msdn.microsoft.com/library/windows/hardware/ff538866)

[**RtlAddAccessAllowedAce**](https://msdn.microsoft.com/library/windows/hardware/ff552092)

[**RtlGetAce**](https://msdn.microsoft.com/library/windows/hardware/ff552288)

[**SID**](https://msdn.microsoft.com/library/windows/hardware/ff556740)

[**システム\_アラーム\_ACE**](https://msdn.microsoft.com/library/windows/hardware/ff556769)

[**システム\_監査\_ACE**](https://msdn.microsoft.com/library/windows/hardware/ff556771)

 

 






