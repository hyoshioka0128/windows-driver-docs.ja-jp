---
title: DRM の要件
description: DRM の要件
ms.assetid: 312b943b-f280-4b29-a5d4-e78c7088bb22
keywords:
- WHQL テスト WDK オーディオ
- デジタル権利管理の WDK オーディオ、コンプライアンスのテスト
- DRM WDK オーディオ、コンプライアンスのテスト
- コンプライアンス テスト WDK オーディオ
- DRM コンプライアンス WDK オーディオのテスト
- Windows XP ロゴの WDK オーディオのテスト用に設計されました。
- ロゴ テスト WDK オーディオ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0ae67b487b82c8f829e0f9a4425df691be4ec2b6
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63333723"
---
# <a name="drm-requirements"></a>DRM の要件


## <span id="drm_requirements"></span><span id="DRM_REQUIREMENTS"></span>


このセクションでは、Microsoft Windows Hardware Quality Lab (WHQL) によって渡す DRM 対応がテストされたオーディオのミニポート ドライバーが満たす必要のある要件を表示します。 WaveCyclic と WavePci を具体的にはこれらの要件が適用[オーディオ ミニポート ドライバー](audio-miniport-drivers.md)ポートのクラス ライブラリ (Portcls.sys) WavePci と WaveCyclic ポート ドライバーに対応するハードウェアに固有であります。 DRM 対応のテストでは、USB ドライバーを現在使用できません。

Windows Me と Windows xp 以降で、信頼済みのオーディオ ドライバーのみが DRM で保護されたコンテンツを再生できます。 Windows では、ドライバーの .cat (カタログ) ファイルに格納されている DRM に固有のデジタル署名を使用して信頼されたドライバーを識別します。 Microsoft では、WHQL によって管理されるハードウェアの互換性テストの一部として DRM 準拠テストに合格するドライバーに対してのみ DRM 署名を発行します。

Windows Me ドライバー、DRM 準拠テストは省略可能であり、ハードウェア ベンダーの要求でのみ実行されます。 DRM 署名は、Windows ロゴの署名に加え、およびから分離されています。 渡しますが、Windows ロゴ テスト、DRM 準拠テストではないドライバーもコンテンツを再生できます DRM セキュリティで保護されていないに注意してください。

Windows XP 以降、DRM 準拠テストが WHQL テストに必要です。 ドライバーは、"Windows XP 用に設計されています"のロゴの対象にするには、DRM 準拠テストを渡す必要があります。

DRM 対応のテストには、以下を行う場合は、信頼されたオーディオ ドライバーが必要です。

-   オーディオのミニポート ドライバーを実装する必要があります、 [IDrmAudioStream](https://msdn.microsoft.com/library/windows/hardware/ff536568)インターフェイスの IID のクエリを実行している場合、IDrmAudioStream 型のオブジェクトを返す必要があります、そのストリーム オブジェクト\_IDrmAudioStream します。

-   コピー防止が要求された場合 ([**DRMRIGHTS**](https://msdn.microsoft.com/library/windows/hardware/ff536355).**CopyProtect** = **TRUE**)、オーディオ ドライバーには、現在の再生中のストリームをキャプチャする機能が無効にする必要があります。 これは、ドライバーがハード ディスク、EEPROM、メモリ カード、およびメモリ スティックが含まれていますが、不揮発性ストレージの形態に保護されていないデジタル コンテンツを保存する必要があることを意味します。 また、ドライバーは出力の D のコンバーターのマルチプレクサーのキャプチャを無効にし、できないデジタル コンテンツのループバックする必要があります。

-   オーディオ ドライバーは、デバイスのデジタル オーディオ出力を無効にするように求められます (DRMRIGHTS **。DigitalOutputDisable** = **TRUE**)、標準の相互接続スキームを通じて標準的なインターフェイス経由でコンテンツを転送することができるすべてのデジタル オーディオ出力が無効にする必要があります。 デジタル出力は--を含めるし、--S/PDIF、IEEE 1394、パラレル、シリアル、モデムに厳密に限定されませんが、ネットワーク ポート。 (この要件は現在当てはまりません usb。)

-   セキュリティで保護されたコンテンツを処理するときに、オーディオ ドライバーがそのスタックに、信頼されていないドライバーを関連付ける必要があることはありません。 つまり、オーディオ ドライバーは、DRM 署名を含めることもその他のコンポーネントのみに依存する必要があります。 ドライバーでは、DRM 署名がない任意のコンポーネントへのオーディオ データの転送を容易にする必要があることはありません。 具体的には、ドライバーは、デジタル コンテンツを別のコンポーネントに合格した場合、ドライバーする必要があります、DRM Api を使用してカーネルの通知、 [DRMK システム ドライバー](kernel-mode-wdm-audio-components.md#drmk_system_driver)この事実です。

DRM 準拠テストを渡すだけでなく、ユーザーの操作モードを選択してそのララェホを許可しない必要があります、オーディオ デバイスとドライバーまたは subverts カーネルの DRM コンポーネント。 具体的には、レジストリ設定、ユーザー コントロール パネル、または DRM 関数を無効にするには、他の手段、ドライバーを提供しない必要があります。

 

 




