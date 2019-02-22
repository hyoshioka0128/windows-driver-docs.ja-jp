---
title: Rs-232 ポートでプラグ アンド プレイ シリアル デバイスを削除します。
description: Rs-232 ポートでプラグ アンド プレイ シリアル デバイスを削除します。
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
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56549740"
---
# <a name="removing-a-plug-and-play-serial-device-on-an-rs-232-port"></a>Rs-232 ポートでプラグ アンド プレイ シリアル デバイスを削除します。





プラグ アンド プレイ マネージャーは、シリアル デバイス スタックの先頭に削除要求を送信することによって、シリアル デバイスを削除します。 Serenum シリアル デバイスの削除要求を受信した後、デバイスの PDO を削除し、要求を完了します。 Serenum は、rs-232 ポートが削除されるシリアル デバイスについては、親デバイスであるために、要求を rs-232 ポート スタックに渡されません。

 

 




