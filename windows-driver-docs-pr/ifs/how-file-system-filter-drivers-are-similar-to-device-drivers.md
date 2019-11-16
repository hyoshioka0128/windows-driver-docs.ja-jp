---
title: ファイル システム フィルター ドライバーとデバイス ドライバーの類似点
description: ファイル システム フィルター ドライバーとデバイス ドライバーの類似点
ms.assetid: 7797239e-e0cc-4422-bcc6-31cfe6efd8e4
keywords:
- フィルタードライバー WDK ファイルシステム、およびデバイスドライバー
- ファイルシステムフィルタードライバー WDK、およびデバイスドライバー
- デバイスドライバー WDK ファイルシステム
ms.date: 10/16/2019
ms.localizationpriority: medium
ms.openlocfilehash: 31fab5bd1fab434cd0dd782b52f2f4d07e32bf0e
ms.sourcegitcommit: 2a1c24db881ed843498001493c3ce202c9aa03f1
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/16/2019
ms.locfileid: "74128456"
---
# <a name="how-file-system-filter-drivers-are-similar-to-device-drivers"></a>ファイル システム フィルター ドライバーとデバイス ドライバーの類似点

Microsoft Windows オペレーティングシステムのファイルシステムフィルタードライバーとデバイスドライバーは、次の点で似ています。

- **類似の構造体**

  デバイスドライバーと同様に、ファイルシステムフィルタードライバーには[**Driverentry**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_initialize)、 [Dispatch](https://docs.microsoft.com/windows-hardware/drivers/kernel/writing-dispatch-routines)、および[i/o 完了](https://docs.microsoft.com/windows-hardware/drivers/kernel/using-iocompletion-routines)ルーチンがあります。 デバイスドライバーが呼び出したのと同じカーネルモードルーチンの多くを呼び出し、関連付けられているデバイス (つまり、ファイルシステムボリューム) の i/o 要求をフィルター処理します。

- **同様の機能**

  - ファイルシステムフィルタードライバーとデバイスドライバーは i/o システムの一部であるため、i/o[要求パケット](https://docs.microsoft.com/windows-hardware/drivers/kernel/packet-driven-i-o-with-reusable-irps)(irp) を受信して操作します。

  - デバイスドライバーと同様に、ファイルシステムフィルタードライバーは独自の Irp を作成し、下位レベルのドライバーに送信することもできます。

  - どちらの種類のドライバーも、さまざまなシステムイベントの通知を (コールバック関数を使用して) 登録できます。

- **その他の類似点**

  - デバイスドライバーと同様に、ファイルシステムフィルタードライバーは、 [I/o 制御コード](https://docs.microsoft.com/windows-hardware/drivers/kernel/introduction-to-i-o-control-codes)(ioctl) の概要を受け取ることができます。 ファイルシステムフィルタードライバーは、[ファイルシステム制御コード](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)(FSCTLs) を受信して定義することもできます。

  - デバイスドライバーと同様に、ファイルシステムフィルタードライバーは、システムの起動時に読み込まれるように構成することも、システムの起動プロセスが完了した後に読み込むように構成することもできます。
