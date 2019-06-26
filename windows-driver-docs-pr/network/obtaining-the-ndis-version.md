---
title: NDIS バージョンの取得
description: NDIS バージョンの取得
ms.assetid: f7bbd11c-b6ec-4adb-8c42-ec438d518ed8
keywords:
- WDK、NDIS バージョンについては、オペレーティング システムのバージョンとの比較
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7ae668097acb96772b3918536e022613aa923dbd
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67354503"
---
# <a name="obtaining-the-ndis-version"></a>NDIS バージョンの取得





バージョンの NDIS では、オペレーティング システムのバージョンと同じである可能性がありますされません。 たとえば、使用する場合、 [**ために RtlGetVersion** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-rtlgetversion)と[ **RtlVerifyVersionInfo** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-rtlverifyversioninfo)オペレーティング システムのバージョンを取得するためのルーチン操作を行う特定の NDIS バージョンで保証されたアソシエーションを取得できません。 したがって、NDIS ドライバーする必要がありますを取得、NDIS バージョンとオペレーティング システムのバージョンとは別にします。 NDIS ドライバーで NDIS バージョンを取得できます、 [ **NdisGetVersion** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisgetversion)関数。

## <a name="related-topics"></a>関連トピック


[NDIS のバージョンの概要](overview-of-ndis-versions.md)

[NDIS バージョン情報を指定します。](specifying-ndis-version-information.md)

 

 






