---
title: 複数ページ IStream 転送
description: 複数ページ IStream 転送
ms.assetid: 0d17cfa8-f200-4d87-a2cb-cfd8dbc24e1e
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8d6da0a66408ede46f7e7adb6756df8b0d03abaf
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56578433"
---
# <a name="multipage-istream-transfers"></a>複数ページ IStream 転送


通常、データ転送が要求された場合、アイテムでは、その項目からデータを転送すると、アイテムのプロパティを指定する設定を使用しています。 たとえば、アプリケーションは、スキャナーの「ベッド」アイテムでは、データ転送が「フラット ベッド」アイテムの WIA プロパティに格納されている設定を使用して、フラット ベッドからのスキャンで発生します。

ただし、Windows Vista では、別の種類の転送は使用可能な: 複数の項目を転送するとも呼ばれます*フォルダー取得*します。 この種類の転送でアプリケーションを要求する、転送フォルダーの項目を指定したフラグを使用して (WIA\_転送\_ACQUIRE\_子)、およびそのフォルダー内のリーフ ノードのそれぞれからの転送の転送の結果アイテムのサブツリーです。

このセクションの内容:

[複数の転送中にドライバーの動作](driver-behavior-during-multipage-transfers.md)

 

 




