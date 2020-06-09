---
title: Visual Studio でのネットワーク ケーブル経由でのカーネルモード デバッグの設定
description: Microsoft Visual Studio を使用すると、イーサネットネットワーク経由でカーネルモードのデバッグを設定して実行できます。
ms.assetid: 4D442355-526A-4F39-8341-614BB7A41A3E
keywords:
- ネットワークデバッグ visual studio
- visual studio のイーサネットデバッグ
- イーサネットでのデバッグ visual studio
ms.date: 05/16/2018
ms.localizationpriority: medium
ms.openlocfilehash: 6aa5b5762d93eac10d65fbb5d6b479c24d00748f
ms.sourcegitcommit: dadc9ced1670d667e31eb0cb58d6a622f0f09c46
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/09/2020
ms.locfileid: "84533913"
---
# <a name="setting-up-kernel-mode-debugging-over-a-network-cable-in-visual-studio"></a>Visual Studio でのネットワーク ケーブル経由でのカーネルモード デバッグの設定

> [!IMPORTANT]
> この機能は、Windows 10 バージョン1507以降のバージョンの WDK では使用できません。
>

Microsoft Visual Studio を使用すると、イーサネットネットワーク経由でカーネルモードのデバッグを設定して実行できます。 Visual Studio を使用してカーネルモードのデバッグを行うには、Visual Studio に Windows Driver Kit (WDK) が統合されている必要があります。 統合環境をインストールする方法の詳細については、「 [Visual Studio を使用したデバッグ](debugging-using-visual-studio.md)」を参照してください。

Visual Studio を使用してイーサネットデバッグを設定する代わりに、セットアップを自動的に実行することもできます。 詳細については、「 [KDNET Network カーネルデバッグの自動](setting-up-a-network-debugging-connection-automatically.md)セットアップ」を参照してください。

イーサネットネットワークでのデバッグは、他の種類のケーブルを使ったデバッグと比較して次のような利点があります。

-   ホストコンピューターとターゲットコンピューターは、ローカルネットワーク上の任意の場所に配置できます。
-   1台のホストコンピューターから、多くの対象コンピューターを簡単にデバッグできます。
-   ネットワークケーブルは安価であり、すぐに利用できます。
-   2台のコンピューターがある場合は、どちらにもイーサネットアダプターがあると考えられます。 両方にシリアルポートがあるか、どちらも1394ポートを持っている可能性は低くなります。

デバッガーを実行するコンピューターは*ホストコンピューター*と呼ばれ、デバッグ対象のコンピューターは*ターゲットコンピューター*と呼ばれます。 ホストコンピューターは Windows XP 以降を実行している必要があり、対象のコンピューターは Windows 8 以降を実行している必要があります。

## <a name="span-idsupported_network_adaptersspanspan-idsupported_network_adaptersspanspan-idsupported_network_adaptersspansupported-network-adapters"></a><span id="Supported_network_adapters"></span><span id="supported_network_adapters"></span><span id="SUPPORTED_NETWORK_ADAPTERS"></span>サポートされているネットワークアダプター


ホストコンピューターは、任意の有線またはワイヤレスネットワークアダプターを使用できますが、ターゲットコンピューターでは、Windows 用デバッグツールでサポートされているネットワークアダプターを使用する必要があります。 サポートされているネットワークアダプターの一覧については、「 [Windows 8.1 でのネットワークカーネルデバッグのサポートされているイーサネット nic](supported-ethernet-nics-for-network-kernel-debugging-in-windows-8-1.md) 」および「 [Windows 10 でのネットワークカーネルデバッグ用のサポートされているイーサネット nic](supported-ethernet-nics-for-network-kernel-debugging-in-windows-10.md)

## <a name="span-idconfiguring_the_host_and_target_computerspanspan-idconfiguring_the_host_and_target_computerspanspan-idconfiguring_the_host_and_target_computerspanconfiguring-the-host-and-target-computer"></a><span id="Configuring_the_host_and_target_computer"></span><span id="configuring_the_host_and_target_computer"></span><span id="CONFIGURING_THE_HOST_AND_TARGET_COMPUTER"></span>ホストとターゲットコンピューターの構成


