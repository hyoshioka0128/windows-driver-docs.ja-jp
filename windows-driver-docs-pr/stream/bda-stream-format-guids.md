---
title: BDA ストリーム形式の GUID
description: BDA ストリーム形式の GUID
ms.assetid: 216fb02c-b49b-4b9f-b7a5-220c718fb202
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 29af6951e89db2d2d99b90f858280fe6d73226e0
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56571804"
---
# <a name="bda-stream-format-guids"></a>BDA ストリーム形式の GUID


## <span id="ddk_bda_stream_format_guids_ks"></span><span id="DDK_BDA_STREAM_FORMAT_GUIDS_KS"></span>


BDA ミニドライバーは BDA ストリーム形式の Guid を使用して、サポート データ形式を指定します。 BDA ミニドライバー割り当てます Guid のメンバーに、 [ **KSDATARANGE** ](https://msdn.microsoft.com/library/windows/hardware/ff561658)構造体。 *Bdamedia.h*ヘッダー ファイルには、これらの Guid が定義されています。 フィルターのピンは、これらの範囲をサポートするその他のフィルターのピンに接続するためにサポートされるデータ形式の範囲を指定します。

Guid の次のストリームは BDA で使用できます。

<span id="KSDATAFORMAT_TYPE_BDA_ANTENNA"></span><span id="ksdataformat_type_bda_antenna"></span>KSDATAFORMAT\_型\_BDA\_アンテナ  
BDA ミニドライバーは、この GUID を割り当てます、 **MajorFormat**のメンバー、 **DataRange**のメンバー、 [ **KS\_DATARANGE\_BDA\_アンテナ**](https://msdn.microsoft.com/library/windows/hardware/ff567343)ネットワーク プロバイダーのフィルターなどの特定のアップ ストリーム フィルターへの接続を有効にする構造体。

<span id="KSDATAFORMAT_SUBTYPE_BDA_MPEG2_TRANSPORT"></span><span id="ksdataformat_subtype_bda_mpeg2_transport"></span>KSDATAFORMAT\_サブタイプ\_BDA\_MPEG2\_トランスポート  
BDA ミニドライバーは、この GUID を割り当てます、**サブフォーマット**もこのサブ形式を代入するフィルターの暗証番号 (pin) への接続を有効にする KSDATARANGE 構造体のメンバー。

<span id="KSDATAFORMAT_SPECIFIER_BDA_TRANSPORT"></span><span id="ksdataformat_specifier_bda_transport"></span>KSDATAFORMAT\_指定子\_BDA\_トランスポート  
BDA ミニドライバーは、この GUID を割り当てます、**指定子**か KSDATARANGE 構造体のメンバー、または**DataRange**のメンバー、 [ **KS\_DATARANGE\_BDA\_トランスポート**](https://msdn.microsoft.com/library/windows/hardware/ff567346)もこの指定子を指定するフィルターの暗証番号 (pin) への接続を有効にする構造体。

<span id="KSDATAFORMAT_TYPE_BDA_IF_SIGNAL"></span><span id="ksdataformat_type_bda_if_signal"></span>KSDATAFORMAT\_型\_BDA\_場合\_シグナル  
BDA ミニドライバーは、この GUID を割り当てます、 **MajorFormat**もこのメジャーの形式を代入するフィルターの暗証番号 (pin) への接続を有効にする KSDATARANGE 構造体のメンバー。

<span id="KSDATAFORMAT_TYPE_MPEG2_SECTIONS"></span><span id="ksdataformat_type_mpeg2_sections"></span>KSDATAFORMAT\_型\_MPEG2\_セクション  
BDA ミニドライバーは、この GUID を割り当てます、 **MajorFormat**もこのメジャーの形式を代入するフィルターの暗証番号 (pin) への接続を有効にする KSDATARANGE 構造体のメンバー。

<span id="KSDATAFORMAT_SUBTYPE_ATSC_SI"></span><span id="ksdataformat_subtype_atsc_si"></span>KSDATAFORMAT\_サブタイプ\_ATSC\_SI  
BDA ミニドライバーは、この GUID を割り当てます、**サブフォーマット**もこのサブ形式を代入するフィルターの暗証番号 (pin) への接続を有効にする KSDATARANGE 構造体のメンバー。

<span id="KSDATAFORMAT_SUBTYPE_DVB_SI"></span><span id="ksdataformat_subtype_dvb_si"></span>KSDATAFORMAT\_サブタイプ\_DVB\_SI  
BDA ミニドライバーは、この GUID を割り当てます、**サブフォーマット**もこのサブ形式を代入するフィルターの暗証番号 (pin) への接続を有効にする KSDATARANGE 構造体のメンバー。

<span id="KSDATAFORMAT_SUBTYPE_BDA_OPENCABLE_PSIP"></span><span id="ksdataformat_subtype_bda_opencable_psip"></span>KSDATAFORMAT\_サブタイプ\_BDA\_OPENCABLE\_PSIP  
BDA ミニドライバーは、この GUID を割り当てます、**サブフォーマット**もこのサブ形式を代入するフィルターの暗証番号 (pin) への接続を有効にする KSDATARANGE 構造体のメンバー。

<span id="KSDATAFORMAT_SUBTYPE_BDA_OPENCABLE_OOB_PSIP"></span><span id="ksdataformat_subtype_bda_opencable_oob_psip"></span>KSDATAFORMAT\_サブタイプ\_BDA\_OPENCABLE\_OOB\_PSIP  
BDA ミニドライバーは、この GUID を割り当てます、**サブフォーマット**もこのサブ形式を代入するフィルターの暗証番号 (pin) への接続を有効にする KSDATARANGE 構造体のメンバー。

<span id="KSDATAFORMAT_TYPE_BDA_IP"></span><span id="ksdataformat_type_bda_ip"></span>KSDATAFORMAT\_型\_BDA\_IP  
BDA ミニドライバーは、この GUID を割り当てます、 **MajorFormat**もこのメジャーの形式を代入するフィルターの暗証番号 (pin) への接続を有効にする KSDATARANGE 構造体のメンバー。

<span id="KSDATAFORMAT_SUBTYPE_BDA_IP"></span><span id="ksdataformat_subtype_bda_ip"></span>KSDATAFORMAT\_サブタイプ\_BDA\_IP  
BDA ミニドライバーは、この GUID を割り当てます、**サブフォーマット**もこのサブ形式を代入するフィルターの暗証番号 (pin) への接続を有効にする KSDATARANGE 構造体のメンバー。

<span id="KSDATAFORMAT_SPECIFIER_BDA_IP"></span><span id="ksdataformat_specifier_bda_ip"></span>KSDATAFORMAT\_指定子\_BDA\_IP  
BDA ミニドライバーは、この GUID を割り当てます、**指定子**もこの指定子を指定するフィルターの暗証番号 (pin) への接続を有効にするか KSDATARANGE 構造体のメンバー。

<span id="KSDATAFORMAT_TYPE_BDA_IP_CONTROL"></span><span id="ksdataformat_type_bda_ip_control"></span>KSDATAFORMAT\_型\_BDA\_IP\_コントロール  
BDA ミニドライバーは、この GUID を割り当てます、 **MajorFormat**もこのメジャーの形式を代入するフィルターの暗証番号 (pin) への接続を有効にする KSDATARANGE 構造体のメンバー。

<span id="KSDATAFORMAT_SUBTYPE_BDA_IP_CONTROL"></span><span id="ksdataformat_subtype_bda_ip_control"></span>KSDATAFORMAT\_サブタイプ\_BDA\_IP\_コントロール  
BDA ミニドライバーは、この GUID を割り当てます、**サブフォーマット**もこのサブ形式を代入するフィルターの暗証番号 (pin) への接続を有効にする KSDATARANGE 構造体のメンバー。

<span id="KSDATAFORMAT_TYPE_MPE"></span><span id="ksdataformat_type_mpe"></span>KSDATAFORMAT\_型\_MPE  
BDA ミニドライバーは、この GUID を割り当てます、 **MajorFormat**もこのメジャーの形式を代入するフィルターの暗証番号 (pin) への接続を有効にする KSDATARANGE 構造体のメンバー。

 

 





