---
title: WIA ドライバー イベントのサポート
description: WIA ドライバー イベントのサポート
ms.assetid: 544c756b-4222-4d59-8393-924d3691e0f8
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b09ce9ffcf2543dd93d447647a11e6bf19bc182e
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63366894"
---
# <a name="wia-driver-event-support"></a>WIA ドライバー イベントのサポート





2 つの種類の WIA ミニドライバーをサポートできるイベント メカニズムがあります。

<a href="" id="interrupt-events"></a>イベントを中断します。  
デバイスは、デバイスのアクションが発生するたびに、ミニドライバーに要請されていない非同期通知を送信します。

<a href="" id="polling-events"></a>イベントのポーリング  
WIA サービスは、新しいイベントが発生したかどうかを判断するデバイスを照会するミニドライバーを定期的に確認します。 既定では、WIA サービスは、ドライバーを 1 秒ごとにポーリングします。 この値は、デバイスの INF ファイルで構成可能な (を参照してください[WIA デバイスの INF ファイル](inf-files-for-wia-devices.md)詳細については)。

WIA ミニドライバーでは、これらのイベント メカニズムのいずれかのみを使用できます。 割り込みイベント メカニズムが信頼性の向上とパフォーマンスのためお勧めします。

サポートされているイベントの 3 つのメカニズムがあります。

1.  Windows Me では、STI イベントは、STI イベントに登録されているアプリケーションを起動します。 このアプリケーションでは、デバイスの TWAIN データ ソースを開きます。

2.  Windows Me、Windows XP で WIA イベントが後で、WIA イベントに登録されているアプリケーションを起動するとします。 このアプリケーションでは、WIA サービスを使用して、デバイスにアクセスします。

3.  Windows XP 以降では、WIA サービス STI イベントに登録されているアプリケーションのイベントを STI WIA イベントに変換します。 このアプリケーションが使用 WIA を TWAIN TWAIN を通じてデバイスにアクセスする互換性レイヤーです。

このセクションでは、次のトピックについて説明します。

[中断イベントのサポートを追加します。](adding-interrupt-event-support.md)

[ポーリングのイベントのサポートを追加します。](adding-polling-event-support.md)

[イベント通知を提供します。](providing-event-notification.md)

 

 




