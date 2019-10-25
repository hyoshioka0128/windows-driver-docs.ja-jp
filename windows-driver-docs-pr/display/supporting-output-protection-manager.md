---
title: Output Protection Manager のサポート
description: Output Protection Manager のサポート
ms.assetid: 2c138dbd-55ca-4c71-8c8b-b2efd1ca80f2
keywords:
- COPP WDK DirectX VA、出力保護マネージャー
- 出力保護マネージャーの WDK 表示
- OPM WDK ディスプレイ
- コピー防止 WDK ディスプレイ
- ビデオコピー防止 WDK ディスプレイ
- 保護されたビデオ WDK ディスプレイ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 96a11c1dbe5cde248b901eeff483475d09deca6b
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72825609"
---
# <a name="supporting-output-protection-manager"></a>Output Protection Manager のサポート


出力保護マネージャー (OPM) device driver interface (DDI) を使用すると、グラフィックスアダプターのさまざまなコネクタによって出力されるビデオ信号のコピー保護を有効にすることができます。 グラフィックスアダプターによって出力されるコンテンツを Windows Vista で保護する方法の詳細については、出力[Content Protection と Windows Vista](https://download.microsoft.com/download/5/D/6/5D6EAF2B-7DDF-476B-93DC-7CF0072878E6/output_protect.doc)の web サイトで出力 Content Protection ドキュメントをダウンロードしてください。

OPM は、 [Windows 2000 display driver model](windows-2000-display-driver-model-design-guide.md)によって提供される[認定出力保護プロトコル (copp)](copp-processing.md)の後継です。 OPM は、すべての COPP 機能をサポートしています。 COPP の機能の詳細については、「 [COPP の概要](introduction-to-copp.md)」を参照してください。 OPM では、新機能もサポートされています。

## <a name="opm-interface"></a>OPM インターフェイス

**OPM DDI**は[copp DDI](sample-functions-for-copp.md)と意味が似ています。これは、OPM は基本的には Windows Vista display driver MODEL の場合は copp 1.1 であるためです。 ただし、OPM DDI は COPP DDI よりはるかに簡単です。 OPM DDI は、DirectDraw および DirectX Video アクセラレーション (VA) DDI を介して、COPP DDI がマップされている一連の関数で構成されているためです。

アプリケーションとドライバーの間で、保護されたコマンド、情報、および状態を渡すことがサポートされている場合、Microsoft DirectX graphics kernel subsystem (*Dxgkrnl*) は、ドライバーの OPM DDI を正常に開くことができます。

OPM インターフェイスを使用する必要があるカーネルモードコンポーネントは、インターフェイスを取得するために、ディスプレイミニポートドライバーの[DxgkDdiQueryInterface](https://docs.microsoft.com/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkddi_query_interface)関数の呼び出しを開始します。 OPM インターフェイス関数へのポインターは、 [QUERY_INTERFACE](https://docs.microsoft.com/windows-hardware/drivers/ddi/video/ns-video-_query_interface)構造体のインターフェイスメンバーが指す[DXGK_OPM_INTERFACE](https://docs.microsoft.com/windows-hardware/drivers/ddi/dispmprt/ns-dispmprt-_dxgk_opm_interface)構造体で返されます。 この QUERY_INTERFACE は、DxgkDdiQueryInterface 呼び出しの*QueryInterface*パラメーターによってポイントされます。

次の出力保護マネージャー (OPM) インターフェイス関数は、いくつかのディスプレイミニポートドライバーによって実装されています。

* [DXGKDDI_OPM_GET_CERTIFICATE_SIZE](https://docs.microsoft.com/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkddi_opm_get_certificate_size)
* [DXGKDDI_OPM_GET_CERTIFICATE](https://docs.microsoft.com/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkddi_opm_get_certificate)
* [DXGKDDI_OPM_CREATE_PROTECTED_OUTPUT](https://docs.microsoft.com/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkddi_opm_create_protected_output)
* [DXGKDDI_OPM_GET_RANDOM_NUMBER](https://docs.microsoft.com/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkddi_opm_get_random_number)
* [DXGKDDI_OPM_SET_SIGNING_KEY_AND_SEQUENCE_NUMBERS](https://docs.microsoft.com/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkddi_opm_set_signing_key_and_sequence_numbers)
* [DXGKDDI_OPM_GET_INFORMATION](https://docs.microsoft.com/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkddi_opm_get_information)
* [DXGKDDI_OPM_GET_COPP_COMPATIBLE_INFORMATION](https://docs.microsoft.com/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkddi_opm_get_copp_compatible_information)
* [DXGKDDI_OPM_CONFIGURE_PROTECTED_OUTPUT](https://docs.microsoft.com/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkddi_opm_configure_protected_output)
* [DXGKDDI_OPM_DESTROY_PROTECTED_OUTPUT](https://docs.microsoft.com/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkddi_opm_destroy_protected_output)

次のトピックでは、OPM の新機能と、OPM DDI をサポートおよび使用する方法について説明します。

[OPM の用語](opm-terminology.md)

[OPM の機能](opm-features.md)

[ハードウェア機能のスキャンの実行](performing-a-hardware-functionality-scan.md)

[OPM DDI を取得する](retrieving-the-opm-ddi.md)

[OPM DDI の使用](using-the-opm-ddi.md)

[OPM を使用した保護レベルの処理](handling-protection-levels-with-opm.md)

[ディスプレイデバイスの損失の処理](handling-the-loss-of-a-display-device.md)

[保護された出力に関する情報の取得](retrieving-information-about-a-protected-output.md)

[保護された出力に関する COPP と互換性のある情報の取得](retrieving-copp-compatible-information-about-a-protected-output.md)

[保護された出力の構成](configuring-a-protected-output.md)

[保護された出力の状態の報告](reporting-status-of-a-protected-output.md)

[OPM の実装のヒントと要件](implementation-tips-and-requirements-for-opm.md)

 

 





