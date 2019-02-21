---
title: 共同インストーラーの機能
description: 共同インストーラーの機能
ms.assetid: ce8a5ab4-d5ce-4255-a959-9619ff736e37
keywords:
- 共同インストーラー WDK デバイス インストールの機能
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5cdd6adb874bdb16b005a5411b85191b0b099eb1
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56529215"
---
# <a name="co-installer-functionality"></a>共同インストーラーの機能





共同インストーラーとは、する通常、レジストリに追加の構成情報を書き込みますかは、INF が書き込まれるときに使用できない情報を必要とするその他のインストール タスクを実行するユーザー モードの Win32 DLL です。

共同インストーラーには、次の一部またはすべてを実行します。

-   1 つ以上の処理、[デバイス インストールの関数コード](https://msdn.microsoft.com/library/windows/hardware/ff541307)(差分コード) が受信した、[共同インストーラー エントリ ポイント](co-installer-interface.md#co-installer-entry-point)関数。

-   説明に従って、クラスまたはデバイスのインストーラーが呼び出された後、関連付けられているクラスまたはデバイスのインストーラーが呼び出される前に操作またはその両方を実行[共同インストーラー操作](co-installer-operation.md)します。

-   [デバイスのプロパティ ページを提供](providing-device-property-pages.md)ユーザーがデバイスのパラメーターを変更できるようにデバイス マネージャーに表示されるは。

-   以降、Windows Vista で提供[完了-インストール アクション](finish-install-actions--windows-vista-and-later-.md)(への応答を[ **DIF_FINISHINSTALL_ACTION** ](https://msdn.microsoft.com/library/windows/hardware/ff543684)要求) アプリケーションをインストールします。

処理後に呼び出されると、共同インストーラーを確認する必要があります、 **InstallResult**のメンバー、 [COINSTALLER_CONTEXT_DATA](co-installer-interface.md#coinstaller-context-data)構造体。 共同インストーラーする必要があります操作をクリーンアップするのに必要なし、の適切な値を返す場合、その値は NO_ERROR、 **InstallResult**します。

共同インストーラーは、ユーザーから情報を取得することができる場合があります。 このような情報は、追加のデバイスのパラメーターを含めることができるかどうかは、ユーザーがインストールされているデバイスに固有のアプリケーションまたはします。 共同インストーラーは、[インストールの完了] ページとデバイスのプロパティ ページを提供することで、ユーザー インターフェイスを作成できます。 ユーザー インターフェイスの他の形式は許可されません。 Windows では、(新しいハードウェアの検出またはハードウェアの更新プログラムの場合) 内にインストールの最後に、[インストール完了] ページが表示されます。 デバイス マネージャーは、プロパティ ページ を表示し、これらのページに表示されるパラメーターを変更する管理者特権を持つユーザーをできます。

 

 





