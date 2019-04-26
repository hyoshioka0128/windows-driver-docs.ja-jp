---
title: 存在するかカスタム WDTF 単純な I/O 操作プラグインの必要性をテストします。
description: Visual Studio を使用してテストするためのリモート コンピューターを構成した場合は、WDTF 単純な I/O プラグインがあるすべてのデバイスを表示するユーティリティ テストを実行することができます。
ms.assetid: 7AD2F8DD-8428-4C30-A3B0-B6678986DCCD
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 478f985390705c6744c7bd2c1cb747a2f81cbee1
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63355443"
---
# <a name="how-to-determine-if-a-custom-wdtf-simple-io-action-plug-in-is-required-for-your-device"></a>カスタム WDTF 単純な I/O 操作のプラグインが、デバイスに必要なかどうかを判断する方法


Visual Studio を使用してテストするためのリモート コンピューターを構成した場合は、WDTF 単純な I/O プラグインがあるすべてのデバイスを表示するユーティリティ テストを実行することができます。テストは、WDTF 単純な I/O のサポートがないテスト コンピューターにもデバイスの一覧を返します。 デバイスがサポートされていない場合は、Visual Studio を使用して 1 つを作成、 **WDTF 単純な I/O 操作プラグイン**テンプレートを参照してください[WDTF 単純な I/O 操作のプラグインを使用してデバイスの I/O をカスタマイズする方法](to-customize-i-o-for-your-device-using-the-wdtf-simple-i-o-action-plug-in.md)します。

### <a name="prerequisites"></a>前提条件

-   テスト対象のデバイスは、テスト コンピューターにインストールされます。
-   テストは、ドライバー パッケージは署名され、テスト コンピューターにインストールされています。 ドライバーが正しくインストールされていることを確認するには、ドライバー パッケージをテストする方法を参照してください。
-   展開用に構成され、プロビジョニングされたテスト コンピューター。 参照してください[Visual Studio を使用して実行時のドライバーをテストします。](https://msdn.microsoft.com/windows-drivers/develop/testing_a_driver_at_runtime)

<a name="instructions"></a>手順
------------

### <a name="test-your-device-to-see-if-you-need-to-customize-the-wdtf-simple-io-action-plug-in"></a>デバイスをテストして WDTF 単純な I/O 操作のプラグインをカスタマイズする必要があるかどうかを参照してください。

WDK ユーティリティ テストを提供する、デバイスの種類のプラグイン WDTF 単純な I/O があるかどうかを行うことができます。

1.  開く、**ドライバー テスト グループ エクスプ ローラー**します。 ドライバーのメニューから**ドライバー&gt;テスト&gt;ドライバー テスト グループ エクスプ ローラー**します。
2.  新しいテスト グループを作成します。
3.  ドライバー テスト グループ ウィンドウで、次のようにクリックします。**追加/削除テスト**します。
4.  **の追加と削除テスト**ダイアログ ボックスで、**すべてのテスト\\ユーティリティ**から、**デバイス テスト カテゴリ**、一覧表示し、テストを追加**単純な I/O の WDTF プラグインのデバイスを表示**します。**[OK]** をクリックします。 テスト グループを保存します。
5.  ユーティリティのテストを含むテスト グループを実行**WDTF 単純な I/O プラグインのデバイスを表示**します。
6.  テストの TestTextlog を開き、デバイスがプラグイン WDTF 単純な I/O があるデバイスとして報告されることを確認します。 デバイスが表示されている場合は、単純な I/O デバイスのプラグインを作成する必要はありません。 デバイスの基本的なテストと、適切なを実行するプラグイン、デバイスの種類が自動的に選択します。 指定されたテストについては、次を参照してください。[を選択し、デバイスの基本的なテストを構成する方法](https://msdn.microsoft.com/windows-drivers/develop/how_to_select_and_configure_the_device_fundamental_tests)します。

    プラグイン、デバイスの I/O がない場合は、指定された単純な I/O 操作のプラグインの WDTF テンプレートをカスタマイズする 1 つを作成する必要があります。

**テストのテキスト ログの例**

``` syntax
WDTF_TEST                 : INFO  : 
WDTF_TEST                 : INFO  :  Devices that we do NOT have a simple I/O Plug-in for
WDTF_TEST                 : INFO  : 
WDTF_TEST                 : INFO  :      Intel(R) ICH10 Family USB Universal Host Controller - 3A68 PCI\VEN_8086&DEV_3A68&SUBSYS_3035103C&REV_02\3&33FD14CA&0&D1 
WDTF_TEST                 : INFO  :      Generic Non-PnP Monitor DISPLAY\DEFAULT_MONITOR\5&1934D7DD&0&UID259 

....

WDTF_TEST                 : INFO  :  Devices that we have a simple I/O Plug-in for
WDTF_TEST                 : INFO  : 
WDTF_TEST                 : INFO  :      Generic volume (I:) STORAGE\VOLUME\{A6EA1A2E-87E6-11E1-9834-806E6F6E6963}#0000006F7FD00000
WDTF_TEST                 : INFO  :      Generic volume (G:) STORAGE\VOLUME\_??_USBSTOR#DISK&VEN_GENERIC&PROD_STORAGE_DEVICE&REV_9744#000000000010&2#{53F56307-B6BF-11D0-94F2-00A0C91EFB8B} 

..... 

```

## <a name="related-topics"></a>関連トピック
[WDTF シンプル I/O アクション プラグインを使ってデバイスの I/O をカスタマイズする方法](to-customize-i-o-for-your-device-using-the-wdtf-simple-i-o-action-plug-in.md)  
[提供されている WDTF シンプル I/O プラグイン](provided-wdtf-simpleio-plug-ins.md)  



