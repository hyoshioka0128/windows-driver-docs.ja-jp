---
title: C28637
description: 警告 C28637 グローバル初期化子内の関数の呼び出しは安全ではありません。
ms.assetid: 9b392995-9583-4847-aded-f32e1daf28ed
ms.date: 04/20/2017
ms.localizationpriority: medium
f1_keywords:
- C28637
ms.openlocfilehash: 0c80dadb44602f714710ccbfe9ef0fe560218488
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63327178"
---
# <a name="c28637"></a>C28637


C28637 を警告します。グローバル初期化子内の関数の呼び出しが安全

ケースが頻繁に DLL を使用して、静的コンス トラクターは、DllMain から呼び出されます。 拡張 Dll から他の関数の呼び出しに適用される制約を数多くあります。 具体的には、DLL が読み込まれ、動的にアンロードされた場合は、メモリ リークを作成することができます。 詳細については、次を参照してください。、 [DllMain のコールバック関数](https://go.microsoft.com/fwlink/p/?linkid=133876)します。

 

 





