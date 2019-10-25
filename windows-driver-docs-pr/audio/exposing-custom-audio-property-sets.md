---
title: カスタム オーディオ プロパティ セットの公開
description: カスタム オーディオ プロパティ セットの公開
ms.assetid: dc45f0fb-f462-4d20-967a-0665e18019e4
keywords:
- ハードウェア高速化 WDK DirectSound、カスタムオーディオプロパティセット
- カスタムオーディオプロパティ設定 WDK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6edf4f21c81d608ea48c0a8c4f35992f1af1ce83
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72831232"
---
# <a name="exposing-custom-audio-property-sets"></a>カスタム オーディオ プロパティ セットの公開


## <span id="exposing_custom_audio_property_sets"></span><span id="EXPOSING_CUSTOM_AUDIO_PROPERTY_SETS"></span>


DirectSound は、サウンドカードのカスタムプロパティの使用をサポートし、この目的で**IKsPropertySet**インターフェイスを提供します。

ヘッダーファイル Dsound と Ksk Proxy. h は、類似しているが互換性のないバージョンの**IKsPropertySet**インターフェイスを定義します **。  ** DirectSound アプリケーションでは、Dsound で定義されているバージョンを使用する必要があります。 **IKsPropertySet**の directsound バージョンは、Microsoft Windows SDK ドキュメントの directsound 参照ページで定義されています。 Ksk プロキシバージョンについては、「 [IKsPropertySet](https://docs.microsoft.com/windows-hardware/drivers/ddi/dsound/nn-dsound-ikspropertyset)」を参照してください。

 

カスタムオーディオプロパティセットは、Windows 98 Second Edition および Windows Me では既定で有効になっており、Windows XP 以降では既定で有効になっています。 既定では、DirectSound は windows 2000 のカスタムプロパティセット、および windows Server 2003 以降のサーバーバージョンの Windows では無視します。 DirectSound でこれらのオペレーティングシステムのいずれかで設定されたカスタムプロパティを認識するには、まず、ユーザーのシステムでカスタムプロパティセットを有効にする必要があります。

たとえば、Windows 2000 でカスタムオーディオプロパティセットを有効にするには、次のようにします。

1.  コントロールパネルで、 **[サウンドとマルチメディア]** アイコンをダブルクリックします (または、mmsys を実行するだけです)。

2.  **[オーディオ]** タブで、 **[サウンド再生]** の一覧から適切なデバイスを選択します。

3.  [詳細設定] ボタンをクリックします。

4.  **[パフォーマンス]** タブで、 **[ハードウェアアクセラレータ]** スライダーを **[完全]** にスライドします。

5.  **[適用]** をクリックします。

DirectSound が有効になり、カスタムプロパティセットをドライバーに渡すことができるようになりました。

**[ハードウェアの高速化]** スライダーでは、次の4つの設定を使用できます。

-   **なし**

-   **基本的な**

-   **標準**

-   **全角**

カスタムプロパティセットは、スライダーが**Full**に設定されている場合にのみ有効になります。 詳細については、「 [DirectSound のハードウェアアクセラレータおよび SRC スライダー](directsound-hardware-acceleration-and-src-sliders.md)」を参照してください。

 

 




