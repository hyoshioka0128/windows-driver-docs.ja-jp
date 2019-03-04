---
title: ドライバーの展開およびテストのためのコンピューターのプロビジョニング (WDK 10)
description: ターゲット コンピューターやテスト コンピューターのプロビジョニングは、自動ドライバー展開、テスト、デバッグ用にコンピューターを構成するプロセスです。 コンピューターをプロビジョニングするには、Microsoft Visual Studio を使います。
ms.assetid: A2615EE9-316E-4AE2-BBAA-B9E153090016
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 672f1eba11799e6b110d7c6e898551e9576cb3f4
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56518971"
---
# <a name="provision-a-computer-for-driver-deployment-and-testing-wdk-10"></a>ドライバーの展開およびテストのためのコンピューターのプロビジョニング (WDK 10)


*ターゲット コンピューターやテスト コンピューターのプロビジョニング*は、自動ドライバー展開、テスト、デバッグ用にコンピューターを構成するプロセスです。 コンピューターをプロビジョニングするには、Microsoft Visual Studio を使います。

テスト環境とデバッグ環境には、*ホスト コンピューター*と*ターゲット コンピューター*という、2 台のコンピューターがあります。 ターゲット コンピューターは*テスト コンピューター*とも呼ばれます。 ドライバーの開発とビルドは、ホスト コンピューター上の Visual Studio で行います。 デバッガーはホスト コンピューター上で実行され、Visual Studio のユーザー インターフェイスで利用できます。 ドライバーのテストとデバッグを行うときは、ドライバーをターゲット コンピューター上で実行します。

ホスト コンピューターとターゲット コンピューターが、名前によって相互に ping できる必要があります。 ホスト コンピューターとターゲット コンピューターの両方が同じワークグループまたは同じネットワーク ドメインに参加している場合、この ping は簡単に行うことができます。 お使いのコンピューターがワークグループに属している場合は、ハブやスイッチではなくルーターにコンピューターを接続することをお勧めします。 

> [!TIP]
> WDK の自動プロビジョニング プロセスでは、仮想マシンのプロビジョニングはサポートされません。 ただし、[ステップ バイ ステップ ラボ (Echo カーネル モード)](../debugger/debug-universal-drivers---step-by-step-lab--echo-kernel-mode-.md) の説明に従って手動でターゲット VM をセットアップすると、VM 上のドライバーをテストできます。

## <a name="span-idpreparingthetargetcomputerforprovisioningspanspan-idpreparingthetargetcomputerforprovisioningspanprepare-the-target-computer-for-provisioning"></a><span id="preparing_the_target_computer_for_provisioning"></span><span id="PREPARING_THE_TARGET_COMPUTER_FOR_PROVISIONING"></span>ターゲット コンピューターのプロビジョニングの準備


1.  ターゲット コンピューターには、ドライバーの実行とテストに使うオペレーティング システムをインストールします。

