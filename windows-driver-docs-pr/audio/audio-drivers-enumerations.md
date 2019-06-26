---
title: オーディオ ドライバーの列挙
description: このセクションでは、さまざまなオーディオのプロパティと構造体で使用される列挙体について説明します。
ms.assetid: 9C7530BE-C63F-438C-A853-9A7E47C240E9
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: c29c0a1084bb3cfd2adf69ca1495f93365776cc6
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67355725"
---
# <a name="audio-drivers-enumerations"></a>オーディオ ドライバーの列挙


このセクションでは、さまざまなオーディオのプロパティと構造体で使用される列挙体について説明します。

## <a name="span-idwindows10andlateroperatingsystemsspanspan-idwindows10andlateroperatingsystemsspanspan-idwindows10andlateroperatingsystemsspanwindows10-and-later-operating-systems"></a><span id="Windows_10_and_later_operating_systems"></span><span id="windows_10_and_later_operating_systems"></span><span id="WINDOWS_10_AND_LATER_OPERATING_SYSTEMS"></span>Windows 10 および以降のオペレーティング システム


次の列挙型は、Windows 10 以降のオペレーティング システムで使用されます。

[**テレフォニー\_CALLCONTROLOP**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ne-ksmedia-telephony_callcontrolop)します。 オーディオ ドライバー構造で使用すると、電話で実行する操作を指定します。

[**テレフォニー\_CALLSTATE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ne-ksmedia-telephony_callstate)します。 オーディオ ドライバー構造で使用すると、電話の状態を指定します。

[**テレフォニー\_CALLTYPE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ne-ksmedia-telephony_calltype)します。 電話の種類を指定する、オーディオ ドライバー構造で使用されます。

[**テレフォニー\_PROVIDERCHANGEOP**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ne-ksmedia-telephony_providerchangeop)します。 オーディオ ドライバー構造で使用すると、プロバイダーによって要求された変更操作の種類を指定します。

## <a name="span-idwindows8andlateroperatingsystemsspanspan-idwindows8andlateroperatingsystemsspanspan-idwindows8andlateroperatingsystemsspanwindows8-and-later-operating-systems"></a><span id="Windows_8_and_later_operating_systems"></span><span id="windows_8_and_later_operating_systems"></span><span id="WINDOWS_8_AND_LATER_OPERATING_SYSTEMS"></span>Windows 8 およびそれ以降のオペレーティング システム


次の列挙型は、Windows 8 およびそれ以降のオペレーティング システムで使用されます。

[**オーディオ\_曲線\_型**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ne-ksmedia-audio_curve_type)します。 オーディオ ドライバー構造で使用すると、ボリューム レベルの制御のオーディオ データ ストリームに適用する曲線アルゴリズムの種類を指定します。

[**EPcMiniportEngineEvent**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/ne-portcls-epcminiportengineevent)します。 オーディオ エンジンを使用して、故障エラーに関連する情報を提供します。

[**PC\_終了\_待機時間**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/ne-portcls-_pc_exit_latency)します。 オーディオ ポート クラス ドライバー (PortCls) をスリープ状態を終了するための最大遅延時間を示すために使用状態を完全に機能の状態を入力します。

[**eEngineFormatType**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/ne-portcls-eengineformattype)します。 ミニポートで使用されることを示すドライバー、オーディオ エンジンでサポートされている種類の形式します。

[**eChannelTargetType**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/ne-portcls-echanneltargettype)します。 ミニポート ドライバーで使用すると、オーディオ データ ストリームのパスのノード (ターゲット) の型を指定します。

## <a name="span-idwindows7andearlieroperatingsystemsspanspan-idwindows7andearlieroperatingsystemsspanspan-idwindows7andearlieroperatingsystemsspanwindows7-and-earlier-operating-systems"></a><span id="Windows_7_and_earlier_operating_systems"></span><span id="windows_7_and_earlier_operating_systems"></span><span id="WINDOWS_7_AND_EARLIER_OPERATING_SYSTEMS"></span>Windows 7 と以前のオペレーティング システム


次の列挙型は、Windows 7 と以前のオペレーティング システムで導入されました。

[**KSPROPERTY\_AUDIOENGINE**](ksproperty-audioengine.md)します。 ミニポート ドライバーで使用すると、属性と、オーディオ エンジンのセットアップ パラメーターを指定します。

[**KSPROPERTY\_ジャック**](ksproperty-jack.md)します。 ミニポート ドライバーによって、エンドポイントのオーディオ ジャックの属性を指定するために使用します。

 

 





