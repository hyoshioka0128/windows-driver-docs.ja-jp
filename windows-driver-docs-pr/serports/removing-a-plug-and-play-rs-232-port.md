---
title: PnP RS-232 ポートを削除する
description: PnP RS-232 ポートを削除する
ms.assetid: b439dc51-09f2-4149-a562-2e376bb504c5
keywords:
- Rs-232 WDK シリアル デバイスをポートします。
- Serenum ドライバー WDK、プラグ アンド プレイ デバイス
- プラグ アンド プレイ シリアル デバイス WDK
- シリアル デバイス WDK、プラグ アンド プレイ
- rs-232 ポートを削除します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2ea89439b59d7b1f35b1f7d3194e3e0ed5403af2
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63388040"
---
# <a name="removing-a-plug-and-play-rs-232-port"></a>PnP RS-232 ポートを削除する





プラグ アンド プレイ manager rs-232 ポート スタックの先頭に削除要求を送信することによって、rs-232 ポートを削除します。 Serenum は、デバイス スタック ダウン要求を渡す、スタックでは、ポート、フィルター操作を実行を削除し、存在する場合に、関連付けられている PDO を削除します。 Rs-232 ポートの削除には、シリアル ポートに接続されているデバイスも削除されます。

 

 




