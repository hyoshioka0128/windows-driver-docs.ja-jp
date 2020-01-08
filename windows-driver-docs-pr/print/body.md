---
title: body 要素
description: 必須の body 要素は、イベント通知メッセージに表示されるテキストを提供します。 このテキストは、プリンターイベントについてのユーザー固有の詳細を提供します。
ms.assetid: 3343c272-5090-4b60-ab04-08038d2583ff
keywords:
- body 要素の印刷デバイス
topic_type:
- apiref
api_name:
- body
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 61da9d170f9a90f078296677893aaddda49f49f8
ms.sourcegitcommit: ab64169b631da4db3f0b895600f1c38a22cb7e2e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/03/2020
ms.locfileid: "75652865"
---
# <a name="body-element"></a>body 要素

必須の**body**要素は、イベント通知メッセージに表示されるテキストを提供します。 このテキストは、プリンターイベントについてのユーザー固有の詳細を提供します。

**Body**要素は、この URI: [https://schemas.microsoft.com/2003/print/asyncui/v1/request](https://schemas.microsoft.com/2003/print/asyncui/v1/request)の*asyncui*名前空間で定義されています。 (このリソースは、一部の言語および国では使用できません。)

## <a name="usage"></a>使用方法

```xml
<body
  stringID = "xs:string"
  resourceDll = "xs:string">
  child elements
</body>
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
<td><p><strong>resourceDll</strong></p></td>
<td><p>xs:string</p></td>
<td><p>必須ではない</p></td>
<td><p></p>
<p>イベント通知メッセージに表示する本文テキストを含むリソース DLL を指定する、省略可能な属性です。 この DLL は、プリンタドライバの依存ファイルである必要があり、ドライバリソースフォルダに存在する必要があります (たとえば、%SYSTEMROOT%\system32\spool\drivers\w32x86\3)。</p></td>
</tr>
<tr class="even">
<td><p><strong>stringID</strong></p></td>
<td><p>xs:string</p></td>
<td><p>[はい]</p></td>
<td><p></p>
<p>イベント通知メッセージの本文に表示するテキストを指定する必須の属性です。 属性値は、リソース DLL 内のテキスト文字列の場所を指定します。</p></td>
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
<td><p><a href="parameter.md" data-raw-source="[&lt;strong&gt;parameter&lt;/strong&gt;](parameter.md)"><strong>引き</strong></a></p></td>
<td><p></p>
<p>本文テキスト指定のパラメーターの代わりに使用するテキスト文字列を指定する省略可能な要素。</p></td>
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
<p>クライアントコンピューターにメッセージバルーンを表示するために使用される省略可能な要素。</p></td>
</tr>
<tr class="even">
<td><p><a href="messageboxui.md" data-raw-source="[&lt;strong&gt;messageBoxUI&lt;/strong&gt;](messageboxui.md)"><strong>messageBoxUI</strong></a></p></td>
<td><p></p>
<p>クライアントコンピューターにメッセージボックスを表示するために使用される省略可能な要素。</p></td>
</tr>
</tbody>
</table>

## <a name="remarks"></a>注釈

リソース DLL から読み込まれた本文のテキストには、パーセンテージ (%) を含めることができます。[**parameter**](parameter.md)子要素によって指定されたテキスト文字列で置き換えられるタグ。

複数の**本文**タグを順番に使用できます。この場合、それぞれによって生成されるテキストは、イベント通知メッセージで連結されます。 テキスト文字列の各ペアの間にスペースが挿入されます。 同じ通知メッセージには、"プリンターがインク切れです" のような状態情報と、ユーザーの指示 (たとえば、"インクカートリッジを交換し、プリンターの再開ボタンを押して続行する" など) が表示されます。

**Body**要素に含まれるテキストは、使用可能なアクションをユーザーに知らせる必要があります。

次の推奨事項を使用して、メッセージテキストをわかりやすく簡潔にします。

- 終了区切り記号付きの完全な文を使用します。
- 他の言語にローカライズされている場合、255文字未満の本文テキストを作成します。 たとえば、英語のメッセージでは、他の言語にローカライズするために、通常は200文字を超える文字を使用しないようにする必要があります。
- ユーザーが要求されたアクション (特定のオブジェクト名、ユーザー名、ファイル名、Url など) を完了できるようにするための重要な情報を含めます。 ユーザーは、このような情報を見つけるために別のウィンドウを開く必要はありません。
- オブジェクト名を二重引用符で囲みます ("用紙ビン 1" など)。 ただし、オブジェクト名にユーザー名などの大文字の単語が使用されている場合は引用符を使用しないでください。また、コロン (たとえば、プリンター名: マイプリンター) でオフセットされているか、コンテキストから簡単に判断することもできます。
- ローカライズに対応するためにオブジェクト名を固定された最大サイズに切り捨てる必要がある場合は、省略記号 (...) を使用して切り捨てを指定します。
- 通知メッセージにユーザー操作のボタンが表示される場合は、メッセージ情報とボタンの間に2つの改行があることを確認してください。 ボタンに単純なアクション指向の語句 ("クリックして印刷を再開する"、"クリックして詳細を表示する" など) を付けます。
- ユーザーが自由に無視できる重要ではない情報についてのみ、通知メッセージを使用します。 本文のテキストは、ユーザーがアクションを実行する必要があるとは限りません。
- ユーザーがアクションを実行する必要がある場合は、アクションを実行したときの重要度と結果を明確に記述します。
- ユーザーが問題を解決する方法に関する特定の情報を、プレーンな言語で問題について説明します。
- ユーザーに関連する方法でイベントを記述します。 通知メッセージは、ユーザーが通知の結果としてタスクを実行したり、動作を変更したりする可能性がある場合に関連します。
- 技術的な問題の観点からではなく、ユーザーの目標に基づいてイベントを記述します。

## <a name="examples"></a>例

**Body**要素の使用方法を次のコード例に示します。

```xml
<?xml version="1.0" ?>
   <asyncPrintUIRequest
    xmlns="https://schemas.microsoft.com/2003/print/asyncui/v1/request">
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

## <a name="see-also"></a>「

[balloonUI](balloonui.md)

[messageBoxUI](messageboxui.md)

[parameter](parameter.md)