1.  ターゲットコンピューターのネットワークアダプターをネットワークハブに接続するか、および適切なネットワークケーブルを使用してスイッチを切り替えます。 ホストコンピューターのネットワークアダプターをネットワークハブに接続するか、標準ケーブルまたはワイヤレス接続を使用してスイッチします。
2.  「[ドライバーの展開およびテスト用にコンピューターをプロビジョニングする (WDK 8.1)](https://docs.microsoft.com/windows-hardware/drivers/gettingstarted/provision-a-target-computer-wdk-8-1)」の説明に従って、ホストとターゲットコンピューターの構成を開始します。
3.  ホストコンピューターの Visual Studio で、[コンピューターの構成] ダイアログボックスが表示されたら、[コンピューターのプロビジョニング] を選択し、[**デバッガーの設定**] を選択します。
4.  [**接続の種類**] で [**ネットワーク**] を選択します。

    ![[接続の種類]、[ターゲット名]、[バスパラメーター] の各フィールドの値を含むデバッガー設定の例を示すスクリーンショット](images/setupnetvs.png)

    [**ポート番号**] では、既定値をそのまま使用するか、任意の値を入力します。 49152 ~ 65535 の任意の数を選択できます。 選択したポートは、ホストコンピューターで実行されているデバッガーによる排他アクセスのために開かれます。 ホストコンピューター上で実行されている他のアプリケーションで使用されていないポート番号を選択してください。

    **メモ**   ネットワークデバッグに使用できるポート番号の範囲は、会社のネットワークポリシーによって制限される場合があります。 ホストコンピューターから、どのような制限があるのかを判断する方法はありません。 会社のポリシーによってネットワークデバッグに使用できるポートの範囲が制限されているかどうかを確認するには、ネットワーク管理者に確認してください。

    **キー**については、自動的に生成された既定値を使用することを強くお勧めします。 ただし、必要に応じて独自のキーを入力することもできます。 詳細については、このトピックで後述[する「独自のキーの作成](#creating-your-own-key)」を参照してください。 [**ホスト IP**] で、既定値をそのまま使用します。 これは、ホストコンピューターの IP アドレスです。

    ターゲットコンピューターにネットワークアダプターが1つしかない場合は、**バスパラメーター**を空のままにすることができます。 対象のコンピューターに複数のネットワークアダプターがある場合は、ターゲットコンピューターでデバイスマネージャーを使用して、デバッグに使用するアダプターの PCI バス、デバイス、および関数番号を決定します。 [**バスパラメーター**] に「 *b*」と入力します。*d*。*f*の場合、 *b*、 *d*、および*f*は、アダプターのバス番号、デバイス番号、および関数番号です。

5.  構成プロセスには数分かかり、対象のコンピューターが1回または2回自動的に再起動される場合があります。 プロセスが完了したら、[**完了**] をクリックします。

**注意**   ターゲットコンピューターがドッキングステーションにあり、ドッキングステーションの一部であるネットワークアダプターに対してネットワークデバッグが有効になっている場合は、ドッキングステーションからコンピューターを削除しないでください。 ドッキングステーションから対象のコンピューターを削除する必要がある場合は、まずカーネルデバッグを無効にします。 ターゲットコンピューターでカーネルデバッグを無効にするには、管理者としてコマンドプロンプトウィンドウを開き、コマンド**bcdedit/debug off**を入力します。 ターゲット コンピューターを再起動します。

 

**メモ**   ターゲットコンピューターに Hyper-v の役割をインストールする場合は、「[仮想マシンホストのネットワークデバッグの](setting-up-network-debugging-of-a-virtual-machine-host.md)セットアップ」を参照してください。

 

## <a name="span-idverifying_dbgsettings_on_the_target_computerspanspan-idverifying_dbgsettings_on_the_target_computerspanspan-idverifying_dbgsettings_on_the_target_computerspanverifying-dbgsettings-on-the-target-computer"></a><span id="Verifying_dbgsettings_on_the_Target_Computer"></span><span id="verifying_dbgsettings_on_the_target_computer"></span><span id="VERIFYING_DBGSETTINGS_ON_THE_TARGET_COMPUTER"></span>ターゲットコンピューターの dbgsettings を確認しています

> [!IMPORTANT]
> BCDEdit を使用してブート情報を変更する前に、テスト PC で BitLocker やセキュアブートなどの Windows のセキュリティ機能を一時的に停止することが必要になる場合があります。
> セキュリティ機能が無効になっている場合は、テストが完了し、テスト PC を適切に管理するときに、これらのセキュリティ機能を再び有効にします。

ターゲットコンピューターで、管理者としてコマンドプロンプトウィンドウを開き、次のコマンドを入力します。

**bcdedit/dbgsettings**

**bcdedit/enum**

```console
...
key                     RF8...KNE
debugtype               NET
hostip                  10.125.5.10
port                    50001
dhcp                    Yes
...
busparams               0.29.7
...
```

*Debugtype*が NET で、 *port*がホストコンピューターの Visual Studio で指定したポート番号であることを確認します。 また、 *key*が、Visual Studio で自動的に生成されたキー (または指定したキー) であることを確認します。

Visual Studio で**バスパラメーター**を入力した場合は、指定したバスパラメーターと*busparams*が一致していることを確認します。

**バスパラメーター**に入力した値が表示されない場合は、次のコマンドを入力します。

**bcdedit/set "{dbgsettings}" busparams** <em>b</em>**。**<em>d</em>**。**<em>f</em>

ここで、 *b*、 *d*、および*f*は、デバッグに使用するように選択したターゲットコンピューター上のネットワークアダプターのバス、デバイス、および関数番号です。

次に例を示します。

**bcdedit/set "{dbgsettings}" busparams 0.29.7**

## <a name="span-idstarting_the_debugging_sessionspanspan-idstarting_the_debugging_sessionspanspan-idstarting_the_debugging_sessionspanstarting-the-debugging-session"></a><span id="Starting_the_Debugging_Session"></span><span id="starting_the_debugging_session"></span><span id="STARTING_THE_DEBUGGING_SESSION"></span>デバッグセッションを開始しています


1.  ホストコンピューターで、Visual Studio の [**ツール**] メニューの [**プロセスにアタッチ**] をクリックします。
2.  [**トランスポート**] で、[ **Windows カーネルモードデバッガー**] を選択します。
3.  [**修飾子**] で、以前に構成したターゲットコンピューターの名前を選択します。
4.  **[アタッチ]** をクリックします。

## <a name="span-idallowing_the_debugger_through_the_firewallspanspan-idallowing_the_debugger_through_the_firewallspanspan-idallowing_the_debugger_through_the_firewallspanallowing-the-debugger-through-the-firewall"></a><span id="Allowing_the_debugger_through_the_firewall"></span><span id="allowing_the_debugger_through_the_firewall"></span><span id="ALLOWING_THE_DEBUGGER_THROUGH_THE_FIREWALL"></span>ファイアウォールを介したデバッガーの許可


ネットワークデバッグ接続を初めて確立しようとすると、ファイアウォール経由でのデバッグアプリケーション (Microsoft Visual Studio) を許可するように求められる場合があります。 Windows のクライアントバージョンではプロンプトが表示されますが、Windows のサーバーバージョンにはプロンプトは表示されません。 [ドメイン]、[プライベート]、および [パブリック] の3種類のネットワークすべてのチェックボックスをオンにして、プロンプトに応答します。 プロンプトが表示されない場合、またはプロンプトが使用可能になったときにチェックボックスをオンにしなかった場合は、コントロールパネルを使用してファイアウォール経由のアクセスを許可する必要があります。 [**コントロールパネル] [ &gt; システムとセキュリティ**] を開き、[ **Windows ファイアウォールによるアプリの許可**] をクリックします。 アプリケーションの一覧で、チェックボックスを使用して、Visual Studio がファイアウォールを通過できるようにします。 Visual Studio を再起動します。

## <a name="span-idcreating-your-own-keyspanspan-idcreating-your-own-keyspancreating-your-own-key"></a><span id="creating-your-own-key"></span><span id="CREATING-YOUR-OWN-KEY"></span>独自のキーを作成する


ターゲットコンピューターのセキュリティを維持するには、ホストコンピューターと対象コンピューター間で移動するパケットを暗号化する必要があります。 ターゲットコンピューターを構成するときに、自動的に生成された暗号化キー (Visual Studio 構成ウィザードによって提供される) を使用することを強くお勧めします。 ただし、独自のキーを作成することもできます。 ネットワークデバッグでは、4 64 ビット値として指定されている256ビットキーを使用します。ベース36は、ピリオドで区切られています。 各64ビット値は、最大13文字で指定されます。 有効な文字は、a ~ z の文字、0 ~ 9 の数字です。 特殊文字は使用できません。 次の一覧は、有効な (ただし、厳密ではない) キーの例を示しています。

-   1.2.3.4
-   abc. 123. .def. 456
-   避けてください。以前のキーを使用します。

## <a name="span-idtroubleshooting_tips_for_debugging_over_a_network_cablespanspan-idtroubleshooting_tips_for_debugging_over_a_network_cablespantroubleshooting-tips-for-debugging-over-a-network-cable"></a><span id="troubleshooting_tips_for_debugging_over_a_network_cable"></span><span id="TROUBLESHOOTING_TIPS_FOR_DEBUGGING_OVER_A_NETWORK_CABLE"></span>ネットワークケーブル経由でのデバッグに関するトラブルシューティングのヒント


### <a name="span-iddebugging_application_must_be_allowed_through_firewallspanspan-iddebugging_application_must_be_allowed_through_firewallspanspan-iddebugging_application_must_be_allowed_through_firewallspandebugging-application-must-be-allowed-through-firewall"></a><span id="Debugging_application_must_be_allowed_through_firewall"></span><span id="debugging_application_must_be_allowed_through_firewall"></span><span id="DEBUGGING_APPLICATION_MUST_BE_ALLOWED_THROUGH_FIREWALL"></span>デバッグアプリケーションはファイアウォール経由で許可されている必要があります

デバッガー (WinDbg または KD) は、ファイアウォール経由でアクセスできる必要があります。 コントロールパネルを使用して、ファイアウォール経由のアクセスを許可できます。 [**コントロールパネル] [ &gt; システムとセキュリティ**] を開き、[ **Windows ファイアウォールによるアプリの許可**] をクリックします。 アプリケーションの一覧で、チェックボックスを使用して、Visual Studio がファイアウォールを通過できるようにします。 Visual Studio を再起動します。

### <a name="span-idport_number_must_be_in_range_allowed_by_network_policyspanspan-idport_number_must_be_in_range_allowed_by_network_policyspanspan-idport_number_must_be_in_range_allowed_by_network_policyspanport-number-must-be-in-range-allowed-by-network-policy"></a><span id="Port_number_must_be_in_range_allowed_by_network_policy"></span><span id="port_number_must_be_in_range_allowed_by_network_policy"></span><span id="PORT_NUMBER_MUST_BE_IN_RANGE_ALLOWED_BY_NETWORK_POLICY"></span>ポート番号は、ネットワークポリシーで許可されている範囲内である必要があります

ネットワークデバッグに使用できるポート番号の範囲は、会社のネットワークポリシーによって制限される場合があります。 会社のポリシーによってネットワークデバッグに使用できるポートの範囲が制限されているかどうかを確認するには、ネットワーク管理者に確認してください。

ポート番号を変更する必要がある場合は、次の手順を使用します。

1.  ホスト コンピューター上の Visual Studio の **[ドライバー]** メニューで、 **[Test (テスト)] &gt; [Configure Computers (コンピューターの構成)]** の順に選びます。
2.  テストコンピューターの名前を選択し、[**次へ**] をクリックします。
3.  [**コンピューターのプロビジョニング**] を選択し、[デバッガーの設定] を選択します。 **[次へ]** をクリックします。
4.  [**ポート番号**] に、ネットワーク管理者が指定できる範囲内の番号を入力します。 **[次へ]** をクリックします。
5.  再構成プロセスには数分かかり、ターゲットコンピューターが自動的に再起動されます。 プロセスが完了したら、[**次へ**] をクリックして**完了**します。

### <a name="span-idspecify_busparams_if_target_computer_has_multiple_network_adaptersspanspan-idspecify_busparams_if_target_computer_has_multiple_network_adaptersspanspan-idspecify_busparams_if_target_computer_has_multiple_network_adaptersspanspecify-busparams-if-target-computer-has-multiple-network-adapters"></a><span id="Specify_busparams_if_target_computer_has_multiple_network_adapters"></span><span id="specify_busparams_if_target_computer_has_multiple_network_adapters"></span><span id="SPECIFY_BUSPARAMS_IF_TARGET_COMPUTER_HAS_MULTIPLE_NETWORK_ADAPTERS"></span>ターゲットコンピューターに複数のネットワークアダプターがある場合は、busparams を指定します

ターゲットコンピューターに複数のネットワークアダプターがある場合は、デバッグに使用するネットワークアダプターのバス、デバイス、および関数番号を指定する必要があります。 バスパラメーターを指定するにはデバイスマネージャーを開き、デバッグに使用するネットワークアダプターを探します。 ネットワークアダプターのプロパティページを開き、バス番号、デバイス番号、および関数番号をメモしておきます。 管理者特権でのコマンドプロンプトウィンドウで、次のコマンドを入力します。ここで、 *b*、 *d*、および*f*は、10進形式のバス、デバイス、および関数の数値です。

**bcdedit-"{dbgsettings}" busparams** <em>b</em>**を設定します。**<em>d</em>**。**<em>f</em>

ターゲット コンピューターを再起動します。

## <a name="span-idrelated_topicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック


[Visual Studio でのカーネル モード デバッグの設定](setting-up-kernel-mode-debugging-in-visual-studio.md)

[Windows 10 でネットワーク カーネル デバッグ用にサポートされているイーサネット NIC](supported-ethernet-nics-for-network-kernel-debugging-in-windows-10.md)

[Windows 8.1 でネットワーク カーネル デバッグ用にサポートされているイーサネット NIC](supported-ethernet-nics-for-network-kernel-debugging-in-windows-8-1.md)

[Windows 8 でネットワーク カーネルのデバッグ用にサポートされているイーサネット NIC](supported-ethernet-nics-for-network-kernel-debugging-in-windows-8.md)

 

 






