---
title: アクセス権の指定
description: アクセス権の指定
ms.assetid: 8ef4b4bb-5f4e-4095-b4ab-1182c0f75619
ms.localizationpriority: High
ms.date: 10/17/2018
ms.openlocfilehash: 1b19187224fcfb23dcd82370c4aeb9ed2e3e3492
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72828687"
---
# <a name="specifying-access-rights"></a>アクセス権の指定


ACCESS\_MASK の種類は、[アクセス制御エントリ](https://docs.microsoft.com/windows-hardware/drivers/ifs/access-control-entry)の[アクセス マスク](https://docs.microsoft.com/windows-hardware/drivers/ifs/access-mask)にアクセス権のセットを指定するビットマスクです。

``` syntax
typedef ULONG  ACCESS_MASK;
```

次の標準固有のアクセス権は、すべての種類の実行可能オブジェクトに適用されます。

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
<td><p>呼び出し元が、オブジェクトを削除できます。</p></td>
</tr>
<tr class="even">
<td><p>READ_CONTROL</p></td>
<td><p>呼び出し元が、ファイルのアクセス制御リスト (ACL) と所有権に関する情報を読み取ることができます。</p></td>
</tr>
<tr class="odd">
<td><p>SYNCHRONIZE</p></td>
<td><p>呼び出し元が、オブジェクトに対して待機操作を実行できます。 (たとえば、オブジェクトを <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kewaitformultipleobjects" data-raw-source="[&lt;strong&gt;KeWaitForMultipleObjects&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kewaitformultipleobjects)"><strong>KeWaitForMultipleObjects</strong></a> に渡すことができます。)</p></td>
</tr>
<tr class="even">
<td><p>WRITE_DAC</p></td>
<td><p>呼び出し元が、オブジェクトの随意アクセス制御リスト (DACL) 情報を変更できます。</p></td>
</tr>
<tr class="odd">
<td><p>WRITE_OWNER</p></td>
<td><p>呼び出し元が、ファイルの所有権情報を変更できます。</p></td>
</tr>
</tbody>
</table>

 

通常、ドライバー ライターにとって重要なのは DELETE と SYNCHRONIZE のみです。

次の汎用アクセス権を指定することもできます。 これらも、すべての種類の実行可能オブジェクトに適用されます。 各汎用アクセス権の意味は、そのオブジェクトの種類に固有です。

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
<td><p>呼び出し元が、オブジェクトに対して通常の読み取り操作を実行できます。</p></td>
</tr>
<tr class="even">
<td><p>GENERIC_WRITE</p></td>
<td><p>呼び出し元が、オブジェクトに対して通常の書き込み操作を実行できます。</p></td>
</tr>
<tr class="odd">
<td><p>GENERIC_EXECUTE</p></td>
<td><p>呼び出し元が、オブジェクトを実行できます。 (これは通常、ファイル オブジェクトやセクション オブジェクトなど、特定の種類のオブジェクトでのみ意味があります。)</p></td>
</tr>
<tr class="even">
<td><p>GENERIC_ALL</p></td>
<td><p>呼び出し元が、オブジェクトに対して通常のすべての操作を実行できます。</p></td>
</tr>
</tbody>
</table>

 

標準固有のアクセス権の次の組み合わせも定義されています。 これらは通常、直接は使用されませんが、他のビットマスクを定義するテンプレートとして使用されます。 (たとえば、ファイル オブジェクトに対して GENERIC\_READ を指定すると、システムは特定のアクセス権の FILE\_GENERIC\_READ ビットマスクにこれをマップします。 FILE\_GENERIC\_READ は、STANDARD\_RIGHTS\_READ に関して定義されています。)

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
<td><p>GENERIC_READ に対応する標準固有の権限</p></td>
</tr>
<tr class="even">
<td><p>STANDARD_RIGHTS_WRITE</p></td>
<td><p>GENERIC_WRITE に対応する標準固有の権限</p></td>
</tr>
<tr class="odd">
<td><p>STANDARD_RIGHTS_EXECUTE</p></td>
<td><p>GENERIC_EXECUTE に対応する標準固有の権限</p></td>
</tr>
<tr class="even">
<td><p>STANDARD_RIGHTS_REQUIRED</p></td>
<td><p>GENERIC_ALL に対応する標準固有の権限 これには DELETE が含まれますが、SYNCHRONIZE は含まれません。</p></td>
</tr>
<tr class="odd">
<td><p>STANDARD_RIGHTS_ALL</p></td>
<td><p>すべての標準アクセス権。</p></td>
</tr>
</tbody>
</table>

 

オブジェクトの種類ごとに、独自の追加アクセス権を持つことができます。 ファイル、ディレクトリ、またはデバイスに適用できるアクセス権の詳細については、[**ZwCreateFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-ntcreatefile) に関するページを参照してください。 オブジェクト マネージャー ディレクトリに適用できるアクセス権の詳細については、[**ZwCreateDirectoryObject**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-zwcreatedirectoryobject) に関するページを参照してください。 レジストリ キーに適用できるアクセス権の詳細については、[**ZwCreateKey**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-zwcreatekey) に関するページを参照してください。 セクション オブジェクトに適用できるアクセス権の詳細については、[**ZwOpenSection**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-zwopensection) に関するページを参照してください。 WMI データ ブロックに適用できるアクセス権の詳細については、[**IoWMIOpenBlock**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iowmiopenblock) に関するページを参照してください。

アクセス権の詳細については、Microsoft Windows SDK のドキュメントの次のトピックを参照してください。

-   [アクセス権とアクセス マスク](https://docs.microsoft.com/windows/desktop/SecAuthZ/access-rights-and-access-masks)
-   [ACCESS\_MASK](https://docs.microsoft.com/windows/desktop/SecAuthZ/access-mask)

Wdm.h (Wdm.h、Ntddk.h、Ntifs.h を含む)

## <a name="related-topics"></a>関連トピック
[**IoWMIOpenBlock**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iowmiopenblock)  
[**ZwCreateDirectoryObject**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-zwcreatedirectoryobject)  
[**ZwCreateFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-ntcreatefile)  
[**ZwCreateKey**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-zwcreatekey)  
[**ZwOpenSection**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-zwopensection)  



