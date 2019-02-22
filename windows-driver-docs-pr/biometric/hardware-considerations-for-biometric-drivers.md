---
title: 生体認証ドライバーのハードウェアに関する考慮事項
description: 生体認証ドライバーのハードウェアに関する考慮事項
ms.assetid: 07b16cfb-d3aa-4458-b6e3-acb76afe9b19
keywords:
- 生体認証ドライバー WDK、ハードウェアの考慮事項
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7b6078cc591e97111c05150c36511d7c013d3143
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56530363"
---
# <a name="hardware-considerations-for-biometric-drivers"></a>生体認証ドライバーのハードウェアに関する考慮事項


WBDI フレームワークを使用する生体認証デバイスには、次の要件を満たす必要があります。

-   WBDI ベースのドライバーが従う必要があります[DEVFUND 0010 ガイドライン](https://go.microsoft.com/fwlink/p/?linkid=26140)のターミナル サービスのリダイレクト。

    この要件は、デバイスとそのドライバーがサポートしているターミナル サービス セッションを使用したリダイレクト経由での PnP デバイス リダイレクトのフレームワークを示しています。

-   生体認証デバイス能力を最大限にフル スキャンをキャッシュし、中断モードに十分な大きさである内部バッファーが必要です。

    大きなバッファー サイズには、処理システムの再開中の処理のスキャンと定期的スキャン中にタイミングで以下の依存関係を意味します。

-   デバイスは、キャプチャ モードを入力し、ホストからコマンドを追加せず、スキャン中に内部状態遷移を作成できる必要があります。

 

 





