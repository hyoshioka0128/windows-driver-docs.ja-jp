---
title: WDK を使った ARM64 ドライバーのビルド
description: このトピックでは、Windows Driver Kit (WDK) で ARM64 ドライバーをビルドする方法について説明します。
ms.date: 01/18/2018
ms.localizationpriority: medium
ms.openlocfilehash: 7ed6c60f9bba51e679797cc625ec4770f2150ede
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56518599"
---
# <a name="building-arm64-drivers-with-the-wdk"></a>WDK を使った ARM64 ドライバーのビルド

バージョン 1709 から、ARM64 プロセッサ搭載のコンピューターでも Windows 10 Desktop (Pro エディションおよび S エディション) を実行できるようになりました。  ただし、ARM 版 Windows 10 では、カーネル モード ドライバーの x86 エミュレーションがサポートされないため、以下の手順を使用して、カーネル モード ドライバーを ARM64 用に再コンパイルする必要があります。

## <a name="setup"></a>セットアップ

1. [Visual Studio 2017 Preview](https://www.visualstudio.com/vs/preview/) をダウンロードします。  15.4.0 Preview 2.0 以上のバージョンが必要です。
2. Windows のスタート メニューで、「**Visual Studio インストーラー**」と入力します。  次に、**[ワークロード]** タブの **[C++ によるデスクトップ開発]** を選択します。  
![[ワークロード] タイルの [Windows] オプションから [C++ によるデスクトップ開発] を選択する](images/VS-workloads.png)

2. **[個別のコンポーネント]** タブで、次のいずれかのオプションを選択します。
    *  **ARM 用 Visual C++ コンパイラとライブラリ**
    *  **ARM64 用 Visual C++ コンパイラとライブラリ**  
![インストールする ARM 用コンポーネントを選択する](images/VS-individual-components.png)

3.  Visual Studio をインストールし、再起動します。
4.  [Windows SDK](https://developer.microsoft.com/windows/downloads/windows-10-sdk) をダウンロードします。  SDK バージョン 16299 (Windows 10 バージョン 1709) 以降があることを確認します。
5.  [WDK](../download-the-wdk.md) をダウンロードします。  WDK Version 16299 以降が必要です。

## <a name="building-an-arm64-driver-with-the-wdk"></a>WDK を使った ARM64 ドライバーのビルド

1.  Visual Studio で、ドライバー ソリューションを開きます。  自身のソリューションを使用することも、[Windows-driver-samples](https://github.com/Microsoft/Windows-driver-samples) リポジトリにあるソリューションを使用することもできます。
2.  ソリューションのプラットフォームをクリックし、**[構成マネージャー]** を選択します。  
![上部のツール バーで 2 番目のドロップダウンから構成マネージャーを選択する](images/VS-config-mgr.png)
  
3.  **[アクティブ ソリューション プラットフォーム]** で、**[新規作成]** を選択します。  
![[アクティブ ソリューション プラットフォーム] ドロップダウンから [新規作成] を選択する](images/VS-active-solution-platform.png)

4.  **[新しいプラットフォームを入力または選択してください]** で、**[ARM64]** を選択します。  設定のコピー元として **[Win32]** を選択します。  **[OK]**、**[閉じる]** の順にクリックします。  
![ツール バー レベルのドロップダウンからビルド対象として ARM64 を選択する](images/VS-build-ARM64.png)

5.  対象プラットフォームとして **[ARM64]** を選択し、リビルドを行います。

## <a name="see-also"></a>参照

* [ARM64 のデバッグ](../debugger/debugging-arm64.md)
* [ARM 版 Windows 10](https://docs.microsoft.com/windows/uwp/porting/apps-on-arm)
* [HLK ARM64 ファースト ステップ ガイド](https://docs.microsoft.com/windows-hardware/test/hlk/getstarted/hlk-arm64-getting-started-guide)
