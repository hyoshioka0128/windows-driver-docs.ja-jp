---
title: INX ファイルを確認してください。
description: このトピックでは、サンプル センサー ドライバーの場合に、ターゲット デバイスにセンサーのドライバーをインストールするために最適な INF ファイルを変更する方法を示します。
ms.assetid: 1D326C5F-5B69-4C5C-AE52-14153DF964E9
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ab3c989c935fb290dde31c22eb58374aa147ad4d
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56548912"
---
# <a name="review-the-inx-file"></a>INX ファイルを確認してください。


このトピックでは、サンプル センサー ドライバーの場合に、ターゲット デバイスにセンサーのドライバーをインストールするために最適な INF ファイルを変更する方法を示します。

Windows では、デバイス ドライバーをインストールするプロセスの一部として (INF ファイルとも呼ばれます) の情報ファイルをセットアップします。 センサー ドライバーのサンプルが生成された INF ファイル*ADXL345Acc.inf*します。 このファイルには、加速度計センサー ドライバーをインストールするときにサメ Cove で Windows のインストールが使用する情報が含まれています。

Microsoft Visual Studio でドライバーのプロジェクトを作成すると、INX ファイルが最初に生成されます。 この汎用 INX ファイルを変更するには、ドライバーをビルドすると、ビルド プロセスに INX ファイル、ドライバーのインストールに使用される INF ファイルに変換します。 ビルド プロセスは、センサー ドライバーのインストールに使用することができます INF ファイルを生成するかどうかを確認する、ドライバーをビルドする前に、次の手順を効率的に管理を使用します。

## <a name="review-the-adxl345accinx-file"></a>ADXL345Acc.inx ファイルを確認してください。


掲載 INX ファイルを確認する必要がありますが、次の手順を 2 つの重要なセクションは指摘します。

1. をクリックして、 *ADXL345Acc.inx*を開き、ファイルを見つけて、\[バージョン\]ファイルの先頭付近の「セクション。
   ```cpp
   [Version]
   Class       = Sensor
   ClassGuid   = {5175D334-C371-4806-B3BA-71FD53C9258D}
   ```

デバイスのクラスが「センサー」と適切な GUID に設定されているので注意が提供されます。 デバイス クラス GUID の Windows の詳細については、次を参照してください。[ベンダー デバイス セットアップ クラスできるベンダー](https://docs.microsoft.com/windows-hardware/drivers/install/system-defined-device-setup-classes-available-to-vendors)します。

2. 検索、 \[ADXL345Acc\_Device.NT$ARCH$\]セクション。
   ```cpp
   [ADXL345Acc_Device.NT$ARCH$]
   ; DisplayName       Section          DeviceId
   ; -----------       -------          --------
   %ADXL345Acc_DevDesc% = ADXL345Acc_Inst, ACPI\ADXL345Acc
   ```

セカンダリ システムの説明テーブル (SSDT) と呼ばれる 'ハードウェア情報' ファイルを更新するために使用するデバイス名に対応しています (この例では、"ADXL345Acc") では、前のスニペットで、デバイス Id の値に注意してください。 重要です。

場合は、モバイル デバイスでサンプル センサー ドライバー インストールしない、し INX ファイルなど、関連する一般的なファイルを更新した後を参照してください[センサー ドライバーをビルド](build-the-sensor-driver.md)、Visual Studio でのドライバーをビルドする方法を確認します。 ビルド プロセスには、Windows はサメ Cove にドライバーをインストールするときに使用する INF ファイルを含む、センサー ドライバー ファイルが生成されます。

## <a name="inf-file-for-a-mobile-device"></a>モバイル デバイスの INF ファイル


サンプル ドライバーをテストするためにターゲット デバイスとしてサメ Cove ではなく、モバイル デバイスを使用している場合、は、INF ファイルを更新する次の追加タスクを実行します。

1. *ADXL345Acc.inx*ファイルで、検索、 \[ADXL345Acc\_Inst.NT.HW\]セクション、およびが空であることに注意してください。

**重要な**  、モバイルで使用される INF ファイルを更新しないかどうかは、おく必要があります、 \[ADXL345Acc\_Inst.NT.HW\]セクションが空です。 その場合は、このセクションでタスクをスキップしに移動、[センサー ドライバー](build-the-sensor-driver.md)トピック。

 

2. 空のセクションに次のコード スニペットを追加します。

```cpp
[ADXL345Acc_Inst.NT.HW]
AddReg=Sensor_Inst_SecurityAddReg

[Sensor_Inst_SecurityAddReg]
HKR,,Security,,"D:P(A;;GA;;;BA)(A;;GA;;;SY)(A;;GA;;;S-1-5-84-0-0-0-0-0)"    ; Allow all UMDF drivers to access this driver
```

**重要な**  AddReg フィールドの値をメモしてください。 次の手順で更新するファイルに追加する値のいずれかが正確に一致する必要があります。 上記のスニペットの例からのメモをするつもり*センサー\_Inst\_SecurityAddReg*します。

 

3. [モバイルのパッケージを作成する](creating-a-mobile-package.md)のモバイル デバイスでサンプル ドライバーをインストールします。

## <a name="related-topics"></a>関連トピック

[モバイルのパッケージを作成します。](creating-a-mobile-package.md)



