---
title: ポートの開始と終了
description: ポートの開始と終了
ms.assetid: 8bfdb3af-51d4-4252-ae1c-7910f973f5f6
keywords:
- 印刷モニター WDK、ポート管理
- ポート管理 WDK 印刷、ポートの開放
- 印刷ポートを開く
- ポート管理 WDK 印刷、ポートの終了
- 印刷ポートを閉じる
- OpenPort
- OpenPortEx
- ClosePort
- スプーラポートのオープンと終了の WDK 印刷
- 印刷スプーラポートを開いて閉じます。 WDK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a9759909f099ea92a02344225a56632c66c4574b
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844487"
---
# <a name="opening-and-closing-a-port"></a>ポートの開始と終了





ポートを追加した後、「ポートの[追加](adding-a-port.md)」で説明されているように、スプーラは適切な言語モニターの[**openportex**](https://docs.microsoft.com/previous-versions/ff559596(v=vs.85))関数を呼び出すことによってポートを開くことができます。

言語モニターは**Openportex**関数を使用してポートハンドルを作成し、返します。 通常、言語モニターは、関連付けられているポートモニターの[**openport**](https://docs.microsoft.com/windows-hardware/drivers/ddi/winsplp/nf-winsplp-openport)関数を呼び出します。言語モニターは、ポートモニターの**openport**から取得したハンドルのみを返します。

言語モニターがポートに関連付けられていない場合、スプーラはポートモニターの**Openport**関数を直接呼び出します。

スプーラでは、ポートへの複数のパスを一度に有効にすることはできません。 このため、特定のモニターで**Openportex** (または**openport**) を呼び出した後は、閉じる前に同じポートを再度開く必要はありません。

ポートを開いた後、スプーラーは、「[印刷ジョブ](printing-a-print-job.md)の印刷」で説明されているように、入力引数としてポートハンドルを使用して、ジョブを印刷するための追加の関数を呼び出すことができます。 ポートを開いた後、スプーラーがポートを閉じる前に複数の印刷ジョブを送信できるように、モニターを作成する必要があります。

スプーラーは、別の言語モニターを使用してジョブを送信する必要がある場合、ポートに印刷キューが関連付けられていない場合、またはシステムがシャットダウンした場合に、ポートを閉じます。 ポートを閉じるには、スプーラは言語モニターの[**Closeport**](https://docs.microsoft.com/windows-hardware/drivers/ddi/winsplp/nf-winsplp-closeport)関数を呼び出します。 関数は、ポートを開いたときに作成されたハンドルを無効にします。 言語モニターは、通常、関連付けられているポートモニターによって定義された**closeport**関数を呼び出します。

言語モニターがポートに関連付けられていない場合、スプーラはポートモニターの**closeport**関数を直接呼び出します。

 

 




