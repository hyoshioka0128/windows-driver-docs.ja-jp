---
title: DRM の要件
description: DRM の要件
ms.assetid: 312b943b-f280-4b29-a5d4-e78c7088bb22
keywords:
- WHQL テスト (WDK オーディオ)
- デジタル Rights Management WDK オーディオ、コンプライアンステスト
- DRM WDK オーディオ, コンプライアンステスト
- WDK オーディオの準拠テスト
- DRM 準拠の WDK オーディオのテスト
- Windows XP ロゴテスト用 WDK オーディオ用に設計
- ロゴテスト WDK オーディオ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6c68740d885ba8d751d5e5d70ca891ee46a069ed
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72833430"
---
# <a name="drm-requirements"></a>DRM の要件


## <span id="drm_requirements"></span><span id="DRM_REQUIREMENTS"></span>


このセクションでは、Microsoft Windows Hardware Quality Lab (WHQL) による DRM 準拠テストに合格するために、オーディオミニポートドライバーが満たす必要のある要件を示します。 これらの要件は、特に、WaveCyclic および WavePci[オーディオミニポートドライバー](audio-miniport-drivers.md)に適用されます。これは、ポートクラスライブラリ (Portcls) の WavePci および WaveCyclic ポートドライバーに対応するハードウェア固有のものです。 DRM 準拠テストは、現在 USB ドライバーでは使用できません。

Windows Me および Windows XP 以降では、信頼できるオーディオドライバーのみが DRM で保護されたコンテンツを再生できます。 Windows は、ドライバーの .cat (カタログ) ファイルに保存されている DRM 固有のデジタル署名を使って、信頼されたドライバーを識別します。 Microsoft は、WHQL によって管理されるハードウェア互換性テストの一部として DRM 準拠テストに合格するドライバーに対してのみ DRM 署名を発行します。

Windows Me ドライバーの場合、DRM 準拠テストはオプションであり、ハードウェアベンダーの要求でのみ実行されます。 DRM 署名は、Windows ロゴ署名に加えて、とは別のものです。 Windows ロゴテストに合格しても DRM 準拠テストではないドライバーは、DRM セキュリティで保護されていないコンテンツを再生できることに注意してください。

ただし、Windows XP 以降では、DRM 準拠テストは、WHQL テストの必須部分です。 ドライバーは、"Windows XP 用に設計" ロゴを修飾するために、DRM 準拠テストに合格する必要があります。

DRM 準拠テストでは、次の操作を行うために、信頼できるオーディオドライバーが必要です。

-   オーディオミニポートドライバーは、 [IDrmAudioStream](https://docs.microsoft.com/windows-hardware/drivers/ddi/drmk/nn-drmk-idrmaudiostream)インターフェイスをそのストリームオブジェクトに実装する必要があります。この場合、IID\_IDrmAudioStream に対してクエリを実行する場合は、IDrmAudioStream 型のオブジェクトを返す必要があります。

-   コピー防止が要求された場合 ([**Drmrights**](https://docs.microsoft.com/windows-hardware/drivers/ddi/drmk/ns-drmk-tagdrmrights))。**CopyProtect** = **TRUE**)、オーディオドライバーは、現在再生されているストリームをキャプチャする機能を無効にする必要があります。 つまり、ドライバーは、保護されていないデジタルコンテンツを、ハードディスク、EEPROM、メモリカード、メモリスティックを含む任意の形式の不揮発性ストレージに保存することはできません。 また、ドライバーは出力 D/A コンバーターで capture マルチプレクサーを無効にし、それ以外の場合はデジタルコンテンツのループバックを防止する必要があります。

-   オーディオドライバーからデバイスのデジタルオーディオ出力を無効にするように求められた場合 (DRMRIGHTS)。**DigitalOutputDisable** = **TRUE**) では、標準の相互接続スキームを使用して標準インターフェイス経由でコンテンツを送信できるすべてのデジタルオーディオ出力を無効にする必要があります。 デジタル出力は、--S/PDIF、IEEE 1394、パラレル、シリアル、モデム、およびネットワークポートに厳密に限定されていません。 (現時点では、この要件は USB には適用されません)。

-   セキュリティで保護されたコンテンツを処理する場合、オーディオドライバーは、信頼されていないドライバーをそのスタックにアタッチすることはできません。 つまり、オーディオドライバーは、DRM 署名も含まれる他のコンポーネントのみに依存する必要があります。 このドライバーでは、DRM 署名のないコンポーネントへのオーディオデータの転送を容易にすることはできません。 特に、ドライバーがデジタルコンテンツを別のコンポーネントに渡す場合、ドライバーはカーネルの DRM Api を使用して、この事実を[Drmk システムドライバー](kernel-mode-wdm-audio-components.md#drmk_system_driver)に通知する必要があります。

DRM 準拠テストを渡すだけでなく、オーディオデバイスとドライバーでは、カーネル内の DRM コンポーネントを無効にしたり、管理したりする操作のモードをユーザーが選択できないようにする必要があります。 具体的には、ドライバーは、レジストリ設定、ユーザーコントロールパネル、または DRM 機能を無効にするその他の手段を提供してはなりません。

 

 




