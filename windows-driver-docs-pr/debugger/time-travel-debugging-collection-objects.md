---
title: TTD Collection オブジェクト
description: このセクションでは、タイムトラベルデバッグに関連付けられている範囲モデルオブジェクトについて説明します。
ms.date: 09/25/2017
ms.localizationpriority: medium
ms.openlocfilehash: cd66ce58d402f6462db2a245aee607ec99e712af
ms.sourcegitcommit: 8e8aa927cf4ab56d0af652fa5e988a8ed6967904
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/25/2019
ms.locfileid: "72916223"
---
# <a name="ttd-collection-objects"></a>TTD Collection オブジェクト

> [!NOTE]
> このトピックの情報は暫定的なものです。 更新された情報は、ドキュメントの今後のリリースで提供される予定です。
>

## <a name="description"></a>説明

## <a name="children"></a>Children


| オブジェクト | 説明 |
| --- | --- |
| MinPosition | 範囲に関連する最も早い位置を示す[位置オブジェクト](time-travel-debugging-position-objects.md)。 |

### <a name="ttd-collection-object-methods"></a>TTD Collection オブジェクトのメソッド

**Contains (otherstring)** -文字列に指定されたサブ文字列が含まれているかどうかを返すメソッドを返します。

**EndsWith (OtherString)** -文字列が指定された文字列で終わるかどうかを返すメソッド。

**IndexOf (OtherString)** -指定した文字列内で最初に見つかった部分文字列のインデックスを返すメソッド。  このような発生が存在しない場合は、-1 が返されます。

**LastIndexOf (OtherString)** -指定された文字列内の部分文字列が最後に出現する位置のインデックスを返すメソッド。  このような発生が存在しない場合は、-1 が返されます。

**Length** -文字列の長さを返すプロパティ。

**Padleft (TotalWidth)** -文字列の左側にスペースを挿入して、指定した幅に文字列を配置するメソッドです。

**PadRight (TotalWidth)** -文字列の右側にスペースを挿入することによって、指定した幅に文字列を配置するメソッド。

**Remove (StartPos, [Length])** -文字列の指定した位置から始まるすべての文字を削除するメソッド。  省略可能な長さが指定されている場合は、開始位置よりも多くの文字が削除されます。

**Replace (searchstring, replacestring)** -指定された検索文字列の出現をすべて置換文字列に置き換えるメソッド。

**StartsWith (OtherString)** -文字列が指定された文字列で始まるかどうかを返すメソッド。

**Substring (StartPos, [Length])** -指定した文字列から部分文字列を取得するメソッド。  部分文字列は、指定された文字位置から開始し、文字列の末尾または必要に応じて指定された長さに続きます。

**ToLower ()** -この文字列のコピーを小文字に変換して返します。

**ToUpper ()** -この文字列のコピーを大文字に変換して返します。

## <a name="example-usage"></a>使用例

*保留中の情報*



## <a name="see-also"></a>参照

[タイムトラベルデバッグ-タイムトラベルデバッグオブジェクトの概要](time-travel-debugging-object-model.md)

[タイムトラベルのデバッグ-概要](time-travel-debugging-overview.md)
