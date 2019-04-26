---
title: スタック トレースの調査
description: スタック トレースの調査
ms.assetid: ca203f29-841f-411e-915a-81abaa96a8e6
keywords:
- デバッガー エンジン API、スタック トレース
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: f384f3a25510c3fa8a8bd4bde2bea077501bf0fa
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63347784"
---
# <a name="examining-the-stack-trace"></a>スタック トレースの調査


A*コール スタック*スレッドによって行われた関数呼び出しのデータが含まれています。 各関数呼び出しのデータと呼びます、*スタック フレーム*戻り値のアドレスでは、関数、および関数のローカル変数に渡されるパラメーターが含まれています。 関数呼び出しには、新しいスタック フレームが行われるたびは、スタックの一番上にプッシュされます。 その関数から制御が戻るときに、スタック フレームはスタックからポップします。

各スレッドは、そのスレッドで呼び出しを表す、独自のコール スタックを持っています。

スタック トレースを取得するメソッドを使用して、 [ **GetStackTrace** ](https://msdn.microsoft.com/library/windows/hardware/ff548425)と[ **GetContextStackTrace**](https://msdn.microsoft.com/library/windows/hardware/ff545748)します。 スタック トレースを使用して印刷できる[ **OutputStackTrace** ](https://msdn.microsoft.com/library/windows/hardware/ff553252)と[ **OutputContextStackTrace**](https://msdn.microsoft.com/library/windows/hardware/ff553203)します。

 

 





