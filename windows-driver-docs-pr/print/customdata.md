---
title: customData 要素
description: 省略可能な customData 要素には、この非同期通知の XML スキーマのカスタム データ ソースを指定します。
ms.assetid: 5e14a627-72c0-440d-b616-6963c3d69d2b
keywords:
- customData 要素印刷デバイス
topic_type:
- apiref
api_name:
- customData
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: ea25442cd8a1eabed1831b904a72b2526b7c90b7
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63365552"
---
# <a name="customdata-element"></a>customData 要素


省略可能な**customData**要素は、この非同期通知の XML スキーマのカスタム データ ソースを指定します。

**CustomData**で要素が定義されている、 *asyncui*この URI に、名前空間: http://schemas.microsoft.com/2003/print/asyncui/v1/request します。 (このリソースできない場合がありますのいくつかの言語および国。)

<a name="usage"></a>使用方法
-----

```xml
<customData
  dll = "xs:string"
  entryPoint = "xs:string"
  bidi = "xs:string">
  child elements
</customData>
```

<a name="attributes"></a>属性
----------

<table>
<colgroup>
<col width="25%" />
<col width="25%" />
<col width="25%" />
<col width="25%" />
</colgroup>
<thead>
<tr class="header">
<th>属性</th>
<th>種類</th>
<th>必須</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>bidi</strong></p></td>
<td><p>xs:string</p></td>
<td><p>〇</p></td>
<td><p></p>
<p>プリンター ドライバーと、イベント通知メッセージ間の通信の種類を指定する必須の属性。 値が場合<strong>true</strong>通信は双方向、およびリソース DLL のドライバー関数は、文字列を返す必要があります。 値が場合<strong>false</strong>通信が、イベント通知メッセージに、プリンター ドライバーからの一方向です。 詳細については、次の例と「解説」セクションを参照してください。</p></td>
</tr>
<tr class="even">
<td><p><strong>dll</strong></p></td>
<td><p>xs:string</p></td>
<td><p>〇</p></td>
<td><p></p>
<p>カスタム データ ソースが含まれている dll を指定する必須の属性。 この DLL は、プリンター ドライバーの依存ファイルである必要があり、ドライバーのリソース フォルダー (たとえば、%systemroot%\system32\spool\drivers\w32x86\3) に存在する必要があります。</p></td>
</tr>
<tr class="odd">
<td><p><strong>entryPoint</strong></p></td>
<td><p>xs:string</p></td>
<td><p>〇</p></td>
<td><p></p>
<p>リソース DLL で、データ ソースのエントリ ポイントを指定する必須の属性。</p></td>
</tr>
</tbody>
</table>

## <a name="child-elements"></a>子要素


<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>要素</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>何か</strong></p></td>
<td><p></p>
<p>カスタム データ スキーマに従ってすべての子要素を指定します。 詳細については、次の例のセクションを参照してください。</p></td>
</tr>
</tbody>
</table>

## <a name="parent-elements"></a>親要素


<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>要素</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="requestopen.md" data-raw-source="[&lt;strong&gt;requestOpen&lt;/strong&gt;](requestopen.md)"><strong>requestOpen</strong></a></p></td>
<td><p></p>
<p>クライアント コンピューターのイベント通知メッセージを開くために使用する要素。</p></td>
</tr>
</tbody>
</table>

<a name="remarks"></a>注釈
-------

としてキャプチャするカスタムのデータを提供する必要があります、 **CDATA**型。

<a name="examples"></a>例
--------

次のコード例を使用する方法を示しています、 **customData**カスタム データを取得する要素。

```xml
<?xml version="1.0"?>
  <asyncPrintUIRequest xmlns="http://schemas.microsoft.com/2003/print/asyncui/v1/request"
      xmlns:myco="http://www.myprintercompany.com">
    <requestOpen>
      <customData dll="abc.dll" entrypoint="IHVFunction" bidi="true">
        <IHV:anyXMLData />
          CDATA
      </customData>
    </requestOpen>
</asyncPrintUIRequest>
```

## <a name="see-also"></a>関連項目

[requestOpen](requestopen.md)
