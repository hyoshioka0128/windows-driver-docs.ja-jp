---
title: Windows 10 用のグローバルナビゲーションサテライトシステム (GNSS) ドライバー設計ガイド
description: Windows 10 の収束 Windows の位置スタック用のグローバルナビゲーションサテライトシステム (GNSS) 用のユニバーサル Windows UMDF 2.0 ドライバーの設計要件とアーキテクチャについて説明します。
ms.assetid: FD8503DC-A43F-43B2-A1E9-D80778E326F9
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5690e43ddeaa5982e987e7bad2b1d00874f003cb
ms.sourcegitcommit: 96f94bffe426b7f92913fa0ffff1918c76e0e52c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/04/2020
ms.locfileid: "76980685"
---
# <a name="global-navigation-satellite-system-gnss-driver-design-guide-for-windows-10"></a>Windows 10 用のグローバルナビゲーションサテライトシステム (GNSS) ドライバー設計ガイド

このガイドでは、Windows 10 の収束 Windows の位置スタック用のユニバーサル Windows driver for GNSS (UMDF 2.0) の設計とアーキテクチャについて説明します。

## <a name="in-this-section"></a>このセクションの内容

| トピック | 説明 |
| --- | --- |
| [GNSS ドライバーの概要](gnss-driver-overview.md) | Gnss ドライバー設計ガイドを使用して、gnss ドライバーを使用して**DeviceIoControl** api を実装する方法を学習します。これにより、gnss アダプターのような高度なオペレーティングシステムコンポーネント (hlos) が目的の gnss 機能にアクセスできるようになります。 |
| [GNSS ドライバーの要件](gnss-driver-requirements.md) | Windows 10 用の GNSS ドライバーを開発する際に考慮すべき要件、前提条件、および制約について説明します。 |
| [GNSS ドライバーのアーキテクチャ](gnss-driver-architecture.md) | GNSS UMDF 2.0 ドライバーアーキテクチャと i/o に関する考慮事項の概要を示し、いくつかの種類の追跡と修正セッションについて説明します。 |
| [GNSS ドライバーの設計](gnss-driver-design.md) | データ構造、エラー報告、ドライバーのバージョン管理など、Windows 10 用の GNSS ドライバーを開発する際に考慮する設計原則について説明します。 |
