---
title: DispatchRead、DispatchWrite、DispatchReadWrite ルーチン
description: DispatchRead、DispatchWrite、DispatchReadWrite ルーチン
ms.assetid: 2982939a-4afb-4b21-9a96-0ac758f0fb6c
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
ms.openlocfilehash: c29c3d97b5b080923c38f399823f5e9693701f45
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56570207"
---
# <a name="dispatchread-dispatchwrite-and-dispatchreadwrite-routines"></a>DispatchRead、DispatchWrite、DispatchReadWrite ルーチン





ドライバーの[ *DispatchRead* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)と[ *DispatchWrite* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)ルーチンの I/O 関数のコードの Irp の処理[ **IRP\_MJ\_読み取り**](https://msdn.microsoft.com/library/windows/hardware/ff550794)と[ **IRP\_MJ\_書き込み**](https://msdn.microsoft.com/library/windows/hardware/ff550819)、それぞれします。 または、組み合わされた[ *DispatchReadWrite* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)ルーチンは、これらの I/O 関数コードの両方の Irp を処理できます。

コンピューターをシステムに転送元となるデータ デバイスのすべてのドライバーが必要、 *DispatchRead*ルーチン。 すべてのドライバーをシステムからデータを転送できるデバイスの必要があります、 *DispatchWrite*ルーチン。 双方向のデータを転送する任意のドライバーが組み合わされたことができますが*DispatchReadWrite*ルーチン。

下位レベルのドライバーが処理**IRP\_MJ\_読み取り**と**IRP\_MJ\_書き込み**非同期的に要求します。 そのため、 *DispatchRead*や*DispatchWrite*ルーチン最上位レベルのドライバーで渡す必要がありますこれらの要求さらに処理する、要求は、そのドライバーの有効なパラメーターを持っていれば、IRP の I/O スタックの場所。

バッファリングまたはダイレクト I/O のドライバーがそのデバイス オブジェクトを設定かどうかは、転送要求を処理する方法に影響します。 具体的には、DMA 操作を実行するダイレクト I/O を使用するドライバーが満たすために小さな転送操作のシーケンスに大きな転送要求を分割する必要があります、 **IRP\_MJ\_読み取り**または**IRP\_MJ\_書き込み**要求。 詳細については、[入力/出力手法](i-o-programming-techniques.md)を参照してください。

次のサブセクションでは、いくつかの設計と実装の考慮事項について説明します*DispatchReadWrite*ルーチン バッファー内の I/O と直接の I/O を使用する最下位レベルのデバイス ドライバーおよび上位レベルのドライバーそれらの上に配置します。

[転送を非同期的に処理します。](handling-transfers-asynchronously.md)

[バッファー内の I/O を使用して DispatchReadWrite](dispatchreadwrite-using-buffered-i-o.md)

[ダイレクト I/O を使用して DispatchReadWrite](dispatchreadwrite-using-direct-i-o.md)

[上位レベルのドライバーで DispatchReadWrite](dispatchreadwrite-in-higher-level-drivers.md)

[読み取り/書き込みディスパッチ ルーチンの概要](summary-of-read-write-dispatch-routines.md)

 

 




