---
title: ダイレクト I/O を使用した DispatchReadWrite
description: ダイレクト I/O を使用した DispatchReadWrite
ms.assetid: 5174fe1f-aee5-4c8a-87a1-7f185ed4e242
keywords:
- DispatchReadWrite ルーチン
- ディスパッチ ルーチンの WDK カーネル、DispatchReadWrite ルーチン
- 読み取り/書き込みディスパッチ ルーチン WDK カーネル
- IRP_MJ_WRITE I/O 関数のコード
- IRP_MJ_READ I/O 関数のコード
- データ転送の WDK カーネル、読み取り/書き込みディスパッチ ルーチン
- データ転送の WDK カーネル、読み取り/書き込みディスパッチ ルーチン
- ダイレクト I/O WDK カーネル
- I/O WDK カーネルでは、ダイレクト I/O
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: c1b2f72145086b17d8f7a78b18f256503e17f1ec
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63387190"
---
# <a name="dispatchreadwrite-using-direct-io"></a>ダイレクト I/O を使用した DispatchReadWrite





MDL によって定義されたシステム物理メモリのデバイスからのダイレクト I/O では、読み取り要求を満たすデータを返すことによって、そのデバイス オブジェクトを設定する下位レベルのデバイス ドライバーに転送された**Irp-&gt;MdlAddress**. そのデバイスを物理メモリをシステムからデータを転送して、書き込み要求を満たします。

下位レベルのドライバーでは、非同期的に読み取り/書き込み要求を処理する必要があります。 そのため、すべて低いレベルのドライバーの[ *DispatchReadWrite* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)ルーチンに渡す必要があります[ **IRP\_MJ\_読み取り**](https://msdn.microsoft.com/library/windows/hardware/ff550794)と[ **IRP\_MJ\_書き込み**](https://msdn.microsoft.com/library/windows/hardware/ff550819) 」の説明に従って、その他のドライバー ルーチンに有効なパラメーターで Irp[ドライバー ダウン Irp を渡すスタック](passing-irps-down-the-driver-stack.md)します。

下位レベルのドライバーに送信される Irp を読み取り/書き込み、ページの物理メモリの説明で MDL によって**Irp -&gt;MdlAddress**要求された転送を実行する適切なアクセス権を調査が既にあり既にロックされたチェーンの最上位レベルのドライバーまたは I/O マネージャー。 ダイレクト I/O は呼び出さないでくださいのデバイス オブジェクトを設定する中間または最下位レベルのドライバー [ **MmProbeAndLockPages** ](https://msdn.microsoft.com/library/windows/hardware/ff554664)が既に実行されているためです。 最下位レベルのドライバーは呼び出し[ **MmGetSystemAddressForMdlSafe**](https://msdn.microsoft.com/library/windows/hardware/ff554559)します。 (Windows 98 用のドライバーを呼び出す[ **MmGetSystemAddressForMdl** ](https://msdn.microsoft.com/library/windows/hardware/ff554556)代わりにします。 Windows Me、Windows 2000 および Windows の以降のバージョンのドライバーを使用する必要があります**MmGetSystemAddressForMdlSafe**)。

中間または最下位レベルのデバイス ドライバーの*DispatchReadWrite*ルーチンは有効な Irp のみを渡すためのより高度なドライバーを信頼できない場合、I/O スタックの場所の読み取り/書き込みの Irp では、パラメーターを検証する必要がありますパラメーター。 場合、 *DispatchReadWrite*ルーチン パラメーター エラーを検出、適切なエラー状態で IRP を完了する必要があります\_*XXX* 」で既に説明した[完了Irp](completing-irps.md)します。 パラメーターが、有効な場合、中間ドライバー *DispatchReadWrite*ルーチンのガイドラインに従って、さらに処理するため要求を転送する必要があります[Higher-Level ドライバーDispatchReadWrite](dispatchreadwrite-in-higher-level-drivers.md).

最下位レベルのデバイス ドライバーの*DispatchReadWrite*ルーチンを呼び出す必要があります[ **IoMarkIrpPending** ](https://msdn.microsoft.com/library/windows/hardware/ff549422)転送要求を渡す IRP さらに他の処理ドライバーのルーチン、および状態の戻り値\_」の説明に従って、PENDING[ドライバー スタックを渡して Irp](passing-irps-down-the-driver-stack.md)します。

なお、デバイス ドライバーの*DispatchReadWrite*ルーチンを Irp は呼び出すことによってキューの高速な I/O スループットは、そのデバイスには、順序を制御できます[ **IoStartPacket** ](https://msdn.microsoft.com/library/windows/hardware/ff550370)ドライバー決定で*キー*値。 ドライバーで他のルーチンは IRP を後でキューから要求された長さは部分的な転送操作では、分割する必要があるかどうかを判断します、およびデータを転送するデバイスのプログラムします。

一般に、デバイス ドライバをそのデバイスの制限事項に合わせて大規模な転送要求を分割する必要がありますでは、特定の転送要求のデバイスをセットアップする前にまでこれらの操作を延期する必要があります。 このようなデバイス ドライバーの*DispatchReadWrite*ルーチンがなく、I/O スタックの場所を確認したデバイスに固有の転送制約の Irp を受信されない場合に、ドライバーが、部分的な転送の範囲を計算しようとしています。直前まで、これらのチェックを延期その[ *StartIo* ](https://msdn.microsoft.com/library/windows/hardware/ff563858) (またはその他のドライバーのルーチンの) 転送操作のデバイスをプログラムします。

 

 




