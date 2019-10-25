---
title: OPM DDI の使用
description: OPM DDI の使用
ms.assetid: cd3c78a4-0241-48ab-9005-c544db199eb5
keywords:
- OPM WDK display、about DDI
- OPM WDK 表示、保護された出力の作成
- OPM WDK 表示、保護された出力の破棄
- OPM WDK 表示、証明書の取得
- OPM WDK 表示、保護された出力の構成
- OPM WDK 表示、保護された出力情報の取得
- OPM WDK ディスプレイ、グラフィックスアダプター情報の取得
- 保護レベル WDK 表示、変更
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 162101ace8f03fbd11660a79b229cceb6725b9b3
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72829254"
---
# <a name="using-the-opm-ddi"></a>OPM DDI の使用


Microsoft DirectX グラフィックスのカーネルサブシステム (Dxgkrnl) は、OPM DDI を使用して、OPM で保護された出力の作成、保護された出力の破棄、証明書の取得、保護された出力の構成、保護された出力に関する情報の取得、および取得を行い*ます。* グラフィックスアダプターに関する情報。 DirectX graphics カーネルサブシステムは、ディスプレイミニポートドライバーの[**DxgkDdiQueryInterface**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkddi_query_interface)関数を呼び出して、GUID\_devinterface\_OPM および DXGK によって識別されるインターフェイスを照会するときに、OPM DDI 関数へのポインターを取得します。\_OPM\_INTERFACE\_VERSION\_1。 次のシーケンスは、OPM DDI が OPM 保護された出力を作成、操作、および破棄するために通常使用される方法を示しています。

1.  DirectX graphics カーネルサブシステムは、 [**DxgkDdiOPMCreateProtectedOutput**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkddi_opm_create_protected_output)関数を呼び出して、OPM によって保護された出力を作成します。 OPM で保護された出力は、常に1つの物理的なビデオ出力に対応します。 *DxgkDdiOPMCreateProtectedOutput*は、新しく作成された出力へのハンドルを返します。

2.  DirectX graphics カーネルサブシステムは、 [**DxgkDdiOPMGetCertificateSize**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkddi_opm_get_certificate_size)関数と[**DxgkDdiOPMGetCertificate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkddi_opm_get_certificate)関数を呼び出して、ディスプレイミニポートドライバーの OPM 証明書または copp 証明書とそのサイズを取得します。
    **注**  *DxgkDdiOPMCreateProtectedOutput*、 *DxgkDdiOPMGetCertificateSize*、 *DxgkDdiOPMGetCertificate*は、DirectX グラフィックスカーネルサブシステムが保護された出力ハンドルを渡さない唯一の OPM DDI 関数です.

     

3.  DirectX graphics カーネルサブシステムは、 [**DxgkDdiOPMGetRandomNumber**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkddi_opm_get_random_number)関数を呼び出して、保護された出力の乱数を取得します。

