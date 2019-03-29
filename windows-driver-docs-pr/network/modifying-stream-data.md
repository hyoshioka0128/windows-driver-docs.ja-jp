---
title: ストリーム データの変更
description: ストリーム データの変更
ms.assetid: 8f591bc1-272c-4e53-8e49-3350c6a3a33e
keywords:
- WDK Windows フィルタ リング プラットフォーム、ストリーム データの変更のコールアウトを分類します。
- ストリームのデータ変更 WDK Windows フィルタ リング プラットフォーム
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0612f461a8b6f780115296af5a52ba759eacd4e8
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56574989"
---
# <a name="modifying-stream-data"></a>ストリーム データの変更


コールアウトは、ストリーム レイヤーのデータを処理するときにその[ *classifyFn* ](https://msdn.microsoft.com/library/windows/hardware/ff544890)コールアウト関数は、データ ストリーム内のデータを変更できます。 吹き出しの*classifyFn*コールアウト関数が変更されていない場合、ブロック データを削除するには、ストリームを通過するストリームで許容可能なデータを許可し、適切な場合は、ストリームに新しいまたは変データを挿入します。

吹き出しできますと交換してストリーム内のデータを他のデータが置き換えられますが、データをブロックすることと同時に、ストリームに新しいデータを挿入します。 このような状況で、新しいデータは、ストリームからブロックされているデータの削除を同じ時点でストリームに挿入されます。

データ ストリームにデータを挿入するコールアウト ドライバーの場合は、最初インジェクション ハンドルを作成する必要があります。 これは、ネットワーク スタックに変更されたパケットのデータの挿入用に作成した同じインジェクション ハンドルを指定できます。 参照してください[パケットを検査し、Stream データ](inspecting-packet-and-stream-data.md)インジェクション ハンドルを作成する方法についてはします。

ストリーム データを変更する方法については、サンプルを参照して、"Windows フィルタ リング プラットフォーム Stream 編集"で、[ハードウェア サンプル](https://go.microsoft.com/fwlink/p/?LinkId=618052)コード ギャラリー。

 

 





