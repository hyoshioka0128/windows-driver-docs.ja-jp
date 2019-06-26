---
title: セキュリティ\_情報
description: セキュリティ\_情報
ms.assetid: 28023f0f-62ae-407b-b81b-1c98499df9a2
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 29d4ba2e9766057e6ed226a81c75d80f4b7027f0
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67371335"
---
# <a name="securityinformation"></a>セキュリティ\_情報


セキュリティ\_情報

``` syntax
typedef ULONG SECURITY_INFORMATION, *PSECURITY_INFORMATION;
```




セキュリティの種類の値を\_設定または照会されるオブジェクトに関連するセキュリティ情報を識別する情報が使用されます。 このセキュリティ情報が含まれます。

-   オブジェクトの所有者

-   オブジェクトのプライマリ グループ

-   オブジェクトの随意アクセス制御リスト (DACL)

-   オブジェクトのシステム ACL (SACL)

セキュリティ情報の各項目は、ビット フラグで指定されます。 次の値は、ビットを指定します。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">Value</th>
<th align="left">説明</th>
<th align="left">アクセス権</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>DACL_SECURITY_INFORMATION</p></td>
<td align="left"><p>オブジェクトの DACL されていることを示しますセットまたはクエリを実行します。</p>
<p>次の項目の DACL がクエリします。</p>
<p>IRP_MJ_QUERY_SECURITY</p>
<p>FLT_PARAMETERS (IRP_MJ_QUERY_SECURITY 用)</p>
<p>FltQuerySecurityObject</p>
<p>SeQuerySecurityDescriptorInfo</p>
<p>次のものでは、DACL を設定します。</p>
<p>IRP_MJ_SET_SECURITY</p>
<p>FLT_PARAMETERS (IRP_MJ_SET_SECURITY 用)</p>
<p>FltSetSecurityObject</p>
<p>SeSetSecurityDescriptorInfo</p>
<p>SeSetSecurityDescriptorInfoEx</p></td>
<td align="left"><p>READ_CONTROL のアクセスが必要です。</p>
<p>IRP_MJ_QUERY_SECURITY</p>
<p>FLT_PARAMETERS (IRP_MJ_QUERY_SECURITY 用)</p>
<p>FltQuerySecurityObject</p>
<p>SeQuerySecurityDescriptorInfo</p>
<p>対する WRITE_DAC アクセス許可が必要です。</p>
<p>IRP_MJ_SET_SECURITY</p>
<p>FLT_PARAMETERS (IRP_MJ_SET_SECURITY 用)</p>
<p>FltSetSecurityObject</p>
<p>SeSetSecurityDescriptorInfo</p>
<p>SeSetSecurityDescriptorInfoEx</p></td>
</tr>
<tr class="even">
<td align="left"><p>GROUP_SECURITY_INFORMATION</p></td>
<td align="left"><p>オブジェクトのプライマリ グループ識別子がされていることを示すセットまたはクエリを実行します。</p>
<p>次の項目のグループ識別子がクエリします。</p>
<p>IRP_MJ_QUERY_SECURITY</p>
<p>FLT_PARAMETERS (IRP_MJ_QUERY_SECURITY 用)</p>
<p>FltQuerySecurityObject</p>
<p>SeQuerySecurityDescriptorInfo</p>
<p>IRP_MJ_SET_SECURITY</p>
<p>FLT_PARAMETERS (IRP_MJ_SET_SECURITY 用)</p>
<p>次の項目のグループ識別子が設定されます。</p>
<p>FltSetSecurityObject</p>
<p>SeSetSecurityDescriptorInfo</p>
<p>SeSetSecurityDescriptorInfoEx</p></td>
<td align="left"><p>READ_CONTROL のアクセスが必要です。</p>
<p>IRP_MJ_QUERY_SECURITY</p>
<p>FLT_PARAMETERS (IRP_MJ_QUERY_SECURITY 用)</p>
<p>FltQuerySecurityObject</p>
<p>SeQuerySecurityDescriptorInfo</p>
<p>WRITE_OWNER のアクセスが必要です。</p>
<p>IRP_MJ_SET_SECURITY</p>
<p>FLT_PARAMETERS (IRP_MJ_SET_SECURITY 用)</p>
<p>FltSetSecurityObject</p>
<p>SeSetSecurityDescriptorInfo</p>
<p>SeSetSecurityDescriptorInfoEx</p></td>
</tr>
<tr class="odd">
<td align="left"><p>OWNER_SECURITY_INFORMATION</p></td>
<td align="left"><p>オブジェクトの所有者の識別子がされていることを示すセットまたはクエリを実行します。</p>
<p>次の項目の所有者の識別子がクエリします。</p>
<p>IRP_MJ_QUERY_SECURITY</p>
<p>FLT_PARAMETERS (IRP_MJ_QUERY_SECURITY 用)</p>
<p>FltQuerySecurityObject</p>
<p>SeQuerySecurityDescriptorInfo</p>
<p>IRP_MJ_SET_SECURITY</p>
<p>FLT_PARAMETERS (IRP_MJ_SET_SECURITY 用)</p>
<p>次の項目の所有者の識別子を設定します。</p>
<p>FltSetSecurityObject</p>
<p>SeSetSecurityDescriptorInfo</p>
<p>SeSetSecurityDescriptorInfoEx</p></td>
<td align="left"><p>READ_CONTROL のアクセスが必要です。</p>
<p>IRP_MJ_QUERY_SECURITY</p>
<p>FLT_PARAMETERS (IRP_MJ_QUERY_SECURITY 用)</p>
<p>FltQuerySecurityObject</p>
<p>SeQuerySecurityDescriptorInfo</p>
<p>WRITE_OWNER のアクセスが必要です。</p>
<p>IRP_MJ_SET_SECURITY</p>
<p>FLT_PARAMETERS (IRP_MJ_SET_SECURITY 用)</p>
<p>FltSetSecurityObject</p>
<p>SeSetSecurityDescriptorInfo</p>
<p>SeSetSecurityDescriptorInfoEx</p></td>
</tr>
<tr class="even">
<td align="left"><p>SACL_SECURITY_INFORMATION</p></td>
<td align="left"><p>オブジェクトの SACL されていることを示しますセットまたはクエリを実行します。</p>
<p>次のものでは、SACL がクエリします。</p>
<p>IRP_MJ_QUERY_SECURITY</p>
<p>FLT_PARAMETERS (IRP_MJ_QUERY_SECURITY 用)</p>
<p>FltQuerySecurityObject</p>
<p>SeQuerySecurityDescriptorInfo</p>
<p>IRP_MJ_SET_SECURITY</p>
<p>FLT_PARAMETERS (IRP_MJ_SET_SECURITY 用)</p>
<p>次のものでは、SACL を設定します。</p>
<p>FltSetSecurityObject</p>
<p>SeSetSecurityDescriptorInfo</p>
<p>SeSetSecurityDescriptorInfoEx</p></td>
<td align="left"><p>すべてのケースで ACCESS_SYSTEM_SECURITY へのアクセスが必要です。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>PROCESS_TRUST_LABEL_SECURITY_INFORMATION</p></td>
<td align="left"><p>予約済み。</p></td>
<td align="left"></td>
</tr>
</tbody>
</table>

 

## <a name="requirements"></a>必要条件


Wdm.h (Wdm.h を含む)

## <a name="related-topics"></a>関連トピック


[**ACL**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_acl)

[**セキュリティ\_記述子**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff556610(v=vs.85))

[**SeQuerySecurityDescriptorInfo**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-sequerysecuritydescriptorinfo)

[**SeSetSecurityDescriptorInfo**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-sesetsecuritydescriptorinfo)

[**SeSetSecurityDescriptorInfoEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-sesetsecuritydescriptorinfoex)

[**ZwQuerySecurityObject**](https://msdn.microsoft.com/library/windows/hardware/ff567066)

[**ZwSetSecurityObject**](https://msdn.microsoft.com/library/windows/hardware/ff567106)

 

 






