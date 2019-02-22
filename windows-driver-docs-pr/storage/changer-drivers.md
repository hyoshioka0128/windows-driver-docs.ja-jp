---
title: チェンジャー ドライバー
description: チェンジャー ドライバー
ms.assetid: 47310de7-e69d-4f06-9995-3d95783d607a
keywords:
- チェンジャー ドライバー WDK ストレージ
- 記憶域チェンジャー ドライバー WDK
- ストレージ ドライバー WDK、チェンジャー ドライバー
- チェンジャー ドライバー WDK ストレージ、チェンジャー ドライバーについて
- チェンジャー ドライバーに関するチェンジャー ドライバー WDK、ストレージ
- オートローダ WDK ストレージ
- オートチェン ジャー WDK ストレージ
- ジュークボックス WDK ストレージ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6448d7eec54d0611dbc81f8efa2f27b45332008c
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56553685"
---
# <a name="changer-drivers"></a>チェンジャー ドライバー


## <span id="ddk_changer_drivers_kg"></span><span id="DDK_CHANGER_DRIVERS_KG"></span>


このセクションには、次の情報が含まれています。

[システム提供のチェンジャー ドライバー](system-supplied-changer-drivers.md)

[チェンジャーのベンダーから提供されたドライバー](vendor-supplied-changer-drivers.md)

[チェンジャーのデバイスの拡張機能にデバイスに固有の情報を格納します。](storing-device-specific-information-in-the-changer-s-device-extension.md)

[チェンジャー デバイス制御要求の処理](processing-changer-device-control-requests.md)

チェンジャー ドライバーの制御、メディア ライブラリの要素または*チェンジャー* (とも呼ばれる、*オートローダー*、 *"オート チェンジャ"*、または*ジュークボックス*). NT ベースのオペレーティング システムでは、次のチェンジャー用のドライバーで構成されます。

-   ライブラリとして提供されるシステム提供のチェンジャー クラスのドライバーを*mcd.lib*、チェンジャー ドライバーをすべてに共通の機能を提供します。

-   デバイスに固有の miniclass ドライバーでは、静的にリンクする*mcd.lib*チェンジャーの特定の種類をサポートするために、チェンジャー クラス ドライバーによって呼び出されるルーチンを提供します。

このセクションには、新しいチェンジャー miniclass ドライバーの記述に関するガイドラインが含まれています。

 

 




