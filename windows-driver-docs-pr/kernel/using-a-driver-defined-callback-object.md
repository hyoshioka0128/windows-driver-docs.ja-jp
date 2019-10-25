---
title: ドライバーによって定義されたコールバック オブジェクトの使用
description: ドライバーによって定義されたコールバック オブジェクトの使用
ms.assetid: b3b32534-0641-4818-9384-65fd45f689e8
keywords:
- コールバックオブジェクト WDK カーネル
- ドライバーで定義されたコールバックオブジェクトの WDK カーネル
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 43c87ccd6c865ba117601a41df282483a5b551be
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72836068"
---
# <a name="using-a-driver-defined-callback-object"></a>ドライバーによって定義されたコールバック オブジェクトの使用





別のドライバーによって定義されたコールバックオブジェクトを使用するには、次の図に示すように、ドライバーがオブジェクトを開き、コールバックがトリガーされたときに呼び出されるルーチンを登録します。 通知を要求するドライバーは、コールバックオブジェクトの名前を認識している必要があり、コールバックルーチンに渡される引数のセマンティクスを理解している必要があります。

![コールバック通知の登録を示す図](images/3reg-cbk.png)

オブジェクトを開く前に、ドライバーは[**Initializeobjectattributes**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfwdm/nf-wudfwdm-initializeobjectattributes)を呼び出して属性ブロックを作成し、オブジェクトの名前を指定する必要があります。 属性ブロックへのポインターを取得した後、 [**ExCreateCallback**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-excreatecallback)を呼び出します。これは、属性ポインター、コールバックへのハンドルを受け取る場所、および*Create*パラメーターの**FALSE**を呼び出し、既存のが必要であることを示します。コールバックオブジェクト。

ドライバーは、返されたハンドルを使用して[**Exregistercallback**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-exregistercallback)を呼び出し、コールバックルーチンを登録できます。

コールバックルーチンには、次のプロトタイプがあります。

```cpp
typedef VOID (*PCALLBACK_FUNCTION ) (
    IN PVOID CallbackContext,
    IN PVOID Argument1,
    IN PVOID Argument2
    );
```

コールバック*コンテキスト*パラメーターは、呼び出されるたびにコールバックルーチンに渡されるコンテキストポインターです。 通常、このパラメーターはコンテキストデータのブロックへのポインターであり、ルーチンをディスパッチ\_レベルで呼び出すことができる場合は、呼び出し元が非ページプールから割り当てる必要があります。 2つの引数は、コールバックを作成したコンポーネントによって定義されます。 通常、引数は、コールバックをトリガーした条件に関する情報を提供します。

コールバックの作成者が通知をトリガーすると、システムは、コンテキストへのポインターと2つの引数を渡して、登録されたルーチンを呼び出します。 引数の値は、コールバックを作成したコンポーネントによって提供されます。 コールバックルーチンは、作成元のドライバーが通知をトリガーしたときと同じ IRQL で呼び出されます。これは、常に IRQL &lt;= ディスパッチ\_レベルです。

コールバックルーチンでは、ドライバーは、現在の条件に必要なすべてのタスクを実行できます。

ドライバーが通知を必要としなくなった場合は、 [**Exunregistercallback**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-exunregistercallback)を呼び出して、登録されているコールバックの一覧からルーチンを削除し、コールバックオブジェクトへの参照を削除する必要があります。

 

 