4.  DirectX graphics カーネルサブシステムは、 [**DxgkDdiOPMSetSigningKeyAndSequenceNumbers**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkddi_opm_set_signing_key_and_sequence_numbers)関数の呼び出しで256バイトのバッファーを渡します。 バッファーには、表示ミニポートドライバーの公開キーのいずれかで暗号化されたデータが含まれています。 公開キーの詳細については、出力[Content Protection と Windows Vista](https://download.microsoft.com/download/5/D/6/5D6EAF2B-7DDF-476B-93DC-7CF0072878E6/output_protect.doc)の web サイトから出力 Content Protection ドキュメントをダウンロードしてください。 使用される公開キーは、保護された出力のセマンティクスによって異なります。 保護された出力に OPM セマンティクスがある場合は、表示ミニポートドライバーの OPM 証明書の公開キーが使用されます。 保護された出力に COPP のセマンティクスがある場合は、表示ミニポートドライバーの COPP 証明書の公開キーが使用されます。 データの暗号化に使用される暗号化スキームは、保護された出力のセマンティクスにも依存します。 保護された出力に OPM セマンティクスがある場合、保護された出力に COPP セマンティクスと RSAES-OAEP-ENCRYPT OAEP 暗号化スキームがある場合、データは標準の RSA アルゴリズムで暗号化されます。 RSA、AES、RSAES-OAEP-ENCRYPT-OAEP の詳細については、 [Rsa 研究所](https://go.microsoft.com/fwlink/p/?linkid=70411)の web サイトを参照してください。 表示ミニポートドライバーは、適切な秘密キーと復号化方法を使用してデータの暗号化を解除します。 復号化されたデータには、乱数値、2つのランダムなシーケンス番号、および128ビットの AES キーがあります。 ミニポートドライブの表示では、 [**DxgkDdiOPMGetRandomNumber**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkddi_opm_get_random_number)関数が呼び出されたときにドライバーから返された乱数とランダムな数値が一致することが保証されます。 ドライバーは、2つのシーケンス番号と128ビット AES キーを格納します。

5.  DirectX graphics カーネルサブシステムは、 [**DxgkDdiOPMGetInformation**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkddi_opm_get_information)または[**DxgkDdiOPMGetCOPPCompatibleInformation**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkddi_opm_get_copp_compatible_information)関数を呼び出して、保護された出力から情報を取得できるようになりました。 DirectX graphics カーネルサブシステムは、 [**DxgkDdiOPMConfigureProtectedOutput**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkddi_opm_configure_protected_output)を呼び出して、保護された出力を構成することもできます。 *DxgkDdiOPMGetInformation*は、出力に OPM セマンティクスがある場合にのみ呼び出すことができ、 *DxgkDdiOPMGetCOPPCompatibleInformation*は出力が copp セマンティクスを持っている場合にのみ呼び出すことができます。 通常、DirectX graphics カーネルサブシステムは、 *DxgkDdiOPMGetInformation*または*DxgkDdiOPMGetCOPPCompatibleInformation*を呼び出して出力に関する情報を取得し、 *DxgkDdiOPMConfigureProtectedOutput* 1 つ以上を呼び出します。出力を構成する時間。 次に、DirectX graphics カーネルサブシステムが*DxgkDdiOPMGetInformation*または*DxgkDdiOPMGetCOPPCompatibleInformation*を再度呼び出します。 DirectX グラフィックスカーネルサブシステムは、 *DxgkDdiOPMGetInformation*または*DxgkDdiOPMGetCOPPCompatibleInformation*を呼び出すことによって、次の種類の情報を取得できます。

    -   出力のコネクタの種類。
    -   出力がサポートするコンテンツ保護の種類。 現在、の出力では、アナログコピー保護 (ACP)、[コンテンツ生成管理システムのアナログ (CGMS)](cgms-a-standards.md)、高帯域幅のデジタル CONTENT PROTECTION (HDCP)、DisplayPort Content Protection (cp) がサポートされています。 ACP の詳細については、 [Rovi (旧称 Macrovision)](https://go.microsoft.com/fwlink/p/?linkid=71273)の web サイトを参照してください。 HDCP の詳細については、「 [Hdcp 仕様のリビジョン 1.1](https://go.microsoft.com/fwlink/p/?linkid=38728)」を参照してください。 DisplayPort の詳細については、 [DisplayPort](https://go.microsoft.com/fwlink/p/?linkid=71382)の Web 記事を参照してください。
    -   特定の保護の種類に対する出力の現在の仮想保護レベル。
    -   物理出力の特定の保護の種類の実際の保護レベル。
    -   出力が現在使用している、HDCP システム Renewability メッセージ (SRM) のバージョン。 HDCP SRM の詳細については、「 [Hdcp 仕様のリビジョン 1.1](https://go.microsoft.com/fwlink/p/?linkid=38728)」を参照してください。 この情報を取得できるのは[**DxgkDdiOPMGetInformation**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkddi_opm_get_information)だけです。
    -   接続された HDCP デバイスのキー選択ベクター (KSV) と、HDCP デバイスがリピータであるかどうか。 この情報を取得できるのは[**DxgkDdiOPMGetCOPPCompatibleInformation**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkddi_opm_get_copp_compatible_information)だけです。 HDCP リピータと KSVs の詳細については、「 [Hdcp 仕様のリビジョン 1.1](https://go.microsoft.com/fwlink/p/?linkid=38728)」を参照してください。
    -   グラフィックスアダプターが使用する拡張バスの種類。 PCI と AGP は、拡張バスの例です。
    -   保護された出力に関連付けられている物理コネクタからモニターに送信されるイメージの形式。
    -   保護された出力がサポートする CGMS と ACP のシグナル化標準。 この情報を取得できるのは[**DxgkDdiOPMGetCOPPCompatibleInformation**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkddi_opm_get_copp_compatible_information)だけです。
    -   出力の識別子。
    -   デジタルビデオインターフェイス (DVI) 出力コネクタの電気的特性。

    DirectX グラフィックスのカーネルサブシステムでは、 [**DxgkDdiOPMConfigureProtectedOutput**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkddi_opm_configure_protected_output)を呼び出すことによって次の設定を変更できます。

    -   出力のいずれかの保護の種類の現在の保護レベル。 たとえば、 *DxgkDdiOPMConfigureProtectedOutput*では、HDCP を有効または無効にしたり、acp 保護を無効にしたり、現在の acp 保護レベルを変更したりできます。
    -   保護された出力が使用する現在の HDCP の SRM。
    -   保護された出力が使用する現在のシグナル化標準。 この変更は、出力に COPP セマンティクスがある場合にのみ実行できます。

6.  DirectX graphics カーネルサブシステムは、保護された出力オブジェクトの使用が終了したときに[**DxgkDdiOPMDestroyProtectedOutput**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkddi_opm_destroy_protected_output)を呼び出します。

 

 





