---
title: 静止画像ドライバーのセキュリティの問題
description: 静止画像ドライバーのセキュリティの問題
ms.assetid: ad795cf0-8bff-4b9b-ac43-94c74cc19d60
ms.date: 07/18/2018
ms.localizationpriority: medium
ms.openlocfilehash: 74890262952d804bef97e64a814c159b197a92f9
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63356202"
---
# <a name="security-issues-for-still-image-drivers"></a>静止画像ドライバーのセキュリティの問題

イメージの取得 API を使用してアプリケーションから、または Windows サービスとして実装されます静止画像イベント モニターからユーザー モードのミニドライバーを呼び出すことができますに注意してください。 これら複数の呼び出し元のソースに関連付けられているセキュリティへの影響があります。 たとえば、ユーザー モードのミニドライバーが既定のセキュリティ記述子を使用して、ミュー テックスを作成します (指定することによって、 **NULL**セキュリティ記述子)、1 つのミュー テックスは、イベントの監視と呼ばれるミニドライバーのインスタンス間で共有することはできませんイメージの取得 API から 1 つが呼び出されます。
