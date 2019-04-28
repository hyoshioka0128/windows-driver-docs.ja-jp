---
title: イベントのレポート
description: イベントのレポート
ms.assetid: 4c3ffa7e-d0b3-483c-9f6b-3fe8ae997cf0
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: efefb17f0a8f8ec846fb46bf837ada50810c1b31
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63373134"
---
# <a name="event-reporting"></a>イベントのレポート





WIA アーキテクチャでは、デバイスで何らかのアクションが発生したときに、WIA ミニドライバーを通知する静止画像デバイス、します。 たとえば、スキャナーは、ユーザー、デバイスから直接スキャンの開始を有効にすると、フロント パネルで、クリック 1 回があります。 WIA ミニドライバーは、WIA サービスに通知できますので、このイベントの通知する必要があります。 このイベントの受信を登録したすべての実行中のアプリケーションが通知されます。 さらに、アプリケーションが、イベントの前にこのイベントの結果として開始する登録されている場合、WIA サービスは、そのアプリケーションを起動します。

WIA アーキテクチャでは、割り込みのイベントをサポートしているし、イベントをポーリングします。 これらのイベントに関する詳細については、次を参照してください。 [WIA ドライバー イベント サポート](wia-driver-event-support.md)します。

 

 




