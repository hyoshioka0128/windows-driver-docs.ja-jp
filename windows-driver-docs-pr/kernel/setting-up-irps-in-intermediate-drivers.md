---
title: 中間ドライバーでの IRP の設定
description: 中間ドライバーでの IRP の設定
ms.assetid: 0d04a951-a68e-4fa1-bdc6-dd92ec49deae
keywords:
- リムーバブル メディア WDK カーネルでは、中間ドライバー Irp
- 中間ドライバー WDK の Irp のリムーバブル メディア
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: d7813993310450bc1fb2947f5aa895e96eeac7bb
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67371238"
---
# <a name="setting-up-irps-in-intermediate-drivers"></a>中間ドライバーでの IRP の設定





ファイル システム ドライバーとリムーバブル メディア デバイス ドライバーの間に階層化された中間ドライバーは、Irp で、[次へ] の下位レベルのドライバーの I/O スタックの場所を設定する必要があります。 着信から[ **IRP\_MJ\_読み取り**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-read)、 [ **IRP\_MJ\_書き込み**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-write)と[ **IRP\_MJ\_デバイス\_コントロール**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-device-control)を要求する中間のドライバーが、自身の I/O スタックの場所にコピーする必要があります**フラグ** 、下位レベルの次のドライバーの I/O に下位のドライバーの I/O スタックの場所を設定するときに場所をスタックします。

中間のドライバーが下位のリムーバブル メディアのドライバーの新しい Irp を割り当てた場合、それらの Irp をよう設定する必要があります。

-   転送の要求の設定があります各ドライバーに割り当てられた IRP のスレッド コンテキストにある値から**Tail.Overlay.Thread**元の IRP でします。

-   **IRP\_MJ\_読み取り**、 **IRP\_MJ\_書き込み**、および**IRP\_MJ\_デバイス\_コントロール**要求すると、I/O スタックの場所をコピーする必要があります**フラグ**各ドライバーに割り当てられた IRP を元の IRP から。

それ以外の場合、ファイル システムはキャッシュされたファイル データの整合性を維持することも原因ユーザーに、開いているファイルを保持するメディアを再マウントするように求められます。

 

 




