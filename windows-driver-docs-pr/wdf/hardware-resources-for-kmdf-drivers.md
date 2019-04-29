---
title: ハードウェア リソースの処理
description: システムのハードウェア リソースは、I/O ポート、ベクトルの割り込み、ダイレクト メモリ アクセス (DMA) チャネル、およびシステムに接続されている各デバイスに割り当てる必要があるその他の通信パスです。
ms.assetid: 30ceb7db-f11e-498c-a0c0-a63218627c6e
keywords:
- PnP WDK KMDF、ハードウェア リソース
- プラグ アンド プレイ WDK KMDF、ハードウェア リソース
- ハードウェア リソース WDK KMDF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7b1565d982c3d4904b3d2227e8a6ef79dd6eb20d
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63391876"
---
# <a name="handling-hardware-resources"></a>ハードウェア リソースの処理


システムのハードウェア リソースは、I/O ポート、ベクトルの割り込み、ダイレクト メモリ アクセス (DMA) チャネル、およびシステムに接続されている各デバイスに割り当てる必要があるその他の通信パスです。 このセクションのトピックでは、方法カーネル モード ドライバー フレームワーク (KMDF) ドライバー デバイスのハードウェア リソース要件をネゴシエート提案されたリソースの一覧を確認し、割り当てられたリソースが表示されるについて説明します。 このセクションでは、KMDF とユーザー モード ドライバー フレームワーク (UMDF) ドライバーへのアクセスとマップの両方がリソースを割り当てる方法についても説明します。




## <a name="in-this-section"></a>このセクションの内容


-   [ハードウェア リソースの概要](introduction-to-hardware-resources.md)
-   [ハードウェア リソースのフレームワーク オブジェクト](framework-objects-for-hardware-resources.md)
-   [リソース要件の一覧を作成します。](creating-a-resource-requirements-list.md)
-   [リソース要件の一覧を変更します。](modifying-a-resource-requirements-list.md)
-   [ブート構成のリソースの一覧を作成します。](creating-a-resource-list-for-a-boot-configuration.md)
-   [リソースの一覧を変更します。](modifying-a-resource-list.md)
-   [Raw と翻訳されたリソース](raw-and-translated-resources.md)
-   [検索して、ハードウェア リソースのマッピング](finding-and-mapping-hardware-resources.md)
-   [読み取りと書き込みをデバイスの登録](reading-and-writing-to-device-registers.md)

 

 





