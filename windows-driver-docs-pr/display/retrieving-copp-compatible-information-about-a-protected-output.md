---
title: 保護されている出力に関する COPP 互換情報の取得
description: 表示ミニポートドライバーは、グラフィックスアダプターの物理出力コネクタに関連付けられている保護された出力に関する、COPP と互換性のある情報を取得する要求を受け取ることができます。
ms.assetid: 9114f232-4123-47a8-b43d-62d14b9f6b08
keywords:
- OPM WDK の表示、COPP と互換性のある情報の取得
ms.date: 12/06/2018
ms.localizationpriority: medium
ms.custom: seodec18
ms.openlocfilehash: 0e74c2c8a5f6118c356f36d8d0fd5a2293c65bd0
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72825833"
---
# <a name="retrieving-copp-compatible-information-on-protected-output"></a>保護されている出力に関する COPP 互換情報の取得


表示ミニポートドライバーは、グラフィックスアダプターの物理出力コネクタに関連付けられている保護された出力に関する、COPP と互換性のある情報を取得する要求を受け取ることができます。 表示ミニポートドライバーの[**DxgkDdiOPMGetCOPPCompatibleInformation**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkddi_opm_get_copp_compatible_information)関数には、 [**Dxgkmdt\_OPM\_COPP\_互換性のある\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmdt/ns-d3dkmdt-_dxgkmdt_opm_copp_compatible_get_info_parameters) 、情報要求を含む*parameters*パラメーターに\_INFO\_parameters 構造体へのポインターが渡されます。 *DxgkDdiOPMGetCOPPCompatibleInformation*は、必要な情報を[**Dxgkmdt\_OPM\_要求された\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmdt/ns-d3dkmdt-_dxgkmdt_opm_requested_information)構造体に書き込み、 *requestedinformation*パラメーターが指しています。 DXGKMDT\_OPM\_COPP\_互換性の\_ある、\_INFO\_のパラメーターの**guidinformation**と**abparameters**のメンバーは、情報の要求を指定します。 情報の要求に応じて、表示ミニポートドライバーは、 [**dxgkmdt\_OPM\_標準\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmdt/ns-d3dkmdt-_dxgkmdt_opm_standard_information)、 [**dxgkmdt\_OPM\_実際\_出力\_形式**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmdt/ns-d3dkmdt-_dxgkmdt_opm_actual_output_format)、 [**DXGKMDT\_OPM\_ACP\_と\_CGMSA\_シグナリング**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmdt/ns-d3dkmdt-_dxgkmdt_opm_acp_and_cgmsa_signaling)、または[**DXGKMDT\_OPM\_接続さ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmdt/ns-d3dkmdt-_dxgkmdt_opm_connected_hdcp_device_information)れている必要のあるデバイス\_情報構造を設定します。また、DXGKMDT\_OPM の**Abrequestedinformation**メンバーが、その構造に\_情報を要求\_ます。\_\_ ドライバーが**cbRequestedInformationSize**を指定した後 (たとえば、 <strong>sizeof (</strong>dxgkmdt\_OPM\_標準\_情報<strong>)</strong>) と、DXGKMDT\_OPM\_要求された\_情報**について**、ドライバーは、dxgkmdt\_OPM 内のデータに対して1キー暗号ブロックチェーン (CBC) モードのメッセージ認証コード (omac) を計算する必要があり、この omac**を**DXGKMDT\_OPM の omac メンバーは、要求された\_情報\_ます。\_\_ OMAC の計算の詳細については、「 [omac-1 アルゴリズム](https://go.microsoft.com/fwlink/p/?linkid=70417)」を参照してください。

[**DxgkDdiOPMGetCOPPCompatibleInformation**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkddi_opm_get_copp_compatible_information)が返される前に、表示ミニポートドライバーは、DXGKMDT の**ulSequenceNumber**メンバーに指定されているシーケンス番号\_OPM\_copp\_互換性のある\_取得\_情報\_パラメーターが、ドライバーに現在格納されているシーケンス番号と一致していることを確認する必要が**あり  。** 次に、ドライバーは、格納されているシーケンス番号をインクリメントする必要があります。

 

**   ドライバー**は、dxgkmdt\_OPM\_の標準\_情報、DXGKMDT\_OPM\_実際\_出力\_形式、DXGKMDT\_OPM\_ACP\_と\_CGMSA\_シグナ**リング、また**は dxgkmdt\_OPM\_接続されている\_デバイス\_の情報を128返します。\_ ランダムな数値は、送信元アプリケーションによって生成されたものであり、DXGKMDT\_OPM\_COPP\_互換性の\_ある\_INFO\_PARAMETERS パラメーターの**rnRandomNumber**メンバーに指定されています。

 

ドライバーは、指定された要求に対して次の情報を返します。

-   DXGKMDT\_OPM\_\_サポートされている\_PROTECTION\_、 **Guidinformation**メンバーで設定されている型と、DXGKMDT\_OPM\_Copp の**abparameters**メンバーで定義されていない型を取得します。これらの\_は、互換性のある\_GET\_INFO\_パラメーターを示します。 使用可能な保護の種類を示すために、ドライバーは、dxgkmdt [ **\_OPM\_protection\_TYPE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmdt/ne-d3dkmdt-_dxgkmdt_opm_protection_type)列挙\_\_体からの値の有効なビットごとの or の組み合わせを返します。\_ DXGKMDT\_OPM\_PROTECTION\_TYPE\_ACP、DXGKMDT\_OPM\_PROTECTION\_TYPE\_CGMSA、および DXGKMDT\_OPM\_PROTECTION\_TYPE\_COPP\_互換性のある\_HDCP 値が有効です。

-   DXGKMDT\_OPM\_**Guidinformation**で設定された\_コネクタ\_型を取得し、 **abparameters**では定義されていない場合、ドライバーはコネクタの種類を示します。 コネクタの種類を示すために、ドライバーは、DXGKMDT\_OPM\_標準\_情報の**Ulinformation**メンバーの[**D3DKMDT\_VIDEO\_出力\_テクノロジ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmdt/ne-d3dkmdt-_d3dkmdt_video_output_technology)列挙体から、値の有効なビットごとの or の組み合わせを返します。

-   DXGKMDT\_OPM\_GET\_VIRTUAL\_PROTECTION\_LEVEL または DXGKMDT\_OPM\_\_の実際\_保護\_レベルを設定**します**。また、 **abparameters**で設定されている保護の種類には、 [**DXGKMDT\_OPM\_STANDARD\_INFORMATION**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmdt/ns-d3dkmdt-_dxgkmdt_opm_standard_information)の**ulinformation**メンバーの保護レベルの値が返されます。 保護の種類が DXGKMDT\_OPM\_PROTECTION\_TYPE\_ACP の場合、保護レベルの値は、 [**Dxgkmdt\_OPM\_acp\_protection\_level**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmdt/ne-d3dkmdt-_dxgkmdt_opm_acp_protection_level)列挙です。 保護の種類が DXGKMDT\_OPM\_PROTECTION\_TYPE\_CGMSA の場合、保護レベルの値は[**dxgkmdt\_OPM\_CGMSA**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmdt/ne-d3dkmdt-_dxgkmdt_opm_cgmsa)列挙の値です。 保護の種類が DXGKMDT\_OPM\_PROTECTION\_TYPE\_COPP\_互換性のある\_HDCP の場合、保護レベルの値は[**Dxgkmdt\_OPM\_hdcp\_protection\_level**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmdt/ne-d3dkmdt-_dxgkmdt_opm_hdcp_protection_level)列挙です。

    DXGKMDT\_OPM\_GET\_VIRTUAL\_PROTECTION\_LEVEL 要求は、現在保護されている出力の保護レベルを設定します。 DXGKMDT\_OPM\_GET\_実際の\_保護\_レベルの要求では、保護された出力に関連付けられている物理コネクタに対して現在設定されている保護レベルが返されます。

-   DXGKMDT\_OPM\_**Guidinformation**で設定された\_アダプター\_バス\_型を取得し、 **abparameters**では定義されていない場合、ドライバーはグラフィックスアダプターをマザーボードチップセットの北ブリッジに接続するバスの種類を識別します。 バスの種類を識別するために、ドライバーは、dxgkmdt [ **\_OPM\_bus\_type\_および\_実装**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmdt/ne-d3dkmdt-_dxgkmdt_opm_bus_type_and_implementation)列挙体から、DXGKMDT\_OPM\_標準\_情報の**ulinformation**メンバー内の値の有効なビットごとの or の組み合わせを返します。

    このドライバーでは、DXGKMDT\_OPM\_COPP\_互換性のある\_BUS\_TYPE\_INTEGRATED (0x80000000) 値とバス型の値のいずれかを組み合わせることができます。これは、グラフィックスアダプターとその他のサブシステムの間のインターフェイス信号が、公開されている仕様と標準コネクタの種類を使用する拡張バスで使用でき メモリバスは、この定義から除外されます。

-   DXGKMDT\_OPM\_\_、 **Guidinformation**で設定された実際の\_出力\_形式が設定されていて、 **abparameters**では定義されていない場合、ドライバーは、保護された出力に関連付けられている物理コネクタを通過する信号がどのように書式設定されるかを示す、 [**DXGKMDT\_OPM**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmdt/ns-d3dkmdt-_dxgkmdt_opm_actual_output_format)\_\_\_

-   DXGKMDT\_OPM\_\_の ACP\_および\_CGMSA\_シグナリングのシグナル**設定を取得し**、 **abparameters**では定義されていない場合、ドライバーは、保護された出力に関連付けられている物理コネクタを通過する信号が保護される方法を説明する[**DXGKMDT\_OPM\_ACP\_および\_CGMSA\_シグナリング**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmdt/ns-d3dkmdt-_dxgkmdt_opm_acp_and_cgmsa_signaling)

-   DXGKMDT\_OPM\_\_接続されている\_HDCP\_デバイス\_情報**に設定**され、 **abparameters**では定義されていない場合、ドライバーは[**dxgkmdt\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmdt/ns-d3dkmdt-_dxgkmdt_opm_connected_hdcp_device_information)のメンバーの情報を返します。この情報は、帯域幅のデジタル\_(HDCP) 情報を含む、デバイス\_\_のです。\_

 

 





