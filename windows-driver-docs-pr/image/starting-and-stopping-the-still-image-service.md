---
title: 静止画像サービスの開始と停止
description: 静止画像サービスの開始と停止
ms.assetid: 52770566-1d03-4ae8-9925-240fffcc5f57
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 30f4ef05bee8372ad25a4d711ab1475f76aff0ef
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56582482"
---
# <a name="starting-and-stopping-the-still-image-service"></a>静止画像サービスの開始と停止





静止イメージ サービスを開始または停止をユーザーが通常必要はありませんが、開発者が開始またはインストールまたはドライバーをアンインストールしたときに、このサービスを停止する必要があります。 2 つの方法のいずれかでまだイメージのサービスを停止および開始できます。

コマンド ウィンドウでコマンドを発行します。

静止イメージ サービスを開始するには、このコマンドを発行します。

```console
net start stisvc
```

静止画像サービスを停止するには、このコマンドを発行します。

```console
net stop stisvc
```

Microsoft 管理コンソール (MMC) を使用します。

**サービス**を選択します**イメージ サービスを引き続き**します。 サービス、右クリックし、およびクリック開始**開始**表示されるメニューから。

サービス、右クリックしとクリックを停止する**停止**表示されるメニューから。
