---
title: ミニフィルターの高度の要求
description: ミニフィルターの高度の要求
ms.assetid: 4861E5FC-9883-455F-A925-EBAFC890F568
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8c99b5c69c030bf1d5796ede21386c89bc9824a4
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56536196"
---
# <a name="minifilter-altitude-request"></a>ミニフィルターの高度の要求


ミニフィルターの高度割り当ての要求は、Microsoft に電子メールとして送信されます。 電子メールの本文には、次のフィールドと対応する情報を含める必要があります。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">フィールド</th>
<th align="left">Comment</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left">会社名:</td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left">連絡先の電子メール。</td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left">製品名:</td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left">製品の URL:</td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left">製品/フィルターの説明:</td>
<td align="left">Microsoft のフィルターの適切な高度の決定を支援する 1 つの段落概要です。</td>
</tr>
<tr class="even">
<td align="left">ファイル名をフィルター処理します。</td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left">フィルターの種類:</td>
<td align="left">これらの値のいずれか:レジストリ、ファイル システムでは、両方</td>
</tr>
<tr class="even">
<td align="left">開始の種類をフィルター処理します。</td>
<td align="left">これらの値のいずれか:ブート、システム、Auto、オンデマンド</td>
</tr>
<tr class="odd">
<td align="left">ロード順序グループのフィルターを要求します。</td>
<td align="left">参照してください、<a href="allocated-altitudes.md" data-raw-source="[File System Minifilter Allocated Altitudes](allocated-altitudes.md)">ファイル システム ミニフィルター割り当てられた高度</a>の利用可能なロード順序グループ。</td>
</tr>
<tr class="even">
<td align="left">要求された高度:</td>
<td align="left">Microsoft は、要求された高度で、高度の可用性に応じて、フィルター ドライバーの機能とは異なる高度を割り当てる権利を留保します。</td>
</tr>
<tr class="odd">
<td align="left">追加情報:</td>
<td align="left">このフィールドを使用して、Microsoft がこのフィルターを高度を割り当てるときに検討するか、情報があるかどうかを報告します。</td>
</tr>
</tbody>
</table>

 

この情報を送信する ASCII テキスト電子メール メッセージで[ fsfcomm@microsoft.com ](mailto:fsfcomm@microsoft.com?subject=Minifilter%20altitude%20request)件名。「ミニフィルターの高度要求」します。 このフィルターの高度は、指定した連絡先の電子メール アドレスにメールで送信できます。

割り当ての要求電子メールの本文の例を次に示します。

``` syntax
Hi,

Below is the request information to assign an altitude for our Contoso DataKleen file system minifilter.

Company name: Contoso Ltd.
Contact e-mail: filterdev@contoso.com
Product name: Contoso DataKleen
Product URL: http://fsfilters.contoso.com
Product/Filter Description:
    The Contoso DataKleen filter removes all occurences of any byte having a value
    between 128 and 255 during file reads. Our minifilter removes this value since
    it is not displayable on TTY devices.
Filter filename: ContosoDK.sys
Filter type: FileSystem
Filter start-type: Demand
Requested filter load order group: FSFilter Content Screener
Requested altitude: 268400
Additional information: None

Thanks,

FilterDev
```

**注:**  
-   すべてのフィールドに入力する必要があります。
-   処理を高度を割り当てる 2 週間 Microsoft をかかる場合があります。 不足している情報は、割り当てに遅れる可能性があります。
-   割り当てられた高度で表示されている高度に最終的に反映される[ファイル システム ミニフィルター割り当てられた高度](allocated-altitudes.md)します。 Microsoft のみを更新するこのリスト年 1 回に注意してください。

 

 

 




