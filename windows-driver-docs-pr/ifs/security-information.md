---
title: セキュリティ\_情報
description: セキュリティ\_情報
ms.assetid: 28023f0f-62ae-407b-b81b-1c98499df9a2
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: ee146129b5cadeeed2eb84597108ab6439b4c569
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840968"
---
# <a name="security_information"></a>セキュリティ\_情報


セキュリティ\_情報

``` syntax
typedef ULONG SECURITY_INFORMATION, *PSECURITY_INFORMATION;
```




セキュリティ\_情報型の値は、設定または照会するオブジェクトに関連するセキュリティ情報を識別するために使用されます。 このセキュリティ情報には次のものが含まれます。

-   オブジェクトの所有者

-   オブジェクトのプライマリグループ

-   オブジェクトの随意アクセス制御リスト (DACL)

-   オブジェクトのシステム ACL (SACL)

セキュリティ情報の各項目は、ビットフラグによって指定されます。 次の値はビットを指定します。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">Value</th>
<th align="left">意味</th>
<th align="left">アクセス権</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>DACL_SECURITY_INFORMATION</p></td>
<td align="left"><p>オブジェクトの DACL が設定または照会されていることを示します。</p>
<p>次の項目に対して、DACL に対するクエリが実行されます。</p>
<p>IRP_MJ_QUERY_SECURITY</p>
<p>FLT_PARAMETERS (IRP_MJ_QUERY_SECURITY 用)</p>
<p>FltQuerySecurityObject</p>
<p>Sequerysecurity記述子情報</p>
<p>次の項目について、DACL が設定されます。</p>
<p>IRP_MJ_SET_SECURITY</p>
<p>FLT_PARAMETERS (IRP_MJ_SET_SECURITY 用)</p>
<p>FltSetSecurityObject</p>
<p>Sesetsecurity記述子情報</p>
<p>Sesetsecurity記述子 Infoex</p></td>
<td align="left"><p>次の場合に READ_CONTROL アクセスが必要:</p>
<p>IRP_MJ_QUERY_SECURITY</p>
<p>FLT_PARAMETERS (IRP_MJ_QUERY_SECURITY 用)</p>
<p>FltQuerySecurityObject</p>
<p>Sequerysecurity記述子情報</p>
<p>次の場合に WRITE_DAC アクセスが必要:</p>
<p>IRP_MJ_SET_SECURITY</p>
<p>FLT_PARAMETERS (IRP_MJ_SET_SECURITY 用)</p>
<p>FltSetSecurityObject</p>
<p>Sesetsecurity記述子情報</p>
<p>Sesetsecurity記述子 Infoex</p></td>
</tr>
<tr class="even">
<td align="left"><p>GROUP_SECURITY_INFORMATION</p></td>
<td align="left"><p>オブジェクトのプライマリグループ識別子が設定または照会されていることを示します。</p>
<p>次の項目について、グループ識別子が照会されます。</p>
<p>IRP_MJ_QUERY_SECURITY</p>
<p>FLT_PARAMETERS (IRP_MJ_QUERY_SECURITY 用)</p>
<p>FltQuerySecurityObject</p>
<p>Sequerysecurity記述子情報</p>
<p>IRP_MJ_SET_SECURITY</p>
<p>FLT_PARAMETERS (IRP_MJ_SET_SECURITY 用)</p>
<p>次の項目では、グループ識別子が設定されます。</p>
<p>FltSetSecurityObject</p>
<p>Sesetsecurity記述子情報</p>
<p>Sesetsecurity記述子 Infoex</p></td>
<td align="left"><p>次の場合に READ_CONTROL アクセスが必要:</p>
<p>IRP_MJ_QUERY_SECURITY</p>
<p>FLT_PARAMETERS (IRP_MJ_QUERY_SECURITY 用)</p>
<p>FltQuerySecurityObject</p>
<p>Sequerysecurity記述子情報</p>
<p>次の場合に WRITE_OWNER アクセスが必要:</p>
<p>IRP_MJ_SET_SECURITY</p>
<p>FLT_PARAMETERS (IRP_MJ_SET_SECURITY 用)</p>
<p>FltSetSecurityObject</p>
<p>Sesetsecurity記述子情報</p>
<p>Sesetsecurity記述子 Infoex</p></td>
</tr>
<tr class="odd">
<td align="left"><p>OWNER_SECURITY_INFORMATION</p></td>
<td align="left"><p>オブジェクトの所有者識別子が設定または照会されていることを示します。</p>
<p>次の項目について、所有者識別子が照会されます。</p>
<p>IRP_MJ_QUERY_SECURITY</p>
<p>FLT_PARAMETERS (IRP_MJ_QUERY_SECURITY 用)</p>
<p>FltQuerySecurityObject</p>
<p>Sequerysecurity記述子情報</p>
<p>IRP_MJ_SET_SECURITY</p>
<p>FLT_PARAMETERS (IRP_MJ_SET_SECURITY 用)</p>
<p>次の項目については、所有者識別子が設定されます。</p>
<p>FltSetSecurityObject</p>
<p>Sesetsecurity記述子情報</p>
<p>Sesetsecurity記述子 Infoex</p></td>
<td align="left"><p>次の場合に READ_CONTROL アクセスが必要:</p>
<p>IRP_MJ_QUERY_SECURITY</p>
<p>FLT_PARAMETERS (IRP_MJ_QUERY_SECURITY 用)</p>
<p>FltQuerySecurityObject</p>
<p>Sequerysecurity記述子情報</p>
<p>次の場合に WRITE_OWNER アクセスが必要:</p>
<p>IRP_MJ_SET_SECURITY</p>
<p>FLT_PARAMETERS (IRP_MJ_SET_SECURITY 用)</p>
<p>FltSetSecurityObject</p>
<p>Sesetsecurity記述子情報</p>
<p>Sesetsecurity記述子 Infoex</p></td>
</tr>
<tr class="even">
<td align="left"><p>SACL_SECURITY_INFORMATION</p></td>
<td align="left"><p>オブジェクトの SACL が設定または照会されていることを示します。</p>
<p>次の項目に対して、SACL が照会されます。</p>
<p>IRP_MJ_QUERY_SECURITY</p>
<p>FLT_PARAMETERS (IRP_MJ_QUERY_SECURITY 用)</p>
<p>FltQuerySecurityObject</p>
<p>Sequerysecurity記述子情報</p>
<p>IRP_MJ_SET_SECURITY</p>
<p>FLT_PARAMETERS (IRP_MJ_SET_SECURITY 用)</p>
<p>次の項目について、SACL が設定されます。</p>
<p>FltSetSecurityObject</p>
<p>Sesetsecurity記述子情報</p>
<p>Sesetsecurity記述子 Infoex</p></td>
<td align="left"><p>常に ACCESS_SYSTEM_SECURITY アクセスが必要です。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>PROCESS_TRUST_LABEL_SECURITY_INFORMATION</p></td>
<td align="left"><p>予約済み。</p></td>
<td align="left"></td>
</tr>
</tbody>
</table>

 

## <a name="requirements"></a>要件


Wdm (Wdm を含む)

## <a name="related-topics"></a>関連トピック


[ **.ACL**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_acl)

[**セキュリティ\_記述子**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff556610(v=vs.85))

[**Sequerysecurity記述子情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-sequerysecuritydescriptorinfo)

[**Sesetsecurity記述子情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-sesetsecuritydescriptorinfo)

[**Sesetsecurity記述子 Infoex**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-sesetsecuritydescriptorinfoex)

[**ZwQuerySecurityObject**](https://msdn.microsoft.com/library/windows/hardware/ff567066)

[**ZwSetSecurityObject**](https://msdn.microsoft.com/library/windows/hardware/ff567106)

 

 






