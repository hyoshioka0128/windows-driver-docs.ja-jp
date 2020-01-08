---
title: messageBoxUI 要素
description: オプションの messageBoxUI 要素は、クライアントコンピューターにメッセージボックスを表示するために使用されます。
ms.assetid: 83fe67fe-72b0-42e2-864e-242b7b9989d9
keywords:
- messageBoxUI 要素の印刷デバイス
topic_type:
- apiref
api_name:
- messageBoxUI
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: e58f0806bbd16ead88d6486bb679c6ed0902ad76
ms.sourcegitcommit: ab64169b631da4db3f0b895600f1c38a22cb7e2e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/03/2020
ms.locfileid: "75652851"
---
# <a name="messageboxui-element"></a>messageBoxUI 要素

オプションの**Messageboxui**要素は、クライアントコンピューターにメッセージボックスを表示するために使用されます。

**Messageboxui**要素は、この URI: [https://schemas.microsoft.com/2003/print/asyncui/v1/request](https://schemas.microsoft.com/2003/print/asyncui/v1/request)の*asyncui*名前空間で定義されています。 (このリソースは、一部の言語および国では使用できません。)

## <a name="usage"></a>使用方法

```xml
<messageBoxUI>
  child elements
</messageBoxUI>
```

## <a name="attributes"></a>属性

属性はありません。

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
<td><p><a href="bitmap.md" data-raw-source="[&lt;strong&gt;bitmap&lt;/strong&gt;](bitmap.md)"><strong>マップ</strong></a></p></td>
<td><p></p>
<p>メッセージボックス内の本文の左側にビットマップイメージを表示するために使用される省略可能な要素。</p></td>
</tr>
<tr class="even">
<td><p><a href="body.md" data-raw-source="[&lt;strong&gt;body&lt;/strong&gt;](body.md)"><strong>body</strong></a></p></td>
<td><p></p>
<p>イベント通知メッセージに表示されるテキストを提供する必須の要素。 このテキストは、プリンターイベントについてのユーザー固有の詳細を提供します。</p></td>
</tr>
<tr class="odd">
<td><p><a href="buttons.md" data-raw-source="[&lt;strong&gt;buttons&lt;/strong&gt;](buttons.md)"><strong>83'7b</strong></a></p></td>
<td><p></p>
<p>クライアントコンピューターのイベント通知メッセージボックスに表示される1つ以上のボタンを指定する必須の要素。</p></td>
</tr>
<tr class="even">
<td><p><a href="title.md" data-raw-source="[&lt;strong&gt;title&lt;/strong&gt;](title.md)"><strong>題</strong></a></p></td>
<td><p></p>
<p>イベント通知メッセージのタイトルに表示されるテキストを提供する必須の要素。</p></td>
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

## <a name="remarks"></a>注釈

**[OK** ] ボタンと **[キャンセル**] ボタンをメッセージボックスに配置する方法を示すコード例については、「[**ボタン**](button.md)」を参照してください。 メッセージボックスのボタンクリックをキャプチャする方法の詳細については、「**例**」のセクションを参照してください。

## <a name="examples"></a>例

次のコード例は、メッセージボックスで **[OK]** ボタンがクリックされたことをプリンタードライバーに通知する方法を示しています。

```xml
<?xml version="1.0" ?> 
  <asyncPrintUIResponse xmlns="https://schemas.microsoft.com/2003/print/asyncui/v1/response">
    <v1>
      <requestClose>
        <messageBoxUI>
          <buttonID>IDOK</buttonID>
        </messageBoxUI >
      </requestClose>
    </v1>
  </asyncPrintUIResponse>
```

## <a name="see-also"></a>「

[ビットマップ](bitmap.md)

[body](body.md)

[button](button.md)

[buttons](buttons.md)

[requestOpen](requestopen.md)

[title](title.md)
