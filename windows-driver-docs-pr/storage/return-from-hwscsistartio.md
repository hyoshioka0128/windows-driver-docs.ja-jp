---
title: HwScsiStartIo からの戻り値
description: HwScsiStartIo からの戻り値
ms.assetid: e3d5e21a-4dc2-41bf-97a2-9ac2aa5a1af2
keywords:
- SCSI ミニポート ドライバー WDK ストレージ、HwScsiStartIo
- HwScsiStartIo
- WDK SCSI の値を返す
- 状態値は WDK SCSI
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a8c57e337946cd1fd902b43fee19dfcb74266307
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63325290"
---
# <a name="return-from-hwscsistartio"></a>HwScsiStartIo からの戻り値


## <span id="ddk_return_from_hwscsistartio_kg"></span><span id="DDK_RETURN_FROM_HWSCSISTARTIO_KG"></span>


すべて[ **HwScsiStartIo** ](https://msdn.microsoft.com/library/windows/hardware/ff557323)ルーチンを返す必要があります**TRUE**、入力要求が処理されたことを示します。

場合、 *HwScsiStartIo*ルーチンは、呼び出されると、要求された操作を実行できない*HwScsiStartIo*次を実行する必要があります。

1.  セットの入力 SRB の**SrbStatus** SRB に\_状態\_ビジーです。

2.  呼び出す[ **ScsiPortNotification** ](https://msdn.microsoft.com/library/windows/hardware/ff564657)で、 *NotificationType * * * RequestComplete** SRB の入力を使用しています。

3.  呼び出す**ScsiPortNotification**で、 *NotificationType * * * NextRequest** だけ完了 SRB 場合は、ドライバーは、のものと異なるターゲット論理ユニットに要求を受け入れることができます。

4.  返す**TRUE**します。

と共に返されるすべての要求ポートのドライバーを再送信、 **SrbStatus**値 SRB\_状態\_ミニポート ドライバーのビジー *HwScsiStartIo*ルーチンを後で。

最終的には、すべてのミニポート ドライバーを呼び出す必要があります**ScsiPortNotification**に SRB 入力のそれぞれに対して 2 回その*HwScsiStartIo*ルーチン: 最初に、要求を完了する (*NotificationType ***RequestComplete**) とを呼び出すポート ドライバーに指示する、2 番目、 *HwScsiStartIo*次 SRB を使用して日常的な (* NotificationType ***NextRequest**または**NextLuRequest**)。

*HwScsiStartIo*ポーリング呼び出し専用の HBA を管理するミニポート ドライバーの日常的な**ScsiPortNotification**で、 *NotificationType * * * RequestTimerCall** へのポインター、 *HwScsiTimer*ルーチン。 詳細については、 *HwScsiTimer*ルーチンを参照してください[SCSI ミニポート ドライバー HwScsiTimer ルーチン](scsi-miniport-driver-s-hwscsitimer-routine.md)します。

 

 




