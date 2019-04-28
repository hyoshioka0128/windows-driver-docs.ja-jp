---
title: 中間ドライバーでの IRP の設定
description: 中間ドライバーでの IRP の設定
ms.assetid: 0d04a951-a68e-4fa1-bdc6-dd92ec49deae
keywords:
- リムーバブル メディア WDK カーネルでは、中間ドライバー Irp
- 中間ドライバー WDK の Irp のリムーバブル メディア
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: cc848103b57c6c6b52c96c89c88c452004c5375e
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63367867"
---
# <a name="setting-up-irps-in-intermediate-drivers"></a>中間ドライバーでの IRP の設定





ファイル システム ドライバーとリムーバブル メディア デバイス ドライバーの間に階層化された中間ドライバーは、Irp で、[次へ] の下位レベルのドライバーの I/O スタックの場所を設定する必要があります。 着信から[ **IRP\_MJ\_読み取り**](https://msdn.microsoft.com/library/windows/hardware/ff550794)、 [ **IRP\_MJ\_書き込み**](https://msdn.microsoft.com/library/windows/hardware/ff550819)と[ **IRP\_MJ\_デバイス\_コントロール**](https://msdn.microsoft.com/library/windows/hardware/ff550744)を要求する中間のドライバーが、自身の I/O スタックの場所にコピーする必要があります**フラグ** 、下位レベルの次のドライバーの I/O に下位のドライバーの I/O スタックの場所を設定するときに場所をスタックします。

中間のドライバーが下位のリムーバブル メディアのドライバーの新しい Irp を割り当てた場合、それらの Irp をよう設定する必要があります。

-   転送の要求の設定があります各ドライバーに割り当てられた IRP のスレッド コンテキストにある値から**Tail.Overlay.Thread**元の IRP でします。

-   **IRP\_MJ\_読み取り**、 **IRP\_MJ\_書き込み**、および**IRP\_MJ\_デバイス\_コントロール**要求すると、I/O スタックの場所をコピーする必要があります**フラグ**各ドライバーに割り当てられた IRP を元の IRP から。

それ以外の場合、ファイル システムはキャッシュされたファイル データの整合性を維持することも原因ユーザーに、開いているファイルを保持するメディアを再マウントするように求められます。

 

 




