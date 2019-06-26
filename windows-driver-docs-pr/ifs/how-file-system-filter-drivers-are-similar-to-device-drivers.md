---
title: ファイル システム フィルター ドライバーとデバイス ドライバーの類似点
description: ファイル システム フィルター ドライバーとデバイス ドライバーの類似点
ms.assetid: 7797239e-e0cc-4422-bcc6-31cfe6efd8e4
keywords:
- フィルター ドライバー WDK ファイル システム、デバイス ドライバーとの比較
- ファイル システム フィルター ドライバー WDK、デバイス ドライバーとの比較
- デバイス ドライバー WDK ファイル システム
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9c1d639ef67c5a0efcf0e6021581c98dfb19e708
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67365865"
---
# <a name="how-file-system-filter-drivers-are-similar-to-device-drivers"></a>ファイル システム フィルター ドライバーとデバイス ドライバーの類似点


## <span id="ddk_how_file_system_filter_drivers_are_similar_to_device_drivers_if"></span><span id="DDK_HOW_FILE_SYSTEM_FILTER_DRIVERS_ARE_SIMILAR_TO_DEVICE_DRIVERS_IF"></span>


次のサブセクションでは、ファイル システム フィルター ドライバーと Microsoft Windows オペレーティング システム内のデバイス ドライバーの間の類似点について説明します。

### <a name="span-idsimilarstructurespanspan-idsimilarstructurespanspan-idsimilarstructurespansimilar-structure"></a><span id="Similar_Structure"></span><span id="similar_structure"></span><span id="SIMILAR_STRUCTURE"></span>同様の構造

ファイル システム フィルター ドライバーがある、デバイス ドライバーなど[ **DriverEntry**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_initialize)、[ディスパッチ](https://docs.microsoft.com/windows-hardware/drivers/kernel/writing-dispatch-routines)、および[I/O 完了](https://docs.microsoft.com/windows-hardware/drivers/kernel/using-iocompletion-routines)ルーチン。 さまざまなデバイス ドライバーを呼び出すと、同じのカーネル モード ルーチンを呼び出すし、I/O 要求が関連付けられているデバイス (つまり、ファイル システム ボリューム) のフィルターを適用します。

### <a name="span-idsimilarfunctionalityspanspan-idsimilarfunctionalityspanspan-idsimilarfunctionalityspansimilar-functionality"></a><span id="Similar_Functionality"></span><span id="similar_functionality"></span><span id="SIMILAR_FUNCTIONALITY"></span>同様の機能

ファイル システム フィルター ドライバーとデバイス ドライバーは、I/O システムの一部なので、両方を受信[I/O 要求パケット](https://docs.microsoft.com/windows-hardware/drivers/kernel/packet-driven-i-o-with-reusable-irps)(Irp) して操作します。

デバイス ドライバーなど、ファイル システム フィルター ドライバーも独自の Irp を作成し、下位レベルのドライバーに送信できます。

ドライバーの両方の種類はことができます (をコールバック関数を使用) 通知の登録のさまざまなシステム イベント。

### <a name="span-idothersimilaritiesspanspan-idothersimilaritiesspanspan-idothersimilaritiesspanother-similarities"></a><span id="Other_Similarities"></span><span id="other_similarities"></span><span id="OTHER_SIMILARITIES"></span>他類似点

ファイル システム フィルター ドライバーを受信できるデバイスのドライバーのような[I/O 制御コードの概要](https://docs.microsoft.com/windows-hardware/drivers/kernel/introduction-to-i-o-control-codes)(Ioctl)。 ただし、ファイル システム フィルター ドライバーも受信--でき、定義--[システム コントロールのコードをファイル](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)(FSCTLs)。

デバイス ドライバーのようなシステムの起動時に読み込まれるか、または読み込まれた後で、システムの起動処理が完了したら、ファイル システム フィルター ドライバーを構成できます。

 

 




