---
title: NFC の設計ガイド
description: Windows は、次のプラットフォームを含め、NFC テクノロジを使用するさまざまなエクスペリエンスを公開しています。
ms.assetid: 26BFE25A-AC46-4634-8330-990DB447E55A
keywords:
- NFC
- 近距離無線通信
- proximity
- 近距離近接通信
- NFP
ms.date: 04/20/2017
ms.topic: article
ms.prod: windows-hardware
ms.technology: windows-devices
ms.openlocfilehash: 683ae52d151ad6769dbae1eb780fd76cb4123358
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67386203"
---
# <a name="near-field-communications-nfc-design-guide"></a>近距離無線通信 (NFC) 設計ガイド


Windows は、次のプラットフォームを含め、NFC テクノロジを使用するさまざまなエクスペリエンスを公開しています。

-   近接通信プラットフォーム - NFC を介してデバイス間でコンテンツのピアツーピア共有を開始するプラットフォームを提供します。Windows デバイスだけでなく、その他の NFC 準拠のモバイル デバイス、NFC フォーラム準拠のタグのコンテンツの読み取り/書き込みに焦点が当てられています。

-   ウォレット プラットフォーム - 電源投入デバイスの支払いシナリオだけでなく、実店舗での支払いやその他の NFC トランザクションに、セキュリティで保護されたストレージとトランザクション機能を提供します。

NFC のサポートを有効にするために、Microsoft は、これらのトピックで定義されているデバイス ドライバー インターフェイス (DDI) を実装するデバイス ドライバーを提供するために、IHV を利用しています。

User-Mode Driver Framework (UMDF) 2.0 を使用して、デスクトップ エディション (Home、Pro、Enterprise、および Education) 用の Windows 10 および Windows 10 Mobile 用の NFC ドライバーを作成します。

## <a name="related-topics"></a>関連トピック
 [UMDF の概要](https://docs.microsoft.com/windows-hardware/drivers/wdf/getting-started-with-umdf-version-2)  
 [NFC デバイス ドライバー インターフェイス (DDI) リファレンス](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)    


----------
