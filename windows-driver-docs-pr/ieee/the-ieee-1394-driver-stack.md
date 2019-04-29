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
ms.openlocfilehash: 905dcdc0fc71127055ae60e6bf043fd7d3622ce2
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63390317"
---
# <a name="the-ieee-1394-driver-stack"></a>IEEE 1394 ドライバー スタック





次の図は、新しい 1394 バス ドライバーと Microsoft でサポートされている 1394 クライアント ドライバーは、IEEE 1394 ドライバー スタックを示しています。

![ieee 1394 のドライバー スタックを示す図](images/1394driverstack.png)

IEEE 1394 バス ドライバーに接続するデバイス用のクライアント ドライバーは、IEEE 1394 のドライバー スタックの一番上に配置されます。 バス ドライバーは、IEEE 1394 バス ハードウェアに依存しないインターフェイスを提供します。 デバイス ドライバーは、IEEE 1394 バス ドライバーによって処理される、Irp を送信することによって、デバイスと通信します。 Windows 7 では、前に、バス ドライバーは、ポート ドライバー (1394bus.sys) およびマザーボードのホスト コント ローラー (ochi1394.sys) 用のプライマリのミニポート ドライバーの組み合わせをでした。 Windows 7 およびそれ以降のバージョンでは、バスのレガシ ポート/ミニポート ドライバーが 1394ohci.sys、カーネル モード ドライバー フレームワーク (KMDF) を使用して実装されているモノリシック IEEE 1394 バス ドライバーによって置き換えられます。 1394ohci.sys バス ドライバーは、レガシ 1394 バス ドライバーと完全に下位互換性です。 新しいバス ドライバーと従来の 1394 バス ドライバーの動作の既知のいくつか違いの詳細については、次を参照してください。 [Windows 7 での IEEE 1394 バス ドライバー](https://msdn.microsoft.com/library/windows/hardware/gg266402)します。

次の図は、レガシ エンジンと新しい 1394 バス ドライバー間のリレーションシップを示します。

![従来と新しい 1394 バス ドライバー間のリレーションシップを示す図。](images/1394busdriver.png)

コマンドをバスに接続されているデバイスを実行するにはドライバー発行、 [ **IRP\_MJ\_デバイス\_コントロール**](https://msdn.microsoft.com/library/windows/hardware/ff550744)コントロールのコードの IRP [ **IOCTL\_1394\_クラス**](https://msdn.microsoft.com/library/windows/hardware/ff537232)します。 ドライバー パッケージ、IEEE 1394 I/O 要求のブロック内のパラメーター ([**IRB**](https://msdn.microsoft.com/library/windows/hardware/ff537350))、内でポインターを渡すと、 **Parameters.Others.Argument1** IRP のメンバー。 **FunctionNumber** 、IRB のメンバーは、操作の種類を決定します。 および**u**メンバーが、操作について説明します。 バス ドライバーは、IOCTL\_1394\_クラス IRP バスとホスト コント ローラーの両方へのインターフェイスを表示します。

IRB 構造体には、バスの各要求に適用されるパラメーターと要求固有のパラメーターが含まれています。 **U** IRB のメンバーには、要求の種類ごとに 1 つのデータ構造体の共用体の要求固有のパラメーターが含まれています。

通常の操作中にドライバーが通常の I/O 要求を受信 (など[ **IRP\_MJ\_読み取り**](https://msdn.microsoft.com/library/windows/hardware/ff550794))、適切なの IEEE 1394 操作に変換し、ディスパッチします。IOCTL を介してデバイスに操作\_1394\_クラス。

## <a name="related-topics"></a>関連トピック
[Windows 7 での IEEE 1394 バス ドライバー](https://msdn.microsoft.com/library/windows/hardware/gg266402)  



