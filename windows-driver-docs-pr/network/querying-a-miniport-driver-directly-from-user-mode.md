---
title: ユーザー モードから直接のミニポート ドライバーのクエリ
description: ユーザー モードから直接のミニポート ドライバーのクエリ
ms.assetid: e0d153bf-0e50-47bc-b4e2-10f04c532b99
keywords:
- ユーザー モード ドライバー クエリ WDK ネットワーク
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 45c501fd0efd92a89deecadef7ada927760d7a66
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385441"
---
# <a name="querying-a-miniport-driver-directly-from-user-mode"></a>ユーザー モードから直接のミニポート ドライバーのクエリ





アプリケーションで使用できます[ **IOCTL\_NDIS\_クエリ\_GLOBAL\_STATS** ](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff548975(v=vs.85))ミニポート ドライバーの NIC からの情報を直接照会する この操作で、アプリケーションは、OID ミニポート ドライバーがサポートする任意のクエリを使用できます。

 

 





