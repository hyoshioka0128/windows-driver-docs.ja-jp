---
title: グローバルナビゲーションサテライトシステム (GNSS) ドライバーの概要
description: このガイドを使用して、GNSS アダプターなどの HLOS が GNSS の機能にアクセスできるように、グローバルナビゲーションサテライトシステム (GNSS) ドライバーを使用して DeviceIoControl Api を実装する方法について説明します。
ms.assetid: 1887097A-C495-4295-9904-B2964F46A81D
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3bd3e46849d1e4b760d56562e7b2fc262fc1d7b9
ms.sourcegitcommit: 96f94bffe426b7f92913fa0ffff1918c76e0e52c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/04/2020
ms.locfileid: "76980687"
---
# <a name="global-navigation-satellite-system-gnss-driver-overview"></a>グローバルナビゲーションサテライトシステム (GNSS) ドライバーの概要

グローバルナビゲーションサテライトシステム (GNSS) ドライバー設計ガイドを使用して、gnss ドライバーを使用して**DeviceIoControl** api を実装する方法を学習します。これにより、gnss アダプターのような高レベルのオペレーティングシステムコンポーネント (hlos) が目的の gnss 機能にアクセスできるようになります。

この機能は、IHV によって強化され、電力コストを削減したり、必要に応じてより優れたパフォーマンスを提供したりすることができます。

新しい GNSS ドライバーは、Ihv によって完全に所有および配信されます。カーネルモードで実行される Microsoft 所有のコードはありません。

> [!NOTE]
> Ihv は、GNSS/Location スタックにフィルタードライバーを追加することはできません。 フィルタードライバーはデバッグと保守が困難であるため、一般的には推奨されません。 さらに、今後、Microsoft は、機能を拡張するために GNSS デバイススタックにフィルタードライバーを追加することが必要になる場合があります。また、Ihv から追加のフィルタードライバーを使用すると、アーキテクチャが不必要に複雑になります。

ドライバーは、関数ドライバーの汎用の UMDF 2.0 モデル (ユーザーモードドライバーフレームワーク) に従います。 KMDF (カーネルモードドライバーフレームワーク) ドライバーを使用することもできますが、プラットフォームが不安定になるリスクが高くなり、デバッグが困難になり、ユーザーモードの OS コンポーネントを直接使用できないため、推奨されません。
この設計ガイドでは、UMDF 2.0、Windows カーネルモードプログラミング、カーネル i/o 管理、電源管理、および PnP デバイススタックに関する基本的な知識があることを前提としています。

## <a name="related-topics"></a>関連トピック

[グローバルナビゲーションサテライトシステム (GNSS) ドライバーの要件](gnss-driver-requirements.md)  

[グローバルナビゲーションサテライトシステム (GNSS) ドライバーのアーキテクチャ](gnss-driver-architecture.md)  
