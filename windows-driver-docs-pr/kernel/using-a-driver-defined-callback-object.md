---
title: ドライバーによって定義されたコールバック オブジェクトの使用
description: ドライバーによって定義されたコールバック オブジェクトの使用
ms.assetid: b3b32534-0641-4818-9384-65fd45f689e8
keywords:
- コールバック オブジェクトの WDK カーネル
- ドライバー定義のコールバック オブジェクトの WDK カーネル
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 17f3c0d64f1ca8dcc31b7ba5109f81dab1dd2724
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67382925"
---
# <a name="using-a-driver-defined-callback-object"></a>ドライバーによって定義されたコールバック オブジェクトの使用





別のドライバーで定義されたコールバック オブジェクトを使用するには、ドライバー、オブジェクトを開きを使用し、次の図に示すように、コールバックがトリガーされたときに呼び出されるルーチンを登録します。 ドライバーの要求元の通知では、コールバック オブジェクトの名前を知っている必要があり、コールバック ルーチンに渡される引数のセマンティクスを理解する必要があります。

![通知のコールバックの登録を示す図](images/3reg-cbk.png)

オブジェクトを開くことには、前に、ドライバーを呼び出す必要があります[ **InitializeObjectAttributes** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfwdm/nf-wudfwdm-initializeobjectattributes)オブジェクトの名前を指定する、属性ブロックを作成します。 属性ブロックへのポインターがある、後に呼び出して[ **ExCreateCallback**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-excreatecallback)、属性、ポインター、コールバックを識別するハンドルを受信する場所を渡すと**FALSE**の*作成*パラメーター、コールバックの既存のオブジェクトが必要であることを示します。

ドライバーを呼び出して[ **ExRegisterCallback** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-exregistercallback)コールバック ルーチンを登録する、返されたハンドルを使用します。

コールバック ルーチンでは、次のプロトタイプがあります。

```cpp
typedef VOID (*PCALLBACK_FUNCTION ) (
    IN PVOID CallbackContext,
    IN PVOID Argument1,
    IN PVOID Argument2
    );
```

*CallbackContext*パラメーターはこれが呼び出されるたびに、コールバック ルーチンに渡されるコンテキスト ポインターです。 通常、このパラメーターは、コンテキストのデータは、ディスパッチにルーチンを呼び出すことができる場合、呼び出し元が非ページ プールから割り当てる必要がありますのブロックへのポインター\_レベル。 2 つの引数は、コールバックを作成するコンポーネントによって定義されます。 通常、引数は、コールバックをトリガーする状態に関する情報を提供します。

トリガーのコールバック通知の作成者、システムを呼び出すと登録済みのルーチンでは、ポインター、コンテキストと 2 つの引数を渡します。 引数の値は、コールバックを作成するコンポーネントによって提供されます。 コールバック ルーチンが作成、ドライバーが、IRQL では常に通知をトリガーするされる同じ IRQL でと呼ばれる&lt;= ディスパッチ\_レベル。

そのコールバック ルーチンでは、ドライバーがの現在の条件が必要にどのようなタスクを実行できます。

呼び出す必要がありますが、ドライバーでは、通知が必要なくなる、 [ **ExUnregisterCallback** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-exunregistercallback)登録されたコールバックの一覧からそのルーチンを削除して、コールバック オブジェクトへの参照を削除します。

 

 




