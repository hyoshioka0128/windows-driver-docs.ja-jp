---
title: RS-232 ポート上の PnP シリアル デバイスを削除する
description: RS-232 ポート上の PnP シリアル デバイスを削除する
ms.assetid: a9019445-3013-49b2-94fd-1ab8a85c3d7a
keywords:
- Rs-232 WDK シリアル デバイスをポートします。
- Serenum ドライバー WDK、プラグ アンド プレイ デバイス
- プラグ アンド プレイ シリアル デバイス WDK
- シリアル デバイス WDK、プラグ アンド プレイ
- プラグ アンド プレイ デバイスを削除します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 64492606b8f580092d74d96175b1d7e2b7aafc53
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63388025"
---
# <a name="removing-a-plug-and-play-serial-device-on-an-rs-232-port"></a>RS-232 ポート上の PnP シリアル デバイスを削除する





プラグ アンド プレイ マネージャーは、シリアル デバイス スタックの先頭に削除要求を送信することによって、シリアル デバイスを削除します。 Serenum シリアル デバイスの削除要求を受信した後、デバイスの PDO を削除し、要求を完了します。 Serenum は、rs-232 ポートが削除されるシリアル デバイスについては、親デバイスであるために、要求を rs-232 ポート スタックに渡されません。

 

 




