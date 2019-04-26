---
title: Rs-232 ポートに、非 PnP デバイスを構成します。
description: Rs-232 ポートに接続されているプラグ アンド プレイ シリアル デバイスの構成
ms.assetid: 5106e42e-4f87-47c3-a0ec-f70e77daabd3
keywords:
- プラグ アンド プレイ シリアル デバイス WDK
- シリアル デバイス WDK、プラグ アンド プレイ
- プラグ アンド プレイ シリアル デバイス WDK
- Rs-232 WDK シリアル デバイスをポートします。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 149f929b743235455396cb30cde41e11d8eda0a0
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63345012"
---
# <a name="configuration-of-non-plug-and-play-serial-device-connected-to-an-rs-232-port"></a>Rs-232 ポートに接続されているプラグ アンド プレイ シリアル デバイスの構成





このトピックでは、ハードウェア、ドライバー、およびデバイス スタック rs-232 ポートに接続されている従来のシリアル デバイス用の一般的な構成について説明します。

次の図は、プラグ アンド プレイのトースター デバイスに対する一般的な構成を示します。

![トースターのプラグ アンド プレイ デバイスのハードウェアとドライバー-と-デバイスのスタックの構成を示す図します。](images/ser1.png)

Serenum は、プラグ アンド プレイ シリアル デバイスをインストールするのには使用されません。 トースター デバイス スタックのインストールでは、デバイス固有です。 トースター ドライバーを開く、トースター デバイスと通信するのには、 [COM ポート](configuration-of-com-ports.md)rs-232 ポートに関連付けられています。

 

 




