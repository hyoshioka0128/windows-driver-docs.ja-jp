---
title: コールバック オブジェクトの定義
description: コールバック オブジェクトの定義
ms.assetid: 9717795b-dd62-4f17-b931-5ca2b1237e60
keywords:
- コールバック オブジェクトの WDK カーネル
- コールバック通知を登録します。
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1bb49c1adb58f555aab2c0afd139ca8018c5c8e2
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67377134"
---
# <a name="defining-a-callback-object"></a>コールバック オブジェクトの定義





ドライバーは、他のドライバーがドライバーを作成して定義された条件の通知を要求するコールバック オブジェクトを作成できます。 次の図は、コールバック オブジェクトの定義に関連する手順を示します。

![コールバック オブジェクトの定義を示す図](images/3crt-cbk.png)

オブジェクトを作成する前に、ドライバーが呼び出す[ **InitializeObjectAttributes** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfwdm/nf-wudfwdm-initializeobjectattributes)その属性を設定します。 コールバック オブジェクトには、システム定義のコールバック; の名前に一致することはできませんが、名前が必要です。どのようなその他の属性の作成者を対象と、適切な通常 OBJ ことができます\_ケース\_INSENSITIVE です。 次に、ドライバーを呼び出す[ **ExCreateCallback**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-excreatecallback)、初期化された属性と、コールバック オブジェクトを識別するハンドルを取得する位置にポインターを渡すことです。 また、このような名前付きオブジェクトが存在しないとかどうか、オブジェクトを行えるように 1 つ以上登録されたコールバック ルーチン場合に、システムがコールバック オブジェクトを作成する必要があるかどうかを示す 2 つのブール値を渡します。

ドライバーは、登録されたコールバック ルーチンを呼び出してその条件を定義します。 2 つの引数の形式の条件をコールバックを作成するドライバーで定義された各パラメーターをポイントします。 コールバック オブジェクトと、ドライバーのクライアントに対して、通知要求の IRQL の名前と共に、これらの条件を文書化する必要があります。

コールバック状態が発生すると、ドライバー呼び出し[ **ExNotifyCallback**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-exnotifycallback)、コールバック オブジェクトと 2 つの引数をそのハンドルを渡します。 システムは、コールバック ルーチンをすべてで登録された、順番に、コールバック オブジェクトに登録されている 2 つの引数およびポインターのルーチンの登録時に指定されたコンテキストを渡すことを呼び出します。 ドライバーを呼び出す必要があります**ExNotifyCallback** IRQL で&lt;= ディスパッチ\_レベルは、システムは、ドライバーがこの呼び出しが行われた同じ IRQL でコールバック ルーチンを呼び出します。

コールバックを作成するドライバーを呼び出す必要がありますのコールバック オブジェクトとすべての操作が完了したら、 [ **ObDereferenceObject** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-obdereferenceobject)の参照カウントをデクリメントし、オブジェクトがあることを確認するには削除されます。

 

 




