---
title: セキュリティ\_記述子\_コントロール
description: セキュリティ\_記述子\_コントロール
ms.assetid: 6a7fe617-156d-4eb0-83f7-df78104acbde
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9e20fa2d61b7a6e15986a7409c31d289cfd8aaa9
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840972"
---
# <a name="security_descriptor_control"></a>セキュリティ\_記述子\_コントロール


**セキュリティ\_記述子\_コントロール**型は、[**セキュリティ\_記述子**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff556610(v=vs.85))構造体またはそのコンポーネントの意味を修飾する一連のビットフラグです。 各セキュリティ記述子には、**セキュリティ\_記述子\_制御**ビットを格納する**制御**メンバーがあります。

セキュリティ\_記述子\_コントロール

``` syntax
typedef USHORT SECURITY_DESCRIPTOR_CONTROL, *PSECURITY_DESCRIPTOR_CONTROL;
```

コントロールの値には、次の**セキュリティ\_記述子\_制御**ビットフラグの組み合わせを含めることができます。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">Value</th>
<th align="left">意味</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>SE_DACL_AUTO_INHERIT_REQ</p></td>
<td align="left"><p>セキュリティ記述子によって保護されているオブジェクトのプロバイダーが、自動的に DACL を既存の子オブジェクトに伝達するように要求します。 プロバイダーで自動継承がサポートされている場合は、既存の子オブジェクトに DACL を伝達し、オブジェクトとその子オブジェクトのセキュリティ記述子に SE_DACL_AUTO_INHERITED ビットを設定します。</p></td>
</tr>
<tr class="even">
<td align="left"><p>SE_DACL_AUTO_INHERITED</p></td>
<td align="left"><p>Windows 2000 以降、では、DACL が既存の子オブジェクトへの継承可能な Ace の自動伝達をサポートするセキュリティ記述子を示しています。</p>
<p>自動継承をサポートする Windows 2000 Acl の場合、このビットは常に設定されます。 自動継承をサポートしていない Windows NT 4.0 Acl とこれらの Acl を区別するために使用されます。</p>
<p>このビットは、継承可能な Ace の自動伝達をサポートしていない Windows NT 4.0 以前のセキュリティ記述子では設定されません。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>SE_DACL_DEFAULTED</p></td>
<td align="left"><p>既定の DACL を持つセキュリティ記述子を示します。 たとえば、オブジェクトの作成者が DACL を指定していない場合、オブジェクトは作成者のアクセストークンから既定の DACL を受け取ります。 このフラグは、ACE の継承に関して、システムが DACL をどのように処理するかに影響する可能性があります。 SE_DACL_PRESENT フラグが設定されていない場合、システムはこのフラグを無視します。</p>
<p>このフラグは、オブジェクトの最終的な DACL がどのように計算されるかを決定するために使用され、セキュリティ保護可能なオブジェクトのセキュリティ記述子コントロールに物理的に格納されることはありません。</p>
<p>このフラグを設定するには、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-rtlsetdaclsecuritydescriptor" data-raw-source="[&lt;strong&gt;RtlSetDaclSecurityDescriptor&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-rtlsetdaclsecuritydescriptor)"><strong>Rtlsetdaclsecuritydescriptor</strong></a>を使用します。</p></td>
</tr>
<tr class="even">
<td align="left"><p>SE_DACL_PRESENT</p></td>
<td align="left"><p>DACL を持つセキュリティ記述子を示します。 このフラグが設定されていない場合、またはこのフラグが設定され、DACL が<strong>NULL</strong>の場合、セキュリティ記述子はすべてのユーザーにフルアクセスを許可します。</p>
<p>このフラグは、セキュリティ記述子がセキュリティ保護可能なオブジェクトに関連付けられるまで、呼び出し元によって指定されたセキュリティ情報を保持するために使用されます。 セキュリティ記述子がセキュリティ保護可能なオブジェクトに関連付けられると、SE_DACL_PRESENT フラグは常にセキュリティ記述子コントロールで設定されます。</p>
<p>このフラグを設定するには、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-rtlsetdaclsecuritydescriptor" data-raw-source="[&lt;strong&gt;RtlSetDaclSecurityDescriptor&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-rtlsetdaclsecuritydescriptor)"><strong>Rtlsetdaclsecuritydescriptor</strong></a>を使用します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>SE_DACL_PROTECTED</p></td>
<td align="left"><p>セキュリティ記述子の DACL を、継承可能な Ace によって変更されないように保護します。</p></td>
</tr>
<tr class="even">
<td align="left"><p>SE_DACL_UNTRUSTED</p></td>
<td align="left"><p>セキュリティ記述子の DACL によってポイントされた ACL が、信頼されていないソースによって提供されたことを示します。 このフラグが設定されていて、複合 ACE が検出された場合、システムは Ace 内のサーバー Sid に対して既知の有効な Sid を置き換えます。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>SE_GROUP_DEFAULTED</p></td>
<td align="left"><p>セキュリティ記述子のグループ SID を提供する、セキュリティ記述子の元のプロバイダーではなく、既定の機構。</p></td>
</tr>
<tr class="even">
<td align="left"><p>SE_OWNER_DEFAULTED</p></td>
<td align="left"><p>セキュリティ記述子の所有者セキュリティ識別子 (SID) が指定されている場合、セキュリティ記述子の元のプロバイダーではなく、既定の機構。 このフラグを設定するには、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-rtlsetownersecuritydescriptor" data-raw-source="[&lt;strong&gt;RtlSetOwnerSecurityDescriptor&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-rtlsetownersecuritydescriptor)"><strong>RtlSetOwnerSecurityDescriptor</strong></a>を使用します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>SE_RM_CONTROL_VALID</p></td>
<td align="left"><p>セキュリティ記述子のリソースコントロールマネージャービットが有効であることを示します。 リソースマネージャー制御ビットは、構造体にアクセスするリソースマネージャー固有の情報を含む、 <a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff556610(v=vs.85)" data-raw-source="[&lt;strong&gt;SECURITY_DESCRIPTOR&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff556610(v=vs.85))"><strong>SECURITY_DESCRIPTOR</strong></a>構造体の<strong>Sbz1</strong>メンバーの8ビットです。 (詳細については、Microsoft Windows Software Development Kit (SDK) For Windows 7 および .NET Framework 4.0 のドキュメントを参照してください)。</p></td>
</tr>
<tr class="even">
<td align="left"><p>SE_SACL_AUTO_INHERIT_REQ</p></td>
<td align="left"><p>セキュリティ記述子によって保護されているオブジェクトのプロバイダーが、自動的に SACL を既存の子オブジェクトに伝達するように要求します。 プロバイダーで自動継承がサポートされている場合は、既存の子オブジェクトに SACL が伝達され、オブジェクトとその子オブジェクトのセキュリティ記述子に SE_SACL_AUTO_INHERITED ビットが設定されます。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>SE_SACL_AUTO_INHERITED</p></td>
<td align="left"><p>SACL が、既存の子オブジェクトへの継承可能な Ace の自動伝達をサポートするセキュリティ記述子を示します。 このビットは、オブジェクトとその既存の子オブジェクトに対して自動継承アルゴリズムが実行されている場合にのみ設定されます。</p>
<p>このビットは、継承可能な Ace の自動伝達をサポートしていない Windows NT 4.0 以前のセキュリティ記述子では設定されません。</p></td>
</tr>
<tr class="even">
<td align="left"><p>SE_SACL_DEFAULTED</p></td>
<td align="left"><p>SACL によって提供される、セキュリティ記述子の元のプロバイダーではなく、既定の機構。 このフラグは、ACE 継承に関して、システムが SACL をどのように処理するかに影響する可能性があります。 SE_SACL_PRESENT フラグが設定されていない場合、システムはこのフラグを無視します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>SE_SACL_PRESENT</p></td>
<td align="left"><p>SACL を持つセキュリティ記述子を示します。</p></td>
</tr>
<tr class="even">
<td align="left"><p>SE_SACL_PROTECTED</p></td>
<td align="left"><p>継承可能な Ace によってセキュリティ記述子の SACL が変更されないように保護します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>SE_SELF_RELATIVE</p></td>
<td align="left"><p>連続したメモリブロック内のすべてのセキュリティ情報を持つ、自己相対形式のセキュリティ記述子を示します。 このフラグが設定されていない場合、セキュリティ記述子は絶対形式です。 詳細については、Windows SDK のドキュメントの「絶対セキュリティ記述子と自己相対セキュリティ記述子」を参照してください。</p></td>
</tr>
<tr class="even">
<td align="left"><p>SE_SERVER_SECURITY</p></td>
<td align="left"><p>ソース (明示的または既定) に関係なく、ACL が入力 ACL に基づくサーバー ACL を持つオブジェクトのプロバイダーに対して、セキュリティ記述子によって保護されることを要求します。 これは、すべての許可 Ace を、現在のサーバーを許可する複合 Ace に置き換えることによって行われます。 このフラグは、サブジェクトが偽装している場合にのみ意味を持ちます。</p></td>
</tr>
</tbody>
</table>

 

## <a name="requirements"></a>要件


ntifs (ntifs を含む)

## <a name="related-topics"></a>関連トピック


[**ACE**](ace.md)

[ **.ACL**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_acl)

[**RtlSetDaclSecurityDescriptor**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-rtlsetdaclsecuritydescriptor)

[**RtlSetOwnerSecurityDescriptor**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-rtlsetownersecuritydescriptor)

[**セキュリティ\_記述子**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff556610(v=vs.85))

 

 






