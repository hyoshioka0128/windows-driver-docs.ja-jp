---
title: インストールの完了アクションの実装
description: インストールの完了アクションの実装
ms.assetid: accdf2f5-f324-41dc-afc1-18e03b422fcc
keywords:
- 完了-インストール アクション WDK デバイスのインストール
- WDK の操作の完了-インストール
- DI_FLAGSEX_FINISHINSTALL_ACTION
- DIF_FINISHINSTALL_ACTION
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: bdb393883831b65d8359891185c525486d15e6c1
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385935"
---
# <a name="implementing-finish-install-actions"></a>インストールの完了アクションの実装


*インストーラー* (クラスのインストーラー、クラスの共同インストーラーまたはデバイスの共同インストーラー) 完了インストール アクションを指定します。 -インストールが完了アクションは、実行可能プログラムを実行して、プロセスを作成、スレッドを作成、またはデバイス ドライバーのインストールの完了-インストール プロセスでコードを実行できます。

完了-インストール アクション、インストーラーを実装するには。

1.  インストーラーを処理するときに DI_FLAGSEX_FINISHINSTALL_ACTION フラグを設定、 [ **DIF_NEWDEVICEWIZARD_FINISHINSTALL** ](https://docs.microsoft.com/windows-hardware/drivers/install/dif-newdevicewizard-finishinstall) DIF コードを次のエラー コードのいずれかを返します。
    -   ERROR_DI_DO_DEFAULT 完了インストール ウィザードのページがないクラスのインストーラーである場合。
    -   NO_ERROR 完了インストール ウィザードのページまたは 完了-インストール ウィザードのページの有無の共同インストーラー クラスのインストーラーである場合。

2.  処理時に 完了-インストール アクションを実行する[ **DIF_FINISHINSTALL_ACTION** ](https://docs.microsoft.com/windows-hardware/drivers/install/dif-finishinstall-action)要求。

    インストーラーでは、次の表に、エラー コードのいずれかを返します。

    <table>
    <colgroup>
    <col width="50%" />
    <col width="50%" />
    </colgroup>
    <thead>
    <tr class="header">
    <th align="left">エラー コード</th>
    <th align="left">説明</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td align="left"><p>ERROR_DI_DO_DEFAULT</p></td>
    <td align="left"><p>クラスのインストーラー:クラス インストーラーでは、その完了-インストール操作が正常に実行され、その既定の処理を実行する Windows が要求しています。 クラスのインストーラーには、完了-インストール操作が存在しない場合、このエラー コードが返されますもする必要があります。</p>
    <p>デバイスまたはクラスの共同インストーラー:共同インストーラーでは、このエラー コードは返されません。</p></td>
    </tr>
    <tr class="even">
    <td align="left"><p>NO_ERROR</p></td>
    <td align="left"><p>クラスのインストーラー:クラスのインストーラーには、完了-インストール操作が正常に実行します。 Windows では、その既定の処理は実行しないでください。</p>
    <p>デバイスまたはクラスの共同インストーラー:共同インストーラーが正常に完了インストール アクションを実行するか、完了-インストール操作がありません。</p></td>
    </tr>
    <tr class="odd">
    <td align="left"><p>Microsoft Win32 エラー</p></td>
    <td align="left"><p>インストーラーには、エラーが発生しましたが、完了-インストール操作を再試行する必要があります。 Win32 エラー コードを返すには、Windows で完了インストール操作を完了するには、次回デバイスが列挙する別の完了-インストール プロセスが実行されることを示します。</p></td>
    </tr>
    </tbody>
    </table>




**注**完了インストール アクションが失敗し、もう一度は試行しない必要があるかどうか、クラスのインストーラーが ERROR_DI_DO_DEFAULT を返しますおよびデバイスまたはクラスの共同インストーラーには NO_ERROR が返されます。




完了-インストール アクションを開発する方法については、次を参照してください。[完了インストール アクションの実装に関するガイドライン](guidelines-for-implementing-finish-install-actions.md)完了インストール アクションを実装する方法を示すサンプル コードでは、次のトピックを参照してください。

[コードの例:クラスのインストーラーでインストールが完了アクション](code-example--finish-install-actions-in-a-class-installer.md)

[コードの例:共同インストーラー - インストールが完了アクション](code-example--finish-install-actions-in-a-co-installer.md)









