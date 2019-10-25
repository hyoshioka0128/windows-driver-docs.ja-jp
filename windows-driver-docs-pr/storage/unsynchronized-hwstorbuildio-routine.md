---
title: 同期されていない HwStorBuildIo ルーチン
description: 同期されていない HwStorBuildIo ルーチン
ms.assetid: 6b18e3ff-30dd-414b-99b5-4bb914660a67
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c4a4c44f53a39f8059718ad4c08b0782a92920a5
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844441"
---
# <a name="unsynchronized-hwstorbuildio-routine"></a>同期されていない HwStorBuildIo ルーチン


## <span id="ddk_unsynchronized_hwstorbuildio_routine_kg"></span><span id="DDK_UNSYNCHRONIZED_HWSTORBUILDIO_ROUTINE_KG"></span>


SCSI ポートミニポートドライバーの i/o モデルでは、ミニポートドライバーの[**StartIo**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_startio)ルーチン[**HWSCSISTARTIO**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff557323(v=vs.85))は、Scsi 要求ブロック (SRBs) をできるだけ早くハードウェアに送信する必要があります。 これは必須です。これは、割り込みが無効になり、IRQL = ディスパッチ\_レベルでは、ミニポートドライバーの*StartIo*ルーチンで行われる処理が実行されるためです。 残念ながら、このモデルは、一部の高パフォーマンスホストバスアダプター (Hba) のドライバーには適していません。これは、i/o を開始するときに、これらの Hba のミニポートドライバーが大量の処理を行う必要があるためです。 ミニポートドライバーが*StartIo*ルーチンでこの処理を実行すると、システムのパフォーマンスが低下します。

Storport i/o モデルは、ミニポートドライバーの*StartIo*ルーチン[**HwStorStartIo**](https://docs.microsoft.com/windows-hardware/drivers/ddi/storport/nc-storport-hw_startio)から処理負荷の一部を削除するために、 [**HwStorBuildIo**](https://docs.microsoft.com/windows-hardware/drivers/ddi/storport/nc-storport-hw_buildio)ルーチンをサポートしています。 Storport i/o モデルでは、システムはミニポートドライバーの*HwStorStartIo*ルーチンを呼び出す直前に*HwStorBuildIo*を呼び出し、そこでできるだけ多くの処理を行います。 この方法では、 *HwStorBuildIo*が低い IRQL で実行され、同期ロックが保持されないため、CPU サイクルの競合や、デバイス拡張機能などの重要なシステム構造へのアクセスを回避できます。

*HwStorBuildIo*ルーチンは、SRB をより便利なデータ構造に変換し、スキャッター/ギャザーリストを構築し、その他の SRB ごとの処理を実行します。 *HwStorBuildIo*ルーチンの実行中にロックが保持されないため、ミニポートドライバーは、SRB および SRB 拡張機能以外のデータにアクセスしないようにする必要があります。 処理の一部に他の構造体へのアクセスが必要な場合、その部分は*HwStartIo*ルーチンでも実行する必要があります。

最大のパフォーマンスを実現するには、 *HwStorBuildIo*ルーチンを全二重モードと組み合わせて使用する必要があります。

 

 




