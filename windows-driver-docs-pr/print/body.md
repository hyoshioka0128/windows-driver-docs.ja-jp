---
title: 本文要素
description: 必要な本文の要素は、イベントの通知メッセージが表示されるテキストを提供します。 このテキストは、プリンターのイベントの特定の詳細、ユーザーを提供する必要があります。
ms.assetid: 3343c272-5090-4b60-ab04-08038d2583ff
keywords:
- 本文の要素の印刷デバイス
topic_type:
- apiref
api_name:
- body
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: f252d61cb1d699a0804e957d0a23726ccd404bbc
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63330389"
---
# <a name="body-element"></a>本文要素


必要な**本文**要素は、イベント通知メッセージが表示されるテキストを提供します。 このテキストは、プリンターのイベントの特定の詳細、ユーザーを提供する必要があります。

**本文**で要素が定義されている、 *asyncui*この URI に、名前空間: http://schemas.microsoft.com/2003/print/asyncui/v1/request します。 (このリソースできない場合がありますのいくつかの言語および国。)

<a name="usage"></a>使用方法
-----

```xml
<body
  stringID = "xs:string"
  resourceDll = "xs:string">
  child elements
</body>
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
<td><p><strong>ResourceDll</strong></p></td>
<td><p>xs:string</p></td>
<td><p>X</p></td>
<td><p></p>
<p>通知メッセージを表示、イベント本文テキストを含んでいる DLL のリソースを指定する省略可能な属性。 この DLL は、プリンター ドライバーの依存ファイルである必要があり、ドライバーのリソース フォルダー (たとえば、%systemroot%\system32\spool\drivers\w32x86\3) に存在する必要があります。</p></td>
</tr>
<tr class="even">
<td><p><strong>stringID</strong></p></td>
<td><p>xs:string</p></td>
<td><p>〇</p></td>
<td><p></p>
<p>イベント通知メッセージの本文に表示するテキストを指定する必須の属性。 属性の値は、リソース DLL でのテキスト文字列の場所を指定します。</p></td>
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
<td><p><a href="parameter.md" data-raw-source="[&lt;strong&gt;parameter&lt;/strong&gt;](parameter.md)"><strong>パラメーター</strong></a></p></td>
<td><p></p>
<p>テキストを指定する省略可能な要素は、その本文テキストの指定のパラメーターの代替文字列です。</p></td>
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
<td><p><a href="balloonui.md" data-raw-source="[&lt;strong&gt;balloonUI&lt;/strong&gt;](balloonui.md)"><strong>balloonUI</strong></a></p></td>
<td><p></p>
<p>クライアント コンピューターでメッセージ バルーンの表示に使用される省略可能な要素です。</p></td>
</tr>
<tr class="even">
<td><p><a href="messageboxui.md" data-raw-source="[&lt;strong&gt;messageBoxUI&lt;/strong&gt;](messageboxui.md)"><strong>messageBoxUI</strong></a></p></td>
<td><p></p>
<p>クライアント コンピューターのメッセージ ボックスを表示するために使用する省略可能な要素です。</p></td>
</tr>
</tbody>
</table>

<a name="remarks"></a>注釈
-------

リソース DLL から読み込まれた本文が割合 (%) を含めることができます。指定されたテキスト文字列で置き換えられるタグ、 [**パラメーター** ](parameter.md)子要素。

複数**本文**使用できるタグ、順番にイベント通知のメッセージに各によって生成されたテキストの連結された場合。 テキスト文字列の各ペアの間にスペースが挿入されます。 両方同じ通知メッセージを表示できます状態については、"プリンターがインク外です"など、および手順については、ユーザーのなど"インク カートリッジの交換を続行するプリンターの再開 ボタンを押します。"。

含まれるテキスト、**本文**要素をユーザーにどのような操作は使用可能な通知を使用する必要があります。

便利で簡潔なメッセージのテキストを保持するのにには、次の推奨事項を使用します。

-   末尾に句点で完全な文を使用します。
-   その他の言語にローカライズすると、255 文字は、本文を作成します。 たとえば、英語でのメッセージ使用しないでください通常 200 台を超える文字他の言語にローカリゼーションに対応するためにします。
-   特定のオブジェクト名、ユーザー名、ファイル名、または Url など、要求された操作を完了できる重要な情報が含まれます。 ユーザーは、このような情報を検索する別のウィンドウを開くにはありません。
-   オブジェクト名 (たとえば、「用紙ビン 1」) を囲む二重引用符を配置します。 ただしを使用しない引用符がある場合、オブジェクト名は大文字の単語を使用して、ユーザー名など、コロンでオフセットされます (たとえば、プリンター名。プリンター)、または、コンテキストから簡単に決定できます。
-   切り捨てる固定の最大サイズに合わせてローカライズするオブジェクト名がある場合は、省略記号 (...) を使用して、切り捨てを示します。
-   通知メッセージがユーザーの操作のボタンと場合、は、メッセージの情報と、ボタンの間に 2 つの改行があることを確認してください。 「をクリックして再起動印刷、」または「クリックすると、詳細を参照してください」などの単純なアクション指向のフレーズのボタンをラベルします。
-   のみの通知メッセージを使用して、致命的でないについては、ユーザーが自由に無視することができます。 本文のテキストは、ユーザーがアクションを実行する必要がありますと表示されない必要があります。
-   ユーザーは、アクションを実行する必要があります、明らかに、重要度とアクションを実行して結果を説明します。
-   ユーザーが問題を解決する方法に関する特定の情報をプレーンな言語での問題について説明します。
-   ユーザーに関連した方法でイベントについて説明します。 通知メッセージは、関連するは、ユーザーはタスクを実行または通知の結果としての動作を変更する可能性がある場合です。
-   技術的な問題の観点からではなく、ユーザーの目的の観点からのイベントについて説明します。

<a name="examples"></a>例
--------

次のコード例を使用する方法を示しています、**本文**要素。

```xml
<?xml version="1.0" ?>
   <asyncPrintUIRequest
    xmlns="http://schemas.microsoft.com/2003/print/asyncui/v1/request">
    <v1>
      <requestOpen>
        <balloonUI iconID="1" resourceDll="IHV.dll">
          <title stringID="1234" resourceDll="IHV.dll" />
          <body stringID="100" resourceDll="IHV.dll">
            <parameter stringID="5" />
            <parameter stringID="1002" resourceDll="IHV.dll" />
          </body>
        </balloonUI>
      </requestOpen>
    </v1>
  </asyncPrintUIRequest>
```

## <a name="see-also"></a>関連項目

[balloonUI](balloonui.md)

[messageBoxUI](messageboxui.md)

[parameter](parameter.md)
