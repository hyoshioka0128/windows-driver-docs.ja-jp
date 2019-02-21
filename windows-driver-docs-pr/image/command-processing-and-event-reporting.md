---
title: コマンドの処理とイベントのレポート
description: コマンドの処理とイベントのレポート
ms.assetid: f51c082d-1be5-4f34-b7a6-82235e8c14f4
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6108b7eb1bd8616de735dcbb8ebb89090fb089bf
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56550440"
---
# <a name="command-processing-and-event-reporting"></a>コマンドの処理とイベントのレポート





WIA ミニドライバーは、元の WIA アプリケーションや、WIA サービスから直接コマンド要求をサポートできます。 さらに、一部の静止画像デバイスでは、ユーザー アクションの結果として、ドライバーに通知を送信する機能があります。 たとえば、1 つまたは複数のフロント パネル ボタン付きのスキャナーは、ユーザーがこれらのボタンのいずれかのドライバーを通知できます。 この機能により、いくつかのアクションを実行します。 ドライバーは、特定のボタンが押されたことを WIA サービスに通知をするときに、WIA サービスは、イベントを処理するために以前に登録されたアプリケーションを起動できます。

このセクションには、次のトピックが含まれています。

[コマンド処理](command-handling.md)

[イベントの報告](event-reporting.md)

 

 




