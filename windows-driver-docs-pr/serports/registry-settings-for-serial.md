---
title: シリアル用のレジストリ設定
description: シリアル用のレジストリ設定
ms.assetid: be64d9d7-6d6b-4430-96a3-ac071d48b121
keywords:
- シリアル ドライバー WDK、レジストリ設定
- レジストリの WDK シリアル デバイス
- シリアル デバイス WDK、レジストリ設定
- シリアル デバイス シリアル ドライバー WDK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: baa474b998814271090aad38f6c0a97fddc3b233
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56580326"
---
# <a name="registry-settings-for-serial"></a>シリアル用のレジストリ設定





このセクションでは、シリアルを使用してシリアル デバイスを構成する次のレジストリ設定について説明します。

[シリアル サービス用レジストリ設定](registry-settings-for-the-serial-service.md)

[プラグ アンド プレイ シリアル デバイス用のレジストリ設定](registry-settings-for-a-plug-and-play-serial-device.md)

[従来の COM ポートのレジストリ設定](registry-settings-for-a-legacy-com-port.md)

シリアルでは、次のように、シリアル デバイスを構成するのにレジストリ設定を使用します。

-   デバイスに固有のエントリの値が存在する場合は、シリアルを使用します。

-   デバイスに固有のエントリの値が存在しないが、対応するシリアル サービス エントリの値がある場合、シリアルはサービスのエントリの値を使用します。

-   シリアルがで静的に定義されている既定のサービス値を使用してデバイスに固有のエントリの値が存在しない、対応するシリアル サービス エントリの値がない場合は、*スタック*します。

 

 




