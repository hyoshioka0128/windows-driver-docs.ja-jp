---
title: カーネルモード セーフ文字列関数の概要
description: カーネルモード セーフ文字列関数の概要
ms.assetid: 71b67d88-2a9a-4c9d-b64c-5fd7fe7e5cda
keywords:
- 安全な文字列関数 WDK
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 333d6d54eae985508c8bc3360cc7a88b21b27319
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72836224"
---
# <a name="summary-of-kernel-mode-safe-string-functions"></a>カーネルモード セーフ文字列関数の概要





次の表は、カーネルモードドライバーで使用できる安全な文字列関数をまとめたものです。これらのC++関数は、置換する C/言語ランタイムライブラリ関数を示しています。 関数の名前に**Cb**が含まれている場合、関数は文字列をバイトカウントとして扱います。 関数の名前に**Cch**が含まれている場合、関数は文字列を文字カウントとして扱います。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th>関数</th>
<th>目的</th>
<th>もの</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p></p>
<dl>
<dt> <a href="" id="rtlstringcbcat"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntstrsafe/nf-ntstrsafe-rtlstringcbcata" data-raw-source="[&lt;strong&gt;RtlStringCbCat&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntstrsafe/nf-ntstrsafe-rtlstringcbcata)"></a></a>Rtlstringcbcat</dt>
<dd>
</dd>
<dt> <a href="" id="rtlstringcbcatex"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntstrsafe/nf-ntstrsafe-rtlstringcbcatexa" data-raw-source="[&lt;strong&gt;RtlStringCbCatEx&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntstrsafe/nf-ntstrsafe-rtlstringcbcatexa)"></a></a>Rtlstringcbcatex</dt>
<dd>
</dd>
<dt> <a href="" id="rtlstringcchcat"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntstrsafe/nf-ntstrsafe-rtlstringcchcata" data-raw-source="[&lt;strong&gt;RtlStringCchCat&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntstrsafe/nf-ntstrsafe-rtlstringcchcata)"></a></a>Rtlstringcchcat</dt>
<dd>
</dd>
<dt> <a href="" id="rtlstringcchcatex"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntstrsafe/nf-ntstrsafe-rtlstringcchcatexa" data-raw-source="[&lt;strong&gt;RtlStringCchCatEx&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntstrsafe/nf-ntstrsafe-rtlstringcchcatexa)"></a></a>Rtlstringcchcatex</dt>
<dd>
</dd>
<dt> <a href="" id="rtlunicodestringcat"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntstrsafe/nf-ntstrsafe-rtlunicodestringcat" data-raw-source="[&lt;strong&gt;RtlUnicodeStringCat&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntstrsafe/nf-ntstrsafe-rtlunicodestringcat)"></a></a>RtlUnicodeStringCat</dt>
<dd>
</dd>
<dt> <a href="" id="rtlunicodestringcatex"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntstrsafe/nf-ntstrsafe-rtlunicodestringcatex" data-raw-source="[&lt;strong&gt;RtlUnicodeStringCatEx&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntstrsafe/nf-ntstrsafe-rtlunicodestringcatex)"></a></a>RtlUnicodeStringCatEx</dt>
<dd>
</dd>
<dt> <a href="" id="rtlunicodestringcatstring"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntstrsafe/nf-ntstrsafe-rtlunicodestringcatstring" data-raw-source="[&lt;strong&gt;RtlUnicodeStringCatString&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntstrsafe/nf-ntstrsafe-rtlunicodestringcatstring)"></a></a>RtlUnicodeStringCatString</dt>
<dd>
</dd>
<dt> <a href="" id="rtlunicodestringcatstringex"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntstrsafe/nf-ntstrsafe-rtlunicodestringcatstringex" data-raw-source="[&lt;strong&gt;RtlUnicodeStringCatStringEx&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntstrsafe/nf-ntstrsafe-rtlunicodestringcatstringex)"></a></a>RtlUnicodeStringCatStringEx</dt>
<dd>
</dd>
<dt> <a href="" id="rtlunicodestringcbcatstringn"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntstrsafe/nf-ntstrsafe-rtlunicodestringcbcatstringn" data-raw-source="[&lt;strong&gt;RtlUnicodeStringCbCatStringN&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntstrsafe/nf-ntstrsafe-rtlunicodestringcbcatstringn)"></a></a>RtlUnicodeStringCbCatStringN</dt>
<dd>
</dd>
<dt> <a href="" id="rtlunicodestringcbcatstringnex"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntstrsafe/nf-ntstrsafe-rtlunicodestringcbcatstringnex" data-raw-source="[&lt;strong&gt;RtlUnicodeStringCbCatStringNEx&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntstrsafe/nf-ntstrsafe-rtlunicodestringcbcatstringnex)"></a></a>RtlUnicodeStringCbCatStringNEx</dt>
<dd>
</dd>
<dt> <a href="" id="rtlunicodestringcchcatstringn"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntstrsafe/nf-ntstrsafe-rtlunicodestringcchcatstringn" data-raw-source="[&lt;strong&gt;RtlUnicodeStringCchCatStringN&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntstrsafe/nf-ntstrsafe-rtlunicodestringcchcatstringn)"></a></a>RtlUnicodeStringCchCatStringN</dt>
<dd>
</dd>
<dt> <a href="" id="rtlunicodestringcchcatstringnex"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntstrsafe/nf-ntstrsafe-rtlunicodestringcchcatstringnex" data-raw-source="[&lt;strong&gt;RtlUnicodeStringCchCatStringNEx&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntstrsafe/nf-ntstrsafe-rtlunicodestringcchcatstringnex)"></a></a>RtlUnicodeStringCchCatStringNEx</dt>
<dd>
</dd>
</dl></td>
<td><p>2つの文字列を連結します。</p></td>
<td><p></p>
<dl>
<dt><strong>strcat</strong></dt>
<dd>
</dd>
<dt><strong>wcscat</strong></dt>
<dd>
</dd>
</dl></td>
</tr>
<tr class="even">
<td><p></p>
<dl>
<dt> <a href="" id="rtlstringcbcatn"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntstrsafe/nf-ntstrsafe-rtlstringcbcatna" data-raw-source="[&lt;strong&gt;RtlStringCbCatN&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntstrsafe/nf-ntstrsafe-rtlstringcbcatna)"></a></a>Rtlstringcbcatn</dt>
<dd>
</dd>
<dt> <a href="" id="rtlstringcbcatnex"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntstrsafe/nf-ntstrsafe-rtlstringcbcatnexa" data-raw-source="[&lt;strong&gt;RtlStringCbCatNEx&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntstrsafe/nf-ntstrsafe-rtlstringcbcatnexa)"></a></a>RtlStringCbCatNEx</dt>
<dd>
</dd>
<dt> <a href="" id="rtlstringcchcatn"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntstrsafe/nf-ntstrsafe-rtlstringcchcatna" data-raw-source="[&lt;strong&gt;RtlStringCchCatN&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntstrsafe/nf-ntstrsafe-rtlstringcchcatna)"></a></a>Rtlstringcchcatn</dt>
<dd>
</dd>
<dt> <a href="" id="rtlstringcchcatnex"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntstrsafe/nf-ntstrsafe-rtlstringcchcatnexa" data-raw-source="[&lt;strong&gt;RtlStringCchCatNEx&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntstrsafe/nf-ntstrsafe-rtlstringcchcatnexa)"></a></a>RtlStringCchCatNEx</dt>
<dd>
</dd>
<dt> <a href="" id="rtlunicodestringcbcatn"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntstrsafe/nf-ntstrsafe-rtlunicodestringcbcatn" data-raw-source="[&lt;strong&gt;RtlUnicodeStringCbCatN&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntstrsafe/nf-ntstrsafe-rtlunicodestringcbcatn)"></a></a>RtlUnicodeStringCbCatN</dt>
<dd>
</dd>
<dt> <a href="" id="rtlunicodestringcbcatnex"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntstrsafe/nf-ntstrsafe-rtlunicodestringcbcatnex" data-raw-source="[&lt;strong&gt;RtlUnicodeStringCbCatNEx&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntstrsafe/nf-ntstrsafe-rtlunicodestringcbcatnex)"></a></a>RtlUnicodeStringCbCatNEx</dt>
<dd>
</dd>
<dt> <a href="" id="rtlunicodestringcchcatn"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntstrsafe/nf-ntstrsafe-rtlunicodestringcchcatn" data-raw-source="[&lt;strong&gt;RtlUnicodeStringCchCatN&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntstrsafe/nf-ntstrsafe-rtlunicodestringcchcatn)"></a></a>RtlUnicodeStringCchCatN</dt>
<dd>
</dd>
<dt> <a href="" id="rtlunicodestringcchcatnex"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntstrsafe/nf-ntstrsafe-rtlunicodestringcchcatnex" data-raw-source="[&lt;strong&gt;RtlUnicodeStringCchCatNEx&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntstrsafe/nf-ntstrsafe-rtlunicodestringcchcatnex)"></a></a>RtlUnicodeStringCchCatNEx</dt>
<dd>
</dd>
</dl></td>
<td><p>2つのバイトカウント文字列を連結し、追加する文字列のサイズを制限します。</p></td>
<td><p></p>
<dl>
<dt><strong>strncat</strong></dt>
<dd>
</dd>
<dt><strong>wcsncat</strong></dt>
<dd>
</dd>
</dl></td>
</tr>
<tr class="odd">
<td><p></p>
<dl>
<dt> <a href="" id="rtlstringcbcopy"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntstrsafe/nf-ntstrsafe-rtlstringcbcopya" data-raw-source="[&lt;strong&gt;RtlStringCbCopy&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntstrsafe/nf-ntstrsafe-rtlstringcbcopya)"></a></a>Rtlstringcbcopy</dt>
<dd>
</dd>
<dt> <a href="" id="rtlstringcbcopyex"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntstrsafe/nf-ntstrsafe-rtlstringcbcopyexa" data-raw-source="[&lt;strong&gt;RtlStringCbCopyEx&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntstrsafe/nf-ntstrsafe-rtlstringcbcopyexa)"></a></a>Rtlstringcbcopyex</dt>
<dd>
</dd>
<dt> <a href="" id="rtlstringcbcopyunicodestring"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntstrsafe/nf-ntstrsafe-rtlstringcbcopyunicodestring" data-raw-source="[&lt;strong&gt;RtlStringCbCopyUnicodeString&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntstrsafe/nf-ntstrsafe-rtlstringcbcopyunicodestring)"></a></a>RtlStringCbCopyUnicodeString</dt>
<dd>
</dd>
<dt> <a href="" id="rtlstringcbcopyunicodestringex"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntstrsafe/nf-ntstrsafe-rtlstringcbcopyunicodestringex" data-raw-source="[&lt;strong&gt;RtlStringCbCopyUnicodeStringEx&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntstrsafe/nf-ntstrsafe-rtlstringcbcopyunicodestringex)"></a></a>RtlStringCbCopyUnicodeStringEx</dt>
<dd>
</dd>
<dt> <a href="" id="rtlstringcchcopy"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntstrsafe/nf-ntstrsafe-rtlstringcchcopya" data-raw-source="[&lt;strong&gt;RtlStringCchCopy&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntstrsafe/nf-ntstrsafe-rtlstringcchcopya)"></a></a>Rtlstringcchcopy</dt>
<dd>
</dd>
<dt> <a href="" id="rtlstringcchcopyex"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntstrsafe/nf-ntstrsafe-rtlstringcchcopyexa" data-raw-source="[&lt;strong&gt;RtlStringCchCopyEx&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntstrsafe/nf-ntstrsafe-rtlstringcchcopyexa)"></a></a>Rtlstringcchcopyex</dt>
<dd>
</dd>
<dt> <a href="" id="rtlstringcchcopyunicodestring"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntstrsafe/nf-ntstrsafe-rtlstringcchcopyunicodestring" data-raw-source="[&lt;strong&gt;RtlStringCchCopyUnicodeString&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntstrsafe/nf-ntstrsafe-rtlstringcchcopyunicodestring)"></a></a>RtlStringCchCopyUnicodeString</dt>
<dd>
</dd>
<dt> <a href="" id="rtlstringcchcopyunicodestringex"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntstrsafe/nf-ntstrsafe-rtlstringcchcopyunicodestringex" data-raw-source="[&lt;strong&gt;RtlStringCchCopyUnicodeStringEx&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntstrsafe/nf-ntstrsafe-rtlstringcchcopyunicodestringex)"></a></a>RtlStringCchCopyUnicodeStringEx</dt>
<dd>
</dd>
<dt> <a href="" id="rtlunicodestringcopy"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntstrsafe/nf-ntstrsafe-rtlunicodestringcopy" data-raw-source="[&lt;strong&gt;RtlUnicodeStringCopy&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntstrsafe/nf-ntstrsafe-rtlunicodestringcopy)"></a></a>RtlUnicodeStringCopy</dt>
<dd>
</dd>
<dt> <a href="" id="rtlunicodestringcopyex"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntstrsafe/nf-ntstrsafe-rtlunicodestringcopyex" data-raw-source="[&lt;strong&gt;RtlUnicodeStringCopyEx&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntstrsafe/nf-ntstrsafe-rtlunicodestringcopyex)"></a></a>RtlUnicodeStringCopyEx</dt>
<dd>
</dd>
<dt> <a href="" id="rtlunicodestringcopystring"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntstrsafe/nf-ntstrsafe-rtlunicodestringcopystring" data-raw-source="[&lt;strong&gt;RtlUnicodeStringCopyString&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntstrsafe/nf-ntstrsafe-rtlunicodestringcopystring)"></a></a>RtlUnicodeStringCopyString</dt>
<dd>
</dd>
<dt> <a href="" id="rtlunicodestringcopystringex"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntstrsafe/nf-ntstrsafe-rtlunicodestringcopystringex" data-raw-source="[&lt;strong&gt;RtlUnicodeStringCopyStringEx&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntstrsafe/nf-ntstrsafe-rtlunicodestringcopystringex)"></a></a>RtlUnicodeStringCopyStringEx</dt>
<dd>
</dd>
</dl></td>
<td><p>文字列をバッファーにコピーします。</p></td>
<td><p></p>
<dl>
<dt><strong>strcpy</strong></dt>
<dd>
</dd>
<dt><strong>wcscpy</strong></dt>
<dd>
</dd>
</dl></td>
</tr>
<tr class="even">
<td><p></p>
<dl>
<dt> <a href="" id="rtlstringcbcopyn"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntstrsafe/nf-ntstrsafe-rtlstringcbcopyna" data-raw-source="[&lt;strong&gt;RtlStringCbCopyN&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntstrsafe/nf-ntstrsafe-rtlstringcbcopyna)"></a></a>Rtlstringcbcopyn</dt>
<dd>
</dd>
<dt> <a href="" id="rtlstringcbcopynex"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntstrsafe/nf-ntstrsafe-rtlstringcbcopynexa" data-raw-source="[&lt;strong&gt;RtlStringCbCopyNEx&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntstrsafe/nf-ntstrsafe-rtlstringcbcopynexa)"></a></a>Rtlstringcbcop/ex</dt>
<dd>
</dd>
<dt> <a href="" id="rtlstringcchcopyn"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntstrsafe/nf-ntstrsafe-rtlstringcchcopyna" data-raw-source="[&lt;strong&gt;RtlStringCchCopyN&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntstrsafe/nf-ntstrsafe-rtlstringcchcopyna)"></a></a>Rtlstringcchcopyn</dt>
<dd>
</dd>
<dt> <a href="" id="rtlstringcchcopynex"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntstrsafe/nf-ntstrsafe-rtlstringcchcopynexa" data-raw-source="[&lt;strong&gt;RtlStringCchCopyNEx&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntstrsafe/nf-ntstrsafe-rtlstringcchcopynexa)"></a></a>Rtlstringcchcop/ex</dt>
<dd>
</dd>
<dt> <a href="" id="rtlunicodestringcbcopyn"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntstrsafe/nf-ntstrsafe-rtlunicodestringcbcopyn" data-raw-source="[&lt;strong&gt;RtlUnicodeStringCbCopyN&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntstrsafe/nf-ntstrsafe-rtlunicodestringcbcopyn)"></a></a>RtlUnicodeStringCbCopyN</dt>
<dd>
</dd>
<dt> <a href="" id="rtlunicodestringcbcopynex"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntstrsafe/nf-ntstrsafe-rtlunicodestringcbcopynex" data-raw-source="[&lt;strong&gt;RtlUnicodeStringCbCopyNEx&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntstrsafe/nf-ntstrsafe-rtlunicodestringcbcopynex)"></a></a>RtlUnicodeStringCbCopyNEx</dt>
<dd>
</dd>
<dt> <a href="" id="rtlunicodestringcchcopyn"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntstrsafe/nf-ntstrsafe-rtlunicodestringcchcopyn" data-raw-source="[&lt;strong&gt;RtlUnicodeStringCchCopyN&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntstrsafe/nf-ntstrsafe-rtlunicodestringcchcopyn)"></a></a>RtlUnicodeStringCchCopyN</dt>
<dd>
</dd>
<dt> <a href="" id="rtlunicodestringcchcopynex"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntstrsafe/nf-ntstrsafe-rtlunicodestringcchcopynex" data-raw-source="[&lt;strong&gt;RtlUnicodeStringCchCopyNEx&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntstrsafe/nf-ntstrsafe-rtlunicodestringcchcopynex)"></a></a>RtlUnicodeStringCchCopyNEx</dt>
<dd>
</dd>
<dt> <a href="" id="rtlunicodestringcbcopystringn"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntstrsafe/nf-ntstrsafe-rtlunicodestringcbcopystringn" data-raw-source="[&lt;strong&gt;RtlUnicodeStringCbCopyStringN&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntstrsafe/nf-ntstrsafe-rtlunicodestringcbcopystringn)"></a></a>RtlUnicodeStringCbCopyStringN</dt>
<dd>
</dd>
<dt> <a href="" id="rtlunicodestringcbcopystringnex"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntstrsafe/nf-ntstrsafe-rtlunicodestringcbcopystringnex" data-raw-source="[&lt;strong&gt;RtlUnicodeStringCbCopyStringNEx&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntstrsafe/nf-ntstrsafe-rtlunicodestringcbcopystringnex)"></a></a>RtlUnicodeStringCbCopyStringNEx</dt>
<dd>
</dd>
<dt> <a href="" id="rtlunicodestringcchcopystringn"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntstrsafe/nf-ntstrsafe-rtlunicodestringcchcopystringn" data-raw-source="[&lt;strong&gt;RtlUnicodeStringCchCopyStringN&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntstrsafe/nf-ntstrsafe-rtlunicodestringcchcopystringn)"></a></a>RtlUnicodeStringCchCopyStringN</dt>
<dd>
</dd>
<dt> <a href="" id="rtlunicodestringcchcopystringnex"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntstrsafe/nf-ntstrsafe-rtlunicodestringcchcopystringnex" data-raw-source="[&lt;strong&gt;RtlUnicodeStringCchCopyStringNEx&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntstrsafe/nf-ntstrsafe-rtlunicodestringcchcopystringnex)"></a></a>RtlUnicodeStringCchCopyStringNEx</dt>
<dd>
</dd>
</dl></td>
<td><p>コピーされた文字列のサイズを制限しながら、バッファーに文字列をコピーします。</p></td>
<td><p></p>
<dl>
<dt><strong>strncpy</strong></dt>
<dd>
</dd>
<dt><strong>wcsncpy</strong></dt>
<dd>
</dd>
</dl></td>
</tr>
<tr class="odd">
<td><p></p>
<dl>
<dt> <a href="" id="rtlstringcblength"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntstrsafe/nf-ntstrsafe-rtlstringcblengtha" data-raw-source="[&lt;strong&gt;RtlStringCbLength&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntstrsafe/nf-ntstrsafe-rtlstringcblengtha)"></a></a>RtlStringCbLength</dt>
<dd>
</dd>
<dt> <a href="" id="rtlstringcchlength"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntstrsafe/nf-ntstrsafe-rtlstringcchlengtha" data-raw-source="[&lt;strong&gt;RtlStringCchLength&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntstrsafe/nf-ntstrsafe-rtlstringcchlengtha)"></a></a>Rtlstringcchlength</dt>
<dd>
</dd>
<dt> <a href="" id="rtlunalignedstringcblength"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntstrsafe/nf-ntstrsafe-rtlunalignedstringcblengthw" data-raw-source="[&lt;strong&gt;RtlUnalignedStringCbLength&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntstrsafe/nf-ntstrsafe-rtlunalignedstringcblengthw)"></a></a>RtlUnalignedStringCbLength</dt>
<dd>
</dd>
<dt> <a href="" id="rtlunalignedstringcchlength"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntstrsafe/nf-ntstrsafe-rtlunalignedstringcchlengthw" data-raw-source="[&lt;strong&gt;RtlUnalignedStringCchLength&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntstrsafe/nf-ntstrsafe-rtlunalignedstringcchlengthw)"></a></a>RtlUnalignedStringCchLength</dt>
<dd>
</dd>
</dl></td>
<td><p>指定された文字列の長さを判断します。</p></td>
<td><p></p>
<dl>
<dt><strong>strlen</strong></dt>
<dd>
</dd>
<dt><strong>wcslen</strong></dt>
<dd>
</dd>
</dl></td>
</tr>
<tr class="even">
<td><p></p>
<dl>
<dt> <a href="" id="rtlstringcbprintf"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntstrsafe/nf-ntstrsafe-rtlstringcbprintfa" data-raw-source="[&lt;strong&gt;RtlStringCbPrintf&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntstrsafe/nf-ntstrsafe-rtlstringcbprintfa)"></a></a>Rtlstringcbprintf</dt>
<dd>
</dd>
<dt> <a href="" id="rtlstringcbprintfex"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntstrsafe/nf-ntstrsafe-rtlstringcbprintfexa" data-raw-source="[&lt;strong&gt;RtlStringCbPrintfEx&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntstrsafe/nf-ntstrsafe-rtlstringcbprintfexa)"></a></a>Rtlstringcbprintfex</dt>
<dd>
</dd>
<dt> <a href="" id="rtlstringcchprintf"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntstrsafe/nf-ntstrsafe-rtlstringcchprintfa" data-raw-source="[&lt;strong&gt;RtlStringCchPrintf&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntstrsafe/nf-ntstrsafe-rtlstringcchprintfa)"></a></a>Rtlstringcchprintf</dt>
<dd>
</dd>
<dt> <a href="" id="rtlstringcchprintfex"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntstrsafe/nf-ntstrsafe-rtlstringcchprintfexa" data-raw-source="[&lt;strong&gt;RtlStringCchPrintfEx&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntstrsafe/nf-ntstrsafe-rtlstringcchprintfexa)"></a></a>Rtlstringcchprintfex</dt>
<dd>
</dd>
<dt> <a href="" id="rtlunicodestringprintf"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntstrsafe/nf-ntstrsafe-rtlunicodestringprintf" data-raw-source="[&lt;strong&gt;RtlUnicodeStringPrintf&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntstrsafe/nf-ntstrsafe-rtlunicodestringprintf)"></a></a>RtlUnicodeStringPrintf</dt>
<dd>
</dd>
<dt> <a href="" id="rtlunicodestringprintfex"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntstrsafe/nf-ntstrsafe-rtlunicodestringprintfex" data-raw-source="[&lt;strong&gt;RtlUnicodeStringPrintfEx&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntstrsafe/nf-ntstrsafe-rtlunicodestringprintfex)"></a></a>RtlUnicodeStringPrintfEx</dt>
<dd>
</dd>
</dl></td>
<td><p>書式指定文字列と追加の関数引数のセットに基づいて書式設定されたテキスト文字列を作成します。</p></td>
<td><p></p>
<dl>
<dt><strong>sprintf</strong></dt>
<dd>
</dd>
<dt><strong>swprintf</strong></dt>
<dd>
</dd>
<dt><strong>_snprintf</strong></dt>
<dd>
</dd>
<dt><strong>_snwprintf</strong></dt>
<dd>
</dd>
</dl></td>
</tr>
<tr class="odd">
<td><p></p>
<dl>
<dt> <a href="" id="rtlstringcbvprintf"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntstrsafe/nf-ntstrsafe-rtlstringcbvprintfa" data-raw-source="[&lt;strong&gt;RtlStringCbVPrintf&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntstrsafe/nf-ntstrsafe-rtlstringcbvprintfa)"></a></a>RtlStringCbVPrintf</dt>
<dd>
</dd>
<dt> <a href="" id="rtlstringcbvprintfex"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntstrsafe/nf-ntstrsafe-rtlstringcbvprintfexa" data-raw-source="[&lt;strong&gt;RtlStringCbVPrintfEx&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntstrsafe/nf-ntstrsafe-rtlstringcbvprintfexa)"></a></a>Rtlstringcbvprintfex</dt>
<dd>
</dd>
<dt> <a href="" id="rtlstringcchvprintf"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntstrsafe/nf-ntstrsafe-rtlstringcchvprintfa" data-raw-source="[&lt;strong&gt;RtlStringCchVPrintf&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntstrsafe/nf-ntstrsafe-rtlstringcchvprintfa)"></a></a>RtlStringCchVPrintf</dt>
<dd>
</dd>
<dt> <a href="" id="rtlstringcchvprintfex"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntstrsafe/nf-ntstrsafe-rtlstringcchvprintfexa" data-raw-source="[&lt;strong&gt;RtlStringCchVPrintfEx&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntstrsafe/nf-ntstrsafe-rtlstringcchvprintfexa)"></a></a>Rtlstringcchvprintfex</dt>
<dd>
</dd>
<dt> <a href="" id="rtlunicodestringvprintf"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntstrsafe/nf-ntstrsafe-rtlunicodestringvprintf" data-raw-source="[&lt;strong&gt;RtlUnicodeStringVPrintf&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntstrsafe/nf-ntstrsafe-rtlunicodestringvprintf)"></a></a>RtlUnicodeStringVPrintf</dt>
<dd>
</dd>
<dt> <a href="" id="rtlunicodestringvprintfex"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntstrsafe/nf-ntstrsafe-rtlunicodestringvprintfex" data-raw-source="[&lt;strong&gt;RtlUnicodeStringVPrintfEx&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntstrsafe/nf-ntstrsafe-rtlunicodestringvprintfex)"></a></a>RtlUnicodeStringVPrintfEx</dt>
<dd>
</dd>
</dl></td>
<td><p>書式指定文字列と1つの追加の関数引数に基づいて書式設定されたテキスト文字列を作成します。</p></td>
<td><p></p>
<dl>
<dt><strong>vsprintf</strong></dt>
<dd>
</dd>
<dt><strong>vswprintf</strong></dt>
<dd>
</dd>
<dt><strong>_vsnprintf</strong></dt>
<dd>
</dd>
<dt><strong>_vsnwprintf</strong></dt>
<dd>
</dd>
</dl></td>
</tr>
<tr class="even">
<td><p></p>
<dl>
<dt> <a href="" id="rtlunicodestringinit"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntstrsafe/nf-ntstrsafe-rtlunicodestringinit" data-raw-source="[&lt;strong&gt;RtlUnicodeStringInit&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntstrsafe/nf-ntstrsafe-rtlunicodestringinit)"></a></a>RtlUnicodeStringInit</dt>
<dd>
</dd>
<dt> <a href="" id="rtlunicodestringinitex"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntstrsafe/nf-ntstrsafe-rtlunicodestringinitex" data-raw-source="[&lt;strong&gt;RtlUnicodeStringInitEx&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntstrsafe/nf-ntstrsafe-rtlunicodestringinitex)"></a></a>RtlUnicodeStringInitEx</dt>
<dd>
</dd>
<dt> <a href="" id="rtlunicodestringvalidate"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntstrsafe/nf-ntstrsafe-rtlunicodestringvalidate" data-raw-source="[&lt;strong&gt;RtlUnicodeStringValidate&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntstrsafe/nf-ntstrsafe-rtlunicodestringvalidate)"></a></a>RtlUnicodeStringValidate</dt>
<dd>
</dd>
<dt> <a href="" id="rtlunicodestringvalidateex"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntstrsafe/nf-ntstrsafe-rtlunicodestringvalidateex" data-raw-source="[&lt;strong&gt;RtlUnicodeStringValidateEx&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntstrsafe/nf-ntstrsafe-rtlunicodestringvalidateex)"></a></a>RtlUnicodeStringValidateEx</dt>
<dd>
</dd>
</dl></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfwdm/ns-wudfwdm-_unicode_string" data-raw-source="[&lt;strong&gt;UNICODE_STRING&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfwdm/ns-wudfwdm-_unicode_string)"><strong>UNICODE_STRING</strong></a>構造体を初期化または検証します。</p></td>
<td><p>なし</p></td>
</tr>
</tbody>
</table>

 

 

 




