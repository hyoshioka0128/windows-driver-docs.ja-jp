---
title: GNSS ドライバーの概要
description: このガイドを使用して、GNSS アダプターなどの HLOS が GNSS 機能にアクセスできるように、GNSS ドライバーを使用した DeviceIoControl Api を実装する方法について説明します。
ms.assetid: 1887097A-C495-4295-9904-B2964F46A81D
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7f5ef80389d7bbb88c9e5c2496439e6a015727a2
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56553766"
---
# <a name="gnss-driver-overview"></a>GNSS ドライバーの概要


実装する方法については、GNSS ドライバー設計のガイドを使用して、 **DeviceIoControl** GNSS ドライバーを使用した Api GNSS アダプターなどの高レベルのオペレーティング システム コンポーネント (HLOS) が必要な GNSS 機能にアクセスできるようにします。

IHV 電源に低いコストで位置を提供するか、必要なときに、パフォーマンスが向上して GNSS 機能を拡張できます。

新しい GNSS ドライバーが完全に所有されているし、カーネル モードで実行されている Microsoft が所有しているコードがなくても、Ihv によって提供されます。

**注**  Ihv GNSS/場所スタックにフィルター ドライバーを追加する必要があります。 フィルター ドライバーは、デバッグや保守を行うため、一般に、推奨されていません。 今後、さらは Microsoft が機能を拡張すると、Ihv から追加のフィルター ドライバーを持つ GNSS デバイス スタックのフィルター ドライバーと、アーキテクチャより複雑な不必要に追加する必要があります。

 

ドライバーでは、関数のドライバーの汎用 UMDF 2.0 モデル (ユーザー モード ドライバー フレームワーク) に従います。 (カーネル モード ドライバー フレームワーク) KMDF ドライバーを使用できますが、強くお勧め、プラットフォームに不安定性の高いリスクをもたらすをデバッグするが困難とユーザー モード OS コンポーネントを直接使用することはできません。
この設計のガイドには、基本的な知識 UMDF 2.0、Windows カーネル モードのプログラミング、カーネルの I/O の管理、電源管理、および、PnP デバイス スタックが想定しています。

## <a name="related-topics"></a>関連トピック
[GNSS ドライバーの要件](gnss-driver-requirements.md)  
[GNSS ドライバーのアーキテクチャ](gnss-driver-architecture.md)  



