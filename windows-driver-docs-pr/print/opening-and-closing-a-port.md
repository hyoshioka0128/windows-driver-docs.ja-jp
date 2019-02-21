---
title: ポートを開いたり、閉じたりします。
description: ポートを開いたり、閉じたりします。
ms.assetid: 8bfdb3af-51d4-4252-ae1c-7910f973f5f6
keywords:
- 印刷モニター WDK、ポートの管理
- ポート管理 WDK 印刷、ポートを開く
- 印刷ポートを開く
- ポート管理 WDK 印刷、終了ポート
- 印刷ポートを閉じる
- OpenPort
- OpenPortEx
- ClosePort
- WDK のポートを開いたり閉じたりスプーラが印刷します。
- WDK のポートを開いたり、閉じたりする印刷スプーラー
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: fb3f7e5a8687bf04fb00bf84b69972cee670eade
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56529694"
---
# <a name="opening-and-closing-a-port"></a>ポートを開いたり、閉じたりします。





」の説明に従って、ポートが追加された後[ポートを追加する](adding-a-port.md)、適切な言語モニターを呼び出すことによって開くことができます、スプーラー [ **OpenPortEx** ](https://msdn.microsoft.com/library/windows/hardware/ff559596)関数。

言語モニターを使用して、 **OpenPortEx**関数を作成し、ポートのハンドルを返します。 通常、言語モニターが、関連付けられているポート モニターを呼び出す[ **OpenPort** ](https://msdn.microsoft.com/library/windows/hardware/ff559593)関数、およびだけを返しますポート モニターのから取得したハンドルの監視言語**OpenPort。**.

スプーラがポート モニターを呼び出し、言語モニターがポートに関連付けられていない場合は、 **OpenPort**関数を直接します。

スプーラは、ポートを同時に有効にするのには、複数のパスを許可しません。 そのため、後に、呼び出さ**OpenPortEx** (または**OpenPort**)、特定のモニタでは再試行されませんを閉じる前にもう一度同じポートを開きます。

」の説明に従って、ポートが開かれた後、スプーラでは、ジョブを印刷する追加の関数を呼び出すことができます[印刷ジョブを印刷](printing-a-print-job.md)、入力引数としてポート ハンドルを使用します。 ポートが開かれた後、スプーラーがポートを閉じる前に複数の印刷ジョブを送信できるように、モニターを記述する必要があります。

スプーラは、ポートに関連付けられている印刷キューがない場合、別の言語モニターでは、ジョブを送信する必要がありますか、システムのシャット ダウン時にポートを閉じます。 ポートを閉じるには、スプーラーに呼び出す言語モニターの[ **ClosePort** ](https://msdn.microsoft.com/library/windows/hardware/ff545975)関数。 関数には、ポートが開かれたときに作成されたハンドルが無効になります。 通常は呼び出しの監視、言語、 **ClosePort**が関連付けられているポート モニターによって定義された関数。

スプーラがポート モニターを呼び出し、言語モニターがポートに関連付けられていない場合は、 **ClosePort**関数を直接します。

 

 




