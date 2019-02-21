---
title: セキュリティの問題は、ドライバーを静止画像します。
description: セキュリティの問題は、ドライバーを静止画像します。
ms.assetid: ad795cf0-8bff-4b9b-ac43-94c74cc19d60
ms.date: 07/18/2018
ms.localizationpriority: medium
ms.openlocfilehash: 74890262952d804bef97e64a814c159b197a92f9
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56557042"
---
# <a name="security-issues-for-still-image-drivers"></a>セキュリティの問題は、ドライバーを静止画像します。

イメージの取得 API を使用してアプリケーションから、または Windows サービスとして実装されます静止画像イベント モニターからユーザー モードのミニドライバーを呼び出すことができますに注意してください。 これら複数の呼び出し元のソースに関連付けられているセキュリティへの影響があります。 たとえば、ユーザー モードのミニドライバーが既定のセキュリティ記述子を使用して、ミュー テックスを作成します (指定することによって、 **NULL**セキュリティ記述子)、1 つのミュー テックスは、イベントの監視と呼ばれるミニドライバーのインスタンス間で共有することはできませんイメージの取得 API から 1 つが呼び出されます。
