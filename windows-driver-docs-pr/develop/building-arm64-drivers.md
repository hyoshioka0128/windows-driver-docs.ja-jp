---
title: WDK を使った ARM64 ドライバーのビルド
description: このトピックでは、Windows Driver Kit (WDK) で ARM64 ドライバーをビルドする方法について説明します。
ms.date: 01/18/2018
ms.localizationpriority: medium
ms.openlocfilehash: ac4f277ee1a2d0b9a08c004173f68385b1bacdae
ms.sourcegitcommit: 444e055daa9b28e9fd9dc92dd0a3f1e62e215b31
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/10/2020
ms.locfileid: "84666166"
---
# <a name="building-arm64-drivers-with-the-wdk"></a>WDK を使った ARM64 ドライバーのビルド

Windows 10 は、ARM64 プロセッサを搭載したコンピューターで実行できます。  ただし、ARM 版 Windows 10 では、x86 カーネル モード ドライバーのエミュレーションがサポートされないため、以下の手順を使用して、カーネル モード ドライバーを ARM64 用に再コンパイルする必要があります。

## <a name="setup"></a>セットアップ

1. [Visual Studio 2017 または 2019](https://visualstudio.microsoft.com/downloads/) をダウンロードする。  バージョン 15.9 以上が必要です。
2. Windows のスタート メニューで、「**Visual Studio インストーラー**」と入力します。  次に、 **[ワークロード]** タブの **[C++ によるデスクトップ開発]** を選択します。  
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
2.  ソリューションのプラットフォームをクリックし、 **[構成マネージャー]** を選択します。  
![上部のツール バーで 2 番目のドロップダウンから構成マネージャーを選択する](images/VS-config-mgr.png)
  
3.  **[アクティブ ソリューション プラットフォーム]** で、 **[新規作成]** を選択します。  
![[アクティブ ソリューション プラットフォーム] ドロップダウンから [新規作成] を選択する](images/VS-active-solution-platform.png)

4.  **[新しいプラットフォームを入力または選択してください]** で、 **[ARM64]** を選択します。  設定のコピー元として **[Win32]** を選択します。  **[OK]** 、 **[閉じる]** の順にクリックします。  
![ツール バー レベルのドロップダウンからビルド対象として ARM64 を選択する](images/VS-build-ARM64.png)

5.  対象プラットフォームとして **[ARM64]** を選択し、リビルドを行います。

## <a name="see-also"></a>参照

* [ARM64 のデバッグ](../debugger/debugging-arm64.md)
* [ARM 版 Windows 10](https://docs.microsoft.com/windows/uwp/porting/apps-on-arm)
* [HLK ARM64 ファースト ステップ ガイド](https://docs.microsoft.com/windows-hardware/test/hlk/getstarted/hlk-arm64-getting-started-guide)
