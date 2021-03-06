---
title: レジストリ呼び出しのフィルター処理
description: レジストリ呼び出しのフィルター処理
ms.assetid: 6b35c3a0-4ece-4101-b348-e71f5cccf0c8
keywords:
- レジストリの呼び出しの WDK カーネルをフィルター処理
- フィルター ドライバー WDK のカーネルのレジストリ
- RegistryCallback
- レジストリの呼び出しをフィルター処理についてのレジストリ呼び出し WDK カーネル、フィルター処理
- レジストリにレジストリの呼び出しをフィルター処理について、ドライバー WDK カーネルをフィルター処理
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 89bf3dacf84300e4ed6eb2e848f049ea8970e131
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67386603"
---
# <a name="filtering-registry-calls"></a>レジストリ呼び出しのフィルター処理


A*レジストリのドライバーをフィルタ リング*は任意のカーネル モード ドライバーのウイルス対策ソフトウェア パッケージのドライバー コンポーネントなど、レジストリの呼び出しをフィルター処理します。 レジストリを実装するには、configuration manager では、レジストリの関数のすべてのスレッドの呼び出しをフィルター処理するレジストリのフィルター ドライバーを許可します。 Microsoft Windows XP では、レジストリ呼び出しのフィルター処理はサポートが最初。

Windows xp でドライバーをフィルター処理、レジストリを呼び出すことができます[ **CmRegisterCallback** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-cmregistercallback)を登録する、 [ *RegistryCallback* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-ex_callback_function)ルーチンと[**CmUnRegisterCallback** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-cmunregistercallback)コールバック ルーチンの登録を解除します。 *RegistryCallback*ルーチンが、configuration manager は、操作を処理する前に、各レジストリ操作の通知を受信します。 一連の**REG\_*XXX*\_キー\_情報**データ構造は、各レジストリ操作に関する情報を含めることができます。 *RegistryCallback*ルーチンは、レジストリの操作をブロックできます。 コールバック ルーチンは、configuration manager が終了したは、作成するか、レジストリ キーを開くときにも通知を受信します。

Windows Server 2003 では、追加の完了通知を提供します。

Windows Vista では、次の追加レジストリ フィルタ リング機能を提供します。

-   レジストリのフィルター ドライバーはドライバー スタックに階層化でき、各ドライバー スタックでは、レジストリの操作をフィルター処理できます。

-   **CmRegisterCallback**ルーチンを置き換え、 [ **CmRegisterCallbackEx** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-cmregistercallbackex)ルーチン。

-   ドライバーできる完全にレジストリの操作を処理 (または、要求された操作に別の操作をリダイレクト) と、configuration manager が、操作を処理するを防止します。

-   ドライバーは、個々 のレジストリの操作またはキーのオブジェクトにコンテキスト情報を割り当てることができます。

-   ドライバーは、レジストリ操作の出力パラメーターを変更し、値を返します。

-   追加のメンバーすべてに追加された**REG\_*XXX*\_キー\_情報**データ構造体。

-   ドライバーは、追加のレジストリの操作の通知を受信します。

ドライバーは、Windows の各バージョンでフィルター処理できるレジストリの操作の一覧は、次を参照してください。 [ **REG\_通知\_クラス**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ne-wdm-_reg_notify_class)します。

レジストリの呼び出しをフィルター処理の詳細については、次のトピックを参照してください。

[通知を登録します。](registering-for-notifications.md)

[通知の処理](handling-notifications.md)

[階層型のレジストリのドライバーをフィルター処理をサポートしています。](supporting-layered-registry-filtering-drivers.md)

[コンテキスト情報を指定します。](specifying-context-information.md)

[追加のレジストリ情報を取得します。](obtaining-additional-registry-information.md)

[レジストリ通知内のキー オブジェクトが無効なポインター](invalid-key-object-pointers-in-registry-notifications.md)

[ハイブをアプリケーションのレジストリの操作をフィルター処理](filtering-registry-operations-on-application-hives.md)

 

 




