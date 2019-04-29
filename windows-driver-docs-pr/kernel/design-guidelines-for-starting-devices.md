---
title: デバイスの開始に関する設計ガイドライン
description: デバイスの開始に関する設計ガイドライン
ms.assetid: fbdde107-f3a5-4713-a4ac-1c9bafa3c634
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: a82ff0a188147bbe034728fc2a372b7069948182
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63388185"
---
# <a name="design-guidelines-for-starting-devices"></a>デバイスの開始に関する設計ガイドライン





-   PnP マネージャーが失敗するまで、デバイスの要求の作成、 [ **IRP\_MN\_開始\_デバイス**](https://msdn.microsoft.com/library/windows/hardware/ff551749) IRP が完了したことを示すデバイスのすべてのドライバー開始操作を実行しています。

-   [ *DispatchPnP* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch) IRQL パッシブにシステム スレッドのコンテキストで実行されるルーチン\_レベルでメモリが割り当てられた[ **exallocatepoolwithtag に** ](https://msdn.microsoft.com/library/windows/hardware/ff544520)ドライバーがシステムのページング ファイルを保持するデバイスを制御しない限り、ページ プールからの初期化中にのみ使用があることができます。 このようなメモリの割り当てを解放する必要があります[ **ExFreePool** ](https://msdn.microsoft.com/library/windows/hardware/ff544590)する前に、 *DispatchPnP*ルーチンは、コントロールを返します。

-   WDM デバイス ドライバーの ISR でのデバイスのスタートアップ中にも不正な割り込みで呼び出されたかどうかを決定できる必要があります。 呼び出しから返された場合[ **IoConnectInterrupt** ](https://msdn.microsoft.com/library/windows/hardware/ff548371)を処理するコード パスで**IRP\_MN\_開始\_デバイス**、ISR呼び出せるすぐに割り込みがデバイスで有効な場合です。

 

 




