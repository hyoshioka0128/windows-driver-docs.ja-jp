---
title: customData 要素
description: 省略可能な customData 要素は、この非同期通知 XML スキーマのカスタムデータソースを指定します。
ms.assetid: 5e14a627-72c0-440d-b616-6963c3d69d2b
keywords:
- customData 要素の印刷デバイス
topic_type:
- apiref
api_name:
- customData
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: e92b1075380b43a8031d94ac9c67f14a51e19fed
ms.sourcegitcommit: ab64169b631da4db3f0b895600f1c38a22cb7e2e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/03/2020
ms.locfileid: "75652822"
---
# <a name="customdata-element"></a>customData 要素


省略可能な**customData**要素は、この非同期通知 XML スキーマのカスタムデータソースを指定します。

**CustomData**要素は、この URI: [https://schemas.microsoft.com/2003/print/asyncui/v1/request](https://schemas.microsoft.com/2003/print/asyncui/v1/request)の*asyncui*名前空間で定義されています。 (このリソースは、一部の言語および国では使用できません。)

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
<p>プリンタードライバーとイベント通知メッセージの間の通信の種類を指定する必須の属性です。 値が<strong>true</strong>の場合、通信は双方向であり、リソース DLL 内のドライバー関数は文字列を返す必要があります。 値が<strong>false</strong>の場合、プリンタードライバーからイベント通知メッセージまでの通信は一方向です。 詳細については、次の例と「解説」セクションを参照してください。</p></td>
</tr>
<tr class="even">
<td><p><strong>dll</strong></p></td>
<td><p>xs:string</p></td>
<td><p>[はい]</p></td>
<td><p></p>
<p>カスタムデータソースを含むリソース DLL を指定する必須の属性です。 この DLL は、プリンタドライバの依存ファイルである必要があり、ドライバリソースフォルダに存在する必要があります (たとえば、%SYSTEMROOT%\system32\spool\drivers\w32x86\3)。</p></td>
</tr>
<tr class="odd">
<td><p><strong>エントリー</strong></p></td>
<td><p>xs:string</p></td>
<td><p>[はい]</p></td>
<td><p></p>
<p>リソース DLL のデータソースエントリポイントを指定する必須の属性です。</p></td>
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
<p>カスタムデータスキーマに従って、任意の子要素を指定します。 詳細については、次の「例」のセクションを参照してください。</p></td>
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

キャプチャするカスタムデータは、 **CDATA**型として指定する必要があります。

<a name="examples"></a>例
--------

次のコード例は、 **customData**要素を使用してカスタムデータを取得する方法を示しています。

```xml
<?xml version="1.0"?>
  <asyncPrintUIRequest xmlns="https://schemas.microsoft.com/2003/print/asyncui/v1/request"
      xmlns:myco="https://www.myprintercompany.com">
    <requestOpen>
      <customData dll="abc.dll" entrypoint="IHVFunction" bidi="true">
        <IHV:anyXMLData />
          CDATA
      </customData>
    </requestOpen>
</asyncPrintUIRequest>
```

## <a name="see-also"></a>「

[requestOpen](requestopen.md)
