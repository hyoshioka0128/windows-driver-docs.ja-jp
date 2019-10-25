---
title: コンテキスト情報の指定
description: コンテキスト情報の指定
ms.assetid: 7133529f-5a6c-4df1-8d03-1c79c0d98fa9
keywords:
- レジストリのフィルター選択 WDK カーネル、コンテキスト情報
- レジストリフィルタリングドライバー WDK カーネル、コンテキスト情報
- コンテキスト情報
- コンテキスト情報 WDK フィルターのレジストリ呼び出し
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 734645b3ec2ca323a79e063e03aac447febaf8f3
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838415"
---
# <a name="specifying-context-information"></a>コンテキスト情報の指定


構成マネージャーには、レジストリフィルタリングドライバーがレジストリ操作にコンテキスト情報を割り当てるためのいくつかの方法が用意されています。 レジストリフィルタリングドライバーは、次のことが可能です。

-   [*Registrycallback*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-ex_callback_function)ルーチンにコンテキスト情報を割り当てます。

    ドライバーが[**Cmregistercallback**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-cmregistercallback)または[**Cmregistercallback ex**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-cmregistercallbackex)を呼び出してレジストリ操作の通知を登録する場合、ドライバーはドライバーで定義されたコンテキスト値を指定できます。 構成マネージャーがルーチンを呼び出すたびに、このコンテキスト値がドライバーの*Registrycallback*ルーチンに渡されます。

    このコンテキスト情報は、Windows XP 以降でサポートされています。

-   コンテキスト情報をレジストリ操作に割り当てます。

    ドライバーは、ドライバーの*Registrycallback*ルーチンが受信する各**REG\_*XXX*\_キー\_情報**構造体の**CallContext**メンバーに、操作固有のコンテキスト情報を格納できます。 ドライバーがレジストリ操作の事前通知と事後通知の両方を受信する場合、 [**REG\_post\_操作\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_reg_post_operation_information)構造体には、適切な事前通知構造へのポインターが含まれます。 *Registrycallback*ルーチンが **\_操作\_情報構造体の REG\_POST**を受け取ると、その構造の**CallContext**メンバーが事前通知の**CallContext**メンバーと一致します。データ.

    これらの構造体の**CallContext**メンバーは、Windows Vista 以降で使用できます。

-   コンテキスト情報をレジストリキーオブジェクトに割り当てます。

    [*Registrycallback*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-ex_callback_function)ルーチンは、特定のレジストリキーオブジェクトにコンテキスト情報を割り当てることができます。 *Registrycallback*ルーチンが[**CmSetCallbackObjectContext**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-cmsetcallbackobjectcontext)を呼び出してコンテキスト情報をキーオブジェクトに割り当てた場合、オブジェクトに対するすべての操作の後続の事前通知と事後通知には、コンテキスト値が含まれます。各**REG\_*XXX*の OBJECTCONTEXT メンバー\_キー\_情報**構造体。 ドライバーが複数の*Registrycallback*ルーチンを提供する場合、ドライバーは、1つのレジストリキーオブジェクトに対して、ルーチンごとに異なるコンテキスト情報を割り当てることができます。

    ドライバーが**CmSetCallbackObjectContext**を呼び出した場合、ドライバーの*registrycallback*ルーチンは、キーオブジェクトのハンドルが閉じられた後に**Regntcallback objectcontextcleanup**通知を受け取ります。 この通知に応答して、ルーチンは、オブジェクトのコンテキストに割り当てられたリソースを解放する必要があります。 *Registrycallback*ルーチンの*引数 1*パラメーターが**Regnt Objectcontextcleanup**の場合、*引数 2*パラメーターは、 [ **\_レジストリの\_のクリーンアップ\_コンテキストへのポインターです\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_reg_callback_context_cleanup_information)コンテキストへのポインターを格納している情報構造体。

    **CmSetCallbackObjectContext**ルーチンと**Regnt objectcontextcleanup**通知は、Windows Vista 以降で使用できます。

 

 




