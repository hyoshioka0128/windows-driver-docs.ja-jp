---
title: AVStream ミニドライバーの初期化
description: AVStream ミニドライバーの初期化
ms.assetid: 666d6efb-93ec-43f3-87c5-ea1a3983bfd0
keywords:
- AVStream WDK、ミニドライバーの初期化
- ミニドライバー WDK AVStream、初期化
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 44f6c78e8e089e36feb9c5f94e8d74c1ea5ca307
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72845569"
---
# <a name="initializing-an-avstream-minidriver"></a>AVStream ミニドライバーの初期化





独自の呼び出しでデバイスの初期化を処理しない AVStream ミニドライバーは、ミニドライバーの[**Driverentry**](https://docs.microsoft.com/previous-versions/ff554081(v=vs.85))ルーチンから、 [**ksinitializedriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/nf-ks-ksinitializedriver)を呼び出します。 **Ksk Initializedriver**は、IRP のディスパッチ、PnP によるデバイスメッセージの追加、およびアンロードに加えて、avstream ドライバーのドライバーオブジェクトを初期化します。

**Ksinitializedriver**の呼び出しでは、ミニドライバーはドライバーオブジェクトへのポインターを渡して、レジストリパスへのポインターと、必要に応じてデバイス記述子オブジェクトを初期化します。 [**Ksk デバイス\_記述子**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-_ksdevice_descriptor)オブジェクトを渡す必要はありません。 ミニドライバーがデバイス記述子を渡すと、AVStream は、指定された特性を持つデバイスを AddDevice 時に作成します。

デバイス記述子オブジェクトには、 [**Ksk デバイス\_ディスパッチ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-_ksdevice_dispatch)構造体、およびフィルター記述子の配列へのポインターが含まれています。 ミニドライバーでサポートされているフィルターの種類ごとに、 [**Ksk フィルター\_記述子**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-_ksfilter_descriptor)を指定します。 ミニドライバーが[**Ksinitializedriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/nf-ks-ksinitializedriver)を呼び出すと、avstream は、ミニドライバーによって公開されるフィルターの種類ごとにフィルターファクトリオブジェクトを作成します。 個々のフィルターは、関連付けられた create item に対して create IRP を受信したときに、フィルターファクトリによってインスタンス化されます。 各フィルター記述子には、 [**Kspin\_記述子\_EX**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-_kspin_descriptor_ex)オブジェクトの配列へのポインターが含まれています。 AVStream は、ミニドライバーがそのフィルターを通じて公開する pin の種類ごとに、関連するフィルターにピンファクトリを作成します。

フィルターで特定のピンの種類への接続が確立されると、AVStream の pin ファクトリによってピンオブジェクトが作成されます。 各フィルターが少なくとも1つの pin を公開する必要があることに注意してください。 ミニドライバーは、KSPIN\_記述子\_EX の**InstancesNecessary**メンバーを使用して、フィルターが正しく機能するために必要なこの pin の種類のインスタンス数を特定します。 同様に、ミニドライバーは、この構造体の**InstancesPossible**メンバーを使用して、pin ファクトリがインスタンス化できる pin の数に最大値を課すことができます。

AVStream では、[フィルター中心](filter-centric-processing.md)の処理と[ピン中心の](pin-centric-processing.md)処理の2種類の処理がサポートされています。 記述子をレイアウトするときに、各フィルターの種類で実行する処理の種類を決定します。

### <a name="installing-an-avstream-minidriver"></a>AVStream ミニドライバーのインストール

AVStream ミニドライバーには、ドライバーをインストールするためにシステムで使用される INF ファイルが必要です。 AVStream INF ファイルは、「 [Inf ファイルの作成](https://docs.microsoft.com/windows-hardware/drivers/install/overview-of-inf-files)」で説明されている一般的な inf 形式に基づいています。 また、Windows Driver Kit (WDK) の AVStream サンプルドライバーで提供されている INF ファイルを参照することもできます。 次の AVStream 固有のガイドラインに注意してください。

親デバイスのミニドライバーを作成する場合は、INF ファイルの**AddReg**セクションに次の内容が含まれている必要があります。

```INF
[ParentName.AddReg]
HKR,"ENUM\[DeviceName]",pnpid,,"[string]"
```

子デバイスのミニドライバーを作成する場合、 **AddReg**セクションには次のものが含まれている必要があります。

```INF
[Manufacturer]
...=ChildName
[ChildName]
...=ChildName.Device,AVStream\[string]
```

ストリームクラスドライバーの "AVStream" は "ストリーム" であることに注意してください。

すべての AVStream ミニドライバーについて、INF ファイル内のフィルター固有の参照文字列は、 [**Ksk フィルター\_記述子**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-_ksfilter_descriptor)構造体の**referenceguid**メンバーと一致している必要があります。

記述子の詳細については、「 [Avstream 記述子](avstream-descriptors.md)」を参照してください。
