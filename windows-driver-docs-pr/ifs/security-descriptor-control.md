---
title: セキュリティ\_記述子\_コントロール
description: セキュリティ\_記述子\_コントロール
ms.assetid: 6a7fe617-156d-4eb0-83f7-df78104acbde
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3739184af0f8c1c972f523d61683bddfe28e9483
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67371338"
---
# <a name="securitydescriptorcontrol"></a>セキュリティ\_記述子\_コントロール


**セキュリティ\_記述子\_コントロール**型は一連のビット フラグの意味を対象となる、 [**セキュリティ\_記述子**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff556610(v=vs.85))構造体またはそのコンポーネント。 各セキュリティ記述子が、**コントロール**を格納するメンバー、**セキュリティ\_記述子\_コントロール**ビット。

セキュリティ\_記述子\_コントロール

``` syntax
typedef USHORT SECURITY_DESCRIPTOR_CONTROL, *PSECURITY_DESCRIPTOR_CONTROL;
```

コントロールの値は、次の組み合わせを含めることができます**セキュリティ\_記述子\_コントロール**ビット フラグ。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">Value</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>SE_DACL_AUTO_INHERIT_REQ</p></td>
<td align="left"><p>要求が自動的にセキュリティ記述子で保護されているオブジェクトのプロバイダーが既存の子オブジェクトに DACL を継承します。 プロバイダーは、自動継承をサポートする場合に、既存の子オブジェクトの DACL を伝達し、オブジェクトとその子オブジェクトのセキュリティ記述子で SE_DACL_AUTO_INHERITED ビットを設定します。</p></td>
</tr>
<tr class="even">
<td align="left"><p>SE_DACL_AUTO_INHERITED</p></td>
<td align="left"><p>Windows 2000 では、以降には、セキュリティ記述子の DACL に既存の子オブジェクトの継承可能な Ace の自動適用がサポートしていることを示します。</p>
<p>自動継承をサポートする Windows 2000 の Acl、このビットは常に設定します。 自動継承をサポートしない Windows NT 4.0 の Acl からこれらの Acl を区別するために使用されます。</p>
<p>Windows NT 4.0 以降での Ace の継承可能な自動伝達がサポートされていないセキュリティ記述子では、このビットは設定されていません。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>SE_DACL_DEFAULTED</p></td>
<td align="left"><p>既定の DACL のセキュリティ記述子を示します。 たとえば、オブジェクトの作成者は、DACL を指定しない場合、オブジェクトは、作成者のアクセス トークンから既定の DACL を受け取ります。 このフラグは、ACE の継承に関して、DACL の処理方法に影響します。 SE_DACL_PRESENT フラグが設定されていない場合、このフラグは無視されます。</p>
<p>このフラグは、オブジェクトの最終的な DACL の計算方法を決定するために使用され、セキュリティ保護可能なオブジェクトのセキュリティ記述子のコントロールに物理的に格納されていません。</p>
<p>このフラグを設定するには使用<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-rtlsetdaclsecuritydescriptor" data-raw-source="[&lt;strong&gt;RtlSetDaclSecurityDescriptor&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-rtlsetdaclsecuritydescriptor)"> <strong>RtlSetDaclSecurityDescriptor</strong></a>します。</p></td>
</tr>
<tr class="even">
<td align="left"><p>SE_DACL_PRESENT</p></td>
<td align="left"><p>DACL のあるセキュリティ記述子を示します。 このフラグが設定されていない場合、またはこのフラグが設定されていて、DACL は<strong>NULL</strong>のセキュリティ記述子は、すべてのユーザーへのフル アクセスを許可します。</p>
<p>このフラグは、セキュリティ記述子にはセキュリティ保護可能なオブジェクトに関連付けられたまで、呼び出し元によって指定されたセキュリティ情報を保持するために使用されます。 セキュリティ記述子は、セキュリティ保護可能なオブジェクトに関連付けられたが、常にセキュリティ記述子制御 SE_DACL_PRESENT フラグが設定されます。</p>
<p>このフラグを設定するには使用<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-rtlsetdaclsecuritydescriptor" data-raw-source="[&lt;strong&gt;RtlSetDaclSecurityDescriptor&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-rtlsetdaclsecuritydescriptor)"> <strong>RtlSetDaclSecurityDescriptor</strong></a>します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>SE_DACL_PROTECTED</p></td>
<td align="left"><p>Ace の継承によって変更されてからセキュリティ記述子の DACL を保護します。</p></td>
</tr>
<tr class="even">
<td align="left"><p>SE_DACL_UNTRUSTED</p></td>
<td align="left"><p>セキュリティ記述子の DACL を指す ACL が信頼できないソースによって提供されていることを示します。 このフラグを設定し、複合 ACE が発生した場合、は、Sid の Ace で、サーバーの既知の有効な Sid が代用されます。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>SE_GROUP_DEFAULTED</p></td>
<td align="left"><p>セキュリティ記述子の元のプロバイダーではなく、既定の機構には、セキュリティ記述子のグループの SID が用意されています。</p></td>
</tr>
<tr class="even">
<td align="left"><p>SE_OWNER_DEFAULTED</p></td>
<td align="left"><p>セキュリティ記述子の元のプロバイダーではなく、既定の機構を提供、セキュリティ記述子の所有者セキュリティ識別子 (SID)。 このフラグを設定するには使用<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-rtlsetownersecuritydescriptor" data-raw-source="[&lt;strong&gt;RtlSetOwnerSecurityDescriptor&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-rtlsetownersecuritydescriptor)"> <strong>RtlSetOwnerSecurityDescriptor</strong></a>します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>SE_RM_CONTROL_VALID</p></td>
<td align="left"><p>セキュリティ記述子内のリソース コントロール マネージャー ビットが有効であることを示します。 リソース マネージャー コントロール ビットは 8 ビットで、 <strong>Sbz1</strong>のメンバー、 <a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff556610(v=vs.85)" data-raw-source="[&lt;strong&gt;SECURITY_DESCRIPTOR&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff556610(v=vs.85))"> <strong>SECURITY_DESCRIPTOR</strong> </a>リソースに固有の情報を含む構造体構造体にアクセスするマネージャー。 (詳細については、Microsoft Windows ソフトウェア開発キット (SDK) for Windows 7 および .NET Framework 4.0 のドキュメントを参照してください)。</p></td>
</tr>
<tr class="even">
<td align="left"><p>SE_SACL_AUTO_INHERIT_REQ</p></td>
<td align="left"><p>要求が自動的にセキュリティ記述子で保護されているオブジェクトのプロバイダーが既存の子オブジェクトに SACL を継承します。 プロバイダーは、自動継承をサポートする場合に、既存の子オブジェクトに SACL を伝達し、オブジェクトとその子オブジェクトのセキュリティ記述子で SE_SACL_AUTO_INHERITED ビットを設定します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>SE_SACL_AUTO_INHERITED</p></td>
<td align="left"><p>セキュリティ記述子の SACL に既存の子オブジェクトの継承可能な Ace の自動適用がサポートしていることを示します。 自動的な継承をアルゴリズムが、オブジェクトとその既存の子オブジェクトに対して行われた場合にのみ、このビットが設定されます。</p>
<p>Windows NT 4.0 以降での Ace の継承可能な自動伝達をサポートしないセキュリティ記述子では、このビットは設定されていません。</p></td>
</tr>
<tr class="even">
<td align="left"><p>SE_SACL_DEFAULTED</p></td>
<td align="left"><p>セキュリティ記述子の元のプロバイダーではなく、既定の機構には、SACL が用意されています。 このフラグは、ACE の継承に関して、SACL の処理方法に影響します。 SE_SACL_PRESENT フラグが設定されていない場合、このフラグは無視されます。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>SE_SACL_PRESENT</p></td>
<td align="left"><p>Sacl のセキュリティ記述子を示します。</p></td>
</tr>
<tr class="even">
<td align="left"><p>SE_SACL_PROTECTED</p></td>
<td align="left"><p>Ace の継承によって変更されてからセキュリティ記述子の SACL を保護します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>SE_SELF_RELATIVE</p></td>
<td align="left"><p>自己相対形式の連続するメモリ ブロックのすべてのセキュリティ情報のセキュリティ記述子を示します。 このフラグが設定されていない場合は、セキュリティ記述子には絶対形式にします。 詳細については、Windows SDK のドキュメントで「絶対と Self-Relative セキュリティ記述子」を参照してください。</p></td>
</tr>
<tr class="even">
<td align="left"><p>SE_SERVER_SECURITY</p></td>
<td align="left"><p>ACL のセキュリティ記述子でオブジェクトのプロバイダーが保護要求には、ACL が (明示的または既定値) は、そのソースに関係なく、入力、ACL に基づいて、サーバーが必要があります。 これは、すべての許可 Ace 複合 Ace に置き換えることにより、現在のサーバーを許可します。 このフラグは、意味のあるサブジェクトが偽装されている場合のみです。</p></td>
</tr>
</tbody>
</table>

 

## <a name="requirements"></a>要件


ntifs.h (ntifs.h を含む)

## <a name="related-topics"></a>関連トピック


[**ACE**](ace.md)

[**ACL**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_acl)

[**RtlSetDaclSecurityDescriptor**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-rtlsetdaclsecuritydescriptor)

[**RtlSetOwnerSecurityDescriptor**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-rtlsetownersecuritydescriptor)

[**セキュリティ\_記述子**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff556610(v=vs.85))

 

 