2.  x86 または x64 ターゲット コンピューターでセキュア ブートが有効になっている場合は無効にします。 Unified Extensible Firmware Interface (UEFI) とセキュア ブートについては、[UEFI ファームウェア](https://go.microsoft.com/fwlink/p/?LinkID=309386)に関するページをご覧ください。

    ターゲット コンピューターが ARM プロセッサを使っている場合は、Windows デバッグ ポリシーをインストールします。 これを実行できるのは、Microsoft またはターゲット コンピューターの製造元だけです。 セキュア ブートを無効にする必要はありません。

3.  ターゲット コンピューターで、ターゲット コンピューターのプラットフォームに適合する WDK Test Target Setup MSI を実行します。 MSI は、Windows Driver Kit (WDK) インストール ディレクトリの Remote にあります。

    以下に例を示します。C:\\Program Files (x86)\\Windows Kits\\10\\Remote\\x64\\WDK Test Target Setup x64-x64\_en-us.msi

4.  ターゲット コンピューターで N または KN バージョンの Windows を実行している場合、N バージョンと KN バージョンの Windows に対応した Media Feature Pack をインストールします。

    -   [N バージョンと KN バージョンの Windows 8.1 用の Media Feature Pack](https://go.microsoft.com/fwlink/p?linkid=329737)
    -   [N バージョンと KN バージョンの Windows 8 用の Media Feature Pack](https://go.microsoft.com/fwlink/p?linkid=329738)
    -   [N バージョンと KN バージョンの Windows 7 用の Media Feature Pack](https://go.microsoft.com/fwlink/p?linkid=329739)

5.  ターゲット コンピューターで Windows Server を実行している場合、WDK Test Target Setup MSI で作った DriverTest フォルダーを探します  (例: c:\\DriverTest)。 **[DriverTest]** フォルダーを右クリックし、**[プロパティ]** をクリックします。 **[セキュリティ]** タブで、**[Authenticated Users]** グループに **[変更]** のアクセス許可を設定します。

ホスト コンピューターとターゲット コンピューターが互いに ping できることを確認します。 管理者としてコマンド プロンプト ウィンドウを開き、「**ping** <*コンピューター名*>」と入力します。

ホスト コンピューターとターゲット コンピューターがワークグループに参加していて、異なるサブネットにある場合、ホスト コンピューターとターゲット コンピューターが通信できるように一部のファイアウォール設定の調整が必要になることがあります。 次の手順に従います。

1.  ターゲット コンピューターのコントロール パネルで、**[ネットワークとインターネット] &gt; [ネットワークと共有センター]** の順にクリックします。 アクティブなネットワークに注目します。 これは、**[パブリック ネットワーク]**、**[プライベート ネットワーク]**、**[ドメイン]** のどれかになります。
2.  ターゲット コンピューターのコントロール パネルで、**[システムとセキュリティ] &gt; [Windows ファイアウォール] &gt; [詳細設定] &gt; [受信の規則]** の順にクリックします。
3.  受信の規則の一覧で、アクティブなネットワークのネットワーク探索の規則をすべて特定します  (たとえば、**[プロファイル]** が **[プライベート]** になっているネットワーク探索の規則をすべて特定します)。それらの各規則をダブルクリックし、**[スコープ]** タブを開きます。**[リモート IP アドレス]** で、**[任意の IP アドレス]** をクリックします。
4.  受信の規則の一覧で、アクティブなファイルとプリンターの共有の規則をすべて特定します。 それらの規則ごとに、規則をダブルクリックし、**[スコープ]** タブを開きます。**[リモート IP アドレス]** で、**[任意の IP アドレス]** をクリックします。

## <a name="span-idprovisionthetargetcomputerspanspan-idprovisionthetargetcomputerspanspan-idprovisionthetargetcomputerspanprovision-the-target-computer"></a><span id="Provision_the_target_computer"></span><span id="provision_the_target_computer"></span><span id="PROVISION_THE_TARGET_COMPUTER"></span>ターゲット コンピューターのプロビジョニング


ホスト コンピューター上の Visual Studio でターゲット コンピューターをプロビジョニングする準備ができました。

1.  ホスト コンピューター上の Visual Studio の **[ドライバー]** メニューで、**[テスト] &gt; [Configure Devices (デバイスの構成)]** の順にクリックします。

    **[新しいデバイスの追加]** をクリックします。

2.  **[Network host name (ネットワーク ホスト名)]** にターゲット コンピューターの名前またはローカル IP アドレスを入力します。 **[Provision device and choose debugger settings (デバイスをプロビジョニングし、デバッガーの設定を選択する)]** をクリックします。

    ![デバイスの構成に関するダイアログ ボックスのスクリーン ショット](images/vs2015-device-configuration.png)

    **[次へ]** をクリックします。

3.  デバッグ接続の種類を選び、必要なパラメーターを入力します。

    さまざまな種類の接続に対するデバッグのセットアップの詳細については、CHM ファイルまたは [Windows のデバッグ ツールに関するページ](https://go.microsoft.com/fwlink/p/?linkid=223405)にあるオンライン ドキュメントで、「[手動でのカーネル モード デバッグの設定](../debugger/setting-up-kernel-mode-debugging-in-windbg--cdb--or-ntsd.md)」を参照してください。

4.  プロビジョニング プロセスには数分かかり、ターゲット コンピューターが自動的に 1 回か 2 回、再起動されます。 プロビジョニングが完了したら、**[完了]** をクリックします。

 

 





