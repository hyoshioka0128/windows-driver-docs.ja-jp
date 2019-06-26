---
title: NFP プロバイダー モデル
description: フィールドの近く近接 (NFP) プロバイダーのドライバー モデルでは、NFP 機能を使用して、NFP シナリオを有効にして、ユース ケースに Windows の共通のサーフェイスを提供します。
ms.assetid: AD8DC80F-5CE2-4547-B951-A82A280F18ED
keywords:
- NFC
- 近距離無線通信
- proximity
- 近距離近接通信
- NFP
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5b717151b74579fad943a3d7cf84965663a4f9cf
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67373824"
---
# <a name="nfp-provider-model"></a>NFP プロバイダー モデル


フィールドの近く近接 (NFP) プロバイダーのドライバー モデルでは、NFP 機能を使用して、NFP シナリオを有効にして、ユース ケースに Windows の共通のサーフェイスを提供します。

これらの機能が Windows に公開する、互換性のあるデバイスの実装側を実装するデバイス ドライバーを提供する必要があります、 **GUID\_DEVINTERFACE\_NFP**デバイス インターフェイス。 このドライバーは、ソフトウェアやハードウェア、NFP プロバイダーを形成するデバイス上で実装されている基になる NFP テクノロジと連携します。

**GUID\_DEVINTERFACE\_NFP**デバイス インターフェイスは、さまざまな NFP テクノロジを使用して Windows を使用できます。 このデバイスのインターフェイスの実装によって公開されている最も一般的な機能は、ジェネリック、基になる NFP テクノロジに限定されません。 その他の Windows アプリとの通信にこの共通の機能をプログラミングするアプリをアプリのコードを変更することがなく、NFP プロバイダーを使用することがあります。 NFC が NFP 領域の先頭の標準であるため、デバイス インターフェイスは、NFP プロバイダーにネイティブ NDEF パケットを処理する機能を提供することにより特定の NFC 動作をサポートします。 アプリは、この NFC 固有の機能に依存することし、NFP の NFC 対応プロバイダーのみに独自の機能を制限する可能性があります。

互換性のない NFP プロバイダーを使用した 2 台の Pc では、その NFP プロバイダー経由で通信できません。 この仕様では、NFC が有効な少なくとも 1 つのプロバイダーは、Windows システム認定の要件のガイドラインのために、認定済みの 2 つの Windows システムの相互運用をサポートするための十分なサポートを提供します。

NFP プロバイダーは、事前の転送が基になる NFP テクノロジの近接イベントによってトリガーされるパブリッシュ/サブスクライブ モデルを使用して、通信をステージングします。 メッセージがパブリッシュされ、メッセージの種類に基づいてにサブスクライブしています。 2 つのデバイスが近接に従って NFP テクノロジになるは、近接性の状態がトリガーされ、現在パブリッシュされているすべてのメッセージは、その他のデバイス上の現在のサブスクライバーに送信されます。 このメカニズムは、ユーザーが自分のデバイスで何らかのコンテキストを設定し、簡単な方法でシナリオを完了する別のデバイスでそれをタップしたモデルを提供します。

 

 
## <a name="related-topics"></a>関連トピック
[NFC のデバイス ドライバー インターフェイス (DDI) の概要](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)  
[フィールドの近接 DDI 参照の近く](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)  

