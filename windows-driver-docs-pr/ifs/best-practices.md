---
title: ベスト プラクティス
description: ベスト プラクティス
ms.assetid: c01b3fd9-7f4e-4d1a-a726-b31b0eebf094
keywords:
- WDK のコンテキストのファイル システム ミニフィルター、ベスト プラクティス
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 34a915656bd3f24a05af4553aaa30818ba84f482
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56536433"
---
# <a name="best-practices"></a>ベスト プラクティス


## <span id="ddk_registering_the_minifilter_if"></span><span id="DDK_REGISTERING_THE_MINIFILTER_IF"></span>


ミニフィルター ドライバーでは、ボリュームごとに 1 つだけのミニフィルター ドライバーのインスタンスを作成する場合は、パフォーマンス向上のためのボリュームのコンテキストではなく、インスタンス コンテキストを使用してください。

ミニフィルター ドライバーはミニフィルター ドライバーのインスタンス コンテキスト、ストリーム内へのポインターを格納することでパフォーマンスを向上したり、ハンドルのコンテキストをストリームできます。

 

 




