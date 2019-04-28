---
title: Windows Vista と Windows XP 用の単一ドライバー
description: Windows Vista と Windows XP 用の単一ドライバー
ms.assetid: 3fa9c044-ab9d-4bed-b5fc-89396e1269ce
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3edbdf8a89adf63f0270e561755597c2d1ceb724
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63367886"
---
# <a name="single-driver-for-windows-vista-and-windows-xp"></a>Windows Vista と Windows XP 用の単一ドライバー


Windows Vista と Windows XP 用に 1 つのドライバーをする可能性があります。 このような状況では、ドライバーは、フラグをチェックして、データ転送を処理します。 ときに[ **IWiaMiniDrv::drvAcquireItemData** ](https://msdn.microsoft.com/library/windows/hardware/ff543956)ストリーム ベースの転送が呼び出されると、 *lFlags* WIA のどちらかにパラメーターが設定されている\_MINIDRV\_転送\_ダウンロードまたは WIA\_MINIDRV\_転送\_をアップロードします。 転送は、これらのビットのどちらも設定されている場合、*レガシ*転送と、ドライバーが Windows XP のデータ転送に記載されている動作に従う必要があります。

 

 




