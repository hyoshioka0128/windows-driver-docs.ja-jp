---
title: ユーザー モードから直接のミニポート ドライバーのクエリ
description: ユーザー モードから直接のミニポート ドライバーのクエリ
ms.assetid: e0d153bf-0e50-47bc-b4e2-10f04c532b99
keywords:
- ユーザー モード ドライバー クエリ WDK ネットワーク
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: defd016d20795ee0fcd45a388394588ef863e3d3
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63366380"
---
# <a name="querying-a-miniport-driver-directly-from-user-mode"></a>ユーザー モードから直接のミニポート ドライバーのクエリ





アプリケーションで使用できます[ **IOCTL\_NDIS\_クエリ\_GLOBAL\_STATS** ](https://msdn.microsoft.com/library/windows/hardware/ff548975)ミニポート ドライバーの NIC からの情報を直接照会する この操作で、アプリケーションは、OID ミニポート ドライバーがサポートする任意のクエリを使用できます。

 

 





