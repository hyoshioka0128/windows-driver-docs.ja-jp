---
title: BDA ストリーム形式 Guid
description: BDA ストリーム形式 Guid
ms.assetid: 216fb02c-b49b-4b9f-b7a5-220c718fb202
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: ecc7decc5d4f467251b53c2a5981312bb8bd3f83
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840613"
---
# <a name="bda-stream-format-guids"></a>BDA ストリーム形式 Guid


## <span id="ddk_bda_stream_format_guids_ks"></span><span id="DDK_BDA_STREAM_FORMAT_GUIDS_KS"></span>


BDA ミニドライバーは、BDA ストリーム形式の Guid を使用して、サポートするデータ形式を指定します。 BDA ミニドライバーは、これらの Guid を[**Ksk datarの**](https://docs.microsoft.com/previous-versions/ff561658(v=vs.85))構造体のメンバーに割り当てます。 これらの Guid は、 *Bdamedia*ヘッダーファイルで定義されています。 フィルターのピンは、これらの範囲をサポートする他のフィルターのピンに接続するためにサポートするデータ形式の範囲を指定します。

次のストリーム Guid は、BDA で使用できます。

<span id="KSDATAFORMAT_TYPE_BDA_ANTENNA"></span><span id="ksdataformat_type_bda_antenna"></span>KSDATAFORMAT\_TYPE\_BDA\_アンテナ  
BDA ミニドライバーは、この GUID を、ネットワークプロバイダーなどの特定のアップストリームフィルターへの接続を可能にするために、 [ **\_BDA\_アンテナ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/bdamedia/ns-bdamedia-tagks_datarange_bda_antenna)構造の\_の**Datarange**の**MajorFormat**メンバーに割り当てます。フィルター.

<span id="KSDATAFORMAT_SUBTYPE_BDA_MPEG2_TRANSPORT"></span><span id="ksdataformat_subtype_bda_mpeg2_transport"></span>KSDATAFORMAT\_のサブタイプ\_BDA\_の MPEG2\_トランスポート  
BDA ミニドライバーは、この GUID を KSK DATARの構造の**サブフォーマット**メンバーに割り当てて、このサブ形式も割り当てられるフィルターのピンに接続できるようにします。

<span id="KSDATAFORMAT_SPECIFIER_BDA_TRANSPORT"></span><span id="ksdataformat_specifier_bda_transport"></span>KSDATAFORMAT\_指定子\_BDA\_TRANSPORT  
BDA ミニドライバーは、この GUID を、KSDATARANGE 構造体の**指定子**メンバーまたは[ **\_BDA\_トランスポート**](https://docs.microsoft.com/windows-hardware/drivers/ddi/bdamedia/ns-bdamedia-tagks_datarange_bda_transport)構造の**datar**\_メンバーに割り当てて、フィルターのピンに接続できるようにします。また、この指定子を割り当てます。

<span id="KSDATAFORMAT_TYPE_BDA_IF_SIGNAL"></span><span id="ksdataformat_type_bda_if_signal"></span>KSDATAFORMAT\_型\_BDA\_(\_シグナルの場合)  
BDA ミニドライバーは、この GUID を KSK **DatarMajorFormat**構造体のメンバーに割り当てて、このメジャー形式も割り当てられるフィルターのピンに接続できるようにします。

<span id="KSDATAFORMAT_TYPE_MPEG2_SECTIONS"></span><span id="ksdataformat_type_mpeg2_sections"></span>KSDATAFORMAT\_TYPE\_MPEG2\_セクション  
BDA ミニドライバーは、この GUID を KSK **DatarMajorFormat**構造体のメンバーに割り当てて、このメジャー形式も割り当てられるフィルターのピンに接続できるようにします。

<span id="KSDATAFORMAT_SUBTYPE_ATSC_SI"></span><span id="ksdataformat_subtype_atsc_si"></span>KSDATAFORMAT\_サブタイプ\_ATSC\_SI  
BDA ミニドライバーは、この GUID を KSK DATARの構造の**サブフォーマット**メンバーに割り当てて、このサブ形式も割り当てられるフィルターのピンに接続できるようにします。

<span id="KSDATAFORMAT_SUBTYPE_DVB_SI"></span><span id="ksdataformat_subtype_dvb_si"></span>KSDATAFORMAT\_SUBTYPE\_DVB-T\_SI  
BDA ミニドライバーは、この GUID を KSK DATARの構造の**サブフォーマット**メンバーに割り当てて、このサブ形式も割り当てられるフィルターのピンに接続できるようにします。

<span id="KSDATAFORMAT_SUBTYPE_BDA_OPENCABLE_PSIP"></span><span id="ksdataformat_subtype_bda_opencable_psip"></span>KSDATAFORMAT\_SUBTYPE\_BDA\_OPENCABLE\_PSIP  
BDA ミニドライバーは、この GUID を KSK DATARの構造の**サブフォーマット**メンバーに割り当てて、このサブ形式も割り当てられるフィルターのピンに接続できるようにします。

<span id="KSDATAFORMAT_SUBTYPE_BDA_OPENCABLE_OOB_PSIP"></span><span id="ksdataformat_subtype_bda_opencable_oob_psip"></span>KSDATAFORMAT\_SUBTYPE\_BDA\_OPENCABLE\_OOB\_PSIP  
BDA ミニドライバーは、この GUID を KSK DATARの構造の**サブフォーマット**メンバーに割り当てて、このサブ形式も割り当てられるフィルターのピンに接続できるようにします。

<span id="KSDATAFORMAT_TYPE_BDA_IP"></span><span id="ksdataformat_type_bda_ip"></span>KSDATAFORMAT\_TYPE\_BDA\_IP  
BDA ミニドライバーは、この GUID を KSK **DatarMajorFormat**構造体のメンバーに割り当てて、このメジャー形式も割り当てられるフィルターのピンに接続できるようにします。

<span id="KSDATAFORMAT_SUBTYPE_BDA_IP"></span><span id="ksdataformat_subtype_bda_ip"></span>KSDATAFORMAT\_サブタイプ\_BDA\_IP  
BDA ミニドライバーは、この GUID を KSK DATARの構造の**サブフォーマット**メンバーに割り当てて、このサブ形式も割り当てられるフィルターのピンに接続できるようにします。

<span id="KSDATAFORMAT_SPECIFIER_BDA_IP"></span><span id="ksdataformat_specifier_bda_ip"></span>KSDATAFORMAT\_指定子\_BDA\_IP  
BDA ミニドライバーは、この指定子を割り当てるフィルターのピンへの接続を可能にするために、この GUID を KSK DATARの構造体の**指定子**メンバーに割り当てます。

<span id="KSDATAFORMAT_TYPE_BDA_IP_CONTROL"></span><span id="ksdataformat_type_bda_ip_control"></span>KSDATAFORMAT\_TYPE\_BDA\_IP\_制御  
BDA ミニドライバーは、この GUID を KSK **DatarMajorFormat**構造体のメンバーに割り当てて、このメジャー形式も割り当てられるフィルターのピンに接続できるようにします。

<span id="KSDATAFORMAT_SUBTYPE_BDA_IP_CONTROL"></span><span id="ksdataformat_subtype_bda_ip_control"></span>KSDATAFORMAT\_サブタイプ\_BDA\_IP\_制御  
BDA ミニドライバーは、この GUID を KSK DATARの構造の**サブフォーマット**メンバーに割り当てて、このサブ形式も割り当てられるフィルターのピンに接続できるようにします。

<span id="KSDATAFORMAT_TYPE_MPE"></span><span id="ksdataformat_type_mpe"></span>KSDATAFORMAT\_TYPE\_MPE  
BDA ミニドライバーは、この GUID を KSK **DatarMajorFormat**構造体のメンバーに割り当てて、このメジャー形式も割り当てられるフィルターのピンに接続できるようにします。

 

 





