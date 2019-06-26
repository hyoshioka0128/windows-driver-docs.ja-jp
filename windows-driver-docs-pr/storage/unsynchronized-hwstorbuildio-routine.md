---
title: 同期されていない HwStorBuildIo ルーチン
description: 同期されていない HwStorBuildIo ルーチン
ms.assetid: 6b18e3ff-30dd-414b-99b5-4bb914660a67
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e29b6bdcaaeb014372ad2d7de33b4ec6f29ad8c6
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67386799"
---
# <a name="unsynchronized-hwstorbuildio-routine"></a>同期されていない HwStorBuildIo ルーチン


## <span id="ddk_unsynchronized_hwstorbuildio_routine_kg"></span><span id="DDK_UNSYNCHRONIZED_HWSTORBUILDIO_ROUTINE_KG"></span>


SCSI ポート-ミニポートのドライバーの I/O をモデル化、ミニポート ドライバーの[ **StartIo** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_startio)ルーチン、 [ **HwScsiStartIo**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff557323(v=vs.85))SCSI を送信する必要があります可能な限り早くハードウェアをブロック (される Srb) を要求します。 これは非常に重要ですので、ミニポート ドライバーので作業を完了*StartIo*ルーチンは、割り込みを無効にして行われます IRQL = ディスパッチと\_レベル。 残念ながら、I/O が開始されると、これらの Hba のミニポート ドライバーで大量の処理を行う必要がありますので、このモデルは一部の高パフォーマンスのホスト バス アダプター (Hba) のドライバーには適していません。 ミニポート ドライバーでは、この処理を行って場合、 *StartIo*システム パフォーマンスが低下するルーチンをします。

Storport の I/O モデルをサポートしています、 [ **HwStorBuildIo** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/storport/nc-storport-hw_buildio)ミニポート ドライバーから処理負担の一部を削除するために日常的な*StartIo*ルーチン、 [**HwStorStartIo**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/storport/nc-storport-hw_startio)します。 システムの呼び出し、Storport の I/O モデルで*HwStorBuildIo*ミニポート ドライバーの呼び出しの直前*HwStorStartIo*ルーチンと、多くの処理可能な限りがあります。 この方法は、ために CPU サイクルと、デバイスの拡張機能などの重要なシステムの構造体へのアクセスの競合を回避できます*HwStorBuildIo*低い IRQL でを実行し、同期ロックを保持していません。

*HwStorBuildIo*より便利なデータ構造を SRB の変換、スキャッター/ギャザーのリストを構築および他 SRB あたりの処理を実行する必要がありますルーチン。 実行中にロックがないため、 *HwStorBuildIo*ルーチン、ミニポート ドライバーにアクセスしない、SRB および SRB の拡張機能のそれ以外のデータ。 その部分を実行も他の構造体へのアクセスが、処理の一部の必要な場合、 *HwStartIo*ルーチン。

最大のパフォーマンスを実現するために、 *HwStorBuildIo*ルーチンは、全二重モードと組み合わせて使用する必要があります。

 

 




