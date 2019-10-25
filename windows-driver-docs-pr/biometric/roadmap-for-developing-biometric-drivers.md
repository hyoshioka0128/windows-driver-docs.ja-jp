---
title: 生体認証ドライバーの開発のロードマップ
description: 生体認証ドライバーの開発のロードマップ
ms.assetid: 8ed13c75-86d1-4ac0-9f44-05162521b915
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: cc34f68c109a9ae652e4a46af81c2bca0bfd483d
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72833937"
---
# <a name="roadmap-for-developing-biometric-drivers"></a>生体認証ドライバーの開発のロードマップ


生体認証ドライバーを作成するには、次の手順を実行します。

-   手順 1: Windows のアーキテクチャとドライバーについて説明します。

    Windows オペレーティングシステムでのドライバーの動作の基礎を理解しておく必要があります。 基本を理解することで、適切な設計上の決定を行い、開発プロセスを効率化することができます。 ドライバーの基礎の詳細については、「[ドライバーとオペレーティングシステムの基本](https://docs.microsoft.com/windows-hardware/drivers/gettingstarted/concepts-and-knowledge-for-all-driver-developers)について」を参照してください。

-   手順 2: Windows で生体認証ドライバーがサポートされるしくみについて説明します。

    Windows 7 以降のバージョンのオペレーティングシステムには、Windows 生体認証ドライバーインターフェイス (WBDI) が含まれています。 WBDI は、Windows 生体認証フレームワーク (WBF) の一部である IOCTL ベースのドライバーインターフェイスです。 WBDI の詳細については、[生体認証ドライバーを使用したはじめに](getting-started-with-biometric-drivers.md)に関するページを参照してください。

-   手順 3: WDK で生体認証ドライバーのサンプルを確認します。

    Windows 7 以降のオペレーティングシステムの場合、ドライバーコードギャラリーには[WudfBioUsbSample](https://github.com/Microsoft/Windows-driver-samples/tree/master/biometrics/driver)という名前のサンプルが含まれています。 このサンプル WBDI ドライバーは、UMDF ベースであり、 [USB I/o ターゲット](https://docs.microsoft.com/windows-hardware/drivers/wdf/usb-i-o-targets-in-umdf)を使用します。

    WudfBioUsbSample サンプルの詳細については、[サンプルの説明](https://github.com/Microsoft/Windows-driver-samples/tree/master/biometrics)を参照してください。

-   手順 4: 生体認証ドライバーのドライバーモデルを選択します。

    WBDI ドライバーは UMDF ベースであり、USB i/o ターゲットを使用することをお勧めします。 UMDF の詳細については、「 [umdf の概要](https://docs.microsoft.com/previous-versions/ff554928(v=vs.85))」を参照してください。 USB i/o ターゲットの詳細については、「 [usb I/o ターゲットの処理](https://docs.microsoft.com/windows-hardware/drivers/wdf/usb-i-o-targets-in-umdf)」を参照してください。

    [WudfBioUsbSample](https://github.com/Microsoft/Windows-driver-samples/tree/master/biometrics/driver)は、USB i/o ターゲットを使用する UMDF ベースの WBDI ドライバーを実装する方法を示しています。

    UMDF を使用する場合、でC++生体認証ドライバーを開発することをお勧めします。

-   手順 5: Windows ドライバーのビルド、テスト、およびデバッグのプロセスとツールについて説明します。

    ドライバーのビルドは、ユーザーモードアプリケーションの作成とは異なります。 詳細について[は、「ドライバーのビルド](https://docs.microsoft.com/windows-hardware/drivers/develop/building-a-driver)」を参照してください。 フレームワークベースのドライバーを構築する方法の詳細については、「[フレームワークベースのドライバーのビルドと読み込み](https://docs.microsoft.com/windows-hardware/drivers/wdf/building-and-loading-a-kmdf-driver)」を参照してください。

-   手順 6: 生体認証ドライバーについて設計上の決定を行います。

    Ioctl の処理方法の詳細については、「[生体認証 Ioctl 呼び出しシーケンスのサポート](supporting-biometric-ioctl-calling-sequence.md)」を参照してください。 WBDI ドライバーで USB i/o ターゲットを使用する方法の詳細については、「 [WBDI ドライバーでの WinUSB の使用](using-winusb-in-a-wbdi-driver.md)」を参照してください。

-   手順 7: 生体認証ドライバーの開発、ビルド、テスト、およびデバッグを行います。

    WBDI ドライバーで要求キューを管理する方法の詳細については、「 [WBDI ドライバーでのキューの管理](managing-queues-in-a-wbdi-driver.md)」を参照してください。

    WBDI に関連する Ioctl、構造体、およびエラーコードの詳細については、「[生体認証デバイスリファレンス](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)」を参照してください。

    生体認証ドライバーのテスト方法については、「[生体認証ドライバーのテスト](testing-biometric-drivers.md)」を参照してください。

    反復的なビルド、テスト、およびデバッグの詳細については、「[ビルド、デバッグ、およびテストのプロセスの概要](https://docs.microsoft.com/windows-hardware/drivers)」を参照してください。 このプロセスを使用すると、動作するドライバーを確実に作成できます。

-   手順 8: 生体認証ドライバーのドライバーパッケージを作成します。

    詳細については、「[ドライバーパッケージの提供](https://docs.microsoft.com/windows-hardware/drivers)」を参照してください。

    生体認証ドライバーのインストール方法の詳細については、「[生体認証ドライバーのインストール](installing-a-biometric-driver.md)」を参照してください。

-   手順 9: 生体認証ドライバーに署名して配布する。

    最後の手順は、ドライバーに署名して配布することです。 32ビットプラットフォームと64ビットプラットフォームの両方で、エンジンアダプターに署名する必要があります。

    ドライバーが Microsoft ハードウェア認定プログラムに対して定義されている品質基準を満たしている場合は、Microsoft Windows Update プログラムを通じて配布できます。 ドライバーを配布する方法の詳細については、「[ドライバーの配布](https://docs.microsoft.com/windows-hardware/drivers)」を参照してください。

基本的な手順は次のとおりです。 個々のドライバーのニーズに基づいて、追加の手順が必要になる場合があります。

 

 





