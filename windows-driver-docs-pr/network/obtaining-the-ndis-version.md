---
title: NDIS 版を入手します。
description: NDIS 版を入手します。
ms.assetid: f7bbd11c-b6ec-4adb-8c42-ec438d518ed8
keywords:
- WDK、NDIS バージョンについては、オペレーティング システムのバージョンとの比較
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: be779b52198253d9acc8bc7292c9d9169c25861d
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56553757"
---
# <a name="obtaining-the-ndis-version"></a>NDIS 版を入手します。





バージョンの NDIS では、オペレーティング システムのバージョンと同じである可能性がありますされません。 たとえば、使用する場合、 [**ために RtlGetVersion** ](https://msdn.microsoft.com/library/windows/hardware/ff561910)と[ **RtlVerifyVersionInfo** ](https://msdn.microsoft.com/library/windows/hardware/ff563026)オペレーティング システムのバージョンを取得するためのルーチン操作を行う特定の NDIS バージョンで保証されたアソシエーションを取得できません。 したがって、NDIS ドライバーする必要がありますを取得、NDIS バージョンとオペレーティング システムのバージョンとは別にします。 NDIS ドライバーで NDIS バージョンを取得できます、 [ **NdisGetVersion** ](https://msdn.microsoft.com/library/windows/hardware/ff562680)関数。

## <a name="related-topics"></a>関連トピック


[NDIS のバージョンの概要](overview-of-ndis-versions.md)

[NDIS バージョン情報を指定します。](specifying-ndis-version-information.md)

 

 






