---
title: 追加のパラメーターの作成の概要
description: 追加のパラメーターの作成の概要
ms.assetid: e32aeec6-1a0a-4d21-8358-89d9fc0a15eb
ms.date: 10/16/2019
ms.localizationpriority: medium
ms.openlocfilehash: 06e6d4f7265eb3e688af1f1e6ddea105720d169c
ms.sourcegitcommit: 2a1c24db881ed843498001493c3ce202c9aa03f1
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/16/2019
ms.locfileid: "74135162"
---
# <a name="introduction-to-extra-create-parameters"></a>追加のパラメーターの作成の概要

追加のパラメーター (ECPs) は、ファイルの作成に関する追加情報を含むことができる構造体です。 作成操作には、任意の数の ECPs を含めることができます。これは、ECP_LIST を使用してアタッチされます。 オペレーティングシステムコンポーネントでは、ECPs を使用して、ファイルの[**IRP_MJ_CREATE**](https://docs.microsoft.com/windows-hardware/drivers/ifs/irp-mj-create)操作に追加情報を関連付けます。

また、ドライバーは、次の状況で、ECPs を使用して、追加情報を処理したり、ファイルの IRP_MJ_CREATE 操作に関連付けたりすることもできます。

- カーネルモードドライバーが[**FltCreateFileEx2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltcreatefileex2)または[**IoCreateFileEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/nf-ntddk-iocreatefileex)ルーチンを呼び出してファイルを作成または開くとき

- ファイルシステムフィルタードライバーがファイルの[**IRP_MJ_CREATE**](https://docs.microsoft.com/windows-hardware/drivers/ifs/irp-mj-create)操作を処理する場合

以下のセクションでは、ECPs を定義、アタッチ、および使用する方法について説明します。 次のセクションでは、オペレーティングシステムで定義されている ECPs についても説明します。

[カーネルモードドライバーが開始した IRP_MJ_CREATE 操作への ECPs のアタッチ](attaching-ecps-to-irp-mj-create-operations-that-a-kernel-mode-driver-o.md)

[ECPs を使用したファイルシステムの IRP_MJ_CREATE 操作の処理ミニフィルター](using-ecps-to-process-irp-mj-create-operations-in-a-file-system-minifilter.md)

[ユーザー定義の ECPs](user-defined-ecps.md)

[システム定義の ECPs](system-defined-ecps.md)
