---
title: インストールの完了アクションの実行
description: インストールの完了アクションの実行
ms.assetid: 9a5f8e7c-ba11-4a2a-82dd-32cd91c3cc39
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c152108f561f4779b1a3d53ab9ca53931ca49175
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67382276"
---
# <a name="running-finish-install-actions"></a>インストールの完了アクションの実行


Windows 8、および以降のバージョンの Windows には、操作アクションを実行するデバイスのインストールの一部として自動的に実行を完了インストールします。 完了-インストール操作を含むドライバーを使用したデバイスのインストール時に自動的に終了インストール アクションは実行されません。 代わりに、Windows または Windows アクション センターの通知 領域で デバイスのソフトウェアのインストールの完了 をユーザーに要求します。 デバイス ソフトウェアをインストールするには、管理者のアクセス許可が必要です。 インストールに失敗した場合、ソフトウェアは、インストールを再試行するユーザーを求める必要があります。 ドライバーに付随する必要があるサポート対象のソフトウェアのインストールも実現できます - インストールが完了アクションが自動的にインストールされません。

Windows 8 では、前に完了インストール アクションを実行する必要があることをデバイスの場合 Windows 最初にしようと以下のいずれかで、完了-インストール プロセスを実行して、完了-インストール操作を完了します。

-   初めて Windows セットアップの完了後に、管理者が Windows にログオンするとき、Windows セットアップ中にインストールされているデバイス。

-   デバイスをインストールまたは core デバイスのインストールの操作が完了したら、次のように、Windows のインストール後に再インストールします。
    -   [ハードウェア最初インストール](hardware-first-installation.md)Windows デバイスの最初の 完了-インストール プロセスが実行されます。 現在のユーザーが管理者でない場合は、Windows はまず最初に 完了-インストール プロセスを実行する前に、管理者の資格情報を入力するユーザーを求められます。

    -   [ソフトウェア最初インストール](software-first-installation.md)デバイスの Windows がインストールまたは再インストールを開始した管理者のコンテキストで、最初に 完了-インストール プロセスを実行します。

Windows 8 では、以前に完了インストール アクションを実行する初回の試行が成功すると、完了-インストール プロセスは 完了 のインストール操作を実行するフラグが付けられると、デバイスをクリアします。 完了-インストール操作を完了する初回の試行に失敗した場合、完了-インストール プロセスとして、完了 のインストール アクションと終了を実行するフラグが設定されているデバイスをクリアしません。 その後、インストール操作が 完了 を実行するフラグが設定された、デバイスは、Windows は繰り返し、次のように、デバイスが列挙されるたびに、新しい 完了-インストール プロセスを実行して完了-インストール操作の完了を試みます。

-   デバイスがインストールされている、次に、管理者ログオンします。

-   管理者のハードウェア変更のスキャンをクリックした場合、**アクション**デバイス マネージャーのメニューやインストール プログラムを呼び出す[ **CM_Reenumerate_DevNode** ](https://docs.microsoft.com/windows/desktop/api/cfgmgr32/nf-cfgmgr32-cm_reenumerate_devnode)コンテキストで管理者。

完了-インストールが呼び出しを処理するデバイスのインストールが完了操作を実行する場合、 [ **SetupDiCallClassInstaller** ](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdicallclassinstaller)を送信する、 [ **DIF_FINISHINSTALL_ACTION** ](https://docs.microsoft.com/windows-hardware/drivers/install/dif-finishinstall-action)デバイス用のインストーラーを要求します。

インストーラーが完了-インストールの動作を実行しの適切なエラー コードを返しますインストーラーに 完了-インストール操作がある場合、 [ **DIF_FINISHINSTALL_ACTION** ](https://docs.microsoft.com/windows-hardware/drivers/install/dif-finishinstall-action)要求。 インストーラーでは、次の表に、エラー コードのいずれかを返します。

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
<td align="left"><p>クラスのインストーラー:クラス インストーラーでは、その完了-インストール操作が正常に実行され、Windows がその既定の処理を実行することを要求しています。</p>
<p>クラスのインストーラーは、完了-インストールの実行がないか、完了インストール アクションが失敗し、もう一度は試行しない必要がある場合にもこのエラー コードを返します。</p>
<p>デバイスまたはクラスの共同インストーラー:共同インストーラーでは、このエラー コードは返されません。</p></td>
</tr>
<tr class="even">
<td align="left"><p>NO_ERROR</p></td>
<td align="left"><p>クラスのインストーラー:クラスのインストーラーには、完了-インストール操作が正常に実行します。 Windows では、その既定の処理は実行しないでください。</p>
<p>デバイスまたはクラスの共同インストーラー:共同インストーラーが正常に完了インストール アクションを実行するか、完了-インストール操作がありません。</p>
<p>共同インストーラーは、完了インストール アクションが失敗し、もう一度は試行しない必要がある場合にもこのエラー コードを返します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>Microsoft Win32 エラー</p></td>
<td align="left"><p>クラスのインストーラー、デバイスの共同インストーラーまたはクラスの共同インストーラー、完了-インストール アクションの処理中にエラーが発生しましたが、完了インストール アクションをもう一度を処理しようとする必要があります。</p>
<p>Win32 エラー コードを返すことによっては、インストーラーは、Windows が完了-インストール操作を完了するには、次回デバイスが列挙する別の完了-インストール プロセスを実行する必要がありますを示します。 インストーラーでは、ユーザーにこのような状況が通知もする必要があります。</p></td>
</tr>
</tbody>
</table>

 

 

 





