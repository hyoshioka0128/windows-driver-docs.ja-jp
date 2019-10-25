---
title: Windows Vista と Windows XP 用の単一ドライバー
description: Windows Vista と Windows XP 用の単一ドライバー
ms.assetid: 3fa9c044-ab9d-4bed-b5fc-89396e1269ce
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1201153d40e55b3c0f520659a7d86aea8ba65e73
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840748"
---
# <a name="single-driver-for-windows-vista-and-windows-xp"></a>Windows Vista と Windows XP 用の単一ドライバー


Windows Vista と Windows XP の両方に対して1つのドライバーを使用することもできます。 このような場合、ドライバーはフラグをチェックすることによってデータ転送を処理します。 ストリームベースの転送に対して[**IWiaMiniDrv::D rvacquireitemdata**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvacquireitemdata)が呼び出されると、 *LFLAGS*パラメーターは WIA\_MINIDRV\_transfer\_DOWNLOAD または WIA\_MINIDRV\_transfer\_UPLOAD のいずれかに設定されます。 これらのビットのいずれも設定されていない場合、転送は*従来*の転送であり、ドライバーは Windows XP データ転送用に記載されている動作に従う必要があります。

 

 




