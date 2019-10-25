---
title: コールバック オブジェクトの定義
description: コールバック オブジェクトの定義
ms.assetid: 9717795b-dd62-4f17-b931-5ca2b1237e60
keywords:
- コールバックオブジェクト WDK カーネル
- コールバック通知の登録
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: c1d678d5f792cf69dc59a4bfc4cd78cb379fbe11
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72828436"
---
# <a name="defining-a-callback-object"></a>コールバック オブジェクトの定義





ドライバーはコールバックオブジェクトを作成できます。これにより、他のドライバーは、作成するドライバーによって定義された条件の通知を要求できます。 次の図は、コールバックオブジェクトの定義に関連する手順を示しています。

![コールバックオブジェクトの定義を示す図](images/3crt-cbk.png)

オブジェクトを作成する前に、ドライバーは[**Initializeobjectattributes**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfwdm/nf-wudfwdm-initializeobjectattributes)を呼び出して属性を設定します。 コールバックオブジェクトには、システム定義のコールバックの名前と一致しない名前を指定する必要があります。作成者が適切な属性を持つことができます。通常、OBJ\_大文字と小文字\_区別されません。 次に、ドライバーは[**ExCreateCallback**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-excreatecallback)を呼び出し、初期化された属性へのポインターと、コールバックオブジェクトへのハンドルを受け取る位置を渡します。 また、2つのブール値も渡します。これは、このような名前付きオブジェクトがまだ存在しない場合や、オブジェクトが複数の登録済みコールバックルーチンを許可するかどうかを示す、システムがコールバックオブジェクトを作成する必要があるかどうかを示します。

ドライバーは、登録されているコールバックルーチンを呼び出す条件を定義します。 これらの条件は、2つの引数の形式になります。各引数は、コールバックを作成するドライバーによって定義されたパラメーターを指します。 これらの条件は、コールバックオブジェクトの名前と、ドライバーのクライアントが通知を要求する IRQL を記録する必要があります。

コールバック条件が発生すると、ドライバーは[**Exnotifycallback**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-exnotifycallback)を呼び出し、そのハンドルをコールバックオブジェクトと2つの引数に渡します。 次に、コールバックオブジェクトに登録されているすべてのコールバックルーチンが、登録された順序で呼び出され、ルーチンが登録されたときに指定されたコンテキストへの2つの引数とポインターが渡されます。 ドライバーは、IRQL &lt;= DISPATCH\_LEVEL; で**Exnotifycallback**を呼び出す必要があります。システムは、ドライバーがこの呼び出しを行ったのと同じ IRQL でコールバックルーチンを呼び出します。

コールバックオブジェクトを使用してすべての操作が完了したら、コールバックを作成したドライバーは[**ObDereferenceObject**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-obdereferenceobject)を呼び出してその参照カウントをデクリメントし、オブジェクトが削除されていることを確認する必要があります。

 

 




