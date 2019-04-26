---
title: customUI 要素
description: 省略可能な customUI 要素には、クライアント コンピューターに表示されるカスタム ユーザー インターフェイスを指定します。
ms.assetid: 4408dcf2-0928-4ecb-97eb-0027eceef457
keywords:
- customUI 要素印刷デバイス
topic_type:
- apiref
api_name:
- customUI
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: dca4d106772e8e5e97631889d3b6b9b465e0c25a
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63341320"
---
# <a name="customui-element"></a>customUI 要素


省略可能な**customUI**要素は、クライアント コンピューターに表示されるカスタム ユーザー インターフェイスを指定します。

**CustomUI**で要素が定義されている、 *asyncui* この URI に、名前空間: http://schemas.microsoft.com/2003/print/asyncui/v1/request します。 (このリソースできない場合がありますのいくつかの言語および国。)

<a name="usage"></a>使用方法
-----

```xml
<customUI
  dll = "xs:string"
  entrypoint = "xs:string"
  bidi = "xs:string">
  child elements
</customUI>
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
<p>プリンター ドライバーと、イベント通知メッセージ間の通信の種類を指定する必須の属性。 値が場合<strong>true</strong>通信は双方向、およびリソース DLL のドライバー関数は、文字列を返す必要があります。 例を参照してください。 値が場合<strong>false</strong>通信が、イベント通知メッセージに、プリンター ドライバーからの一方向です。</p></td>
</tr>
<tr class="even">
<td><p><strong>dll</strong></p></td>
<td><p>xs:string</p></td>
<td><p>〇</p></td>
<td><p></p>
<p>リソースを表示する機能、カスタム ユーザー インターフェイスを含む DLL を指定する必須の属性。 この DLL は、プリンター ドライバーの依存ファイルである必要があり、ドライバーのリソース フォルダー (たとえば、%systemroot%\system32\spool\drivers\w32x86\3) に存在する必要があります。</p></td>
</tr>
<tr class="odd">
<td><p><strong>entrypoint</strong></p></td>
<td><p>xs:string</p></td>
<td><p>〇</p></td>
<td><p></p>
<p>リソース DLL を呼び出す関数を指定する必須の属性。</p></td>
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
<p>カスタム ユーザー インターフェイスのスキーマに従ったすべての子要素を指定します。 使用例」を参照してください。</p></td>
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

**Bidi**属性に設定されて**true**次の例では、 **IHVFunction**でエントリ ポイント関数、*月*DLL呼び出されます。 **IHVfunction**を返します、 **CDATA**のデータを入力します。

<a name="examples"></a>例
--------

次のコード例を使用する方法を示しています、 **customUI**を呼び出すし、クライアント コンピューターで、カスタム ユーザー インターフェイスを表示する要素。

```cpp
<?xml version="1.0"?>
  <asyncPrintUIRequest xmlns="http://schemas.microsoft.com/2003/print/asyncui/1.0"
      xmlns:myco="http://www.myprintercompany.com">
    <requestOpen>
      <customUI dll="abc.dll" entrypoint="IHVFunction" bidi="true">
        <IHV:anyXMLData />
          CDATA
      </customUI>
    </requestOpen>
  </asyncPrintUIRequest>
```

## <a name="see-also"></a>関連項目


[**requestOpen**](requestopen.md)

 

 




