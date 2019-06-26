---
title: IRP_MJ_CREATE 操作での追加作成パラメーターの使用
description: IRP_MJ_CREATE 操作での追加作成パラメーターの使用
ms.assetid: e32aeec6-1a0a-4d21-8358-89d9fc0a15eb
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f529755102f85ed4e142d2d1a76de2347e4dcab3
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67380269"
---
# <a name="using-extra-create-parameters-with-an-irpmjcreate-operation"></a>IRP のパラメーターを作成する余分なを使用して\_MJ\_作成操作


追加のオペレーティング システムの使用のコンポーネントで追加情報を関連付けるには、(ECPs) のパラメーターを作成、 [ **IRP\_MJ\_作成**](https://docs.microsoft.com/windows-hardware/drivers/ifs/irp-mj-create)ファイルを操作します。 ドライバーの処理または追加情報を関連付ける IRP ECPs を使用できますも\_MJ\_次の状況でファイルを作成する操作。

-   カーネル モード ドライバーを呼び出すと、 [ **FltCreateFileEx2** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltcreatefileex2)または[ **IoCreateFileEx** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/nf-ntddk-iocreatefileex)ルーチンを作成するか、ファイルを開きます

-   ファイル システム フィルター ドライバーを処理すると、 [ **IRP\_MJ\_作成**](https://docs.microsoft.com/windows-hardware/drivers/ifs/irp-mj-create)ファイルの操作

次のセクションでは、定義、アタッチ、および ECPs を使用する方法について説明します。 次のセクションには、オペレーティング システム定義の ECPs もについて説明します。

[IRP への ECPs\_MJ\_作成操作、カーネル モード ドライバーで発生しました。](attaching-ecps-to-irp-mj-create-operations-that-a-kernel-mode-driver-o.md)

[ECPs を使用して、IRP を処理する\_MJ\_作成操作、ファイル システム フィルター ドライバー](using-ecps-to-process-irp-mj-create-operations-in-a-file-system-filter.md)

[ユーザー定義の ECPs](user-defined-ecps.md)

[システム定義の ECPs](system-defined-ecps.md)

 

 




