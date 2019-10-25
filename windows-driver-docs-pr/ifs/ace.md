---
title: ACE
description: ACE
ms.assetid: efdf43ae-d4d4-4950-9435-e10bf5b75cf2
keywords:
- アクセス制御エントリ WDK ファイルシステム
- ACE WDK ファイルシステム
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4214610341bc78bee0277767d4f6ee4d4fb29060
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841498"
---
# <a name="ace"></a>ACE





ACE は、アクセス制御リスト (ACL) のアクセス制御エントリ (ACE) です。

次に、現在定義されている ACE 型を示します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">備わっている</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>ACCESS_ALLOWED_ACE</p></td>
<td align="left"><p>指定された権限をユーザーまたはグループに付与します。 この ACE は、随意 ACL (DACL) に格納されます。</p></td>
</tr>
<tr class="even">
<td align="left"><p>ACCESS_DENIED_ACE</p></td>
<td align="left"><p>ユーザーまたはグループに対して指定された権限を拒否します。 この ACE は、DACL に格納されます。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>SYSTEM_AUDIT_ACE</p></td>
<td align="left"><p>システムレベルの監査を実行するアクセスの種類を指定します。 この ACE は、システム ACL (SACL) に格納されます。</p></td>
</tr>
</tbody>
</table>

 

4つ目の ACE 構造、システム\_アラーム\_ACE は、現在サポートされていません。

ACL には、Ace の一覧が含まれています。 ACE は、特定のユーザーまたはグループのオブジェクトへのアクセスを定義するか、特定のユーザーまたはグループのシステム管理メッセージまたはアラームを生成するアクセスの種類を定義します。 ユーザーまたはグループは、セキュリティ識別子 (SID) によって識別されます。

各 ACE は、ACE\_ヘッダー構造で開始されます。 ヘッダーに続くデータの形式は、ヘッダーに指定されている ACE の種類によって異なります。

この構造体は、32ビットの境界上に配置する必要があります。

要件: ntifs (ntifs を含む)

## <a name="related-topics"></a>関連トピック


[**アクセス\_許可\_ACE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_access_allowed_ace)

[**ACE\_アクセス\_拒否されました**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_access_denied_ace)

[**ACE\_ヘッダー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_ace_header)

[ **.ACL**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_acl)

[**RtlAddAccessAllowedAce**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-rtladdaccessallowedace)

[**RtlGetAce**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-rtlgetace)

[**SID**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_sid)

[**システム\_アラーム\_ACE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_system_alarm_ace)

[**SYSTEM\_AUDIT\_ACE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_system_audit_ace)

 

 






