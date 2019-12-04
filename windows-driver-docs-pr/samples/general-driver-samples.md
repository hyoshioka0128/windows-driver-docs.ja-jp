---
title: 汎用ドライバーのサンプル
description: このディレクトリのサンプルは、デバイスのカスタムドライバーを作成するための開始点として使用されます。
ms.assetid: C5DC72F1-D093-47D0-9AC3-680878C5A868
ms.date: 12/03/2019
ms.localizationpriority: medium
ms.openlocfilehash: ea54e92fb10af5534b82926058923d571249dce5
ms.sourcegitcommit: 30fa63ad13fd5e2e883b76a44f0703e01049ffa1
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/03/2019
ms.locfileid: "74735264"
---
# <a name="general-driver-samples"></a>汎用ドライバーのサンプル

このディレクトリのサンプルは、デバイスのカスタムドライバーを作成するための開始点として使用されます。

| サンプル | 説明 |
| --- | --- |
| [安全な IRP キューをキャンセルする](https://docs.microsoft.com/samples/microsoft/windows-driver-samples/cancel-safe-irp-queue-sample) | キャンセルセーフキュールーチン IoCsqInitialize、IoCsqInsertIrp、IoCsqRemoveIrp、IoCsqRemoveNextIrp の使用方法を示します。 これらのルーチンを使用することにより、ドライバーの開発者は、IRP のキャンセルの競合状態について心配する必要がなくなります。 |
| [KMDF エコー](https://docs.microsoft.com/samples/microsoft/windows-driver-samples/kmdf-echo-sample) | シーケンシャルキューを使用して、ドライバーに提示される読み取り要求と書き込み要求をシリアル化する方法を示します。 |
| [UMDF1 Echo](https://docs.microsoft.com/samples/microsoft/windows-driver-samples/echo-sample-umdf-version-1) | UMDF 1 を使用してドライバーを記述し、ベストプラクティスを採用する方法を示します。 |
| [UMDF2 Echo](https://docs.microsoft.com/samples/microsoft/windows-driver-samples/echo-sample-umdf-version-2) | UMDF 2 を使用してドライバーを記述し、ベストプラクティスを採用する方法を示します。 |
| [UMDF SocketEcho サンプル (UMDF Version 1)](https://docs.microsoft.com/samples/microsoft/windows-driver-samples/umdf-socketecho-sample-umdf-version-1) | UMDF を使用してドライバーを記述し、ベストプラクティスを示す方法を示します。 |
| [ハードウェアイベント](https://docs.microsoft.com/samples/microsoft/windows-driver-samples/hardware-event-sample)| カーネルモードドライバーがハードウェアイベントについてアプリケーションに通知できる2つの異なる方法を示します。 一方向では、イベントベースのメソッドを使用し、もう1つは IRP ベースのメソッドを使用します。 サンプルドライバーでは、タイマー DPC を使用してハードウェアイベントをシミュレートします。 |
| [ファイル履歴](https://docs.microsoft.com/samples/microsoft/windows-driver-samples/file-history-sample)| ファイル履歴サービスが停止されている場合は、そのサービスを開始し、定期的なバックアップをスケジュールするコンソールアプリケーション。 |
| [PnP 以外のドライバーのサンプル](https://docs.microsoft.com/samples/microsoft/windows-driver-samples/non-pnp-driver-sample)| カーネルモードドライバーフレームワークを使用して、PnP 以外のドライバーを記述する方法を示します。 |
| [IOCTL](https://docs.microsoft.com/samples/microsoft/windows-driver-samples/ioctl)| 4つの異なる種類の Ioctl (\_DIRECT のメソッド\_、メソッド\_OUT\_DIRECT、メソッド\_ない、およびメソッド\_バッファリング) の使用方法を示します。 |
| [ObCallback](https://docs.microsoft.com/samples/microsoft/windows-driver-samples/obcallback-callback-registration-driver) | プロセス保護のための登録済みコールバックの使用方法を示します。 ドライバーは、プロセスの作成時に呼び出されるコントロールのコールバックを登録します。 |
| [PCIDRV](https://docs.microsoft.com/samples/microsoft/windows-driver-samples/pcidrv---wdf-driver-for-pci-device) | このサンプルでは、PCI デバイス用の KMDF ドライバーを記述する方法を示します。 このサンプルは、Intel 82557/82558 ベースの PCI イーサネットアダプター (10/100) と Intel 互換機と連携して動作します。 |
| [カーネルカウンター](https://docs.microsoft.com/samples/microsoft/windows-driver-samples/kernel-counter-sample-kcs) | カーネルモードパフォーマンスライブラリの使用方法を示します。 ドライバーは、ハードウェアを制御するのではなく、単にカウンターを提供します。 このコードには、各関数の動作を説明するコメントが含まれています。 |
| [PLX9x5x PCI ドライバー](https://docs.microsoft.com/samples/microsoft/windows-driver-samples/plx9x5x-pci-driver) | Windows ドライバーフレームワーク (WDF) を使用して、汎用 PCI デバイス用のドライバーを記述する方法を示します。 このドライバーのターゲットハードウェアは、PLX9656/9653RDK-LITE ボードです。 |
| [RegFltr](https://docs.microsoft.com/samples/microsoft/windows-driver-samples/regfltr-sample-driver) | レジストリフィルタードライバーを記述する方法について説明します。 |
| [単純なメディアソース](https://docs.microsoft.com/samples/microsoft/windows-driver-samples/simplemediasource-sample) | カスタムメディアソースとドライバーパッケージを作成する方法を示します。 |
| [システム DMA](https://docs.microsoft.com/samples/microsoft/windows-driver-samples/system-dma) | V3 システム DMA の使用方法を示します。 Windows でサポートされているシステム DMA コントローラーを使用して、ドライバーが DMA を使用してハードウェアの場所にデータを書き込む方法を示します。 |
| [トースターサンプルドライバー](https://docs.microsoft.com/samples/microsoft/windows-driver-samples/toaster-sample-driver) | カーネルモードドライバーフレームワーク (KMDF) とユーザーモードドライバーフレームワーク (UMDF) バージョン1の両方の Windows ドライバー開発の基本的な側面を示す反復的な一連のサンプルです。 |
| [トースターパッケージのサンプル](https://docs.microsoft.com/samples/microsoft/windows-driver-samples/toaster-package-sample-driver) | トースターサンプルドライバーのハードウェア優先およびソフトウェア優先インストールをシミュレートします。 |
| [トースターサンプル (UMDF バージョン 2)](https://docs.microsoft.com/samples/microsoft/windows-driver-samples/toaster-sample-umdf-version-2) | ユーザーモードドライバーフレームワーク (UMDF) バージョン2を使用した Windows ドライバー開発の基本的な側面を示す、反復的な一連のサンプルです。 |
| [EventDrv](https://docs.microsoft.com/samples/microsoft/windows-driver-samples/eventdrv) | カーネルモードのトレースプロバイダーとドライバー。 ドライバーは、ハードウェアを制御しません。単にトレースイベントを生成します。 これは、ドライバーでの Windows イベントトレーシング (ETW) API の使用方法を示すために設計されています。 |
| [システムトレースコントロール](https://docs.microsoft.com/samples/microsoft/windows-driver-samples/systemtraceprovider) | イベントトレースコントロール Api を使用して、システムトレースプロバイダーからイベントを収集する方法を示します。 |
| [Tracedrv](https://docs.microsoft.com/samples/microsoft/windows-driver-samples/tracedrv) | ソフトウェアのトレース用にインストルメント化されたサンプルドライバー。|
| [UMDF ドライバースケルトン](https://docs.microsoft.com/samples/microsoft/windows-driver-samples/umdf-driver-skeleton-sample-umdf-version-1) | ユーザーモードドライバーフレームワークを使用して最小限のドライバーを記述し、ベストプラクティスを示す方法を示します。 |
| [ユニバーサルドライバー用ドライバーパッケージインストールツールキット](https://docs.microsoft.com/samples/microsoft/windows-driver-samples/driver-package-installation-toolkit-for-universal-drivers) | ユニバーサルドライバー設計の DCHU の原則を示します。 |
| [WinHEC 2017 ラボ](https://docs.microsoft.com/samples/microsoft/windows-driver-samples/winhec-2017-lab) | WinHEC 2017 Lab: トースター Driver、PlugInToaster、トースター Support App のトースターサンプル。 |
