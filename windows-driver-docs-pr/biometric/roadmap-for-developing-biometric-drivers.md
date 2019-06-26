---
title: 生体認証ドライバーの開発のロードマップ
description: 生体認証ドライバーの開発のロードマップ
ms.assetid: 8ed13c75-86d1-4ac0-9f44-05162521b915
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 12cfc824c46c0ed98011cb267a5d00c30eaa16df
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67364682"
---
# <a name="roadmap-for-developing-biometric-drivers"></a>生体認証ドライバーの開発のロードマップ


生体認証ドライバーを作成するには、次の手順を実行します。

-   手順 1:Windows アーキテクチャとドライバーについて説明します。

    Windows オペレーティング システムでのドライバーのしくみの基礎を理解する必要があります。 基礎を知ることに役立つ適切な設計上の決定を行い、開発プロセスを効率化することができます。 ドライバーの基礎の詳細については、次を参照してください。[理解ドライバーとオペレーティング システムの基礎](https://docs.microsoft.com/windows-hardware/drivers/gettingstarted/concepts-and-knowledge-for-all-driver-developers)します。

-   手順 2:Windows で生体認証ドライバーをサポートする方法について説明します。

    Windows 7 およびそれ以降のオペレーティング システム バージョンには、Windows 生体認証ドライバー インターフェイス (WBDI) が含まれます。 WBDI は、Windows 生体認証フレームワーク (WBF) の一部である IOCTL ベースのドライバー インターフェイスです。 WBDI の詳細については、次を参照してください。[生体認証ドライバーの概要](getting-started-with-biometric-drivers.md)します。

-   手順 3:WDK の生体認証ドライバーのサンプルを確認します。

    Windows 7 と以降のオペレーティング システムでは、ドライバーのコード ギャラリーにはという名前のサンプルが含まれています[WudfBioUsbSample](https://github.com/Microsoft/Windows-driver-samples/tree/master/biometrics/driver)します。 このサンプル WBDI ドライバーは UMDF ベースであり、使用、 [USB I/O ターゲット](https://docs.microsoft.com/windows-hardware/drivers/wdf/usb-i-o-targets-in-umdf)します。

    WudfBioUsbSample サンプルの詳細については、次を参照してください。、[サンプルの説明](https://github.com/Microsoft/Windows-driver-samples/tree/master/biometrics)します。

-   手順 4:生体認証ドライバーのドライバー モデルを選択します。

    WBDI ドライバーは UMDF ベースし、USB I/O ターゲットを使用することをお勧めします。 UMDF については、次を参照してください。 [UMDF 概要](https://docs.microsoft.com/previous-versions/ff554928(v=vs.85))します。 USB I/O ターゲットについては、次を参照してください。 [USB I/O ターゲットを処理](https://docs.microsoft.com/windows-hardware/drivers/wdf/usb-i-o-targets-in-umdf)します。

    [WudfBioUsbSample](https://github.com/Microsoft/Windows-driver-samples/tree/master/biometrics/driver) USB I/O ターゲットを使用する UMDF ベース WBDI ドライバーを実装する方法を示します。

    UMDF を使用する場合は、C++ では、生体認証ドライバーを開発することをお勧めします。

-   手順 5:Windows ドライバーのビルド、テスト、およびデバッグ プロセスおよびツールについて説明します。

    ドライバーの構築は、ユーザー モード アプリケーションの構築とは異なります。 については、次を参照してください。[ドライバーをビルド](https://docs.microsoft.com/windows-hardware/drivers/develop/building-a-driver)します。 フレームワーク ベースのドライバーを構築する方法については、次を参照してください。 [Framework ベースのドライバーの読み込みのビルドと](https://docs.microsoft.com/windows-hardware/drivers/wdf/building-and-loading-a-kmdf-driver)します。

-   手順 6:生体認証ドライバーに関する設計上の決定を行います。

    Ioctl を処理する方法については、次を参照してください。[生体認証の IOCTL の呼び出しシーケンスのサポート](supporting-biometric-ioctl-calling-sequence.md)します。 WBDI ドライバーで USB I/O ターゲットを使用する方法については、次を参照してください。 [WBDI ドライバーを使用して WinUSB](using-winusb-in-a-wbdi-driver.md)します。

-   手順 7:開発、ビルド、テスト、およびデバッグには、生体認証ドライバー。

    WBDI ドライバーでは、要求キューを管理する方法の詳細については、次を参照してください。 [WBDI ドライバーの管理キュー](managing-queues-in-a-wbdi-driver.md)します。

    詳細については、Ioctl、構造、および WBDI に関連するエラー コードは、次を参照してください。[生体認証デバイス参照](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)します。

    生体認証ドライバーをテストする方法については、次を参照してください。[生体認証ドライバーのテスト](testing-biometric-drivers.md)します。

    反復的なビルド、テスト、およびデバッグについては、次を参照してください。[概要のビルド、デバッグ、およびテスト プロセス](https://docs.microsoft.com/windows-hardware/drivers)します。 このプロセスにより動作するドライバーを作成することを確認します。

-   手順 8:生体認証ドライバーのドライバー パッケージを作成します。

    詳細については、次を参照してください。[ドライバー パッケージを提供する](https://docs.microsoft.com/windows-hardware/drivers)します。

    生体認証ドライバーをインストールする方法については、次を参照してください。[生体認証ドライバーをインストールする](installing-a-biometric-driver.md)します。

-   手順 9:署名し、生体認証ドライバーを配布します。

    最後の手順では、署名し、ドライバーを配布します。 32 ビットと 64 ビットの両方のプラットフォームで、エンジン アダプターを署名する必要があります。

    ドライバーが Microsoft のハードウェア認定プログラムに対して定義されている品質基準を満たしている場合は、Microsoft Windows 更新プログラムを介して配布できます。 ドライバーを配布する方法の詳細については、次を参照してください。[ドライバーを配布する](https://docs.microsoft.com/windows-hardware/drivers)します。

これらは、基本的な手順です。 追加の手順は、個々 のドライバーのニーズに基づいて、必要でにあります。

 

 





