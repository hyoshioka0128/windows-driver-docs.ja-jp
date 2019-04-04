---
title: 出力 Protection Manager をサポートしています。
description: 出力 Protection Manager をサポートしています。
ms.assetid: 2c138dbd-55ca-4c71-8c8b-b2efd1ca80f2
keywords:
- COPP WDK DirectX va なので、出力 Protection Manager
- 出力 Protection Manager WDK の表示
- OPM WDK の表示
- コピー防止 WDK の表示
- ビデオのコピー防止 WDK の表示
- WDK のビデオ ディスプレイの保護
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: de880c8af0af882a0d5df662f77301b7f1784d31
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56552059"
---
# <a name="supporting-output-protection-manager"></a>出力 Protection Manager をサポートしています。


出力保護マネージャー (OPM) デバイス ドライバー インターフェイス (DDI) は、グラフィックス アダプターのさまざまなコネクタによって出力されるビデオ信号のコピー保護を有効します。 Windows Vista でコンテンツを保護する方法の詳細についてそのグラフィックス アダプターの出力で出力コンテンツの保護ドキュメントをダウンロードして、[出力 Content Protection と Windows Vista](https://download.microsoft.com/download/5/D/6/5D6EAF2B-7DDF-476B-93DC-7CF0072878E6/output_protect.doc) web サイト。

OPM が後継、[認定出力保護プロトコル (COPP)](copp-processing.md)を[Windows 2000 のディスプレイ ドライバー モデル](windows-2000-display-driver-model-design-guide.md)を提供します。 OPM には、すべての COPP の機能がサポートしています。 COPP の機能については、[COPP 概要](introduction-to-copp.md)を参照してください。 OPM には、新機能もサポートしています。

## <a name="opm-interface"></a>OPM インターフェイス

**OPM DDI**に意味が似て、 [COPP DDI](sample-functions-for-copp.md) OPM が Windows Vista のディスプレイ ドライバー モデルの本質的に COPP 1.1 であるためです。 ただし、OPM DDI は OPM DDI と COPP DDI にマップされている、DirectDraw と DirectX ビデオ アクセラレータ (VA) DDI 中に、一連の関数は COPP DDI よりずっとシンプルです。

ディスプレイのミニポート ドライバーは、アプリケーションと、ドライバーでは、Microsoft DirectX グラフィックスのカーネル サブシステム間の保護されているコマンド、情報、および状態の受け渡しをサポートしている場合 (*Dxgkrnl.sys*) が正常に開いたら、ドライバーの OPM DDI します。

OPM インターフェイスを使用する必要があるカーネル モード コンポーネントは、ディスプレイ ミニポート ドライバーへの呼び出しを開始します。 [DxgkDdiQueryInterface](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dispmprt/nc-dispmprt-dxgkddi_query_interface)インターフェイスを取得します。 OPM インターフェイスの関数へのポインターが返されます、 [DXGK_OPM_INTERFACE](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dispmprt/ns-dispmprt-_dxgk_opm_interface)構造体のインターフェイス メンバーは、 [QUERY_INTERFACE](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/video/ns-video-_query_interface)へのポインターを構造体します。 この QUERY_INTERFACE で指し示されます、 *QueryInterface* DxgkDdiQueryInterface 呼び出しのパラメーター。

次の出力保護マネージャー (OPM) インターフェイスの関数は、いくつか表示ミニポート ドライバーによって実装されます。

* [DXGKDDI_OPM_GET_CERTIFICATE_SIZE](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dispmprt/nc-dispmprt-dxgkddi_opm_get_certificate_size)
* [DXGKDDI_OPM_GET_CERTIFICATE](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dispmprt/nc-dispmprt-dxgkddi_opm_get_certificate)
* [DXGKDDI_OPM_CREATE_PROTECTED_OUTPUT](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dispmprt/nc-dispmprt-dxgkddi_opm_create_protected_output)
* [DXGKDDI_OPM_GET_RANDOM_NUMBER](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dispmprt/nc-dispmprt-dxgkddi_opm_get_random_number)
* [DXGKDDI_OPM_SET_SIGNING_KEY_AND_SEQUENCE_NUMBERS](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dispmprt/nc-dispmprt-dxgkddi_opm_set_signing_key_and_sequence_numbers)
* [DXGKDDI_OPM_GET_INFORMATION](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dispmprt/nc-dispmprt-dxgkddi_opm_get_information)
* [DXGKDDI_OPM_GET_COPP_COMPATIBLE_INFORMATION](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dispmprt/nc-dispmprt-dxgkddi_opm_get_copp_compatible_information)
* [DXGKDDI_OPM_CONFIGURE_PROTECTED_OUTPUT](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dispmprt/nc-dispmprt-dxgkddi_opm_configure_protected_output)
* [DXGKDDI_OPM_DESTROY_PROTECTED_OUTPUT](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dispmprt/nc-dispmprt-dxgkddi_opm_destroy_protected_output)

次のトピックでは、サポートおよび OPM DDI の使用方法と OPM の新機能について説明します。

[OPM 用語集](opm-terminology.md)

[OPM 機能](opm-features.md)

[ハードウェアの機能のスキャンを実行します。](performing-a-hardware-functionality-scan.md)

[OPM DDI を取得します。](retrieving-the-opm-ddi.md)

[OPM DDI を使用します。](using-the-opm-ddi.md)

[OPM 保護レベルの処理](handling-protection-levels-with-opm.md)

[ディスプレイ デバイスの損失を処理](handling-the-loss-of-a-display-device.md)

[保護されている出力に関する情報を取得します。](retrieving-information-about-a-protected-output.md)

[保護されている出力に関する COPP と互換性のある情報を取得します。](retrieving-copp-compatible-information-about-a-protected-output.md)

[保護されている出力の構成](configuring-a-protected-output.md)

[保護されている出力のステータスを報告](reporting-status-of-a-protected-output.md)

[実装のヒントと OPM の要件](implementation-tips-and-requirements-for-opm.md)

 

 





