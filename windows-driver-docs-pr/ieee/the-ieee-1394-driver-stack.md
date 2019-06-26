---
title: IEEE 1394 ドライバー スタック
description: IEEE 1394 ドライバー スタック
ms.assetid: 3c8c218e-d814-451c-9a39-fe7fe5fb7aaf
keywords:
- IEEE 1394 WDK バス ドライバー スタック
- 1394 WDK バス ドライバー スタック
- ドライバー スタック WDK IEEE 1394 バス
- WDK の IEEE 1394 をスタックします。
- デバイス スタック WDK IEEE 1394 バス
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4f4495f0248c59514434152b3f26eb99d08ee05a
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67381029"
---
# <a name="the-ieee-1394-driver-stack"></a>IEEE 1394 ドライバー スタック





次の図は、新しい 1394 バス ドライバーと Microsoft でサポートされている 1394 クライアント ドライバーは、IEEE 1394 ドライバー スタックを示しています。

![ieee 1394 のドライバー スタックを示す図](images/1394driverstack.png)

IEEE 1394 バス ドライバーに接続するデバイス用のクライアント ドライバーは、IEEE 1394 のドライバー スタックの一番上に配置されます。 バス ドライバーは、IEEE 1394 バス ハードウェアに依存しないインターフェイスを提供します。 デバイス ドライバーは、IEEE 1394 バス ドライバーによって処理される、Irp を送信することによって、デバイスと通信します。 Windows 7 では、前に、バス ドライバーは、ポート ドライバー (1394bus.sys) およびマザーボードのホスト コント ローラー (ochi1394.sys) 用のプライマリのミニポート ドライバーの組み合わせをでした。 Windows 7 およびそれ以降のバージョンでは、バスのレガシ ポート/ミニポート ドライバーが 1394ohci.sys、カーネル モード ドライバー フレームワーク (KMDF) を使用して実装されているモノリシック IEEE 1394 バス ドライバーによって置き換えられます。 1394ohci.sys バス ドライバーは、レガシ 1394 バス ドライバーと完全に下位互換性です。 新しいバス ドライバーと従来の 1394 バス ドライバーの動作の既知のいくつか違いの詳細については、次を参照してください。 [Windows 7 での IEEE 1394 バス ドライバー](https://docs.microsoft.com/windows-hardware/drivers/ieee/IEEE-1394-Bus-Driver-in-Windows-7)します。

次の図は、レガシ エンジンと新しい 1394 バス ドライバー間のリレーションシップを示します。

![従来と新しい 1394 バス ドライバー間のリレーションシップを示す図。](images/1394busdriver.png)

コマンドをバスに接続されているデバイスを実行するにはドライバー発行、 [ **IRP\_MJ\_デバイス\_コントロール**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-device-control)コントロールのコードの IRP [ **IOCTL\_1394\_クラス**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/1394/ni-1394-ioctl_1394_class)します。 ドライバー パッケージ、IEEE 1394 I/O 要求のブロック内のパラメーター ([**IRB**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/1394/ns-1394-_irb))、内でポインターを渡すと、 **Parameters.Others.Argument1** IRP のメンバー。 **FunctionNumber** 、IRB のメンバーは、操作の種類を決定します。 および**u**メンバーが、操作について説明します。 バス ドライバーは、IOCTL\_1394\_クラス IRP バスとホスト コント ローラーの両方へのインターフェイスを表示します。

IRB 構造体には、バスの各要求に適用されるパラメーターと要求固有のパラメーターが含まれています。 **U** IRB のメンバーには、要求の種類ごとに 1 つのデータ構造体の共用体の要求固有のパラメーターが含まれています。

通常の操作中にドライバーが通常の I/O 要求を受信 (など[ **IRP\_MJ\_読み取り**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-read))、適切なの IEEE 1394 操作に変換し、ディスパッチします。IOCTL を介してデバイスに操作\_1394\_クラス。

## <a name="related-topics"></a>関連トピック
[Windows 7 での IEEE 1394 バス ドライバー](https://docs.microsoft.com/windows-hardware/drivers/ieee/IEEE-1394-Bus-Driver-in-Windows-7)  



