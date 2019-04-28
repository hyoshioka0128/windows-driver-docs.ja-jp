---
title: コンテキスト情報の指定
description: コンテキスト情報の指定
ms.assetid: 7133529f-5a6c-4df1-8d03-1c79c0d98fa9
keywords:
- レジストリの呼び出しの WDK カーネル、コンテキスト情報をフィルター処理
- レジストリのドライバー WDK カーネルでは、コンテキスト情報をフィルター処理
- コンテキスト情報
- コンテキスト情報 WDK フィルター レジストリ呼び出し
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 42749cfe5bc25ca98405d0061cb3f3acade2dd70
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63367933"
---
# <a name="specifying-context-information"></a>コンテキスト情報の指定


Configuration manager では、レジストリにレジストリの操作にコンテキスト情報を割り当てるドライバーをフィルター処理をいくつかの方法を提供します。 レジストリのフィルター ドライバーを実行できます。

-   コンテキスト情報を割り当てる、 [ *RegistryCallback* ](https://msdn.microsoft.com/library/windows/hardware/ff560903)ルーチン。

    ドライバーを呼び出すと[ **CmRegisterCallback** ](https://msdn.microsoft.com/library/windows/hardware/ff541918)または[ **CmRegisterCallbackEx** ](https://msdn.microsoft.com/library/windows/hardware/ff541921)レジストリ操作の通知に登録するには、ドライバーはドライバーによって定義されたコンテキスト値を指定できます。 Configuration manager では、このコンテキストの値を渡しますドライバーの*RegistryCallback*ルーチンを configuration manager は、ルーチンを呼び出すたびにします。

    このコンテキスト情報は、Windows xp 以降がサポートされます。

-   レジストリの操作にコンテキスト情報を割り当てます。

    ドライバーは、操作固有のコンテキスト情報を格納できる、 **CallContext**のそれぞれに所属**REG\_*XXX*\_キー\_情報**構造体、ドライバーの*RegistryCallback*ルーチンを受け取ります。 事前通知とレジストリ操作では通知後の両方に、ドライバーが受信した場合、 [ **REG\_POST\_操作\_情報**](https://msdn.microsoft.com/library/windows/hardware/ff560971)構造体には、事前の通知の適切な構造体へのポインターが含まれています。 ときに、 *RegistryCallback*ルーチンを受け取る、 **REG\_POST\_操作\_情報**構造、 **CallContext**その構造体のメンバーと一致する、 **CallContext**事前通知の構造体のメンバー。

    **CallContext**これらの構造体のメンバーは、Windows Vista 以降を使用します。

-   コンテキスト情報をレジストリ キー オブジェクトに割り当てます。

    A [ *RegistryCallback* ](https://msdn.microsoft.com/library/windows/hardware/ff560903)ルーチンは、特定のレジストリ キー オブジェクトへのコンテキスト情報を割り当てることができます。 場合、 *RegistryCallback*ルーチンの呼び出し[ **CmSetCallbackObjectContext** ](https://msdn.microsoft.com/library/windows/hardware/ff541924)キー オブジェクト、後続の事前通知にコンテキスト情報を割り当てるとオブジェクトのすべての操作の後の通知には、コンテキスト値にが含まれます、 **ObjectContext**のそれぞれに所属**REG\_*XXX* \_キー\_情報**構造体。 ドライバーは、複数場合*RegistryCallback*ルーチンの場合、ドライバーは 1 つのレジストリ キー オブジェクトの各ルーチンでは、さまざまなコンテキスト情報を割り当てることができます。

    ドライバーが呼び出された場合**CmSetCallbackObjectContext**、ドライバーの*RegistryCallback*ルーチンが表示されます、 **RegNtCallbackObjectContextCleanup**通知後のキー オブジェクトのハンドルが閉じられました。 この通知に応答して、ルーチンはオブジェクトのコンテキストに割り当てられた、すべてのリソースをリリースする必要があります。 ときに、 *[引数 1]* パラメーターを*RegistryCallback*ルーチンは**RegNtCallbackObjectContextCleanup**、 *[引数 2]* パラメーターがへのポインターを[ **REG\_コールバック\_コンテキスト\_クリーンアップ\_情報**](https://msdn.microsoft.com/library/windows/hardware/ff560919)へのポインターを含む構造体コンテキスト。

    **CmSetCallbackObjectContext**ルーチンと**RegNtCallbackObjectContextCleanup**通知は Windows Vista から使用できます。

 

 




