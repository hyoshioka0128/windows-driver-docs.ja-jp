---
title: サンプル カーネルモード ドライバー
description: サンプル カーネルモード ドライバー
ms.assetid: 09d08e07-e991-458f-aedf-018a0dd20af5
keywords:
- カーネルモードドライバー WDK、サンプル
- サンプルドライバー WDK カーネルモード
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 66c41f15c1baf14e98b7b1457de82b44d74a7506
ms.sourcegitcommit: 958a5ced83856df22627c06eb42c9524dd547906
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/12/2020
ms.locfileid: "83235437"
---
# <a name="sample-kernel-mode-drivers"></a>サンプル カーネルモード ドライバー

WDK には、さまざまなサンプルカーネルモードドライバーが用意されています。 WDK をインストールした後、 `src\general` サブディレクトリには、すべてのカーネルモードドライバーに適用できるサンプルドライバーコードが含まれています。 サンプルもオンラインで保持されています。 これらのサンプルには次のものが含まれます。

[**DCHU**](https://github.com/Microsoft/Windows-driver-samples/tree/master/general/DCHU)

DCH design の[原則](../develop/getting-started-with-windows-drivers.md)(宣言型、コンポーネント、およびハードウェアサポートアプリ [HSA]) を適用します。  独自の Windows ドライバーパッケージのモデルとして使用できます。

[**PLX9x5x**](https://github.com/Microsoft/Windows-driver-samples/tree/master/general/PLX9x5x)

このサンプルでは、Windows ドライバーフレームワークを使用して、汎用 PCI デバイス用のドライバーを作成する方法を示します。

[**SimpleMediaSource**](https://github.com/Microsoft/Windows-driver-samples/tree/master/general/SimpleMediaSource)

このサンプルでは、カスタムメディアソースとドライバーパッケージを作成して、カメラとしてインストールし、フレームを生成する方法を示します。

[**SystemDma/wdm**](https://github.com/Microsoft/Windows-driver-samples/tree/master/general/SystemDma/wdm)

このサンプルでは、V3 システム DMA の使用方法を示します。 Windows でサポートされているシステム DMA コントローラーを使用して、ドライバーが DMA を使用してハードウェアの場所にデータを書き込む方法を示します。

[**WinHEC 2017 ラボ**](https://github.com/Microsoft/Windows-driver-samples/tree/master/general/WinHEC%202017%20Lab)

[**WinHEC 2017/Windows パフォーマンスの最適化**](https://github.com/Microsoft/Windows-driver-samples/tree/master/general/WinHEC%202017/Optimizing%20Windows%20Performance)

[**cancel**](https://github.com/Microsoft/Windows-driver-samples/tree/master/general/cancel)  

[キャンセルセーフな IRP キュー](cancel-safe-irp-queues.md)の使用方法を示します。

[**エコー**](https://github.com/Microsoft/Windows-driver-samples/tree/master/general/echo)

[**場合**](https://github.com/Microsoft/Windows-driver-samples/tree/master/general/event)  

アプリケーションが通知を要求した場合に、カーネルモードドライバーがハードウェアイベントをアプリケーションに通知するために使用できる技法を示します。 1つの手法で[イベントオブジェクト](event-objects.md)を使用し、もう1つの方法は、イベントが発生するまで通知要求の[キュー](queuing-and-dequeuing-irps.md)に依存します。

[**filehistory**](https://github.com/Microsoft/Windows-driver-samples/tree/master/general/filehistory)

FileHistory サンプルは、停止している場合はファイル履歴サービスを開始し、定期的なバックアップをスケジュールするコンソールアプリケーションです。 アプリケーションでは、コマンドラインパラメーターとして、既定のバックアップターゲットとして使用するストレージデバイスのパス名を指定する必要があります。

[**IOCTL サンプル**](https://github.com/Microsoft/Windows-driver-samples/tree/master/general/ioctl)

ドライバーで i/o 制御コードをサポートする方法を示します。

[**obcallback**](https://github.com/Microsoft/Windows-driver-samples/tree/master/general/obcallback)

ObCallback サンプルドライバーは、プロセス保護のための登録済みコールバックの使用方法を示しています。 ドライバーは、プロセスの作成時に呼び出されるコントロールのコールバックを登録します。

[**pcidrv**](https://github.com/Microsoft/Windows-driver-samples/tree/master/general/pcidrv)

このサンプルでは、PCI デバイス用の KMDF ドライバーを記述する方法を示します。 このサンプルは、Intel 82557/82558 ベースの PCI イーサネットアダプター (10/100) と Intel 互換機と連携して動作します。

[**perfcounters/kcs**](https://github.com/Microsoft/Windows-driver-samples/tree/master/general/perfcounters/kcs)

Kcs サンプルドライバーは、カーネルモードのパフォーマンスライブラリの使用方法を示しています。

[**レジストリ/regfltr**](https://github.com/Microsoft/Windows-driver-samples/tree/master/general/registry/regfltr)

RegFltr サンプルは、レジストリフィルタードライバーを記述する方法を示しています。

[**toaster**](https://github.com/Microsoft/Windows-driver-samples/tree/master/general/toaster)  

[Windows Driver Model](windows-driver-model.md) (WDM) に準拠した一連のドライバーのサンプルコードを提供します。 このサンプルには、サンプルのインストールソフトウェアも含まれています。

[**tracedrv**](https://github.com/Microsoft/Windows-driver-samples/tree/master/general/tracing/tracedriver)  

[WPP ソフトウェアのトレース](https://docs.microsoft.com/windows-hardware/drivers/devtest/wpp-software-tracing)を使用する方法について説明します。

[**UMDF ドライバースケルトンのサンプル**](https://github.com/Microsoft/Windows-driver-samples/tree/master/general/umdfSkeleton)

このサンプルでは、ユーザーモードドライバーフレームワークのバージョン1を使用して、最小限のドライバーを記述する方法を示します。

[**HID デバイス用 Firefkmdf フィルタードライバー**](https://github.com/Microsoft/Windows-driver-samples/tree/master/hid/firefly)このサンプルでは、フィルタードライバーの記述方法を説明すると共に、リモート i/o ターゲットインターフェイスを使用して、HID コレクションをカーネルモードで開き、IOCTL 要求を送信して機能レポートを設定および取得する方法に加えて、アプリケーションが WMI インターフェイスを使用してフィルタードライバーにコマンドを送信する方法を示します。

ディレクトリの他のサブディレクトリには、 `\src` さまざまな種類のハードウェアのカーネルモードドライバー用のサンプルコードが含まれています。

## <a name="see-also"></a>関連項目

GitHub の[Microsoft Windows ドライバーのサンプル](https://github.com/Microsoft/Windows-driver-samples)
