---
title: '[WDF Drivers](WDF ドライバー) タブ'
description: このトピックでは、WDF Verifier のドライバーを WDF ページに関する詳細情報を提供します。
ms.assetid: e1e1d92e-1173-48ef-b985-688ebfb08bdc
keywords:
- WDF Verifier コントロール アプリケーション WDK
- WDF Verifier WDK
- ツールを WDK を確認しています
- ドライバー WDK WDF のテスト
- ドライバー WDK WDF のデバッグ
- ドライバー WDK WDF の確認
- KMDF verifier ツールを WDK の WDF
- UMDF verifier ツールを WDK の WDF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 42d5dc32f07ef053034be198bf87154ab0de632a
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56573722"
---
# <a name="wdf-drivers-tab"></a>[WDF Drivers]\(WDF ドライバー\) タブ


このトピックでは、WDF Verifier のについて詳細な情報を提供します。 **WDF ドライバー**ページ。 このページには、コンピューター上のすべての WDF ドライバーが一覧表示し、検証の設定と、それらを使用するデバイスの設定を変更することができます。 特定のドライバーに関心がある場合は、ここからを開始します。

アプリケーションを起動するときに、システムで現在 WDF ドライバーとランタイムのバージョンの一覧が表示されます。 それぞれの行では、ドライバーのバイナリ ファイル、そのサービスの表示名、framework のバージョンの名前が含まれていて、KMDF ドライバーでは、型を開始します。

ドライバーを強調表示したときにするドライバーが現在使用しているすべてのデバイスが表示されますだけでなく UMDF ホスト プロセスに関連します。 ホスト プロセスの制御を表示されるは、実行中の UMDF ドライバーが選択されている場合だけです。

![wdf ドライバー タブのスクリーン ショット](images/wdfverifier-tab1.png)

## <a name="span-idcolorschemespanspan-idcolorschemespanspan-idcolorschemespancolor-scheme"></a><span id="Color_Scheme"></span><span id="color_scheme"></span><span id="COLOR_SCHEME"></span>色スキーム


各ドライバーの場合は、色分けされたアイコンは、使用、KMDF、UMDF 1 または UMDF 2 を示します。

カラー コードでは、ドライバーの状態とは、ドライバーの検証の設定の変更が反映されるようにする必要がありますを示します。

-   青は、ドライバーが使用されて、1 つまたは複数の PnP デバイスに関連付けられたことを示します。 変更を反映するには、無効にして、これらのデバイスを再度有効にする必要があります。 WDF Verifier がするのでを選択することができます、**個人設定**タブ。これらのドライバーに対しては、関連付けられているデバイスの一覧を取得します。
-   Red が使用されて、ドライバーは PnP デバイスに関連付けられていることを示します。 変更を有効にします。
    -   Kmdf、再起動する必要があります。
    -   UMDF、停止し、すべて UMDF ホスト プロセスを再起動する必要があります。
-   緑は、ドライバーが現在の使用がないことを示します。 設定を変更する場合、変更反映、次回、ドライバーが読み込まれます。

## <a name="span-idpresetoptionsspanspan-idpresetoptionsspanspan-idpresetoptionsspanpreset-options"></a><span id="Preset_Options"></span><span id="preset_options"></span><span id="PRESET_OPTIONS"></span>事前設定のオプション


ドライバー固有の設定 (KMDF および UMDF 2) を持つドライバーでは、クイック オプション メニューの次のドライバー名を右クリックします。

-   既定の設定に設定します。
-   WDF のブレークポイントとドライバーのコードで確認してくださいマクロを有効にします。
-   (詳細でありより大きな IFR バッファー、下位レベルの検証で検証) のすべての推奨されるテスト設定を有効にします。

ドライバーの設定を変更したが、その変更をコミットしていない場合 (\*)、ドライバー名の後に表示されると、メニューには、変更を元に戻す、追加のオプションが含まれています。

## <a name="span-idchangingindividualverificationsettingsforadriverspanspan-idchangingindividualverificationsettingsforadriverspanspan-idchangingindividualverificationsettingsforadriverspanchanging-individual-verification-settings-for-a-driver"></a><span id="Changing_Individual_Verification_Settings_for_a_Driver"></span><span id="changing_individual_verification_settings_for_a_driver"></span><span id="CHANGING_INDIVIDUAL_VERIFICATION_SETTINGS_FOR_A_DRIVER"></span>ドライバーの個々 の検証の設定を変更します。


ドライバーの検証の現在の設定を表示する色のアイコンの左側にある + をクリックします。 それらを変更する個々 のオプションの右クリックすることができます。

ブール値の設定を右クリックしてそれを切り替えます。 編集コントロールを提示他のユーザー値を入力するときに、いくつかの設定は、有効なオプションの一覧を提示します。 アプリでは、無効な値を入力するとビープ音がします。 キーを押して**Enter**新しい値を使用したり、変更をキャンセルするコントロールの外側をクリックします。

16 進数値を入力する必要があります**AllocateFailCount**、および 10 進値**HostTimeoutSeconds**します。

KMDF 検証機能を必要とする機能を有効にした場合、 **VerifierOn**オプションは現在オフは、アプリはオンにします。 手動で無効することができますも。 ここでは、この機能を説明するテキストを示しますと検証ツールにある場合。 テキストの説明を設定するたびに、設定の状態を確認できますで類似する変更は、その他の設定、またはアプリの検証またはドライバーの検証ツールの使用状況に依存します。

開始しデバイスを停止または新しいドライバーをインストール場合は、在庫を更新する WDF Verifier を再起動する必要があります。

変更する場合、 **WDF ドライバー**  ページで、その変更反映された表示されます、 **WDF を使用してデバイス**ページ。

 

 





