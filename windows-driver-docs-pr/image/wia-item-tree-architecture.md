---
title: WIA 項目ツリーのアーキテクチャ
description: WIA 項目ツリーのアーキテクチャ
ms.assetid: 7e0f2b65-7150-4f8a-9780-abdaf93e44d6
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 39688f4367bf7c60f8b55d98ffe0a12dabf81fa5
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56560401"
---
# <a name="wia-item-tree-architecture"></a>WIA 項目ツリーのアーキテクチャ





アプリケーションが参照できる WIA 項目ツリーは、作成され、WIA ミニドライバーによって維持されるツリーから独立しました。 ミニドライバーは、項目のツリーを作成するとき、WIA サービスは、この WIA 項目のツリーをガイドとして使用して、同一のコピーをイメージング アプリケーションによって表示できるを作成します。 コピーしたツリー内の項目は、アプリケーションのアイテムと呼ばれます。 ミニドライバーで作成されたツリー内の項目は、ドライバーのアイテムと呼ばれます。

詳細については、以下のセクションで使用できます。

[アプリケーションのアイテムとアイテムのドライバー](application-items-and-driver-items.md)

[WIA を WIA 項目を使用してデバイスを記述します。](describing-a-wia-device-using-wia-items.md)

[WIA 項目のツリー構造を変更します。](changing-the-wia-item-tree-structure.md)

 

 




