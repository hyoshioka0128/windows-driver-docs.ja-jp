---
title: 完了-インストール アクションを処理する方法
description: 完了-インストール アクションを処理する方法
ms.assetid: 028cce46-018d-496e-bc99-c8bf6158c898
keywords:
- 完了-インストール アクション WDK デバイスのインストール
- 完了-インストールの既定の操作
- サーバー側インストール WDK
- CONFIG_FINISHINSTALL
- WDK の操作の完了-インストール
- DI_FLAGSEX_FINISHINSTALL_ACTION
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1e8368607b1af9f00f2a2044cfca3a6dd622ffc2
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56558189"
---
# <a name="how-finish-install-actions-are-processed"></a>完了-インストール アクションを処理する方法


によって同じ方法でデバイスのインストールが完了操作が実行される、*インストーラー* (クラスのインストーラー、クラスの共同インストーラーまたはデバイスの共同インストーラー)、インストールをしたかどうかに関係なく、 [ *ハードウェア最初インストール*](hardware-first-installation.md)か、または新しいハードウェアの検出ウィザード、ドライバー ソフトウェアの更新ウィザードまたはベンダーから提供されたインストール プログラム (、などのインストールプログラムを実行して、インストールを開始[*ソフトウェア最初インストール*](software-first-installation.md))。

**注**  管理者 (または、UAC プロンプトを管理者の資格情報を提供できる制限付きユーザー) がアクション センターで Windows 8、Windows 8.1、および Windows 10 では、完了-インストール アクションを完了する必要があります。 ユーザーは、[デバイスのソフトウェアのインストールの完了] をクリックする必要があります。

 

Windows は、その他のすべてのインストール操作が完了しなど、デバイスが起動された後に終了インストール アクションを処理します。

-   デバイスのインストールのコア (とも呼ばれます*サーバー側インストール*) では、デバイスのドライバーがインストールされているし、システムのプラグ アンド プレイ (PnP) マネージャー コンポーネントによって読み込まれます。

Windows は、インストーラーの 完了-インストール アクションを処理する次の手順を実行します。

1.  中核となるデバイスのインストールの最後に、Windows を呼び出す[ **SetupDiCallClassInstaller** ](https://msdn.microsoft.com/library/windows/hardware/ff550922)を送信する、 [ **DIF_NEWDEVICEWIZARD_FINISHINSTALL** ](https://msdn.microsoft.com/library/windows/hardware/ff543702)デバイス用のインストーラーを要求します。

    DIF_NEWDEVICEWIZARD_FINISHINSTALL は、中核となるデバイスのインストールの両方のコンテキストで、クライアントのコンテキストで送信される唯一の差分コードです。 そのため、クラスのインストーラー、クラスの共同インストーラーまたはデバイスの共同インストーラーする必要があることを示す完了インストール アクション DIF_NEWDEVICEWIZARD_FINISHINSTALL 処理中の代わりに DIF_INSTALLDEVICE 処理中にします。

2.  インストーラーは、完了-インストール アクションを提供する場合に応答 DIF_FLAGSEX_FINISHINSTALL_ACTION フラグを設定、 [ **DIF_NEWDEVICEWIZARD_FINISHINSTALL** ](https://msdn.microsoft.com/library/windows/hardware/ff543702)要求。 DIF_FLAGSEX_FINISHINSTALL_ACTION フラグは設定されているすべてのインストーラーが DIF_NEWDEVICEWIZARD_FINISHINSTALL 要求を処理した後場合、デバイスが [完了] のインストール操作を実行するフラグが設定されます。

    この操作の詳細については、次を参照してください。[実行完了-インストール アクションを持つものとして、デバイスをマークする](setting-the-configflag-finishinstall-action-device-configuration-flag.md)します。

3.  Core デバイスのインストールが完了したら、デバイス、Windows は、完了-インストール アクションを実行するデバイスのフラグが設定されているかどうかを確認します。 場合は、Windows は、デバイスに固有の 完了-インストール アクションを実行する 完了-インストール プロセスをキューします。 ユーザーのコンテキストでプロセスを実行します。

    Windows 8 およびそれ以降のバージョンでは、完了-インストール アクションは自動的に実行されませんデバイスのインストールの一部として。 代わりに、管理者 (または、UAC プロンプトを管理者の資格情報を提供できる制限付きユーザー) する必要がありますアクション センターに移動するアイテムに対処して「デバイスのソフトウェアのインストールを完了する」メンテナンス終了インストール アクションを実行するのです。 それまでは、完了-インストール アクションは実行されません。 たとえば、完了-インストール操作を含むドライバーをインストールするデバイスをユーザーが接続される場合完了インストール アクションは自動的に実行されませんその時点で。 完了-インストール アクションは、ユーザーが手動で開始したときに、後で実行されます。 Windows は、完了-インストール アクションを実行すると、操作が 1 つを実行する機会にします。 アクションが失敗した場合をもう一度お試しし、後でユーザーを許可するための適切な手順を実行する必要があります。 ドライバーに付随する必要があるサポート対象のソフトウェアのインストールも実現できます - インストールが完了アクションが、それもいない自動インストールします。

    Windows 7、完了-インストール プロセスは、以下のいずれかの管理者の資格情報を持つユーザーのコンテキストでのみ実行します。

    -   デバイスがアタッチされている間、管理者の資格情報を持つユーザーがログオンする次の時間。
    -   ときに、デバイスを再接続します。
    -   ユーザーが選択すると**ハードウェア変更のスキャン**デバイス マネージャーでします。

    ユーザーが管理者特権なし署名されている場合、Windows には、ユーザーの同意と、管理者コンテキストで、完了-インストール アクションを実行する資格情報が求められます。

4.  ときに操作の実行を完了-インストール、完了-インストール プロセスを開始、デバイスの 完了-インストール ウィザード ページが完了するし、を呼び出して[ **SetupDiCallClassInstaller** ](https://msdn.microsoft.com/library/windows/hardware/ff550922) を送信する[ **DIF_FINISHINSTALL_ACTION** ](https://msdn.microsoft.com/library/windows/hardware/ff543684) 」の説明に従って、デバイスのすべてのインストーラーに要求[- インストールが完了操作を実行している](running-finish-install-actions.md)します。

5.  」の説明に従って Windows が既定の 完了-インストール アクションを実行のインストーラーの 完了-インストール操作を完了すると、[既定の 完了-インストール アクションを実行している](running-the-default-finish-install-action.md)します。

 

 





