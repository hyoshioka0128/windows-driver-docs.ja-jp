---
title: action 要素
description: オプションの action 要素は、ユーザーがバルーンメッセージのボタンをクリックしたときに実行されるアクションを表します。
ms.assetid: dae207ad-072e-4de6-b6a2-f1188ce91065
keywords:
- アクション要素の印刷デバイス
topic_type:
- apiref
api_name:
- action
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: ec58ab45d6e8cea2ff01bcddd697f42de670c5e8
ms.sourcegitcommit: 3ee05aabaf9c5e14af56ce5f1dde588c2c7eb4ec
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/06/2019
ms.locfileid: "74881924"
---
# <a name="action-element"></a>action 要素

オプションの**action**要素は、ユーザーがバルーンメッセージのボタンをクリックしたときに実行されるアクションを表します。

**Action**要素は、この URI: https://schemas.microsoft.com/2003/print/asyncui/v1/request の*asyncui*名前空間で定義されています。 (このリソースは、一部の言語および国では使用できません。)

## <a name="usage"></a>使用方法

```xml
<action
  dll = "xs:string"
  entrypoint = "xs:string">
  text
</action>
```

## <a name="attributes"></a>属性

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
<td><p><strong>dll</strong></p></td>
<td><p>xs:string</p></td>
<td><p>[はい]</p></td>
<td><p></p>
<p>ユーザーがボタンをクリックしたときに呼び出す関数を含む、IHV によって提供される DLL を指定する必須の属性です。</p></td>
</tr>
<tr class="even">
<td><p><strong>エントリー</strong></p></td>
<td><p>xs:string</p></td>
<td><p>[はい]</p></td>
<td><p></p>
<p>IHV によって提供される DLL で呼び出す関数を指定する必須の属性です。 この関数は、呼び出された場合に<strong>NULL</strong>を返します。</p></td>
</tr>
</tbody>
</table>

## <a name="text-value"></a>テキスト値

ドライバーリソース DLL に渡される、CDATA 形式の省略可能な文字列。

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
<p>イベント通知メッセージに表示されるテキストを提供します。 このテキストは、プリンターイベントについてのユーザー固有の詳細を提供します。</p></td>
</tr>
</tbody>
</table>

## <a name="remarks"></a>注釈

**Action**要素は対話型バルーンと共に使用されます。これは通常のバルーンに似ていますが、ユーザーがクリックするボタンが含まれています。

## <a name="examples"></a>例

次の XML コード例では、クライアントコンピューターで IHV プログラムを実行します *。*

```xml
<?xml version="1.0" ?> 
  <asyncPrintUIRequest
    xmlns="https://schemas.microsoft.com/2003/print/asyncui/v1/request">
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

**Action**要素を使用して、リソース DLL にデータを渡す方法を次のコード例に示します。

```xml
<?xml version="1.0" ?>
   <asyncPrintUIRequest
    xmlns="https://schemas.microsoft.com/2003/print/asyncui/v1/request">
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
