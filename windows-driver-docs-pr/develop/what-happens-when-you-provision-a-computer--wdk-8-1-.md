---
ms.assetid: 92F58B13-3447-4715-A6D2-69E63FE04A77
title: コンピューターのプロビジョニングで実行される処理 (WDK 8.1)
description: ここでは、Version 8.1 の Windows Driver Kit (WDK) を使ったターゲット コンピューターのプロビジョニングで実行される処理について説明します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b7d27748364c2e1afdb7eea3c18e472e2c38dd85
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56518800"
---
# <a name="what-happens-when-you-provision-a-computer-wdk-81"></a>コンピューターのプロビジョニングで実行される処理 (WDK 8.1)

ドライバーの展開とドライバーのテストに必要な構成とセットアップは、Microsoft Visual Studio を使って行うことができます。これを "*ターゲット コンピューターのプロビジョニング*" または "*テスト コンピューターのプロビジョニング*" といいます。 プロビジョニングについては、「[ドライバーの展開およびテストのためのコンピューターのプロビジョニング (WDK 8.1)](https://msdn.microsoft.com/Library/Windows/Hardware/Dn745909)」をご覧ください。 ここでは、Version 8.1 の Windows Driver Kit (WDK) を使ったターゲット コンピューターのプロビジョニングで実行される処理について説明します。

## <a name="span-idwhenyouprovisionacomputerwdk80spanspan-idwhenyouprovisionacomputerwdk80spanwhen-you-provision-a-computer-wdk-81"></a><span id="when_you_provision_a_computer_wdk_8_0"></span><span id="WHEN_YOU_PROVISION_A_COMPUTER_WDK_8_0"></span>コンピューターをプロビジョニングする場合 (WDK 8.1)


コンピューターのプロビジョニングでは、以下のタスクが実行されます。

-   インストール ファイルを %SystemDrive%\\DriverTest にコピーする
-   WDKRemoteUser という名前のユーザーを作成し、そのユーザーに切り替える
-   まだインストールされていない場合は、.NET 4.0 をインストールする
-   Microsoft Visual C++ 再頒布可能パッケージ
-   [TAEF (Test Authoring and Execution Framework)](https://msdn.microsoft.com/Library/Windows/Hardware/Hh439725) (WDK クライアント) をインストールする
-   デバッガーをインストールする
-   [WDTF (Windows Device Testing Framework)](https://msdn.microsoft.com/Library/Windows/Hardware/Ff539547) をインストールする
-   AutoReboot をオフにする
-   カーネル メモリ クラッシュ ダンプを有効にする
-   スクリーン セーバーを無効にする
-   ワークステーション ロック ポリシーを無効にする
-   ForceGuest を無効にする
-   電源ポリシーを高電力構成に設定し、システムがアイドル時にスタンバイ モードや休止状態モードに入らないようにする
-   RTC スリープ解除タイマーを有効にする
-   カーネル デバッグを有効にして構成する
-   ドライバーのテスト署名を有効にする
-   必要に応じてターゲット コンピューターを再起動する
-   システムの復元ポイントを作る

## <a name="span-idremovingprovisioningfromthetargetcomputerspanspan-idremovingprovisioningfromthetargetcomputerspanspan-idremovingprovisioningfromthetargetcomputerspanremoving-provisioning-from-the-target-computer"></a><span id="Removing_provisioning_from_the_target_computer"></span><span id="removing_provisioning_from_the_target_computer"></span><span id="REMOVING_PROVISIONING_FROM_THE_TARGET_COMPUTER"></span>ターゲット コンピューターからのプロビジョニングの削除


ターゲット コンピューターをプロビジョニングすると、プロビジョニングを完全に削除することはできなくなります。 ただし、ホスト コンピューター上の Visual Studio を使って、ターゲット コンピューターからほとんどのプロビジョニングを削除できます。 手順は次のとおりです。

1.  ホスト コンピューター上の Visual Studio の **[ドライバー]** メニューで、**[Test (テスト)] &gt; [Configure Computers (コンピューターの構成)]** の順に選びます。
2.  ターゲット コンピューターの名前を選び、**[Delete computer (コンピューターの削除)]** をクリックします。
3.  **[Remove provisioning and delete computer]** (プロビジョニングを削除してコンピューターを削除) を選びます。 **[次へ]** をクリックします。
4.  削除処理が完了したら、**[Finish]** (完了) をクリックします。
5.  ターゲット コンピューターから WDK Test Target Setup をアンストールします。

## <a name="span-idwhenyouremoveprovisioningwdk81spanspan-idwhenyouremoveprovisioningwdk81spanwhen-you-remove-provisioning-wdk-81"></a><span id="when_you_remove_provisioning__wdk_8.1_"></span><span id="WHEN_YOU_REMOVE_PROVISIONING__WDK_8.1_"></span>プロビジョニングを削除する場合 (WDK 8.1)


ターゲット コンピューターからプロビジョニングを削除すると、以下のものが削除されます。

-   Test Automation Framework
-   デバッガー
-   Windows Driver Testing Framework
-   %SystemDrive%\\DriverTest フォルダーとその内容
-   WDKRemoteUser アカウント
-   ワークステーション ロック ポリシー

プロビジョニングを削除しても、以下のものは変更されません。

-   Visual C++ 再頒布可能パッケージ
-   AutoReboot の設定
-   カーネル メモリ クラッシュ ダンプの設定
-   スクリーン セーバーの設定
-   ForceGuest の設定
-   電源ポリシー
-   RTC スリープ解除タイマーの設定
-   カーネル デバッグの設定
-   テスト署名の設定

 

 





