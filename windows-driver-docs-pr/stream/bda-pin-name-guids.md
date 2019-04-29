---
title: BDA ピン名の GUID
description: BDA ピン名の GUID
ms.assetid: 098e4c49-13dd-4c9a-8ce4-06b99b7c5fa3
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: e2eb03d509e2755604b5c0ec3b6519afe32053a8
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63392719"
---
# <a name="bda-pin-name-guids"></a>BDA ピン名の GUID


## <span id="ddk_bda_pin_name_guids_ks"></span><span id="DDK_BDA_PIN_NAME_GUIDS_KS"></span>


BDA ミニドライバーは、名前と pin のサポートのカテゴリを指定するのに BDA 暗証番号 (pin) 名の Guid を使用します。 BDA ミニドライバー割り当てます Guid を**名前**と**カテゴリ**のメンバー、 [ **KSPIN\_記述子**](https://msdn.microsoft.com/library/windows/hardware/ff563533)構造体。 *Bdamedia.h*ヘッダー ファイルには、これらの Guid が定義されています。 フィルターのピンは、その名前ともそれらの名前とカテゴリを指定するその他のフィルターのピンに接続するためのカテゴリを指定します。

次の暗証番号 (pin) 名の Guid を BDA で使用できます。

<span id="PINNAME_BDA_TRANSPORT"></span><span id="pinname_bda_transport"></span>PINNAME\_BDA\_トランスポート  
BDA トランスポート暗証番号 (pin) の暗証番号 (pin) の名前です。

<span id="PINNAME_BDA_ANALOG_VIDEO"></span><span id="pinname_bda_analog_video"></span>PINNAME\_BDA\_アナログ\_ビデオ  
BDA アナログ ビデオ ピンの暗証番号 (pin) の名前。

<span id="PINNAME_BDA_ANALOG_AUDIO"></span><span id="pinname_bda_analog_audio"></span>PINNAME\_BDA\_アナログ\_オーディオ  
BDA アナログ オーディオ ピンの暗証番号 (pin) の名前です。

<span id="PINNAME_BDA_FM_RADIO"></span><span id="pinname_bda_fm_radio"></span>PINNAME\_BDA\_FM\_ラジオ  
BDA FM ラジオ暗証番号 (pin) の暗証番号 (pin) の名前です。

<span id="PINNAME_BDA_IF_PIN"></span><span id="pinname_bda_if_pin"></span>PINNAME\_BDA\_場合\_暗証番号 (PIN)  
BDA 中間頻度暗証番号 (pin) の暗証番号 (pin) の名前です。

<span id="PINNAME_BDA_OPENCABLE_PSIP_PIN"></span><span id="pinname_bda_opencable_psip_pin"></span>PINNAME\_BDA\_OPENCABLE\_PSIP\_暗証番号 (PIN)  
BDA オープン ケーブル PSIP 暗証番号 (pin) の暗証番号 (pin) の名前です。

<span id="PINNAME_IPSINK_INPUT"></span><span id="pinname_ipsink_input"></span>PINNAME\_IPSINK\_入力  
入力ピンの BDA IP シンク ノードに暗証番号 (pin) の名前 (KSNODE\_BDA\_IP\_シンク)。

<span id="PINNAME_MPE"></span><span id="pinname_mpe"></span>PINNAME\_MPE  
マルチ プロトコルのカプセル化 (MPE) の暗証番号 (pin) の暗証番号 (pin) の名前です。

 

 





