---
title: バッファー付き I/O を使用した DispatchReadWrite
description: バッファー付き I/O を使用した DispatchReadWrite
ms.assetid: bb8ce47d-5722-4050-9492-bec154744597
keywords:
- DispatchReadWrite ルーチン
- ディスパッチ ルーチンの WDK カーネル、DispatchReadWrite ルーチン
- 読み取り/書き込みディスパッチ ルーチン WDK カーネル
- IRP_MJ_WRITE I/O 関数のコード
- IRP_MJ_READ I/O 関数のコード
- データ転送の WDK カーネル、読み取り/書き込みディスパッチ ルーチン
- データ転送の WDK カーネル、読み取り/書き込みディスパッチ ルーチン
- バッファー内の I/O の WDK カーネル
- バッファーの I/O の WDK カーネル
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 18d501237309b86db5779d690dd82bbbe0f96c6d
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67384973"
---
# <a name="dispatchreadwrite-using-buffered-io"></a>バッファー付き I/O を使用した DispatchReadWrite





任意の最下位レベルのデバイス ドライバーのデバイスを設定するオブジェクトのバッファー I/O が下のデバイスから、ロックされたに転送されたデータを返すことによって、読み取り要求を満たすシステム領域バッファー **Irp-&gt;AssociatedIrp.SystemBuffer**. そのデバイスに、同じバッファーからデータを転送して、書き込み要求を満たします。

その結果、 *DispatchReadWrite*このようなデバイス ドライバーのルーチンが譲渡要求の受信時に、次を通常は。

1.  呼び出し[ **IoGetCurrentIrpStackLocation** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iogetcurrentirpstacklocation)転送要求の方向を決定します。

2.  要求のパラメーターの有効性を確認します。

    -   読み取り要求をルーチンは、通常チェック、ドライバーの*IoStackLocation*-&gt;**Parameters.Read.Length**バッファーがするのに十分な大きさかどうかを決定する値デバイスから転送されたデータが表示されます。

        たとえば、システム キーボード クラス ドライバーは、Win32 のユーザー入力のスレッドからのみ取得する読み取り要求を処理します。 このドライバーは、キーボード、構造体を定義します\_入力\_デバイスから、特定の時点でキーを格納するためのデータが内部のリング バッファーに戻ったときに、読み取り要求を満たすためにいくつかのこれらの構造を保持する。でします。

    -   書き込み要求の場合、ルーチン、通常、値をチェックしますで**Parameters.Write.Length**とにデータをチェック**Irp -&gt;AssociatedIrp.SystemBuffer**の有効性のために必要な場合: は場合、そのデバイスは、定義されている値の範囲を持つメンバーを格納している唯一の構造化データ パケットを受け入れます。

3.  すべてのパラメーターが有効でない場合、 *DispatchReadWrite*ルーチンですぐに、既に説明されている IRP の完了[Irp の完了](completing-irps.md)します。 それ以外の場合、ルーチン IRP を渡す他のドライバー ルーチンによってさらに処理」の説明に従って[ドライバー スタックを渡して Irp](passing-irps-down-the-driver-stack.md)します。

最下位レベルのデバイスが、通常、バッファー内の I/O を使用するドライバーが要求の発信元がで指定された読み取りまたは書き込みのサイズのデータの転送要求を満たす必要があります。 このようなドライバーがデータの構造を定義する可能性が高いから、そのデバイスに送信されるやシステム キーボード クラス ドライバーは、内部的には、構造化データをバッファーに書き込む可能性があります。

データをバッファーに内部的にドライバーをサポートする必要があります[ **IRP\_MJ\_フラッシュ\_バッファー** ](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-flush-buffers)を要求して、サポートも[ **IRP\_MJ\_シャット ダウン**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-shutdown)要求。

チェーンの最上位レベルのドライバーは、通常の読み取り/書き込み要求を下位のドライバーに渡される前に入力 IRP のパラメーターをチェックします。 その結果、多くの低レベルのドライバーは、読み取り/書き込み IRP では、I/O スタックの場所は、有効なパラメーターであると想定できます。 チェーンの最下位レベルのドライバーがデータ転送のデバイス固有の制約の対応の場合は、そのドライバーが必要です、I/O スタックの場所では、パラメーターの有効性を確認します。

 

 




