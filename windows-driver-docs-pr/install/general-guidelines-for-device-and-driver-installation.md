---
title: デバイスとドライバーのインストールに関する一般的なガイドライン
description: デバイスとドライバーのインストールに関する一般的なガイドライン
ms.assetid: E62906AB-CE32-4b07-B7DB-F523FFE4E6C2
keywords:
- デバイスのインストール WDK、一般的なガイドライン
- ドライバーのインストール WDK、一般的なガイドライン
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d0932ff8a78ebeac39edfc7bac798efe4807114c
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56549280"
---
# <a name="general-guidelines-for-device-and-driver-installation"></a>デバイスとドライバーのインストールに関する一般的なガイドライン


Windows オペレーティング システムでのデバイスとドライバーのインストールの基本的な目標は、ユーザーのプロセスをできるだけ簡単です。 インストールの手順とのコンポーネント、[ドライバー パッケージ](driver-packages.md)とオペレーティング システムのシームレスに動作する必要があります[デバイス インストール コンポーネント](https://msdn.microsoft.com/library/windows/hardware/ff541277)。

最適なユーザー エクスペリエンスを提供するには、設計およびインストールの手順を実装する、次のガイドラインを使用します。

-   自動的にシステムを再起動または絶対に必要である場合を除き、そのためには、ユーザーが必要です。

-   常に使用する[INF ファイル](inf-files.md)のデバイスのインストール。 すべての INF ファイルは整形式ではし、正しい構文を使用してください。

-   インストール後、システム上の INF ファイルのままに削除しないでください。 INF ファイルは、だけでなく、デバイスまたはドライバーのインストール時にまずもドライバー、ユーザーの要求を通じてデバイス マネージャーを更新するときに使用されます。

-   いずれかを使用して、[ベンダーのデバイス セットアップ クラス](https://msdn.microsoft.com/library/windows/hardware/ff553419)します。 そのためには説得力のある理由がある場合を除き、独自のセットアップ クラスを定義してください。

-   場所、形式、またはレジストリ キーまたは値の意味について想定しないでください。 レジストリ キーおよびツリーに関する詳細については、[レジストリ ツリーとデバイスとドライバーのキー](registry-trees-and-keys.md)を参照してください。

 

 





