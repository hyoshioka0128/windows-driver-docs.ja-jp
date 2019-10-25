---
title: レジストリ呼び出しのフィルター処理
description: レジストリ呼び出しのフィルター処理
ms.assetid: 6b35c3a0-4ece-4101-b348-e71f5cccf0c8
keywords:
- レジストリ呼び出しのフィルター WDK カーネル
- レジストリフィルタリングドライバー WDK カーネル
- RegistryCallback
- レジストリのフィルター選択 WDK カーネル、レジストリ呼び出しのフィルター処理について
- レジストリフィルタリングドライバー WDK カーネル、レジストリ呼び出しのフィルター処理について
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: ca5d0791cd6e1eea41ecdef1af956d55f3339e52
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838691"
---
# <a name="filtering-registry-calls"></a>レジストリ呼び出しのフィルター処理


*レジストリフィルタリングドライバー*は、ウイルス対策ソフトウェアパッケージのドライバーコンポーネントなど、レジストリの呼び出しをフィルター処理するカーネルモードドライバーです。 レジストリを実装する構成マネージャーによって、レジストリフィルタードライバーは、レジストリ関数の任意のスレッド呼び出しをフィルター処理できます。 Microsoft Windows XP では、最初にレジストリ呼び出しのフィルター処理がサポートされていました。

Windows XP では、レジストリフィルタリングドライバーは[**Cmregistercallback**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-cmregistercallback)を呼び出して、 [*registrycallback*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-ex_callback_function)ルーチンと[**cmunregistercallback**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-cmunregistercallback)を登録し、コールバックルーチンの登録を解除できます。 *Registrycallback*ルーチンは、configuration manager が操作を処理する前に、各レジストリ操作の通知を受信します。 一連の**REG\_*XXX*\_キー\_情報**のデータ構造には、各レジストリ操作に関する情報が含まれています。 *Registrycallback*ルーチンは、レジストリ操作をブロックできます。 また、コールバックルーチンは、configuration manager がレジストリキーの作成またはオープンを完了したときにも通知を受け取ります。

Windows Server 2003 では、追加の完了通知が提供されます。

Windows Vista には、次のレジストリフィルタリング機能が追加されています。

-   レジストリフィルタリングドライバーは、ドライバースタック内で階層化することができ、スタック内の各ドライバーはレジストリ操作をフィルター処理できます。

-   **Cmregistercallback**ルーチンは、 [**Cmregistercallback ex**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-cmregistercallbackex)ルーチンによって置き換えられています。

-   ドライバーは、レジストリ操作を完全に処理する (または要求された操作を別の操作にリダイレクトする) ことができ、構成マネージャーが操作を処理するのを防ぎます。

-   ドライバーは、個々のレジストリ操作またはキーオブジェクトにコンテキスト情報を割り当てることができます。

-   ドライバーは、レジストリ操作の出力パラメーターと戻り値を変更できます。

-   すべての**REG\_*XXX*\_キー\_情報**データ構造に追加のメンバーが追加されました。

-   ドライバーは、追加のレジストリ操作の通知を受信します。

ドライバーが各バージョンの Windows でフィルター処理できるレジストリ操作の一覧については、「 [**REG\_NOTIFY\_クラス**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ne-wdm-_reg_notify_class)」を参照してください。

レジストリ呼び出しのフィルター処理の詳細については、次のトピックを参照してください。

[通知の登録](registering-for-notifications.md)

[通知の処理](handling-notifications.md)

[階層化レジストリフィルタードライバーのサポート](supporting-layered-registry-filtering-drivers.md)

[コンテキスト情報の指定](specifying-context-information.md)

[追加のレジストリ情報の取得](obtaining-additional-registry-information.md)

[レジストリ通知に無効なキーオブジェクトポインターがあります](invalid-key-object-pointers-in-registry-notifications.md)

[アプリケーションハイブでのレジストリ操作のフィルター処理](filtering-registry-operations-on-application-hives.md)

 

 




