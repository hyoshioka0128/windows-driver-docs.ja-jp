---
title: コマンド処理とイベントのレポート
description: コマンド処理とイベントのレポート
ms.assetid: f51c082d-1be5-4f34-b7a6-82235e8c14f4
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6108b7eb1bd8616de735dcbb8ebb89090fb089bf
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63373193"
---
# <a name="command-processing-and-event-reporting"></a>コマンド処理とイベントのレポート





WIA ミニドライバーは、元の WIA アプリケーションや、WIA サービスから直接コマンド要求をサポートできます。 さらに、一部の静止画像デバイスでは、ユーザー アクションの結果として、ドライバーに通知を送信する機能があります。 たとえば、1 つまたは複数のフロント パネル ボタン付きのスキャナーは、ユーザーがこれらのボタンのいずれかのドライバーを通知できます。 この機能により、いくつかのアクションを実行します。 ドライバーは、特定のボタンが押されたことを WIA サービスに通知をするときに、WIA サービスは、イベントを処理するために以前に登録されたアプリケーションを起動できます。

このセクションでは、次のトピックについて説明します。

[コマンド処理](command-handling.md)

[イベントの報告](event-reporting.md)

 

 




