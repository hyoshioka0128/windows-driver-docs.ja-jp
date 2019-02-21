---
title: action 要素
description: 省略可能なアクション要素には、ユーザーがバルーン メッセージ内のボタンをクリックしたときに完了するアクションについて説明します。
ms.assetid: dae207ad-072e-4de6-b6a2-f1188ce91065
keywords:
- 印刷デバイスの action 要素
topic_type:
- apiref
api_name:
- action
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0e144aa68c24dd78cc398eeba7c6872bb95891a0
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56530334"
---
# <a name="action-element"></a>action 要素


省略可能な**アクション**要素は、ユーザーがバルーン メッセージ内のボタンをクリックしたときに完了する必要がアクションを表します。

**アクション**で要素が定義されている、 *asyncui*この URI に、名前空間:http://schemas.microsoft.com/2003/print/asyncui/v1/requestします。 (このリソースできない場合がありますのいくつかの言語および国。)

<a name="usage"></a>使用方法
-----

```xml
<action
  dll = "xs:string"
  entrypoint = "xs:string">
  text
</action>
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
<td><p><strong>dll</strong></p></td>
<td><p>xs:string</p></td>
<td><p>〇</p></td>
<td><p></p>
<p>ユーザーがボタンをクリックしたときに呼び出す関数を含む、IHV によって提供される DLL を指定する必須の属性。</p></td>
</tr>
<tr class="even">
<td><p><strong>entrypoint</strong></p></td>
<td><p>xs:string</p></td>
<td><p>〇</p></td>
<td><p></p>
<p>IHV によって提供される DLL 内に呼び出される関数を指定する必須の属性。 この関数が返す<strong>NULL</strong>呼び出されるとします。</p></td>
</tr>
</tbody>
</table>

<a name="text-value"></a>テキスト値
----------

ドライバー リソース DLL に渡される、CDATA として書式設定された省略可能な文字列。

## <a name="child-elements"></a>子要素


子要素はありません。

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
<td><p><a href="balloonui.md" data-raw-source="[&lt;strong&gt;balloonUI&lt;/strong&gt;](balloonui.md)"><strong>balloonUI</strong></a></p></td>
<td><p></p>
<p>イベントの通知メッセージが表示されるテキストを提供します。 このテキストは、プリンターのイベントの特定の詳細、ユーザーを提供する必要があります。</p></td>
</tr>
</tbody>
</table>

<a name="remarks"></a>注釈
-------

**アクション**正規バルーンに似ていますが、対話型のバルーンと要素が使用されますが、ユーザーがクリックするためのボタンが含まれています。

<a name="examples"></a>例
--------

次の XML コードの例の実行、 *IHV.exe*クライアント コンピューター上のプログラム

```xml
<?xml version="1.0" ?> 
  <asyncPrintUIRequest
    xmlns="http://schemas.microsoft.com/2003/print/asyncui/v1/request">
    <v1>
      <requestOpen>
        <balloonUI iconID="1" resourceDll="IHV.dll">
          <title stringID="1234" resourceDll="IHV.dll" />
          <body stringID="100" resourceDll="IHV.dll">
            <parameter stringID="<5>" />
            <parameter stringID="1002" resourceDll="IHV.dll" />
          </body>
        </balloonUI>
      </requestOpen>
    </v1>
  </asyncPrintUIRequest>
```

次のコード例を使用する方法を示しています、**アクション**リソース DLL にデータを渡す要素。

```xml
<?xml version="1.0" ?>
   <asyncPrintUIRequest
    xmlns="http://schemas.microsoft.com/2003/print/asyncui/v1/request">
    <v1>
      <requestOpen>
        <balloonUI iconID="1" resourceDll="IHV.dll">
          <title stringID="1234" resourceDll="IHV.dll"/>
          <body stringID="100" resourceDll="IHV.dll">
            <parameter stringID="<5>" />
            <parameter stringID="1002" resourceDll="IHV.dll" />
          </body>
          <action dll="adc.dll" entrypoint="def" >
            IHV CDATA to pass into the resource DLL
          </action>
        </balloonUI>
      </requestOpen>
    </v1>
  </asyncPrintUIRequest>
```

## <a name="see-also"></a>関連項目


[**balloonUI**](balloonui.md)

 

 




