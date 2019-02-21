---
title: TTD コレクション オブジェクト
description: このセクションでは、タイム トラベルのデバッグに関連付けられている範囲のモデル オブジェクトについて説明します。
ms.date: 09/25/2017
ms.localizationpriority: medium
ms.openlocfilehash: bfe3301d049ad5b63e77b2da117332b2d3b680d2
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56549430"
---
> [!NOTE]
> このトピックの情報は暫定的です。 ドキュメントの今後のリリースでは、最新の情報が行われます。 
>

# <a name="ttd-collection-objects"></a>TTD コレクション オブジェクト

## <a name="description"></a>説明

## <a name="children"></a>Children


| オブジェクト | 説明 |
| --- | --- |
| MinPosition | A[位置オブジェクト](time-travel-debugging-position-objects.md)範囲に関連する最初の位置をについて説明します。 |




### <a name="ttd-collection-object-methods"></a>TTD コレクション オブジェクトのメソッド


**Contains(OtherString)** -文字列が指定したサブ文字列を含むかどうかを返すメソッド。

**EndsWith(OtherString)** -文字列が指定された文字列で終わるかどうかを返すメソッド。

**IndexOf(OtherString)** -特定の文字列の部分文字列の最初に見つかった位置のインデックスを返すメソッド。  このような出現が存在しない場合は、-1 が返されます。

**LastIndexOf(OtherString)** -特定の文字列の部分文字列の最後に見つかった位置のインデックスを返すメソッド。  このような出現が存在しない場合は、-1 が返されます。

**長さ**-文字列の長さを返すプロパティ。

**PadLeft(TotalWidth)** -メソッドする権利は、文字列の左側にあるスペースが挿入された幅を指定する文字列を配置します。

**PadRight(TotalWidth)** -どの左寄せで幅を指定する文字列、文字列の右側にあるスペースが挿入されたメソッド。

**(StartPos [長さ]) を削除**-文字列から指定した位置で始まるすべての文字を削除するメソッド。  オプションの長さを指定した場合、開始位置より後に多くの文字を削除することだけです。

**(SearchString ReplaceString) を置き換える**-メソッドごとに出現する指定した検索文字列を置換文字列に置き換えます。

**StartsWith(OtherString)** -、文字列が、指定された文字列で始まるかどうかを返すメソッド。

**部分文字列 (StartPos、[長さ])** -メソッドが、指定した文字列から部分文字列を取得します。  部分文字列は、指定した文字位置から開始し、オプションで指定された長さまたは文字列の末尾に続行します。

**ToLower()** -この文字列のコピーを小文字に変換して返します。

**ToUpper()** -この文字列のコピーを大文字に変換して返します。

## <a name="example-usage"></a>使用例

*保留中の情報*



## <a name="see-also"></a>参照

[タイム トラベル デバッグ - オブジェクトのタイム トラベルのデバッグの概要](time-travel-debugging-object-model.md)

[旅行時間 - デバッグの概要](time-travel-debugging-overview.md)

---


