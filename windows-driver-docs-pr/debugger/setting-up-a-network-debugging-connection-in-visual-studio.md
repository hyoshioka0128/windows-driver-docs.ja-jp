---
title: Visual Studio でのネットワーク ケーブル経由でのカーネルモード デバッグの設定
description: Microsoft Visual Studio を使用して、設定し、イーサネット ネットワーク経由でのカーネル モードのデバッグを実行することができます。
ms.assetid: 4D442355-526A-4F39-8341-614BB7A41A3E
keywords:
- ネットワーク デバッグ visual studio
- イーサネット visual studio のデバッグ
- visual studio のイーサネット経由でのデバッグ
ms.date: 05/16/2018
ms.localizationpriority: medium
ms.openlocfilehash: 8420a344c8072411521aca2dd2f0c2476ab455aa
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67366384"
---
# <a name="setting-up-kernel-mode-debugging-over-a-network-cable-in-visual-studio"></a>Visual Studio でのネットワーク ケーブル経由でのカーネルモード デバッグの設定

> [!IMPORTANT]
> この機能は、Windows 10 バージョン 1507、以降のバージョンの WDK でご利用いただけません。
>

Microsoft Visual Studio を使用して、設定し、イーサネット ネットワーク経由でのカーネル モードのデバッグを実行することができます。 カーネル モードのデバッグを Visual Studio を使用するには、Windows Driver Kit (WDK) の Visual Studio と統合が必要です。 統合環境をインストールする方法については、次を参照してください。 [Windows ドライバー開発](https://go.microsoft.com/fwlink/p?linkid=301383)します。

Visual Studio を使用して、イーサネットのデバッグを設定する代わりに、自動的にセットアップを実行できます。 詳細については、次を参照してください。[設定を KDNET ネットワーク カーネル デバッグを自動的に](setting-up-a-network-debugging-connection-automatically.md)します。

イーサネット ネットワーク経由でのデバッグと、その他の種類のケーブル経由でのデバッグと比較して次の利点があります。

-   ホストおよびターゲット コンピューターは、ローカル ネットワークに任意の場所に配置できます。
-   1 つのホスト コンピューターから多数のターゲット コンピューターのデバッグが容易になります。
-   ネットワーク ケーブルは安価なすぐに利用できます。
-   2 台のコンピューターを指定するには、可能性は両方があることのイーサネット アダプターです。 両方がシリアル ポートに、1394 ポートがある両方に低い可能性があります。

デバッガーを実行しているコンピューターと呼ばれる、*ホスト コンピューター*とは、デバッグ中のコンピューターと呼びます、*対象のコンピュータ*します。 ホスト コンピューターに Windows XP を実行する必要がありますまたはそれ以降、および 8 またはそれ以降、ターゲット コンピューターで Windows が実行する必要があります。

## <a name="span-idsupportednetworkadaptersspanspan-idsupportednetworkadaptersspanspan-idsupportednetworkadaptersspansupported-network-adapters"></a><span id="Supported_network_adapters"></span><span id="supported_network_adapters"></span><span id="SUPPORTED_NETWORK_ADAPTERS"></span>サポートされているネットワーク アダプター


ホスト コンピューターは、任意のワイヤード (有線) またはワイヤレス ネットワーク アダプターを使用できますが、ターゲット コンピューターが Windows のツールをデバッグでサポートされているネットワーク アダプターを使用する必要があります。 サポートされているネットワーク アダプターの一覧は、次を参照してください。[イーサネット Nic を Windows 8.1 でのネットワーク カーネル デバッグのサポートされている](supported-ethernet-nics-for-network-kernel-debugging-in-windows-8-1.md)と[イーサネット Nic を Windows 10 でのネットワーク カーネル デバッグのサポートされている](supported-ethernet-nics-for-network-kernel-debugging-in-windows-10.md)します。

## <a name="span-idconfiguringthehostandtargetcomputerspanspan-idconfiguringthehostandtargetcomputerspanspan-idconfiguringthehostandtargetcomputerspanconfiguring-the-host-and-target-computer"></a><span id="Configuring_the_host_and_target_computer"></span><span id="configuring_the_host_and_target_computer"></span><span id="CONFIGURING_THE_HOST_AND_TARGET_COMPUTER"></span>ホストおよびターゲット コンピューターの構成


1.  スイッチを使用して、適切なネットワーク ケーブルまたはネットワーク ハブに、ターゲット コンピューターのネットワーク アダプターを接続します。 標準ケーブルまたはワイヤレス接続を使用して切り替えるまたはネットワーク ハブに、ホスト コンピューターのネットワーク アダプターを接続します。
2.  」の説明に従って、ホストとターゲット コンピューターの構成を開始[ドライバーの展開のためにコンピューターをプロビジョニングし、テスト (WDK 8.1)](https://docs.microsoft.com/windows-hardware/drivers/gettingstarted/provision-a-target-computer-wdk-8-1)します。
3.  Visual Studio で、ホスト コンピューターで、コンピューターの構成 ダイアログ ボックスのような場合が選択**コンピューターをプロビジョニングし、デバッガーの設定を選択**します。
4.  **接続の種類**、選択**ネットワーク**します。

    ![スクリーン ショットのデバッガーの例を次のフィールドの値の設定を示す: 接続の種類、ターゲットの名前、およびバス パラメーター](images/setupnetvs.png)

    **ポート番号**では、既定値を受け入れるか、任意の値を入力します。 49152 ~ 65535 から任意の数を選択できます。 選択したポートを排他アクセスのホスト コンピューターで実行されているデバッガーでは開けません。 ホスト コンピューター上で実行される他のアプリケーションで使用されていないポート番号を選択するように注意します。

    **注**  ネットワーク デバッグに使用できるポート番号の範囲は、会社のネットワーク ポリシーによって制限される可能性があります。 制限とは何か、ホスト コンピューターから区別する方法はありません。 会社のポリシーがネットワークのデバッグに使用できるポートの範囲を制限するかどうかを判断するには、ネットワーク管理者に確認します。

    **キー**、自動的に生成された既定値を使用することを強くお勧めします。 ただし、使用する場合は、独自のキーを入力できます。 詳細については、次を参照してください。[独自のキーを作成する](#creating-your-own-key)このトピックで後述します。 **ホスト IP**既定値をそのまま使用します。 これは、ホスト コンピューターの IP アドレスです。

    対象のコンピューターに 1 つだけのネットワーク アダプターがある場合は、おくことができます**Bus パラメーター**空です。 ターゲット コンピューターに 1 つ以上のネットワーク アダプターがある場合は、対象のコンピューター デバイス マネージャーを使用して、PCI バス、デバイス、およびデバッグに使用するアダプターの関数の番号を確認します。 **Bus パラメーター**、入力*b*.*d*.*f*場所*b*、 *d*、および*f*はバス番号、デバイスの数、およびアダプターの関数の数。

5.  構成プロセスには数分かかりますが自動的に、コンピューターを再起動ターゲットまたは 2 回。 プロセスが完了したら、クリックして**完了**します。

**注意**  ドッキング ステーションでは、ターゲット コンピューターがネットワーク デバッグ ドッキング ステーションの一部であるネットワーク アダプターを有効になっている必要がある場合では、ドッキング ステーションからコンピューターは削除しないでください。 ドッキング ステーションから対象のコンピュータを削除する必要がある場合は、カーネルの最初のデバッグを無効にします。 ターゲット コンピューター上のカーネル デバッグを無効にするには、管理者としてコマンド プロンプト ウィンドウを開きし、コマンドを入力します**オフ bcdedit/debug**します。 ターゲット コンピューターを再起動します。

 

**注**  ターゲット コンピューターに HYPER-V の役割をインストールする場合を参照してください。[ネットワーク デバッグのセットアップ、バーチャル マシン ホストの](setting-up-network-debugging-of-a-virtual-machine-host.md)します。

 

## <a name="span-idverifyingdbgsettingsonthetargetcomputerspanspan-idverifyingdbgsettingsonthetargetcomputerspanspan-idverifyingdbgsettingsonthetargetcomputerspanverifying-dbgsettings-on-the-target-computer"></a><span id="Verifying_dbgsettings_on_the_Target_Computer"></span><span id="verifying_dbgsettings_on_the_target_computer"></span><span id="VERIFYING_DBGSETTINGS_ON_THE_TARGET_COMPUTER"></span>ターゲット コンピューター上の dbgsettings を確認しています

> [!IMPORTANT]
> BCDEdit を使用してブート情報を変更する前に、テスト用のコンピューターの BitLocker とセキュア ブートなどの Windows セキュリティ機能を一時的に中断する必要があります。
> テストが完了すると、これらのセキュリティ機能を再度有効にし、適切なセキュリティ機能を無効にするテスト PC を管理します。

対象のコンピューターに管理者としてコマンド プロンプト ウィンドウを開きし、これらのコマンドを入力します。

**bcdedit /dbgsettings**

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

いることを確認*debugtype*は NET と*ポート*はホスト コンピューターで Visual Studio で指定したポート番号です。 確認*キー* Visual Studio では、自動的に生成されたキー (または、指定した)。

入力した場合**Bus パラメーター** Visual Studio であることを確認*busparams*指定したバス パラメーターと一致します。

用に入力した値が表示されない場合**Bus パラメーター**、このコマンドを入力します。

**bcdedit /set "{dbgsettings}" busparams** <em>b</em> **.** <em>d</em> **.** <em>f</em>

場所*b*、 *d*、および*f*バス、デバイス、および関数のデバッグに使用する、選択したターゲット コンピューター上のネットワーク アダプター数。

以下に例を示します。

**bcdedit /set "{dbgsettings}" busparams 0.29.7**

## <a name="span-idstartingthedebuggingsessionspanspan-idstartingthedebuggingsessionspanspan-idstartingthedebuggingsessionspanstarting-the-debugging-session"></a><span id="Starting_the_Debugging_Session"></span><span id="starting_the_debugging_session"></span><span id="STARTING_THE_DEBUGGING_SESSION"></span>デバッグ セッションの開始


1.  Visual Studio で、ホスト コンピューター上で、**ツール**] メニューの [選択**プロセスにアタッチ**します。
2.  **トランスポート**、選択**Windows カーネル モードのデバッガー**します。
3.  **修飾子**、以前に構成されているターゲット コンピューターの名前を選択します。
4.  クリックして**アタッチ**します。

## <a name="span-idallowingthedebuggerthroughthefirewallspanspan-idallowingthedebuggerthroughthefirewallspanspan-idallowingthedebuggerthroughthefirewallspanallowing-the-debugger-through-the-firewall"></a><span id="Allowing_the_debugger_through_the_firewall"></span><span id="allowing_the_debugger_through_the_firewall"></span><span id="ALLOWING_THE_DEBUGGER_THROUGH_THE_FIREWALL"></span>デバッガー、ファイアウォールを通過を許可します。


最初のネットワーク デバッグ接続を確立しようとは、ファイアウォール経由でデバッグ アプリケーション (Microsoft Visual Studio) を許可するように求め可能性があります。 Windows のクライアント バージョンは、プロンプトを表示しますが、Windows のサーバー バージョンはプロンプトを表示できません。 3 つのすべてのネットワークの種類のチェック ボックスをオンして、プロンプトに応答します。 ドメイン、プライベート、および公開します。 プロンプトが表示されない場合、または、プロンプトが使用可能なときに、ボックスを確認しなかった場合は、コントロール パネルを使用して、ファイアウォール経由のアクセスを許可する必要があります。 開いている**コントロール パネルの [&gt;システムとセキュリティ**、] をクリック**アプリを Windows ファイアウォールを通過できます**します。 アプリケーションの一覧で、ファイアウォールを介した Visual Studio を許可するのにチェック ボックスを使用します。 Visual Studio を再起動します。

## <a name="span-idcreating-your-own-keyspanspan-idcreating-your-own-keyspancreating-your-own-key"></a><span id="creating-your-own-key"></span><span id="CREATING-YOUR-OWN-KEY"></span>独自のキーを作成します。


対象のコンピュータを保護するため、ホストとターゲットのコンピューター間で移動するパケットを暗号化する必要があります。 (Visual Studio の構成ウィザードによって提供される)、自動的に生成された暗号化キーを使用することを強くお勧め、対象のコンピュータを構成する場合)。 ただし、独自のキーを作成することができます。 ネットワーク デバッグの使用ベース 36、ピリオドで区切られた 4 つの 64 ビット値として指定されている、256 ビット キー。 64 ビットの各値は 13 文字を使用して指定します。 有効な文字は文字 a ~ z および 0 ~ 9 の数字です。 特殊文字は使用できません。 (ただし、厳密ではありません)、次の一覧が有効な例を示しますキー。

-   1.2.3.4
-   abc.123.def.456
-   dont.use.previous.keys

## <a name="span-idtroubleshootingtipsfordebuggingoveranetworkcablespanspan-idtroubleshootingtipsfordebuggingoveranetworkcablespantroubleshooting-tips-for-debugging-over-a-network-cable"></a><span id="troubleshooting_tips_for_debugging_over_a_network_cable"></span><span id="TROUBLESHOOTING_TIPS_FOR_DEBUGGING_OVER_A_NETWORK_CABLE"></span>ネットワーク ケーブル経由でのデバッグのトラブルシューティングのヒント


### <a name="span-iddebuggingapplicationmustbeallowedthroughfirewallspanspan-iddebuggingapplicationmustbeallowedthroughfirewallspanspan-iddebuggingapplicationmustbeallowedthroughfirewallspandebugging-application-must-be-allowed-through-firewall"></a><span id="Debugging_application_must_be_allowed_through_firewall"></span><span id="debugging_application_must_be_allowed_through_firewall"></span><span id="DEBUGGING_APPLICATION_MUST_BE_ALLOWED_THROUGH_FIREWALL"></span>アプリケーションのデバッグを許可するファイアウォールを通過する必要があります。

デバッガー (WinDbg または KD) ファイアウォール経由のアクセスが必要です。 コントロール パネルを使用して、ファイアウォール経由のアクセスを許可することができます。 開いている**コントロール パネルの [&gt;システムとセキュリティ**、] をクリック**アプリを Windows ファイアウォールを通過できます**します。 アプリケーションの一覧で、ファイアウォールを介した Visual Studio を許可するのにチェック ボックスを使用します。 Visual Studio を再起動します。

### <a name="span-idportnumbermustbeinrangeallowedbynetworkpolicyspanspan-idportnumbermustbeinrangeallowedbynetworkpolicyspanspan-idportnumbermustbeinrangeallowedbynetworkpolicyspanport-number-must-be-in-range-allowed-by-network-policy"></a><span id="Port_number_must_be_in_range_allowed_by_network_policy"></span><span id="port_number_must_be_in_range_allowed_by_network_policy"></span><span id="PORT_NUMBER_MUST_BE_IN_RANGE_ALLOWED_BY_NETWORK_POLICY"></span>ポート番号は、ネットワーク ポリシーで許可されている範囲内で指定する必要があります。

ネットワークのデバッグに使用できるポート番号の範囲は、会社のネットワーク ポリシーによって制限される可能性があります。 会社のポリシーがネットワークのデバッグに使用できるポートの範囲を制限するかどうかを判断するには、ネットワーク管理者に確認してください。

ポート番号を変更する必要がある場合は、次の手順を使用します。

1.  ホスト コンピューター上の Visual Studio の **[ドライバー]** メニューで、 **[Test (テスト)] &gt; [Configure Computers (コンピューターの構成)]** の順に選びます。
2.  テスト用コンピューターの名前を選択し、クリックして**次**します。
3.  選択**コンピューターをプロビジョニングし、デバッガーの設定を選択**します。 **[次へ]** をクリックします。
4.  **ポート番号**、ネットワーク管理者によって許可される範囲内にある数値を入力します。 **[次へ]** をクリックします。
5.  再構成プロセスは、数分を受け取り、対象のコンピュータを自動的に再起動されます。 プロセスが完了したら、クリックして**次**と**完了**します。

### <a name="span-idspecifybusparamsiftargetcomputerhasmultiplenetworkadaptersspanspan-idspecifybusparamsiftargetcomputerhasmultiplenetworkadaptersspanspan-idspecifybusparamsiftargetcomputerhasmultiplenetworkadaptersspanspecify-busparams-if-target-computer-has-multiple-network-adapters"></a><span id="Specify_busparams_if_target_computer_has_multiple_network_adapters"></span><span id="specify_busparams_if_target_computer_has_multiple_network_adapters"></span><span id="SPECIFY_BUSPARAMS_IF_TARGET_COMPUTER_HAS_MULTIPLE_NETWORK_ADAPTERS"></span>ターゲット コンピューターに複数のネットワーク アダプターがある場合は、busparams を指定します。

対象のコンピューターに 1 つ以上のネットワーク アダプターがある場合は、バス、デバイス、および関数をデバッグするために使用するネットワーク アダプター数を指定する必要があります。 バス パラメーターを指定するには、デバイス マネージャーを開き、デバッグに使用するネットワーク アダプターを探します。 ネットワーク アダプターのプロパティ ページを開き、バス番号、デバイスの数、および関数の数をメモしておきます。 管理者特権でコマンド プロンプト ウィンドウで、次のコマンドを入力します。 ここ*b*、 *d*、および*f* bus、デバイス、および関数の数値を 10 進数形式では。

**bcdedit -set "{dbgsettings}" busparams** <em>b</em> **.** <em>d</em> **.** <em>f</em>

ターゲット コンピューターを再起動します。

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック


[Visual Studio でのカーネル モード デバッグの設定](setting-up-kernel-mode-debugging-in-visual-studio.md)

[Windows 10 でのデバッグ ネットワーク カーネルのイーサネット Nic をサポート](supported-ethernet-nics-for-network-kernel-debugging-in-windows-10.md)

[Windows 8.1 でのデバッグ ネットワーク カーネルのイーサネット Nic をサポート](supported-ethernet-nics-for-network-kernel-debugging-in-windows-8-1.md)

[Windows 8 でのデバッグ ネットワーク カーネルのイーサネット Nic をサポート](supported-ethernet-nics-for-network-kernel-debugging-in-windows-8.md)

 

 






