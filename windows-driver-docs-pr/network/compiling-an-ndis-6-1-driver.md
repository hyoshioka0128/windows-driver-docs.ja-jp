---
title: コンパイル、NDIS 6.1 ドライバー
description: このセクションは、NDIS 6.1 ドライバーをコンパイルする方法を説明します
ms.assetid: 9606a91c-c1cb-4d93-b648-3829d1b51954
keywords:
- NDIS WDK、コンパイル フラグ
- フラグの WDK ネットワー キングをコンパイルします。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7637120652f512ac2119a84036a09f3f0d3f5b14
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63356912"
---
# <a name="compiling-an-ndis-61-driver"></a>NDIS 6.1 ドライバーのコンパイル





Windows Server 2008 のビルド ユーティリティでは、ヘッダー バージョン管理をサポートします。 ヘッダー バージョン管理は、NDIS 6.1 ドライバーがコンパイル時に適切な NDIS 6.1 データ構造を使用することを確認します。 NDIS 6.1 を示すためにソース ファイルを更新する必要があります。

ドライバーの種類ごとに、次のようにソース ファイルに情報を追加します。

-   ミニポート ドライバーでは、追加 NDIS61\_ミニポート = 1。

-   プロトコル ドライバーでは、追加 NDIS61 = 1。

-   フィルター ドライバーの追加 NDIS61 = 1。

 

 





