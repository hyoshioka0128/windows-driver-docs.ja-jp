---
title: アクセス権の指定
description: アクセス権の指定
ms.assetid: 8ef4b4bb-5f4e-4095-b4ab-1182c0f75619
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: e77526cb40bb9d43d099040fc06cbff517701437
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67363472"
---
# <a name="specifying-access-rights"></a>アクセス権の指定


アクセス\_マスクの種類のアクセス権限のセットを示すビットマスクである、[アクセス マスク](https://docs.microsoft.com/windows-hardware/drivers/ifs/access-mask)の[アクセス制御エントリ](https://docs.microsoft.com/windows-hardware/drivers/ifs/access-control-entry)します。

``` syntax
typedef ULONG  ACCESS_MASK;
```

次の標準の特定のアクセス権は、executive オブジェクトのすべての種類に適用されます。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>Flag</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>DELETE</p></td>
<td><p>呼び出し元は、オブジェクトを削除できます。</p></td>
</tr>
<tr class="even">
<td><p>READ_CONTROL</p></td>
<td><p>呼び出し元には、アクセス制御リスト (ACL) とファイルの所有権情報を読み取ることができます。</p></td>
</tr>
<tr class="odd">
<td><p>SYNCHRONIZE</p></td>
<td><p>呼び出し元は、オブジェクトの待機操作を実行できます。 (たとえばにオブジェクトを渡すことができます<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-kewaitformultipleobjects" data-raw-source="[&lt;strong&gt;KeWaitForMultipleObjects&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-kewaitformultipleobjects)"> <strong>KeWaitForMultipleObjects</strong></a>)。</p></td>
</tr>
<tr class="even">
<td><p>WRITE_DAC</p></td>
<td><p>呼び出し元は、オブジェクトの随意アクセス制御リスト (DACL) 情報を変更できます。</p></td>
</tr>
<tr class="odd">
<td><p>WRITE_OWNER</p></td>
<td><p>呼び出し元は、ファイルの所有権情報を変更できます。</p></td>
</tr>
</tbody>
</table>

 

通常のみの削除と同期がドライバー開発者を対象に注意してください。

次の汎用的なアクセス権を指定することもできます。 これらは、executive オブジェクトのすべての種類にも適用されます。 各汎用的なアクセス権の意味は、そのオブジェクトの種類に固有です。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>Flag</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>GENERIC_READ</p></td>
<td><p>呼び出し元は、オブジェクトの通常の読み取り操作を実行できます。</p></td>
</tr>
<tr class="even">
<td><p>GENERIC_WRITE</p></td>
<td><p>呼び出し元のオブジェクトの通常の書き込み操作を実行できます。</p></td>
</tr>
<tr class="odd">
<td><p>GENERIC_EXECUTE</p></td>
<td><p>呼び出し元は、オブジェクトを実行できます。 (一般にのみ意味を特定の種類のファイルおよびセクション オブジェクトなどのオブジェクトに注意してください)。</p></td>
</tr>
<tr class="even">
<td><p>GENERIC_ALL</p></td>
<td><p>呼び出し元は、オブジェクトに対するすべての通常の操作を実行できます。</p></td>
</tr>
</tbody>
</table>

 

次のような標準の特定のアクセス権の組み合わせも定義されます。 これらは、直接、通常使用はされませんが、他のビットマスクを定義するテンプレートとして使用されます。 (たとえば、ジェネリックを指定する\_ファイル オブジェクトの読み取り、システムでは、このファイルに\_ジェネリック\_特定のアクセス権の読み取りのビットマスク。 ファイル\_ジェネリック\_読み取りが標準の観点から定義されている\_RIGHTS\_読む)。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>ビットマスク</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>STANDARD_RIGHTS_READ</p></td>
<td><p>GENERIC_READ に対応する標準の特定の権限</p></td>
</tr>
<tr class="even">
<td><p>STANDARD_RIGHTS_WRITE</p></td>
<td><p>GENERIC_WRITE に対応する標準の特定の権限</p></td>
</tr>
<tr class="odd">
<td><p>STANDARD_RIGHTS_EXECUTE</p></td>
<td><p>GENERIC_EXECUTE に対応する標準の特定の権限</p></td>
</tr>
<tr class="even">
<td><p>STANDARD_RIGHTS_REQUIRED</p></td>
<td><p>GENERIC_ALL に対応する標準的な特定権限。 これには、DELETE はない同期が含まれます。</p></td>
</tr>
<tr class="odd">
<td><p>STANDARD_RIGHTS_ALL</p></td>
<td><p>すべての標準アクセス権。</p></td>
</tr>
</tbody>
</table>

 

オブジェクトの種類ごとに独自の追加のアクセス権をことができます。 ファイル、ディレクトリ、またはデバイスに適用されるアクセス権については、次を参照してください。 [ **ZwCreateFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-ntcreatefile)します。 オブジェクト マネージャーのディレクトリに適用されるアクセス権については、次を参照してください。 [ **ZwCreateDirectoryObject**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-zwcreatedirectoryobject)します。 レジストリ キーに適用されるアクセス権については、次を参照してください。 [ **ZwCreateKey**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-zwcreatekey)します。 セクション オブジェクトに適用されるアクセス権については、次を参照してください。 [ **ZwOpenSection**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-zwopensection)します。 WMI データのブロックに適用されるアクセス権については、次を参照してください。 [ **IoWMIOpenBlock**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iowmiopenblock)します。

アクセス権の詳細については、Microsoft Windows SDK のドキュメントでは、次のトピックを参照してください。

-   [アクセス権やアクセス マスク](https://docs.microsoft.com/windows/desktop/SecAuthZ/access-rights-and-access-masks)
-   [アクセス\_マスク](https://docs.microsoft.com/windows/desktop/SecAuthZ/access-mask)

Wdm.h (Wdm.h、Ntddk.h、Ntifs.h など)

## <a name="related-topics"></a>関連トピック
[**IoWMIOpenBlock**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iowmiopenblock)  
[**ZwCreateDirectoryObject**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-zwcreatedirectoryobject)  
[**ZwCreateFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-ntcreatefile)  
[**ZwCreateKey**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-zwcreatekey)  
[**ZwOpenSection**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-zwopensection)  



