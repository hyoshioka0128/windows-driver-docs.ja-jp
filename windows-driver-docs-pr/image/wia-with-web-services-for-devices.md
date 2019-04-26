---
title: WIA と Web Services for Devices
description: WIA と Web Services for Devices
ms.assetid: e1f91963-503b-4766-a6f1-c334465f0e73
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 94b977faec1cd5aed54f3b966dd05475142dd423
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63346821"
---
# <a name="wia-with-web-services-for-devices"></a>WIA と Web Services for Devices


、Windows では、オペレーティング システムは、Web Services for Devices (WSD) を実装しているイメージのネットワーク接続されているスキャナーのデバイスをサポートします。

WSD スキャン ドライバーは、web サービス スキャナーの受信トレイ Microsoft Windows Image Acquisition (WIA) クラス ドライバーです。 このドライバーは、スキャナーの Windows デバイス プロトコル (WDP) に準拠しています。

WSD スキャンのドライバー パッケージには、再利用可能なカーネル ドライバー コンポーネントが含まれています*WSDScan.sys*は具体的には、web サービス スキャナーのデバイスをインストールするためのものです。 

Windows にも含まれています、 *WSD 見据えて*、web サービス クライアント、デバイスがオンラインに戻ったときに、デバイスの通信を再確立する接続されていないデバイスのチャレンジをできるようにするモジュールであります。

> [!IMPORTANT]  
> WSD 見据えて機能は非推奨とされているし、WSD の挑戦者に関連するすべてのドキュメントは、2018 年に削除されます。

次のセクションでは、使用方法を説明します*WSDScan.sys* web サービス スキャナー、WIA ドライバーをインストールする機能探索を使用して、WIA ドライバー内からスキャナーのデバイスを使用して SOAP 通信を初期化する方法と方法WSD 見据えてを使用して、切断されたデバイスを課題します。

[WSD を WIA スキャナー ドライバーをインストールします。](installing-a-wia-scanner-driver-with-wsd.md)

[WIA スキャナーの通信を SOAP](soap-communications-for-wia-scanners.md)

[切断されているスキャナー WSD 困難になります](challenging-a-disconnected-scanner-with-the-wsd-challenger.md)

