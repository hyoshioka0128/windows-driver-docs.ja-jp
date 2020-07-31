---
title: Microsoft Bluetooth テストプラットフォームのセットアップ
description: Microsoft Bluetooth テストプラットフォームのセットアップのセットアップ方法
ms.date: 2/14/2020
ms.assetid: 85ac7c5b-b5f7-49e0-85f8-72e191c00974
ms.localizationpriority: medium
ms.openlocfilehash: 5dde498fdc72eb0bf98474788ec3e3c46026caf8
ms.sourcegitcommit: 7a7ce6070ed16673108cc64c33b3ddb894453cfb
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/29/2020
ms.locfileid: "87412525"
---
# <a name="setting-up-the-bluetooth-test-platform-btp"></a>Bluetooth テストプラットフォーム (BTP) の設定

## <a name="hardware-setup"></a>ハードウェアのセットアップ

### <a name="connecting-traduci-to-the-pc"></a>Traduci を PC に接続する

指定された USB A-B ケーブルを使用して、テスト対象のシステム (SUT) の USB ポートに Traduci を接続します。 Traduci が PC のポートに直接接続されていて、Traduci が USB コネクタの右側にある胴体コネクタを介して[9v, 2a 電源アダプター](https://www.digikey.com/product-detail/en/qualtek/QFWB-18-9-US01/Q1181-ND/8260129)を使用している場合は、パフォーマンスが最適です。 Traduci を USB ハブに接続しないでください。

![USB および電源ポートを示す Traduci](images/Traduci_USBPortSidejpg.jpg)

### <a name="connecting-peripherals-to-the-traduci"></a>周辺機器を Traduci に接続する

Traduci には、テスト周辺機器に 4 12 のピンポート (JA、JC、JD) が使用されています。

![USB および電源ポートを示す Traduci](images/Traduci_12PinPortSide.jpg)

周辺無線を Traduci のポートに接続するには、Led とボタンが前面になるように Traduci を向きにします。 次に、MAC アドレスとスイッチが含まれているラジオの印刷されたラベルが前面に表示されるように、ラジオスレッドを向きます。 この向きを維持するには、適切な12ピンポートで周辺機器を接続します。

> [!NOTE]
> 一部の周辺機器は、特定のポートにのみ接続できます。  詳細については、[サポートされているハードウェアのページ](testing-BTP-hw.md)を参照してください。

![周辺機器が接続されている Traduci](images/Traduci_and_DigilentRN42.jpg)

## <a name="software-setup"></a>ソフトウェアのセットアップ

1. [Windows Driver Kit](https://docs.microsoft.com/windows-hardware/drivers/download-the-wdk#download-icon-step-2-install-wdk-for-windows-10-version-1903)をダウンロードします。

2. WDK のインストールが完了する[と、テストの作成と実行フレームワーク (TAEF)](https://docs.microsoft.com/windows-hardware/drivers/taef/)のインストールファイル (* .msi ファイルと * .cab ファイル) がディレクトリに配置され `%ProgramFiles%\Windows Kits\10\Testing\Runtimes` ます。

3. [BTP ソフトウェアパッケージ](testing-BTP-software-package.md)をダウンロードします。これにより、必要なすべてのファイルがディレクトリにインストールされ `C:\BTP` ます。

4. [セキュアブート](https://docs.microsoft.com/windows-hardware/design/device-experiences/oem-secure-boot)が**無効になっ**ていることを確認します。

5. BitLocker が**無効になっ**ていることを確認します。

6. Traduci ボードが SUT に接続されていることを確認します。

7. SUT の管理者特権でのコマンドラインで、ディレクトリに移動 `C:\BTP` し、を実行して `ConfigureMachineForBTP.bat` テストコンピューターを構成します。 再起動が必要な場合があります。

8. パッケージでのテストスクリプトの実行については、「 [BTP テスト](testing-BTP-Tests.md)」を参照してください。

## <a name="known-issues"></a>既知の問題

- 電源: デバイスが電源以外のハブに接続されているか、VCC が5V を提供できない場合、断続的なエラーが発生する可能性があります。 このような場合は、電源が入っている USB ハブを使用するか、9V AC DC バレルアダプターを使用します。
