---
title: ファイルシステムフィルタードライバーとデバイスドライバーの類似点
description: ファイルシステムフィルタードライバーとデバイスドライバーの類似点
ms.assetid: 7797239e-e0cc-4422-bcc6-31cfe6efd8e4
keywords:
- フィルタードライバー WDK ファイルシステム、およびデバイスドライバー
- ファイルシステムフィルタードライバー WDK、およびデバイスドライバー
- デバイスドライバー WDK ファイルシステム
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 06d640ff0c33546389bf0c752658cedd9492e047
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841217"
---
# <a name="how-file-system-filter-drivers-are-similar-to-device-drivers"></a>ファイルシステムフィルタードライバーとデバイスドライバーの類似点


## <span id="ddk_how_file_system_filter_drivers_are_similar_to_device_drivers_if"></span><span id="DDK_HOW_FILE_SYSTEM_FILTER_DRIVERS_ARE_SIMILAR_TO_DEVICE_DRIVERS_IF"></span>


次のサブセクションでは、Microsoft Windows オペレーティングシステムのファイルシステムフィルタードライバーとデバイスドライバーの類似点について説明します。

### <a name="span-idsimilar_structurespanspan-idsimilar_structurespanspan-idsimilar_structurespansimilar-structure"></a><span id="Similar_Structure"></span><span id="similar_structure"></span><span id="SIMILAR_STRUCTURE"></span>類似の構造体

デバイスドライバーと同様に、ファイルシステムフィルタードライバーには[**Driverentry**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_initialize)、 [Dispatch](https://docs.microsoft.com/windows-hardware/drivers/kernel/writing-dispatch-routines)、および[i/o 完了](https://docs.microsoft.com/windows-hardware/drivers/kernel/using-iocompletion-routines)ルーチンがあります。 デバイスドライバーが呼び出したのと同じカーネルモードルーチンの多くを呼び出し、関連付けられているデバイス (つまり、ファイルシステムボリューム) の i/o 要求をフィルター処理します。

### <a name="span-idsimilar_functionalityspanspan-idsimilar_functionalityspanspan-idsimilar_functionalityspansimilar-functionality"></a><span id="Similar_Functionality"></span><span id="similar_functionality"></span><span id="SIMILAR_FUNCTIONALITY"></span>同様の機能

ファイルシステムフィルタードライバーとデバイスドライバーは i/o システムの一部であるため、i/o[要求パケット](https://docs.microsoft.com/windows-hardware/drivers/kernel/packet-driven-i-o-with-reusable-irps)(irp) を受信して操作します。

デバイスドライバーと同様に、ファイルシステムフィルタードライバーは独自の Irp を作成し、下位レベルのドライバーに送信することもできます。

どちらの種類のドライバーも、さまざまなシステムイベントの通知を (コールバック関数を使用して) 登録できます。

### <a name="span-idother_similaritiesspanspan-idother_similaritiesspanspan-idother_similaritiesspanother-similarities"></a><span id="Other_Similarities"></span><span id="other_similarities"></span><span id="OTHER_SIMILARITIES"></span>その他の類似点

デバイスドライバーと同様に、ファイルシステムフィルタードライバーは、 [I/o 制御コード](https://docs.microsoft.com/windows-hardware/drivers/kernel/introduction-to-i-o-control-codes)(ioctl) の概要を受け取ることができます。 ただし、ファイルシステムフィルタードライバーは、--[ファイルシステム制御コード](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)(FSCTLs) を受け取ることもできます。

デバイスドライバーと同様に、ファイルシステムフィルタードライバーは、システムの起動時に読み込まれるように構成することも、システムの起動プロセスが完了した後に読み込むように構成することもできます。

 

 




