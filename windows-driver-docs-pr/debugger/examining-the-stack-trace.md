---
title: スタック トレースの調査
description: スタック トレースの調査
ms.assetid: ca203f29-841f-411e-915a-81abaa96a8e6
keywords:
- デバッガー エンジン API、スタック トレース
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: ef7763af3d112110a3ab0e06c1c97b02282fcfe1
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67361372"
---
# <a name="examining-the-stack-trace"></a>スタック トレースの調査


A*コール スタック*スレッドによって行われた関数呼び出しのデータが含まれています。 各関数呼び出しのデータと呼びます、*スタック フレーム*戻り値のアドレスでは、関数、および関数のローカル変数に渡されるパラメーターが含まれています。 関数呼び出しには、新しいスタック フレームが行われるたびは、スタックの一番上にプッシュされます。 その関数から制御が戻るときに、スタック フレームはスタックからポップします。

各スレッドは、そのスレッドで呼び出しを表す、独自のコール スタックを持っています。

スタック トレースを取得するメソッドを使用して、 [ **GetStackTrace** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugcontrol3-getstacktrace)と[ **GetContextStackTrace**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugcontrol4-getcontextstacktrace)します。 スタック トレースを使用して印刷できる[ **OutputStackTrace** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugcontrol3-outputstacktrace)と[ **OutputContextStackTrace**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugcontrol4-outputcontextstacktrace)します。

 

 





