---
title: ドライバーをシングル for Windows Vista および Windows XP
description: ドライバーをシングル for Windows Vista および Windows XP
ms.assetid: 3fa9c044-ab9d-4bed-b5fc-89396e1269ce
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3edbdf8a89adf63f0270e561755597c2d1ceb724
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56553690"
---
# <a name="single-driver-for-windows-vista-and-windows-xp"></a>ドライバーをシングル for Windows Vista および Windows XP


Windows Vista と Windows XP 用に 1 つのドライバーをする可能性があります。 このような状況では、ドライバーは、フラグをチェックして、データ転送を処理します。 ときに[ **IWiaMiniDrv::drvAcquireItemData** ](https://msdn.microsoft.com/library/windows/hardware/ff543956)ストリーム ベースの転送が呼び出されると、 *lFlags* WIA のどちらかにパラメーターが設定されている\_MINIDRV\_転送\_ダウンロードまたは WIA\_MINIDRV\_転送\_をアップロードします。 転送は、これらのビットのどちらも設定されている場合、*レガシ*転送と、ドライバーが Windows XP のデータ転送に記載されている動作に従う必要があります。

 

 




