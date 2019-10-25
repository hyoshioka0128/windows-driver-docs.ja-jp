---
title: IRP_MJ_CREATE 操作での追加作成パラメーターの使用
description: IRP_MJ_CREATE 操作での追加作成パラメーターの使用
ms.assetid: e32aeec6-1a0a-4d21-8358-89d9fc0a15eb
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9db0913111c33f163e8e07004df19a49ce7102f7
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840939"
---
# <a name="using-extra-create-parameters-with-an-irp_mj_create-operation"></a>IRP\_MJ\_CREATE 操作で追加の Create Parameters を使用する


オペレーティングシステムのコンポーネントでは、追加の作成パラメーター (ECPs) を使用して、ファイルの[**IRP\_MJ\_create**](https://docs.microsoft.com/windows-hardware/drivers/ifs/irp-mj-create)操作に追加情報を関連付けます。 また、ドライバーは、次の状況で、ECPs を使用して、ファイルに対する IRP\_MJ\_CREATE 操作に追加情報を処理したり、関連付けたりすることもできます。

-   カーネルモードドライバーが[**FltCreateFileEx2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltcreatefileex2)または[**IoCreateFileEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-iocreatefileex)ルーチンを呼び出してファイルを作成または開くとき

-   ファイルシステムフィルタードライバーが、ファイルの[**IRP\_MJ\_作成**](https://docs.microsoft.com/windows-hardware/drivers/ifs/irp-mj-create)操作を処理するとき

以下のセクションでは、ECPs を定義、アタッチ、および使用する方法について説明します。 次のセクションでは、オペレーティングシステムで定義されている ECPs についても説明します。

[カーネルモードドライバーが開始する操作を作成するために ECPs を IRP\_MJ にアタッチ\_](attaching-ecps-to-irp-mj-create-operations-that-a-kernel-mode-driver-o.md)

[ECPs を使用して IRP\_MJ を処理し\_ファイルシステムフィルタードライバーで操作を作成する](using-ecps-to-process-irp-mj-create-operations-in-a-file-system-filter.md)

[ユーザー定義の ECPs](user-defined-ecps.md)

[システム定義の ECPs](system-defined-ecps.md)

 

 




