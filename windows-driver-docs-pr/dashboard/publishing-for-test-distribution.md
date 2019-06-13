---
title: セルフホスト デスクトップ ドライバーへのテスト配布のガイダンス
description: セルフホスト デスクトップ ドライバーへのテスト配布のガイダンス
ms.assetid: 67E31BC1-6209-4264-B9F4-8CDFE8CE2E65
ms.topic: article
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 475b6ecc47d50f43cb7f9f47fb023c6c91a1881c
ms.sourcegitcommit: dabd74b55ce26f2e1c99c440cea2da9ea7d8b62c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/13/2019
ms.locfileid: "63337152"
---
# <a name="test-distribution-guidance-to-self-host-desktop-drivers"></a>セルフホスト デスクトップ ドライバーへのテスト配布のガイダンス


ハードウェア パートナーは、OS のアップグレード シナリオをテストできます。そのためには、Windows Update にドライバーを公開し、テスト配布を使用します。 ドライバーが公開されると、IHV/OEM は、定義済みのレジストリ キーの値を構成することによって、これらのドライバーを要求するようにクライアント システムを構成することができます。 テスト用に配布されたドライバーを受け取るだけでなく、同じクライアント マシンに対して、製品版のドライバーも引き続き提供されます。 これにより、プレリリース版のドライバーが Windows Update から提供される製品版のドライバーの一覧に追加されます。 この方法では、プレリリース版のドライバーが一般ユーザーに提供されないように制限されます。

Windows 10 以降では、Windows アップグレード プロセスの間、クライアント システムでテスト配布のドライバーを受け取ることができます。 ハードウェア パートナーは、このテスト配布のプロセスを利用して、OS のアップグレード シナリオをテストできます。

## <a name="span-idwhatistestdistributionandwhydoineeditspanspan-idwhatistestdistributionandwhydoineeditspanspan-idwhatistestdistributionandwhydoineeditspanwhat-is-test-distribution-and-why-do-i-need-it"></a><span id="What_is_test_distribution__and_why_do_I_need_it_"></span><span id="what_is_test_distribution__and_why_do_i_need_it_"></span><span id="WHAT_IS_TEST_DISTRIBUTION__AND_WHY_DO_I_NEED_IT_"></span>テスト配布の概要と必要性


テスト配布用のドライバーを公開し、テスト用に配布されたドライバーを受け取るようにクライアント システムを構成することによって、そのシステムは、Windows Update で公開されているすべてのプレリリース版のドライバーとファームウェアのコンテンツを受け取ることができるようになります。 この方法を利用すると、パートナーは Windows Update を使用して、テスト対象のユーザーにドライバーを公開できます。このとき、製品版のコンシューマー ユーザーは影響を受けません。

## <a name="span-idpublishingdriverswithtestdistributionspanspan-idpublishingdriverswithtestdistributionspanspan-idpublishingdriverswithtestdistributionspanpublishing-drivers-with-test-distribution"></a><span id="Publishing_drivers_with_test_distribution"></span><span id="publishing_drivers_with_test_distribution"></span><span id="PUBLISHING_DRIVERS_WITH_TEST_DISTRIBUTION"></span>テスト配布でのドライバーの公開


Windows 7、Windows 8.x、Windows 10 システム向けにテスト配布用のドライバーを公開することができます。 テスト配布を公開するには、通常どおり[出荷ラベルを作成](manage-driver-distribution-by-submission.md)し、[ターゲット] セクションで、[テスト レジストリ キー] チェック ボックスをオンにします。

![[テスト レジストリ キー] チェック ボックスを示す画像](images/test-registry-key-checkbox.png)

## <a name="span-idremovingdriverspublishedfortestdistributionspanspan-idremovingdriverspublishedfortestdistributionspanspan-idremovingdriverspublishedfortestdistributionspanremoving-drivers-published-for-test-distribution"></a><span id="Removing_drivers_published_for_test_distribution"></span><span id="removing_drivers_published_for_test_distribution"></span><span id="REMOVING_DRIVERS_PUBLISHED_FOR_TEST_DISTRIBUTION"></span>テスト配布用に公開されたドライバーの削除


### <a name="span-idhowdoimanuallyremovemydriverpublishedfortestdistributionspanspan-idhowdoimanuallyremovemydriverpublishedfortestdistributionspanspan-idhowdoimanuallyremovemydriverpublishedfortestdistributionspanhow-do-i-manually-remove-my-driver-published-for-test-distribution"></a><span id="How_do_I_manually_remove_my_driver_published_for_test_distribution_"></span><span id="how_do_i_manually_remove_my_driver_published_for_test_distribution_"></span><span id="HOW_DO_I_MANUALLY_REMOVE_MY_DRIVER_PUBLISHED_FOR_TEST_DISTRIBUTION_"></span>テスト配布用に公開されたドライバーを手動で削除する方法

テスト配布用に公開されたドライバーは、手動で有効期限切れにするか、(通常の) 配布用に再度公開することができます。

