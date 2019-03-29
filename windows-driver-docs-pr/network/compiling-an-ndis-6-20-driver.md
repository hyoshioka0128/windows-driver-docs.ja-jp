---
title: NDIS 6.20 が動作するドライバーをコンパイルします。
description: このセクションは、NDIS 6.20 ドライバーをコンパイルする方法を説明します
ms.assetid: 07940d98-63fb-4629-943c-f56ebdfcdd76
keywords:
- NDIS 6.20 WDK、ドライバーのコンパイル
- NDIS 6.20 ドライバー WDK のコンパイル
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: eb684ca05c4320688ad21317a87460de6b5c4458
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56571332"
---
# <a name="compiling-an-ndis-620-driver"></a>NDIS 6.20 ドライバーのコンパイル





Windows 7 以降のビルド ユーティリティでは、ヘッダー バージョン管理をサポートします。 ヘッダー バージョン管理は、NDIS 6.20 ドライバーがコンパイル時に適切な NDIS 6.20 データ構造を使用することを確認します。 NDIS 6.20 が動作を示すためにソース ファイルを更新する必要があります。

ドライバーの種類ごとに、次のようにソース ファイルに情報を追加します。

-   ミニポート ドライバーでは、追加 NDIS620\_ミニポート = 1。

-   プロトコル ドライバーでは、追加 NDIS620 = 1。

-   フィルター ドライバーの追加 NDIS620 = 1。

 

 





