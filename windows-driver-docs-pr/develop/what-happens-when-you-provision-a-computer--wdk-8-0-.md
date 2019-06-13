---
ms.assetid: A8888EF1-5A6F-4B08-8743-27EEECD4FF72
title: コンピューターのプロビジョニングで実行される処理 (WDK 8.0)
description: ここでは、Version 8.0 の Windows Driver Kit (WDK) を使ったターゲット コンピューターのプロビジョニングで実行される処理について説明します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5c4effdc9c3609072ea8f82aab32987889bd2b5a
ms.sourcegitcommit: dabd74b55ce26f2e1c99c440cea2da9ea7d8b62c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/13/2019
ms.locfileid: "63344096"
---
# <a name="what-happens-when-you-provision-a-computer-wdk-80"></a>コンピューターのプロビジョニングで実行される処理 (WDK 8.0)

ドライバーの展開とドライバーのテストに必要な構成とセットアップは、Microsoft Visual Studio を使って行うことができます。これを "*ターゲット コンピューターのプロビジョニング*" または "*テスト コンピューターのプロビジョニング*" といいます。 Windows Driver Kit (WDK) 8 でのプロビジョニングについては、「[ドライバーの展開およびテストのためのコンピューターのプロビジョニング (WDK 8)](https://msdn.microsoft.com/Library/Windows/Hardware/Hh698272)」をご覧ください。 ここでは、Version 8.0 の Windows Driver Kit (WDK) を使ったターゲット コンピューターのプロビジョニングで実行される処理について説明します。

**注**  WDK 8 は、WDK の最新バージョンではありません。 WDK の最新バージョンを入手し、[ここで説明するプロビジョニングの手順](https://msdn.microsoft.com/Library/Windows/Hardware/Hh698272)に従ってターゲット コンピューターをプロビジョニングすることをお勧めします。

 

## <a name="span-idwhenyouprovisionacomputerwdk80spanspan-idwhenyouprovisionacomputerwdk80spanwhen-you-provision-a-computer-wdk-80"></a><span id="when_you_provision_a_computer_wdk_8_0"></span><span id="WHEN_YOU_PROVISION_A_COMPUTER_WDK_8_0"></span>コンピューターをプロビジョニングする場合 (WDK 8.0)


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

1.  ホスト コンピューター上の Visual Studio の **[ドライバー]** メニューで、 **[Test (テスト)] &gt; [Configure Computers (コンピューターの構成)]** の順に選びます。
2.  ターゲット コンピューターの名前を選び、 **[Delete computer (コンピューターの削除)]** をクリックします。
3.  **[Remove provisioning and delete computer]** (プロビジョニングを削除してコンピューターを削除) を選びます。 **[次へ]** をクリックします。
4.  削除処理が完了したら、 **[Finish]** (完了) をクリックします。

## <a name="span-idwhenyouremoveprovisioningwdk80spanspan-idwhenyouremoveprovisioningwdk80spanwhen-you-remove-provisioning-wdk-80"></a><span id="when_you_remove_provisioning__wdk_8.0_"></span><span id="WHEN_YOU_REMOVE_PROVISIONING__WDK_8.0_"></span>プロビジョニングを削除する場合 (WDK 8.0)


ターゲット コンピューターからプロビジョニングを削除すると、以下のものが削除されます。

-   Visual C++ 再頒布可能パッケージ
-   Test Automation Framework
-   デバッガー
-   Windows Driver Testing Framework
-   %SystemDrive%\\DriverTest フォルダーとその内容
-   WDKRemoteUser アカウント

プロビジョニングを削除しても、以下のものは変更されません。

-   AutoReboot の設定
-   カーネル メモリ クラッシュ ダンプの設定
-   スクリーン セーバーの設定
-   ワークステーション ロック ポリシー
-   ForceGuest の設定
-   電源ポリシー
-   RTC スリープ解除タイマーの設定
-   カーネル デバッグの設定
-   テスト署名の設定

 

 





