---
title: DispatchSetInformation ルーチン
description: DispatchSetInformation ルーチン
ms.assetid: 9fb56504-32a7-47b0-b731-df1dc74ce861
keywords:
- ディスパッチルーチン WDK カーネル、DispatchSetInformation ルーチン
- DispatchSetInformation ルーチン
- 情報ディスパッチルーチン WDK カーネルを設定する
- IRP_MJ_SET_INFORMATION i/o 関数のコード
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: cb899ab163f1fdef95e31e2c6d9d967e6a7a2998
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72836832"
---
# <a name="dispatchsetinformation-routines"></a>DispatchSetInformation ルーチン





ドライバーの[*DispatchSetInformation*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)ルーチンは、\_情報 i/o 関数コード\_設定された[**irp\_MJ**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-set-information)の irp を処理します。 この i/o 関数コードに対するドライバーのサポートは省略可能であり、通常は上位レベルまたはファイルシステムのドライバーで表示されます。 この要求は、i/o マネージャーと他のオペレーティングシステムコンポーネント、およびその他のカーネルモードドライバーによって送信されます。 たとえば、ユーザーモードアプリケーションが[**Setendoffile**](https://docs.microsoft.com/windows/desktop/api/fileapi/nf-fileapi-setendoffile)を呼び出し、カーネルモードコンポーネントが[**Zwsetinformationfile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-ntsetinformationfile)を呼び出すときに送信されます。

 

 




