---
Description: The Windows Hardware Lab Kit (HLK) tests can be used for additional testing of Systems, USB host controllers, hubs, and devices.
title: USB の Windows のハードウェア ラボ キット (HLK) のテスト
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f4ece82c5267b85db8cd658dddbe6191fb43a479
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56532579"
---
# <a name="windows-hardware-lab-kit-hlk-tests-for-usb"></a>USB の Windows のハードウェア ラボ キット (HLK) のテスト


Windows ハードウェア ラボ キット (HLK) テストは、システム、USB ホスト コント ローラー、ハブ、およびデバイスの追加テストに使用できます。 これらのテストは、基本的なデバイス機能、信頼性、および Windows との互換性について説明します。

## <a name="prerequisites"></a>前提条件


前に、ロゴ テストの実行開始は、次の要件を満たしていることを確認してください。

-   これらのテストを実行する少なくとも 2 台のコンピューターが必要: テスト サーバーとテスト クライアント。
-   テスト クライアントでは、Windows の最新バージョンをいる必要があります。
-   テスト クライアントでは、EHCI と xHCI コント ローラー、統合や、アドインのカードをいる必要があります。 コント ローラーには、ユーザーがアクセスできるルート ポート (統合されたハブ) を公開する必要があります。
-   テスト サーバーに Windows HLK をダウンロード[Windows ハードウェア ラボ キット ダウンロード](https://go.microsoft.com/fwlink/p/?linkid=285647)します。

    インストールして Windows HLK の使用方法の詳細については、次を参照してください。 [Windows HLK Getting Started](https://docs.microsoft.com/windows-hardware/test/hlk/getstarted/windows-hlk-getting-started)します。

## <a name="hardware-requirements-for-running-usb-tests-in-the-hlk"></a>HLK で USB テストを実行するためのハードウェア要件


HLK テストを実行するには、次の必要があります。

-   ホスト コント ローラー (統合またはとしてアドイン カード)、ハブ、または認定を受けるデバイス。

    テスト クライアントでデバイス マネージャーを開きを使用する、USB コント ローラーがユーザーからアクセス可能なルート ポート (統合されたハブ) を公開することを確認します。

    ![ルートの usb ポート](images/roothubports.png)

-   外部 SuperSpeed ハブの USB の場合に非準拠システムの互換性を評価します。 これらのハブで HLK テストがテストされています。
    -   [Texas Instruments SuperSpeed (USB 3.0) ハブの参照設計ボード (TUSB8040EVM)](https://go.microsoft.com/fwlink/p/?linkid=248509)します。
    -   SuperMUTT パックします。 参照してください[MUTT デバイス](microsoft-usb-test-tool--mutt--devices.md)します。
-   [MUTT デバイス](microsoft-usb-test-tool--mutt--devices.md)としてテスト ハブおよびコント ローラーのテスト用のデバイス。
-   USB の場合はケーブルおよびシグナル インテグリティの問題を回避するためにコネクタを認定します。 参照してください[USB-製品の場合は一覧](https://go.microsoft.com/fwlink/p/?linkid=617502)します。

ここでの要件の完全なセットが与えられます。

-   [USB バス コント ローラー テスト前提条件](https://go.microsoft.com/fwlink/p/?linkid=617477)
-   [USB Hub.Connectivity Testing の前提条件](https://go.microsoft.com/fwlink/p/?linkid=617499)

## <a name="hlk-test-selection-for-usb"></a>USB の HLK テストの選択


システム、ホスト コント ローラー、ハブ、またはデバイスに適用される USB テストは HLK Studio で自動的に選択します。

手順 1. ~ 5. を実行した後[Windows HLK Getting Started]( https://docs.microsoft.com/windows-hardware/test/hlk/getstarted/windows-hlk-getting-started)、ことを確認します。

-   手順 5 で、適切なデバイスを選択、**選択**HLK Studio のタブ。
-   手順 6 では、デバイスに適用されるすべてのテストに表示されます、**テスト**HLK studio タブ。 これらのテストを実行するには、左側のチェック ボックス テストを選択し、 をクリックする必要があります**選択項目の実行**します。 このドキュメントの次のセクションでは、USB をテストするためのテストが一覧表示します。

テストのスケジュール設定方法の詳細についてを参照してください、手順 2. ~ 6. [Windows HLK Getting Started]( https://docs.microsoft.com/windows-hardware/test/hlk/getstarted/windows-hlk-getting-started)します。

## <a name="recommended-windows-hlk-tests"></a>Windows HLK テストをお勧めします。

だけでなくすべての HLK Studio で自動的に選択されている USB テストには、MUTT または SuperMUTT で同様のテストは、システム、コント ローラーまたはテスト対象のハブに接続されている基礎の実行をお勧めします。 システムのサブミッション、これらは、これらは、デバイスの基本 (DevFund) テスト コント ローラー、ハブ、またはデバイスの送信、システムの基礎 (SysFund) テストです。

-   [システムの基礎 (SysFund)](https://docs.microsoft.com/windows-hardware/test/hlk/testref/system-fundamentals-tests)
-   [デバイスの基本 (DevFund)](https://docs.microsoft.com/windows-hardware/test/hlk/testref/device-devfund-tests)

## <a name="related-topics"></a>関連トピック
[Windows での USB ハードウェア、ドライバー、およびアプリのテスト](usb-driver-testing-guide.md)  



