---
title: ACE
description: ACE
ms.assetid: efdf43ae-d4d4-4950-9435-e10bf5b75cf2
keywords:
- アクセス制御エントリの WDK ファイル システム
- ACE の WDK ファイル システム
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8107b5a02a195ca7113093dc523de87bfec2784a
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67371935"
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


[**アクセス\_許可\_ACE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/ns-ntifs-_access_allowed_ace)

[**アクセス\_DENIED\_ACE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/ns-ntifs-_access_denied_ace)

[**ACE\_ヘッダー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/ns-ntifs-_ace_header)

[**ACL**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_acl)

[**RtlAddAccessAllowedAce**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-rtladdaccessallowedace)

[**RtlGetAce**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-rtlgetace)

[**SID**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/ns-ntifs-_sid)

[**システム\_アラーム\_ACE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/ns-ntifs-_system_alarm_ace)

[**システム\_監査\_ACE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/ns-ntifs-_system_audit_ace)

 

 






