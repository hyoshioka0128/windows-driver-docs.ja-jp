---
title: customUI 要素
description: 省略可能な customUI 要素は、クライアントコンピューターに表示されるカスタムユーザーインターフェイスを指定します。
ms.assetid: 4408dcf2-0928-4ecb-97eb-0027eceef457
keywords:
- customUI 要素の印刷デバイス
topic_type:
- apiref
api_name:
- customUI
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 907b2be97ce48a34b688ac6e6e17b8a216bf0079
ms.sourcegitcommit: 3ee05aabaf9c5e14af56ce5f1dde588c2c7eb4ec
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/06/2019
ms.locfileid: "74881912"
---
# <a name="customui-element"></a>customUI 要素


省略可能な**customUI**要素は、クライアントコンピューターに表示されるカスタムユーザーインターフェイスを指定します。

**CustomUI**要素は、この URI: [http://schemas.microsoft.com/2003/print/asyncui/v1/request](https://schemas.microsoft.com/2003/print/asyncui/v1/request)の*asyncui*名前空間で定義されています。 (このリソースは、一部の言語および国では使用できません。)

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
<th>備わっている</th>
<th>タスクバーの検索ボックスに</th>
<th>必須かどうか</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>bidi</strong></p></td>
<td><p>xs:string</p></td>
<td><p>[はい]</p></td>
<td><p></p>
<p>プリンタードライバーとイベント通知メッセージの間の通信の種類を指定する必須の属性です。 値が<strong>true</strong>の場合、通信は双方向であり、リソース DLL 内のドライバー関数は文字列を返す必要があります。「例」のセクションを参照してください。 値が<strong>false</strong>の場合、プリンタードライバーからイベント通知メッセージまでの通信は一方向です。</p></td>
</tr>
<tr class="even">
<td><p><strong>dll</strong></p></td>
<td><p>xs:string</p></td>
<td><p>[はい]</p></td>
<td><p></p>
<p>カスタムユーザーインターフェイスの表示関数を含むリソース DLL を指定する必須の属性です。 この DLL は、プリンタドライバの依存ファイルである必要があり、ドライバリソースフォルダに存在する必要があります (たとえば、%SYSTEMROOT%\system32\spool\drivers\w32x86\3)。</p></td>
</tr>
<tr class="odd">
<td><p><strong>エントリー</strong></p></td>
<td><p>xs:string</p></td>
<td><p>[はい]</p></td>
<td><p></p>
<p>リソース DLL で呼び出す関数を指定する必須の属性です。</p></td>
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
<p>カスタムユーザーインターフェイススキーマに従って、任意の子要素を指定します。 「使用例」のセクションを参照してください。</p></td>
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
<p>クライアントコンピューターでイベント通知メッセージを開くために使用される要素。</p></td>
</tr>
</tbody>
</table>

<a name="remarks"></a>注釈
-------

次の例では、 **bidi**属性が**true**に設定されているため、 **IHVFunction** dll*内のエントリ*ポイントのエントリポイント関数が呼び出されます。 **IHVfunction**は、 **CDATA**型のデータを返します。

<a name="examples"></a>例
--------

次のコード例は、 **customUI**要素を使用して、クライアントコンピューターでカスタムユーザーインターフェイスを呼び出し、表示する方法を示しています。

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

 

 




