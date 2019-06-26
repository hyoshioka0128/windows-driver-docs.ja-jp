---
title: Windows Vista と Windows XP 用の単一ドライバー
description: Windows Vista と Windows XP 用の単一ドライバー
ms.assetid: 3fa9c044-ab9d-4bed-b5fc-89396e1269ce
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6c8df16e228eed7b90bdc8d800addebf625aeaf5
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67386909"
---
# <a name="single-driver-for-windows-vista-and-windows-xp"></a>Windows Vista と Windows XP 用の単一ドライバー


Windows Vista と Windows XP 用に 1 つのドライバーをする可能性があります。 このような状況では、ドライバーは、フラグをチェックして、データ転送を処理します。 ときに[ **IWiaMiniDrv::drvAcquireItemData** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvacquireitemdata)ストリーム ベースの転送が呼び出されると、 *lFlags* WIA のどちらかにパラメーターが設定されている\_MINIDRV\_転送\_ダウンロードまたは WIA\_MINIDRV\_転送\_をアップロードします。 転送は、これらのビットのどちらも設定されている場合、*レガシ*転送と、ドライバーが Windows XP のデータ転送に記載されている動作に従う必要があります。

 

 




