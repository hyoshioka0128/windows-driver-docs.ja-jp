---
title: スタック トレースの調査
description: スタック トレースの調査
ms.assetid: ca203f29-841f-411e-915a-81abaa96a8e6
keywords:
- デバッガーエンジン API, スタックトレース
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: c633e2221363fdf62a7239f02cd1eaafad79633f
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838037"
---
# <a name="examining-the-stack-trace"></a>スタック トレースの調査


*呼び出し履歴*には、スレッドによって行われる関数呼び出しのデータが含まれます。 各関数呼び出しのデータは*スタックフレーム*と呼ばれ、戻りアドレス、関数に渡されるパラメーター、および関数のローカル変数が含まれます。 関数呼び出しが行われるたびに、新しいスタックフレームがスタックの一番上にプッシュされます。 この関数が戻ると、スタックフレームがスタックからポップされます。

各スレッドには、そのスレッドで行われた呼び出しを表す独自の呼び出し履歴があります。

スタックトレースを取得するには、 [**GetStackTrace**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugcontrol3-getstacktrace)および[**GetContextStackTrace**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugcontrol4-getcontextstacktrace)メソッドを使用します。 スタックトレースは、 [**OutputStackTrace**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugcontrol3-outputstacktrace)と[**OutputContextStackTrace**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugcontrol4-outputcontextstacktrace)を使用して出力できます。

 

 





