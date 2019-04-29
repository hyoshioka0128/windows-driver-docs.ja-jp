---
title: 読み取り/書き込みディスパッチ ルーチンの概要
description: 読み取り/書き込みディスパッチ ルーチンの概要
ms.assetid: 2ab1cde7-89e8-449f-b2a0-12aa0762ebf3
keywords:
- DispatchRead ルーチン
- DispatchWrite ルーチン
- DispatchReadWrite ルーチン
- ディスパッチ ルーチンの WDK カーネル、DispatchReadWrite ルーチン
- ディスパッチ ルーチンの WDK カーネル、DispatchWrite ルーチン
- ディスパッチ ルーチンの WDK カーネル、DispatchRead ルーチン
- 読み取り/書き込みディスパッチ ルーチン WDK カーネル
- IRP_MJ_WRITE I/O 関数のコード
- IRP_MJ_READ I/O 関数のコード
- データ転送の WDK カーネル、読み取り/書き込みディスパッチ ルーチン
- データ転送の WDK カーネル、読み取り/書き込みディスパッチ ルーチン
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 50967db82177f76da45908b461d4701f2b646eb6
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63331933"
---
# <a name="summary-of-readwrite-dispatch-routines"></a>読み取り/書き込みディスパッチ ルーチンの概要





実装する場合、次の点を留意してください、 [ *DispatchRead*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)、 [ *DispatchWrite*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)、または[ *DispatchReadWrite* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)ルーチン。

-   受信した読み取り/書き込み Irp の IRP で、[次へ] の下位レベルのドライバーの I/O スタックの場所を設定する前に有効性のパラメーターをチェックする階層型のドライバーのチェーンの最上位レベルのドライバーの役目です。

-   一般に、中間および最下位レベルのドライバーは有効なパラメーターでの転送要求を渡す、チェーン内の最上位レベルのドライバーを使用できます。 ただし、ドライバーは、I/O スタックの場所、IRP ので、パラメーターの正当性チェックを実行できるし、各デバイス ドライバーのデバイスによって課せられる制限に違反する可能性がありますの条件のパラメーターを確認する必要があります。

-   場合、 *DispatchReadWrite*ルーチンがエラーでは IRP を完了すると、I/O スタックの場所を設定する必要がある**状態**NTSTATUS 型の適切な値を持つメンバーの設定、 **情報**メンバー 0、および呼び出す[ **IoCompleteRequest** ](https://msdn.microsoft.com/library/windows/hardware/ff548343) IRP と*PriorityBoost* IO の\_いいえ\_増分値です。

-   ドライバーは、バッファー内の I/O を使用している場合、転送されるデータを格納する構造体を定義する必要があり、いくつかのこれらの構造を内部的にバッファーする必要があります。

-   確認する必要がありますが、ドライバーは、ダイレクト I/O を使用している場合かどうかに MDL **Irp -&gt;MdlAddress**転送が 1 回で処理するために、基になるデバイスのデータが多すぎる (または多数の改ページ) を格納するバッファーをについて説明します。操作です。 そうである場合、ドライバーが小さな転送操作のシーケンスには、元の転送要求を分割する必要があります。

    密接に結合されたクラス ドライバーを分割で要求する可能性があります、 *DispatchReadWrite*その基になるポート ドライバーの日常的な。 SCSI クラス ドライバーでは、特に、大容量記憶装置の場合は、これを行う必要があります。 SCSI ドライバーの要件の詳細については、次を参照してください。[記憶装置ドライバー](https://msdn.microsoft.com/library/windows/hardware/ff566976)します。

-   低レベル デバイス ドライバーの*DispatchReadWrite*ルーチンが他のドライバー ルーチン デキュー IRP が転送用にデバイスを設定するまで、部分的な転送に大きな転送要求を分割を延期する必要があります。

-   下位レベルのデバイス ドライバーは、読み取り/書き込み IRP を独自のルーチンによってさらに処理キューで場合、呼び出す必要があります[ **IoMarkIrpPending** ](https://msdn.microsoft.com/library/windows/hardware/ff549422) IRP をキューに配置する前にします。 *DispatchReadWrite*ルーチンも状態を持つコントロールを返す必要があります\_このような状況で保留されます。

-   場合、 *DispatchReadWrite*ルーチンに下位のドライバーは IRP を通過する、次の下位 IRP がドライバーの I/O スタックの場所を設定する必要があります。 高度なドライバーも設定するかどうか、 [ *IoCompletion* ](https://msdn.microsoft.com/library/windows/hardware/ff548354)で渡す前に IRP の日常的な[**保留**](https://msdn.microsoft.com/library/windows/hardware/ff548336)その下にある階層化されたドライバーの設計に依存します。

    ただしより高度なドライバーを呼び出す必要があります[ **IoSetCompletionRoutine** ](https://msdn.microsoft.com/library/windows/hardware/ff549679)を呼び出す前に[**保留**](https://msdn.microsoft.com/library/windows/hardware/ff548336)いずれかを割り当てる場合Irp やメモリなどのリソース。 その*IoCompletion*下位のドライバーでは、要求をする前に完了した場合に、ルーチンはドライバーによって割り当てられたリソースを解放する必要があります、 *IoCompletion*ルーチンの呼び出し[ **IoCompleteRequest** ](https://msdn.microsoft.com/library/windows/hardware/ff548343)元 IRP にします。

-   基になるリムーバブル メディア デバイス ドライバーを含む場合がある下位のドライバーのより高度なドライバーが Irp を割り当てると、割り当て、ドライバーは割り当てる各 IRP のスレッド コンテキストを確立する必要があります。

 

 




