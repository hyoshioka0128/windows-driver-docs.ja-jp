---
title: ユーザー モードから直接ミニポート ドライバーのクエリを実行します。
description: ユーザー モードから直接ミニポート ドライバーのクエリを実行します。
ms.assetid: e0d153bf-0e50-47bc-b4e2-10f04c532b99
keywords:
- ユーザー モード ドライバー クエリ WDK ネットワーク
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: defd016d20795ee0fcd45a388394588ef863e3d3
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56530548"
---
# <a name="querying-a-miniport-driver-directly-from-user-mode"></a>ユーザー モードから直接ミニポート ドライバーのクエリを実行します。





アプリケーションで使用できます[ **IOCTL\_NDIS\_クエリ\_GLOBAL\_STATS** ](https://msdn.microsoft.com/library/windows/hardware/ff548975)ミニポート ドライバーの NIC からの情報を直接照会する この操作で、アプリケーションは、OID ミニポート ドライバーがサポートする任意のクエリを使用できます。

 

 





