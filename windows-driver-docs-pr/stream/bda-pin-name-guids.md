---
title: BDA Pin 名 Guid
description: BDA Pin 名 Guid
ms.assetid: 098e4c49-13dd-4c9a-8ce4-06b99b7c5fa3
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: e3b7c68f3af51eb0cd9d356311f15ebd44379f46
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840614"
---
# <a name="bda-pin-name-guids"></a>BDA Pin 名 Guid


## <span id="ddk_bda_pin_name_guids_ks"></span><span id="DDK_BDA_PIN_NAME_GUIDS_KS"></span>


BDA ミニドライバーは、サポートする pin の名前とカテゴリを指定するために、BDA ピン名 Guid を使用します。 BDA ミニドライバーは、これらの Guid を[**Kspin\_記述子**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-kspin_descriptor)構造体の**Name**および**Category**メンバーに割り当てます。 これらの Guid は、 *Bdamedia*ヘッダーファイルで定義されています。 フィルターのピンは、名前とカテゴリを指定して、その名前とカテゴリを指定する他のフィルターのピンに接続します。

BDA では、次のピン名 Guid を使用できます。

<span id="PINNAME_BDA_TRANSPORT"></span><span id="pinname_bda_transport"></span>BDA\_TRANSPORT\_PINNAME  
BDA トランスポートピンの名前を固定します。

<span id="PINNAME_BDA_ANALOG_VIDEO"></span><span id="pinname_bda_analog_video"></span>ピン名\_BDA\_アナログ\_ビデオ  
BDA アナログビデオ pin の pin 名。

<span id="PINNAME_BDA_ANALOG_AUDIO"></span><span id="pinname_bda_analog_audio"></span>BDA\_アナログ\_オーディオ\_PINNAME  
BDA アナログオーディオ pin の名前を固定します。

<span id="PINNAME_BDA_FM_RADIO"></span><span id="pinname_bda_fm_radio"></span>PINNAME\_BDA\_FM\_ラジオ  
BDA FM ラジオの pin の名前を指定します。

<span id="PINNAME_BDA_IF_PIN"></span><span id="pinname_bda_if_pin"></span>PIN\_場合は、PINNAME\_BDA\_  
BDA 中間周波数の pin の名前を固定します。

<span id="PINNAME_BDA_OPENCABLE_PSIP_PIN"></span><span id="pinname_bda_opencable_psip_pin"></span>PINNAME\_BDA\_OPENCABLE\_PSIP\_PIN  
BDA オープンケーブルの PSIP pin の名前を固定します。

<span id="PINNAME_IPSINK_INPUT"></span><span id="pinname_ipsink_input"></span>\_入力の PINNAME\_IPSINK  
入力ピンの名前を BDA IP シンクノード (KSK ノード\_BDA\_IP\_SINK) に固定します。

<span id="PINNAME_MPE"></span><span id="pinname_mpe"></span>\_MPE の PINNAME  
マルチプロトコルカプセル化 (MPE) pin の名前を固定します。

 

 





