---
title: 保護されている出力に関する情報の取得
description: 保護されている出力に関する情報の取得
ms.assetid: 20e268b8-fea0-48dd-a3cd-3cbb4233ef99
keywords:
- OPM WDK 表示、保護された出力情報の取得
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 14c8cea6a9360fbe4ba75ef86a97bc07dbf25630
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72829573"
---
# <a name="retrieving-information-about-a-protected-output"></a>保護されている出力に関する情報の取得


ディスプレイミニポートドライバーは、グラフィックスアダプターの物理出力コネクタに関連付けられている保護された出力に関する情報を取得する要求を受け取ることができます。 表示ミニポートドライバーの[**DxgkDdiOPMGetInformation**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkddi_opm_get_information)関数には、 [**Dxgkmdt\_OPM**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmdt/ns-d3dkmdt-_dxgkmdt_opm_get_info_parameters)にポインターが渡されます。これは、情報要求を格納している*parameters*パラメーターで\_INFO\_PARAMETERS 構造を取得\_ます。 *DxgkDdiOPMGetInformation*は、必要な情報を[**Dxgkmdt\_OPM\_要求された\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmdt/ns-d3dkmdt-_dxgkmdt_opm_requested_information)構造体に書き込み、 *requestedinformation*パラメーターが指しています。 DXGKMDT\_OPM の**Guidinformation**と**abparameters**のメンバーは、情報の要求を指定し\_情報\_のパラメーター\_取得します。 情報の要求に応じて、表示ミニポートドライバーは、 [**dxgkmdt\_OPM\_標準\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmdt/ns-d3dkmdt-_dxgkmdt_opm_standard_information)、 [**dxgkmdt\_OPM\_出力\_ID**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmdt/ns-d3dkmdt-_dxgkmdt_opm_output_id)、または[**DXGKMDT\_OPM\_実際の\_出力\_形式**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmdt/ns-d3dkmdt-_dxgkmdt_opm_actual_output_format)の構造を必要な情報と共に入力し、Dxgkmdt\_OPM の**abrequestedinformation**メンバーをその構造に\_情報を.\_ ドライバーが**cbRequestedInformationSize**を指定した後 (たとえば、SIZEOF (DXGKMDT\_OPM\_標準\_情報))**と、** dxgkmdt\_OPM\_要求された\_情報、ドライバーは、dxgkmdt\_OPM のデータに対して、1キー暗号ブロックチェーン (CBC) モードのメッセージ認証コード (omac) を計算する必要があります。また、要求された\_情報\_、この omac をの**omac**メンバーで設定する必要があります。DXGKMDT\_OPM\_は\_情報を要求しました。 OMAC の計算の詳細については、「 [omac-1 アルゴリズム](https://go.microsoft.com/fwlink/p/?linkid=70417)」を参照してください。

[**DxgkDdiOPMGetInformation**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkddi_opm_get_information)が返される前に、表示ミニポートドライバーは、Dxgkmdt の**omac**メンバーに指定されている omac [ **\_OPM\_GET\_INFO\_PARAMETERS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmdt/ns-d3dkmdt-_dxgkmdt_opm_get_info_parameters)が正しいことを確認する必要があります **。  ** また、ドライバーは、DXGKMDT\_\_\_\_OPM の**ulSequenceNumber**メンバーに指定されているシーケンス番号が、ドライバーに現在格納されているシーケンス番号と一致していることを確認する必要があります。 次に、ドライバーは、格納されているシーケンス番号をインクリメントする必要があります。

 

   ドライバーは、DXGKMDT\_OPM\_標準\_情報、 [**Dxgkmdt\_OPM\_出力\_ID**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmdt/ns-d3dkmdt-_dxgkmdt_opm_output_id)、または DXGKMDT\_OPM\_実際\_出力\_形式の**rnRandomNumber**メンバーで、128ビットの暗号化されたランダムな値を返す必要がある**ことに注意**してください。 乱数は、送信元アプリケーションによって生成されたものであり、DXGKMDT\_OPM の**rnRandomNumber**メンバーに指定されています。\_は\_INFO\_パラメーターを取得します。

 

ドライバーは、指定された要求に対して次の情報を返します。

-   DXGKMDT\_OPM\_\_サポートされている\_PROTECTION\_、 **Guidinformation**メンバーで設定されている種類と、DXGKMDT\_OPM\_GET\_INFO\_PARAMETERS 構造体の**abparameters**メンバーで定義されていない型を取得します。ドライバーは、使用可能な保護メカニズムの種類を示します。 使用可能な保護の種類を示すために、ドライバーは、dxgkmdt [ **\_OPM\_protection\_TYPE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmdt/ne-d3dkmdt-_dxgkmdt_opm_protection_type)列挙\_\_体からの値の有効なビットごとの or の組み合わせを返します。\_ DXGKMDT\_OPM\_PROTECTION\_TYPE\_HDCP および DXGKMDT\_OPM\_PROTECTION\_TYPE\_の値は有効です。

-   DXGKMDT\_OPM\_**Guidinformation**で設定された\_コネクタ\_型を取得し、 **abparameters**では定義されていない場合、ドライバーはコネクタの種類を示します。 コネクタの種類を示すために、ドライバーは、DXGKMDT\_OPM\_標準\_情報の**Ulinformation**メンバーの[**D3DKMDT\_VIDEO\_出力\_テクノロジ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmdt/ne-d3dkmdt-_d3dkmdt_video_output_technology)列挙体から、値の有効なビットごとの or の組み合わせを返します。

-   DXGKMDT\_OPM\_GET\_VIRTUAL\_PROTECTION\_LEVEL または DXGKMDT\_OPM\_\_の実際\_保護\_レベルを設定**します**。また、 **abparameters**で設定されている保護の種類には、 [**DXGKMDT\_OPM\_STANDARD\_INFORMATION**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmdt/ns-d3dkmdt-_dxgkmdt_opm_standard_information)の**ulinformation**メンバーの保護レベルの値が返されます。 保護の種類が DXGKMDT\_OPM\_PROTECTION\_タイプ\_HDCP の場合、保護レベルの値は、 [**Dxgkmdt\_OPM\_HDCP\_protection\_level**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmdt/ne-d3dkmdt-_dxgkmdt_opm_hdcp_protection_level)列挙の値です。 保護の種類が DXGKMDT\_OPM\_PROTECTION\_TYPE\_である場合、保護レベルの値は、 [**Dxgkmdt\_OPM\_cp\_protection\_level**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmdt/ne-d3dkmdt-_dxgkmdt_dpcp_protection_level)列挙の値です。

    DXGKMDT\_OPM\_GET\_VIRTUAL\_PROTECTION\_LEVEL 要求は、現在保護されている出力の保護レベルを設定します。 DXGKMDT\_OPM\_GET\_実際の\_保護\_レベルの要求では、保護された出力に関連付けられている物理コネクタに対して現在設定されている保護レベルが返されます。

-   DXGKMDT\_OPM\_**Guidinformation**で設定された\_アダプター\_バス\_型を取得し、 **abparameters**では定義されていない場合、ドライバーはグラフィックスアダプターをマザーボードチップセットの北ブリッジに接続するバスの種類と実装を識別します。 バスの種類と実装を識別するために、ドライバーは、dxgkmdt [ **\_OPM\_bus\_type\_および\_実装**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmdt/ne-d3dkmdt-_dxgkmdt_opm_bus_type_and_implementation)列挙体から、DXGKMDT\_OPM\_標準\_情報の**ulinformation**メンバーに、有効なビットごとの or の組み合わせを返します。

-   DXGKMDT\_OPM\_、 **Guidinformation**で設定されている現在の\_HDCP\_のバージョンセットを\_取得し、 **abparameters**では定義していない場合、ドライバーは[**DXGKMDT\_OPM\_標準\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmdt/ns-d3dkmdt-_dxgkmdt_opm_standard_information)の**ulinformation**メンバー内の値を返します。この情報は、保護された出力の現在の高帯域幅デジタル\_( 最下位ビット (ビット 0 ~ 15) には、低エンディアン形式での、SRM のバージョン番号が含まれています。 SRM のバージョン番号の詳細については、「 [HDCP 仕様のリビジョン 1.1](https://go.microsoft.com/fwlink/p/?linkid=38728)」を参照してください。

-   DXGKMDT\_OPM\_\_、 **Guidinformation**で設定された実際の\_出力\_形式が設定されていて、 **abparameters**では定義されていない場合、ドライバーは、保護された出力に関連付けられている物理コネクタを通過する信号がどのように書式設定されるかを示す、 [**DXGKMDT\_OPM**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmdt/ns-d3dkmdt-_dxgkmdt_opm_actual_output_format)\_\_\_

-   DXGKMDT\_OPM\_**Guidinformation**で設定された出力\_ID を\_取得し、 **abparameters**では定義されていない場合、ドライバーは、出力コネクタを識別する[**DXGKMDT\_OPM\_output\_id**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmdt/ns-d3dkmdt-_dxgkmdt_opm_output_id)のメンバーの情報を返します。

-   DXGKMDT\_OPM\_、 **Guidinformation**メンバーで設定された\_の DVI\_特性と、DXGKMDT\_OPM\_GET\_INFO\_PARAMETERS 構造体の**abparameters**メンバーに定義されていない場合、ドライバーはデジタルビデオインターフェイス (DVI) 出力コネクタの電気的特性を示します。 DVI の電気的特性を示すために、ドライバーは、Dxgkdt [ **\_OPM\_dvi\_特性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmdt/ne-d3dkmdt-_dxgkdt_opm_dvi_characteristics)の列挙型の値の 1つを[**DXGKDT\_OPM\_標準\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmdt/ns-d3dkmdt-_dxgkmdt_opm_standard_information)に返します。

 

 





