---
title: NFP プロバイダー モデル
description: Near Field 近接 (NFP) プロバイダードライバーモデルは、Windows が NFP 機能を使用し、NFP シナリオとユースケースを有効にするための一般的な画面を提供します。
ms.assetid: AD8DC80F-5CE2-4547-B951-A82A280F18ED
keywords:
- NFC
- 近距離無線通信
- 近接通信
- 近距離近接通信
- NFP
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a75262523a446dcc586a807ae0ff83de40dbed70
ms.sourcegitcommit: 8097a09d2f989a9b3dca250c4e2ffd4cec2172e3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/09/2020
ms.locfileid: "84563130"
---
# <a name="nfp-provider-model"></a>NFP プロバイダー モデル

Near Field 近接 (NFP) プロバイダードライバーモデルは、Windows が NFP 機能を使用し、NFP シナリオとユースケースを有効にするための一般的な画面を提供します。

これらの機能を Windows に公開するには、互換性のあるデバイスの実装側が、 **GUID \_ devinterface \_ NFP**デバイスインターフェイスを実装するデバイスドライバーを提供する必要があります。 このドライバーは、デバイス上のソフトウェアやハードウェアに実装されている、基になる NFP テクノロジと連携して、NFP プロバイダーを形成します。

**GUID \_ devinterface \_ NFP**デバイスインターフェイスにより、WINDOWS はさまざまな NFP テクノロジを使用できます。 このデバイスインターフェイスの実装によって公開される最も一般的な機能はジェネリックであり、基になる NFP テクノロジに固有ではありません。 他の Windows アプリと通信するこの共通機能をプログラミングするアプリでは、アプリのコードを変更せずに、NFP プロバイダーを使用できるようにする必要があります。 NFC は、NFP 空間の先頭の標準であるため、デバイスインターフェイスは、NFP プロバイダーにネイティブの NDEF パケットを処理する機能を提供することで、特定の NFC 動作をサポートします。 アプリは、この NFC 固有の機能に依存し、独自の機能を NFC 対応の NFP プロバイダーのみに制限することができます。

互換性のない NFP プロバイダーを持つ2台の Pc は、NFP プロバイダーを介して通信することはできません。 この仕様では、2つの認定された Windows システムの相互運用をサポートするためのガイドラインを提供しています。これは、少なくとも1つの NFC 対応プロバイダーのサポートが Windows システム認定の要件であるためです。

NFP プロバイダーは、基になる NFP テクノロジの近接イベントによって転送がトリガーされる pub/sub モデルを使用して、通信を事前にステージングします。 メッセージは、メッセージの種類に基づいてパブリッシュおよびサブスクライブされます。 2つのデバイスが NFP テクノロジに従って近接になると、近接状態がトリガーされ、現在公開されているすべてのメッセージが他のデバイスの現在のサブスクライバーに送信されます。 このメカニズムでは、ユーザーがデバイス上でいくつかのコンテキストを設定し、別のデバイスでそれをタップして簡単な方法でシナリオを完了するモデルが提供されます。

## <a name="related-topics"></a>関連トピック

[NFC デバイスドライバーインターフェイス (DDI) の概要](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)  

[近距離無線近接 DDI リファレンス](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)  

