---
title: アクセス権の指定
description: アクセス権の指定
ms.assetid: 8ef4b4bb-5f4e-4095-b4ab-1182c0f75619
ms.localizationpriority: High
ms.date: 10/17/2018
ms.openlocfilehash: 1371cff860e97ddca0d116d3cc055a7c33fed65c
ms.sourcegitcommit: c73954a5909ec8c7e189f77fd5813f2eb749687c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/07/2019
ms.locfileid: "72007640"
---
# <a name="specifying-access-rights"></a>アクセス権の指定


Access @ no__t-0MASK の種類は、アクセス[制御エントリ](https://docs.microsoft.com/windows-hardware/drivers/ifs/access-control-entry)の[アクセスマスク](https://docs.microsoft.com/windows-hardware/drivers/ifs/access-mask)のアクセス権のセットを指定するビットマスクです。

``` syntax
typedef ULONG  ACCESS_MASK;
```

次の標準のアクセス権は、すべての種類の executive オブジェクトに適用されます。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>フラグ</th>
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
<td><p>呼び出し元は、ファイルのアクセス制御リスト (ACL) と所有権に関する情報を読み取ることができます。</p></td>
</tr>
<tr class="odd">
<td><p>SYNCHRONIZE</p></td>
<td><p>呼び出し元は、オブジェクトに対して待機操作を実行できます。 (たとえば、オブジェクトを<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-kewaitformultipleobjects" data-raw-source="[&lt;strong&gt;KeWaitForMultipleObjects&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-kewaitformultipleobjects)"><strong>KeWaitForMultipleObjects</strong></a>に渡すことができます)。</p></td>
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

 

通常、削除と同期だけがドライバーライターにとって重要であることに注意してください。

次の汎用アクセス権を指定することもできます。 これらは、すべての種類の executive オブジェクトにも適用されます。 各汎用アクセス権の意味は、そのオブジェクトの種類に固有です。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>フラグ</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>GENERIC_READ</p></td>
<td><p>呼び出し元は、オブジェクトに対して通常の読み取り操作を実行できます。</p></td>
</tr>
<tr class="even">
<td><p>GENERIC_WRITE</p></td>
<td><p>呼び出し元は、オブジェクトに対する通常の書き込み操作を実行できます。</p></td>
</tr>
<tr class="odd">
<td><p>GENERIC_EXECUTE</p></td>
<td><p>呼び出し元は、オブジェクトを実行できます。 (通常、ファイルオブジェクトやセクションオブジェクトなど、特定の種類のオブジェクトに対してのみ意味があります)。</p></td>
</tr>
<tr class="even">
<td><p>GENERIC_ALL</p></td>
<td><p>呼び出し元は、オブジェクトに対する通常のすべての操作を実行できます。</p></td>
</tr>
</tbody>
</table>

 

標準固有のアクセス権の次の組み合わせも定義されています。 これらは通常直接使用されませんが、他のビットマスクを定義するテンプレートとして使用されます。 (たとえば、ファイルオブジェクトに対して GENERIC @ no__t-0READ を指定すると、特定のアクセス権のファイル @ no__t-1GENERIC @ no__t-2READ ビットマスクにマップされます。 FILE @ no__t-0GENERIC @ no__t-1READ は、STANDARD @ no__t-2RIGHTS @ no__t-3READ の観点で定義されています。)

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>ビットマップ</th>
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
<td><p>GENERIC_ALL に対応する標準固有の権限。 これには、削除が含まれますが、同期は行われません。</p></td>
</tr>
<tr class="odd">
<td><p>STANDARD_RIGHTS_ALL</p></td>
<td><p>すべての標準アクセス権。</p></td>
</tr>
</tbody>
</table>

 

オブジェクトの種類ごとに、独自の追加アクセス権を持つことができます。 ファイル、ディレクトリ、またはデバイスに適用できるアクセス権の詳細については、「 [**Zwcreatefile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-ntcreatefile)」を参照してください。 オブジェクトマネージャーディレクトリに適用できるアクセス権の詳細については、「 [**Zwcreatedirectoryobject**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-zwcreatedirectoryobject)」を参照してください。 レジストリキーに適用できるアクセス権の詳細については、「 [**ZwCreateKey**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-zwcreatekey)」を参照してください。 セクションオブジェクトに適用できるアクセス権の詳細については、「 [**Zwopensection セクション**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-zwopensection)を参照してください。 WMI データブロックに適用できるアクセス権の詳細については、「 [**Iowmiopenblock**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iowmiopenblock)」を参照してください。

アクセス権の詳細については、Microsoft Windows SDK のドキュメントの次のトピックを参照してください。

-   [アクセス権とアクセスマスク](https://docs.microsoft.com/windows/desktop/SecAuthZ/access-rights-and-access-masks)
-   [ACCESS @ NO__T-1 MASK](https://docs.microsoft.com/windows/desktop/SecAuthZ/access-mask)

Wdm (Wdm .h、Ntddk、または Ntifs を含む)

## <a name="related-topics"></a>関連トピック
[**IoWMIOpenBlock**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iowmiopenblock)  
[**ZwCreateDirectoryObject**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-zwcreatedirectoryobject)  
[**ZwCreateFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-ntcreatefile)  
[**ZwCreateKey**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-zwcreatekey)  
[**ZwOpenSection**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-zwopensection)  



