---
title: カスタム オーディオ プロパティ セットの公開
description: カスタム オーディオ プロパティ セットの公開
ms.assetid: dc45f0fb-f462-4d20-967a-0665e18019e4
keywords:
- ハードウェア アクセラレーションにより WDK DirectSound、オーディオのカスタム プロパティの設定します。
- カスタムの音声プロパティは、WDK を設定します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9222b10691459a31fd286f8fe9a5ca7246750dd2
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67360078"
---
# <a name="exposing-custom-audio-property-sets"></a>カスタム オーディオ プロパティ セットの公開


## <span id="exposing_custom_audio_property_sets"></span><span id="EXPOSING_CUSTOM_AUDIO_PROPERTY_SETS"></span>


DirectSound がサウンド カードのカスタム プロパティの使用をサポートし、提供、 **IKsPropertySet**この目的のためのインターフェイス。

**注**   Dsound.h と Ksproxy.h ヘッダー ファイルは似ていますが、互換性のないバージョンを定義、 **IKsPropertySet**インターフェイス。 DirectSound アプリケーションでは、Dsound.h で定義されているバージョンを使用する必要があります。 DirectSound 版**IKsPropertySet** DirectSound リファレンスのページで、Microsoft Windows SDK ドキュメントで定義されます。 KSProxy バージョンでは、次を参照してください。 [IKsPropertySet](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dsound/nn-dsound-ikspropertyset)します。

 

カスタムの音声プロパティ セットは、Windows 98 Second Edition および Windows Me では、および Windows XP では既定で有効になっている以降です。 既定では、DirectSound は、Windows 2000、および Windows Server 2003 および Windows の以降のサーバー バージョンのカスタム プロパティのセットを無視します。 DirectSound でこれらのオペレーティング システムのいずれかで設定されているカスタム プロパティを認識するのユーザーはまずシステム上でのカスタム プロパティのセットを有効にする必要があります。

たとえば、オーディオのカスタム プロパティを有効にする Windows 2000 に設定します。

1.  コントロール パネルで、ダブルクリック、**サウンドとマルチ メディア**アイコン (または実行 mmsys.cpl)。

2.  **オーディオ**タブで、優先する適切なデバイスでの選択、**音の再生**一覧。

3.  **[詳細設定]** ボタンをクリックします。

4.  **パフォーマンス** タブで、スライド、**ハードウェア アクセラレータ**スライダーを**完全**します。

5.  **[適用]** をクリックします。

DirectSound は、ドライバーにカスタム プロパティのセットを渡すには有効になりました。

4 つの設定は、**ハードウェア アクセラレータ**スライダー。

-   **None**

-   **基本**

-   **標準**

-   **Full**

カスタム プロパティのセットが、スライダーに設定されている場合にのみ有効になって**完全**します。 詳細については、次を参照してください。 [DirectSound ハードウェア高速化と SRC スライダー](directsound-hardware-acceleration-and-src-sliders.md)します。

 

 




