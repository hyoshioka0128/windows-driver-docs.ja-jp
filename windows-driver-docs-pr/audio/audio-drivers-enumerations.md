---
title: オーディオ ドライバーの列挙
description: ここでは、さまざまなオーディオプロパティと構造体で使用される列挙体について説明します。
ms.assetid: 9C7530BE-C63F-438C-A853-9A7E47C240E9
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6b30fde28cc6df51351af2e56776a05283914c5f
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72831363"
---
# <a name="audio-drivers-enumerations"></a>オーディオ ドライバーの列挙


ここでは、さまざまなオーディオプロパティと構造体で使用される列挙体について説明します。

## <a name="span-idwindows_10_and_later_operating_systemsspanspan-idwindows_10_and_later_operating_systemsspanspan-idwindows_10_and_later_operating_systemsspanwindows10-and-later-operating-systems"></a><span id="Windows_10_and_later_operating_systems"></span><span id="windows_10_and_later_operating_systems"></span><span id="WINDOWS_10_AND_LATER_OPERATING_SYSTEMS"></span>Windows 10 以降のオペレーティングシステム


Windows 10 以降のオペレーティングシステムでは、次の列挙型が使用されます。

[**テレフォニー\_呼び出し制御 LOP**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ne-ksmedia-telephony_callcontrolop)。 電話で実行する操作を指定するために、オーディオドライバーの構造体によって使用されます。

[**テレフォニー\_CALLSTATE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ne-ksmedia-telephony_callstate)。 オーディオドライバー構造体で、通話の状態を指定するために使用されます。

[**テレフォニー\_CALLTYPE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ne-ksmedia-telephony_calltype)。 オーディオドライバーの構造体で、電話の種類を指定するために使用されます。

[**テレフォニー\_PROVIDERCHANGEOP**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ne-ksmedia-telephony_providerchangeop)。 プロバイダーによって要求された変更操作の種類を指定するために、オーディオドライバー構造体によって使用されます。

## <a name="span-idwindows_8_and_later_operating_systemsspanspan-idwindows_8_and_later_operating_systemsspanspan-idwindows_8_and_later_operating_systemsspanwindows8-and-later-operating-systems"></a><span id="Windows_8_and_later_operating_systems"></span><span id="windows_8_and_later_operating_systems"></span><span id="WINDOWS_8_AND_LATER_OPERATING_SYSTEMS"></span>Windows 8 以降のオペレーティングシステム


Windows 8 以降のオペレーティングシステムでは、次の列挙型が使用されます。

[**オーディオ\_曲線\_型**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ne-ksmedia-audio_curve_type)。 オーディオドライバー構造体によって使用され、ボリュームレベルコントロールのオーディオデータストリームに適用する必要がある曲線アルゴリズムの種類を示します。

[**EPcMiniportEngineEvent**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/ne-portcls-epcminiportengineevent)。 Glitching エラーに関連する情報を提供するためにオーディオエンジンによって使用されます。

[**PC\_終了\_待機時間**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/ne-portcls-_pc_exit_latency)。 オーディオポートクラスドライバー (PortCls) によって使用され、スリープ状態を終了して完全な機能状態になるまでの最大遅延時間を示します。

[**eEngineFormatType**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/ne-portcls-eengineformattype)。 ミニポートドライバーが、オーディオエンジンによってサポートされるデータ形式の種類を示すために使用されます。

[**eChannelTargetType**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/ne-portcls-echanneltargettype)。 ミニポートドライバーが、オーディオデータストリームのパスにあるノード (ターゲット) の種類を示すために使用されます。

## <a name="span-idwindows_7_and_earlier_operating_systemsspanspan-idwindows_7_and_earlier_operating_systemsspanspan-idwindows_7_and_earlier_operating_systemsspanwindows7-and-earlier-operating-systems"></a><span id="Windows_7_and_earlier_operating_systems"></span><span id="windows_7_and_earlier_operating_systems"></span><span id="WINDOWS_7_AND_EARLIER_OPERATING_SYSTEMS"></span>Windows 7 以前のオペレーティングシステム


Windows 7 以前のオペレーティングシステムでは、次の列挙が導入されました。

[**Ksk プロパティ\_AUDIOENGINE**](ksproperty-audioengine.md)。 ミニポートドライバーによって使用され、オーディオエンジンの属性およびセットアップパラメーターを指定します。

[**Ksk プロパティ\_ジャック**](ksproperty-jack.md)。 ミニポートドライバーによって、オーディオエンドポイントジャックの属性を指定するために使用されます。

 

 





