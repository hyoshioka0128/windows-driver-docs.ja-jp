---
title: コールバック オブジェクトの定義
description: コールバック オブジェクトの定義
ms.assetid: 9717795b-dd62-4f17-b931-5ca2b1237e60
keywords:
- コールバック オブジェクトの WDK カーネル
- コールバック通知を登録します。
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: abfeb44e7c5e222f7e2f34877dcc8392d0b071d8
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56560612"
---
# <a name="defining-a-callback-object"></a>コールバック オブジェクトの定義





ドライバーは、他のドライバーがドライバーを作成して定義された条件の通知を要求するコールバック オブジェクトを作成できます。 次の図は、コールバック オブジェクトの定義に関連する手順を示します。

![コールバック オブジェクトの定義を示す図](images/3crt-cbk.png)

オブジェクトを作成する前に、ドライバーが呼び出す[ **InitializeObjectAttributes** ](https://msdn.microsoft.com/library/windows/hardware/ff547804)その属性を設定します。 コールバック オブジェクトには、システム定義のコールバック; の名前に一致することはできませんが、名前が必要です。どのようなその他の属性の作成者を対象と、適切な通常 OBJ ことができます\_ケース\_INSENSITIVE です。 次に、ドライバーを呼び出す[ **ExCreateCallback**](https://msdn.microsoft.com/library/windows/hardware/ff544560)、初期化された属性と、コールバック オブジェクトを識別するハンドルを取得する位置にポインターを渡すことです。 また、このような名前付きオブジェクトが存在しないとかどうか、オブジェクトを行えるように 1 つ以上登録されたコールバック ルーチン場合に、システムがコールバック オブジェクトを作成する必要があるかどうかを示す 2 つのブール値を渡します。

ドライバーは、登録されたコールバック ルーチンを呼び出してその条件を定義します。 2 つの引数の形式の条件をコールバックを作成するドライバーで定義された各パラメーターをポイントします。 コールバック オブジェクトと、ドライバーのクライアントに対して、通知要求の IRQL の名前と共に、これらの条件を文書化する必要があります。

コールバック状態が発生すると、ドライバー呼び出し[ **ExNotifyCallback**](https://msdn.microsoft.com/library/windows/hardware/ff545489)、コールバック オブジェクトと 2 つの引数をそのハンドルを渡します。 システムは、コールバック ルーチンをすべてで登録された、順番に、コールバック オブジェクトに登録されている 2 つの引数およびポインターのルーチンの登録時に指定されたコンテキストを渡すことを呼び出します。 ドライバーを呼び出す必要があります**ExNotifyCallback** IRQL で&lt;= ディスパッチ\_レベルは、システムは、ドライバーがこの呼び出しが行われた同じ IRQL でコールバック ルーチンを呼び出します。

コールバックを作成するドライバーを呼び出す必要がありますのコールバック オブジェクトとすべての操作が完了したら、 [ **ObDereferenceObject** ](https://msdn.microsoft.com/library/windows/hardware/ff557724)の参照カウントをデクリメントし、オブジェクトがあることを確認するには削除されます。

 

 




