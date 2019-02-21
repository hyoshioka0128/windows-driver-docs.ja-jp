---
title: IPrinterBidiSchemaResponses インターフェイス
description: IPrinterBidiSchemaResponses インターフェイスは、USB Bidi 拡張機能 JavaScript メソッド getSchemas と getStatus によって設定されます bidi 応答のセットを表します。
MSHAttr:
- PreferredSiteName:MSDN
- PreferredLib:/library/windows/hardware
ms.assetid: 2E68C4AA-D235-46D2-81D6-D6C7E84C2FEF
keywords:
- IPrinterBidiSchemaResponses 印刷デバイスをインターフェイスします。
- IPrinterBidiSchemaResponses 記載されている印刷デバイスをインターフェイスします。
topic_type:
- apiref
api_name:
- IPrinterBidiSchemaResponses
api_type:
- COM
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: bd0284b80dbeeaf157c5686fb72ba242d816bb1e
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56559666"
---
# <a name="iprinterbidischemaresponses-interface"></a>IPrinterBidiSchemaResponses インターフェイス

IPrinterBidiSchemaResponses インターフェイスが USB Bidi 拡張機能 JavaScript メソッドによって設定されます bidi 応答のセットを表す**getSchemas**と**getStatus**します。

<a name="members"></a>Members
-------

**IPrinterBidiSchemaResponses**インターフェイスから継承、 [ **IUnknown** ](https://docs.microsoft.com/windows/desktop/api/unknwn/nn-unknwn-iunknown)インターフェイス。 **IPrinterBidiSchemaResponses**これらの種類のメンバーがあります。

-   [メソッド](#methods)

### <a name="methods"></a>メソッド

**IPrinterBidiSchemaResponses**インターフェイスがこれらのメソッド。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>メソッド</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><a href="iprinterbidischemaresponses--addbool.md" data-raw-source="[&lt;strong&gt;AddBool&lt;/strong&gt;](iprinterbidischemaresponses--addbool.md)"><strong>AddBool</strong></a></td>
<td><p>AddBool メソッドは、型 BIDI_BOOL の新しい応答をコレクションに追加します。</p></td>
</tr>
<tr class="even">
<td><a href="iprinterbidischemaresponses--addint32.md" data-raw-source="[&lt;strong&gt;AddInt32&lt;/strong&gt;](iprinterbidischemaresponses--addint32.md)"><strong>AddInt32</strong></a></td>
<td><p>AddInt32 メソッドは、型 BIDI_INT の新しい応答をコレクションに追加します。</p></td>
</tr>
<tr class="odd">
<td><a href="iprinterbidischemaresponses-addblob.md" data-raw-source="[&lt;strong&gt;AddBlob&lt;/strong&gt;](iprinterbidischemaresponses-addblob.md)"><strong>AddBlob</strong></a></td>
<td><p>AddBlob メソッドは、型 BIDI_BLOB の新しい応答をコレクションに追加します。</p></td>
</tr>
<tr class="even">
<td><a href="iprinterbidischemaresponses-addenum.md" data-raw-source="[&lt;strong&gt;AddEnum&lt;/strong&gt;](iprinterbidischemaresponses-addenum.md)"><strong>AddEnum</strong></a></td>
<td><p>AddEnum メソッドは、型 BIDI_ENUM の新しい応答をコレクションに追加します。</p></td>
</tr>
<tr class="odd">
<td><a href="iprinterbidischemaresponses-addfloat.md" data-raw-source="[&lt;strong&gt;AddFloat&lt;/strong&gt;](iprinterbidischemaresponses-addfloat.md)"><strong>AddFloat</strong></a></td>
<td><p>AddFloat メソッドは、型 BIDI_FLOAT の新しい応答をコレクションに追加します。</p></td>
</tr>
<tr class="even">
<td><a href="iprinterbidischemaresponses-addnull.md" data-raw-source="[&lt;strong&gt;AddNull&lt;/strong&gt;](iprinterbidischemaresponses-addnull.md)"><strong>AddNull</strong></a></td>
<td><p>AddNull メソッドは、型 BIDI_NULL の新しい応答をコレクションに追加します。</p></td>
</tr>
<tr class="odd">
<td><a href="iprinterbidischemaresponses-addrequerykey.md" data-raw-source="[&lt;strong&gt;AddRequeryKey&lt;/strong&gt;](iprinterbidischemaresponses-addrequerykey.md)"><strong>AddRequeryKey</strong></a></td>
<td><p>GetSchemas 呼び出しからの戻り時に再クエリする新しい QueryKey を AddRequeryKey メソッドに追加します。</p></td>
</tr>
<tr class="even">
<td><a href="iprinterbidischemaresponses-addstring.md" data-raw-source="[&lt;strong&gt;AddString&lt;/strong&gt;](iprinterbidischemaresponses-addstring.md)"><strong>AddString</strong></a></td>
<td><p>AddString メソッドは、型 BIDI_STRING の新しい応答をコレクションに追加します。</p></td>
</tr>
<tr class="odd">
<td><a href="iprinterbidischemaresponses-addtext.md" data-raw-source="[&lt;strong&gt;AddText&lt;/strong&gt;](iprinterbidischemaresponses-addtext.md)"><strong>AddText</strong></a></td>
<td><p>AddText メソッドは、型 BIDI_TEXT の新しい応答をコレクションに追加します。</p></td>
</tr>
</tbody>
</table>
