---
title: 標準ドライバー ルーチンの要件
description: 標準ドライバー ルーチンの要件
ms.assetid: 49b382ad-c282-41d2-b8b3-68eca4e12b9c
keywords:
- 標準のドライバー ルーチン WDK カーネルの要件
- ドライバー ルーチン WDK カーネルの要件
- ルーチンの WDK カーネルの要件
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: cf8a7ddcc099410a4741f8ecb00040ef9721f68b
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63331962"
---
# <a name="standard-driver-routine-requirements"></a>標準ドライバー ルーチンの要件





カーネル モード ドライバーを設計するときに、次の点に注意してくださいにしてください。

-   各ドライバーが必要、 [ **DriverEntry** ](https://msdn.microsoft.com/library/windows/hardware/ff544113)ルーチンで、ドライバー レベルのデータ構造とリソースを初期化します。 I/O マネージャーの呼び出し、 **DriverEntry**ルーチン、ドライバーの読み込み時にします。

-   すべてのドライバーには、少なくとも 1 つのディスパッチ ルーチンを受け取って I/O 要求パケット (Irp) を処理する必要があります。 各ドライバーのディスパッチ ルーチンのエントリ ポイントを配置する必要があります、 [**ドライバー\_オブジェクト**](https://msdn.microsoft.com/library/windows/hardware/ff544174)構造体には、各[IRP の主な機能コード](https://msdn.microsoft.com/library/windows/hardware/ff550710)ドライバーができます。表示されます。 ドライバーには各 IRP の主な機能コードの別のディスパッチ ルーチンまたはいくつかの関数コードを処理する 1 つまたは複数のディスパッチ ルーチンことができます。

-   すべての WDM ドライバーが必要、 [*アンロード*](https://msdn.microsoft.com/library/windows/hardware/ff564886)ルーチン。 ドライバーを配置する必要があります、*アンロード*ドライバーのドライバー オブジェクトのルーチンのエントリ ポイント。 役割を[PnP ドライバーのアンロード ルーチン](pnp-driver-s-unload-routine.md)わずかですが、[非 PnP ドライバーのアンロード ルーチン](non-pnp-driver-s-unload-routine.md)ドライバーを使用しているすべてのシステム リソースを解放する必要があります。

-   すべての WDM ドライバーが必要、 *AddDevice*ドライバー オブジェクトの。 *AddDevice*ルーチンが作成を担当し、各 PnP デバイス ドライバーのコントロール オブジェクト、デバイスを初期化します。

-   ドライバーが持つことができます、 [ *StartIo* ](https://msdn.microsoft.com/library/windows/hardware/ff563858) 、日常的な I/O マネージャーが Irp の I/O 操作を開始するドライバーを呼び出しますがキューに登録するシステム提供の IRP キュー。 任意のドライバーがない、 *StartIo*そのディスパッチ ルーチン内のすべての IRP を完了する必要がありますまたはルーチンを設定し、受信 Irp の内部キューを管理する必要があります。 高度なドライバーがない、 *StartIo*ルーチン、単に渡される Irp 下位レベルのドライバーがディスパッチ ルーチンから直接場合。

-   特定のミニポート ドライバーとは、上記の要件の例外です。 デバイス固有の種類のドキュメントのミニポート ドライバーの要件については Windows Driver Kit (WDK) を参照してください。

-   その機能と (たとえば、かどうかと相互運用システムから提供されたドライバー) システムには、ドライバーの適合、ドライバーに他の種類の標準のルーチンが含まれているかどうかによって異なります。 詳細については、WDK で特定のデバイスの種類のドキュメントを参照してください。

 

 