### <a name="span-idhowlongdoesmydriverpublishedfortestdistributionlastspanspan-idhowlongdoesmydriverpublishedfortestdistributionlastspanspan-idhowlongdoesmydriverpublishedfortestdistributionlastspanhow-long-does-my-driver-published-for-test-distribution-last"></a><span id="How_long_does_my_driver_published_for_test_distribution_last_"></span><span id="how_long_does_my_driver_published_for_test_distribution_last_"></span><span id="HOW_LONG_DOES_MY_DRIVER_PUBLISHED_FOR_TEST_DISTRIBUTION_LAST_"></span>テスト配布用に公開されたドライバーの期間

テスト配布ワークフロー内のドライバーが自動的に期限切れになることははありません。 テストが完了したら、「[Windows Update からドライバーの期限を終了する](expire-a-driver-from-windows-update.md)」で説明されている手順を使用して、ドライバーを手動で削除してください。

## <a name="span-idclientpcconfigurationspanspan-idclientpcconfigurationspanspan-idclientpcconfigurationspanclient-pc-configuration"></a><span id="Client_PC_configuration"></span><span id="client_pc_configuration"></span><span id="CLIENT_PC_CONFIGURATION"></span>クライアント PC の構成

### <a name="span-idhowdoiconfiguremymachinetoreceivetestdistributiondriversspanspan-idhowdoiconfiguremymachinetoreceivetestdistributiondriversspanspan-idhowdoiconfiguremymachinetoreceivetestdistributiondriversspanhow-do-i-configure-my-machine-to-receive-test-distribution-drivers"></a><span id="How_do_I_configure_my_machine_to_receive_test_distribution_drivers_"></span><span id="how_do_i_configure_my_machine_to_receive_test_distribution_drivers_"></span><span id="HOW_DO_I_CONFIGURE_MY_MACHINE_TO_RECEIVE_TEST_DISTRIBUTION_DRIVERS_"></span>テスト配布のドライバーを受け取るためのコンピュータの構成方法

テスト配布の更新プログラムを受け取るようにシステムを構成するには、次の手順に従います。

1.  Windows レジストリ エディター (regedit.exe) を開きます
2.  HKLM\\Software\\Microsoft\\ に移動します
3.  サブキー \\DriverFlighting\\Partner\\ を作成します
4.  \\Partner サブキーの下に、 **[TargetRing]** という文字列を作成し、値として 「**Drivers**」と入力します
5.  次に示すように設定されていることを確認します。

    ![Windows レジストリ エディターで、パートナーのサブキーの下に作成された文字列を示す画像](images/registry-editor-drivers.png)

6.  Windows レジストリ エディターを終了します。 変更後、コンピューターを再起動する必要はありません。
7.  次のいずれかの操作を行います。
    -   Windows Update を実行して、更新プログラムがないか確認します。
    -   デバイス マネージャーで対象のデバイスを右クリックして、 **[デバイス ソフトウェアの更新]** を選択します。
8.  テスト ドライバーが正常に提供されることを確認します。

    -   問題が生じた場合は、カスタマー サービス & サポートにお問い合わせください。

        ![カスタマー サービス & サポートに連絡するボタンを示す画像](images/dashboard-help-button.png)

### <a name="span-idhowdoistopmypcfromreceivingtestdistributiondriversspanspan-idhowdoistopmypcfromreceivingtestdistributiondriversspanspan-idhowdoistopmypcfromreceivingtestdistributiondriversspanhow-do-i-stop-my-pc-from-receiving-test-distribution-drivers"></a><span id="How_do_I_stop_my_PC_from_receiving_test_distribution_drivers_"></span><span id="how_do_i_stop_my_pc_from_receiving_test_distribution_drivers_"></span><span id="HOW_DO_I_STOP_MY_PC_FROM_RECEIVING_TEST_DISTRIBUTION_DRIVERS_"></span>PC でテスト配布のドライバーの受け取りを停止する方法

テスト配布のドライバーの受け取りを停止するには、前のセクションで作成した **[TargetRing]** レジストリ データの値を削除します。 **[Drivers]** データの値をダブルクリックして削除してから、 **[OK]** をクリックします。 この操作を行うと、クライアント システムにプレリリース版のドライバーが提供されなくなります。

**注**  システムは、Windows Update からすべての製品版のドライバーを引き続き受け取ります。

 

1.  Windows レジストリ エディター (regedit.exe) を開きます
2.  HKLM\\Software\\Microsoft\\DriverFlighting\\Partner に移動します。 これらのキーが存在しない場合、作業は完了しています。それ以外の場合は、次の手順に進みます。
3.  \\Partner サブキーで、 **[TargetRing]** のデータの値を削除します
4.  次に示すように設定されていることを確認します。

    ![Windows レジストリ エディターで、パートナーのサブキーの下で削除された文字列値を示す画像](images/registry-editor-no-drivers.png)

5.  Windows レジストリ エディターを終了します。 変更後、コンピューターを再起動する必要はありません。
6.  次のいずれかの操作を行います。
    -   Windows Update を実行して更新プログラムを確認します
    -   デバイス マネージャーで対象のデバイスを右クリックして、 **[デバイス ソフトウェアの更新]** を選択します。

 

 





