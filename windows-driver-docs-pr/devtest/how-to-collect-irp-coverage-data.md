---
title: IRP カバレッジ データを収集する方法
description: IRP カバレッジ データを収集する方法
ms.assetid: f65422fe-f524-41c1-a532-a2c615d65f72
keywords:
- ドライバー カバレッジ Toolkit WDK は、データの収集
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 740fdf45211eec9df18b69db9aa876817604dcc1
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67358273"
---
# <a name="how-to-collect-irp-coverage-data"></a>IRP カバレッジ データを収集する方法


**注**  ドライバーのカバレッジ Toolkit は Windows 10 で不要になったと、インストーラーが WDK に含まれていません。 ここで説明されている Windows 10 でタスクを実行する代わりに使用[Driver Verifier](driver-verifier.md)と[IRP のログ記録](irp-logging.md)します。

 

次の手順は、ドライバーのカバレッジ ツールを使用して I/O 要求パケット (Irp) のカバレッジ データを収集する方法を説明し、[ドライバー カバレッジ フィルター ドライバー](driver-coverage-filter-driver.md)します。 ツールはの一部、[デバイス基礎テスト](device-fundamentals-tests.md)カバレッジのカテゴリの下。

WDK と Visual Studio のテスト環境の設定の詳細については、次を参照してください。 [Visual Studio を使用して実行時にドライバーをテストする方法](https://docs.microsoft.com/windows-hardware/drivers)します。 選択して、テストとツールのパラメーターの構成については、次を参照してください。[を選択して、デバイスの基本テストを構成する方法](https://docs.microsoft.com/windows-hardware/drivers)と[デバイス基礎テスト パラメーター](https://docs.microsoft.com/windows-hardware/drivers)します。

1.  インストール、[ドライバー カバレッジ フィルター ドライバー](driver-coverage-filter-driver.md)テスト コンピューター。

    -   フィルター ドライバーをインストールして、指定されたデバイス上の IRP のカバレッジを有効にする、実行、 **IRP を有効にするカバレッジ データ コレクション**ツール。 ツールはの一部、[デバイス基礎テスト](device-fundamentals-tests.md)、カバレッジ。

    -   フィルター ドライバーをインストールして、指定されたデバイス上の IRP のカバレッジを有効にするを使用して、 *DQ*を監視するデバイスを指定するパラメーター。

    -   デバイスを使用、上位フィルター ドライバーまたは低いフィルター ドライバーとドライバー カバレッジ フィルター ドライバーをインストールする、 *UpperFilter*パラメーター。 カバレッジ フィルター ドライバーに関する情報と、ドライバーをインストールする方法についてのガイドラインでは、次を参照してください[ドライバー カバレッジ フィルター ドライバー。](driver-coverage-filter-driver.md)

    については、ツールを実行して、次を参照してください。 [Visual Studio を使用して実行時にドライバーをテストする方法](https://docs.microsoft.com/windows-hardware/drivers)と[を選択して、デバイスの基本テストを構成する方法](https://docs.microsoft.com/windows-hardware/drivers)します。

2.  現在の IRP カバレッジ データを消去します。

    1 つまたは複数のデバイスで、コード カバレッジのテストを開始する前に、まずによって既に収集された IRP カバレッジ データをクリア、[ドライバー カバレッジ フィルター ドライバー](driver-coverage-filter-driver.md)します。 これを行うには、実行、 **IRP カバレッジ データのクリア**テスト コンピューター上のツール。

3.  テスト コンピューターを再起動します。

    インストールした後、[ドライバー カバレッジ フィルター ドライバー](driver-coverage-filter-driver.md) 1 つまたは複数のデバイス ドライバの対応のフィルター ドライバーの読み込みし、IRP のカバレッジを開始するには、テスト コンピューターを再起動します。

4.  確認、[ドライバー カバレッジ フィルター ドライバー](driver-coverage-filter-driver.md)インストールします。

    テスト コンピューターが再起動したら、フィルター ドライバーがインストールされているし、IRP のカバレッジの適切なデバイスが有効になっていることを確認します。 これを行うには、実行、 **IRP カバレッジ データ コレクションを有効になっているディスプレイ デバイス**テスト コンピューター上のツール。

    ```
    Drvcov /D
    ```

    次の例では、このツールからの出力例を示します。

    ```
    |------------------------------------------------------------------
    | List of devices we can get coverage data from.
    |------------------------------------------------------------------
    |  Device # : 1 
    |  Devnode #: 3884 Class:  USB Desc:  USB Root Hub
    |  Device ID: " USB\ROOT_HUB\4&413399C&0"
    |------------------------------------------------------------------
    | 1 device(s) found.
    |------------------------------------------------------------------
    ```

5.  IRP のカバレッジ データを収集します。

    デバイスの IRP カバレッジ データを収集する準備が整いました。 まず、テスト コンピューターで、コード カバレッジのテストを実行します。 コード カバレッジのテストの実行が完了したら、IRP カバレッジ レポートを表示できます。 これを行うには、実行、**表示 IRP カバレッジ データを収集する**テスト コンピューター上のツール。

    IRP のカバレッジ データを分析する方法については、次を参照してください。 [IRP カバレッジ データを分析する方法](how-to-analyze-irp-coverage-data.md)します。

6.  IRP のカバレッジを無効にして、アンインストール、[ドライバー カバレッジ フィルター ドライバー](driver-coverage-filter-driver.md)します。

    後のコード カバレッジのテストを完全に演習するが、無効にできます IRP のカバレッジのすべてのデバイスを実行して、 **IRP を無効にするカバレッジ データ コレクション**テスト コンピューター上のツール。

    IRP のカバレッジの最後のデバイスを無効にすると、テスト コンピューターを再起動するたびに、フィルター ドライバーは不要になった読み込みます。 ただし、メモリからフィルター ドライバーをアンロードするには、テスト コンピューターを再起動する必要があります。

 

 





