---
title: オーディオ ドライバーの構造体
description: オーディオ ドライバーの構造体
ms.assetid: 8257342f-474a-42b3-809d-96fdeede398b
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2c4f571f489db5b64795718c78cbe6a3082deb46
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56582352"
---
# <a name="audio-drivers-structures"></a>オーディオ ドライバーの構造体


## <span id="ddk_audio_drivers_structures_ks"></span><span id="DDK_AUDIO_DRIVERS_STRUCTURES_KS"></span>


このセクションでは、WDM オーディオ ミニポート ドライバーによって使用される構造について説明します。 構造体のリストは次のとおりです。

[**APO\_REG\_プロパティ**](https://msdn.microsoft.com/library/windows/hardware/dn425140)

[**APOInitBaseStruct**](https://msdn.microsoft.com/library/windows/hardware/jj151545)

[**APOInitSystemEffects**](https://msdn.microsoft.com/library/windows/hardware/jj151546)

[**APOInitSystemEffects2**](https://msdn.microsoft.com/library/windows/hardware/dn659347)

[**AudioFXExtensionParams**](https://docs.microsoft.com/windows/desktop/api/audioenginebaseapo/ns-audioenginebaseapo-audiofxextensionparams)

[**DMU\_カーネル\_イベント**](https://msdn.microsoft.com/library/windows/hardware/ff536340)

[**DRMFORWARD**](https://msdn.microsoft.com/library/windows/hardware/ff536350)

[**DRMRIGHTS**](https://msdn.microsoft.com/library/windows/hardware/ff536355)

[**DS3DVECTOR**](https://msdn.microsoft.com/library/windows/hardware/ff536367)

[**KSAC3\_ALTERNATE\_AUDIO**](https://msdn.microsoft.com/library/windows/hardware/ff537055)

[**KSAC3\_ビット\_ストリーム\_モード**](https://msdn.microsoft.com/library/windows/hardware/ff537077)

[**KSAC3\_ダイアログ\_レベル**](https://msdn.microsoft.com/library/windows/hardware/ff537078)

[**KSAC3\_ミックス ダウン**](https://msdn.microsoft.com/library/windows/hardware/ff537079)

[**KSAC3\_エラー\_の非表示**](https://msdn.microsoft.com/library/windows/hardware/ff537080)

[**KSAC3\_言語\_コード**](https://msdn.microsoft.com/library/windows/hardware/ff537081)

[**KSAC3\_ROOM\_TYPE**](https://msdn.microsoft.com/library/windows/hardware/ff537082)

[**KSAUDIO\_チャネル\_構成**](https://msdn.microsoft.com/library/windows/hardware/ff537083)

[**KSAUDIO\_コピー\_保護**](https://msdn.microsoft.com/library/windows/hardware/ff537084)

[**KSAUDIO\_動的\_範囲**](https://msdn.microsoft.com/library/windows/hardware/ff537085)

[**KSAUDIO\_MIC\_配列\_GEOMETRY**](https://msdn.microsoft.com/library/windows/hardware/ff537087)

[**KSAUDIO\_マイク\_調整**](https://msdn.microsoft.com/library/windows/hardware/ff537086)

[**KSAUDIO\_混在\_キャップ**](https://msdn.microsoft.com/library/windows/hardware/ff537090)

[**KSAUDIO\_MIXCAP\_テーブル**](https://msdn.microsoft.com/library/windows/hardware/ff537088)

[**KSAUDIO\_ミキシング レベル**](https://msdn.microsoft.com/library/windows/hardware/ff537089)

[**KSAUDIO\_PACKETSIZE\_制約**](https://msdn.microsoft.com/library/windows/hardware/dn965561)

[**KSAUDIO\_PACKETSIZE\_CONSTRAINTS2**](https://msdn.microsoft.com/library/windows/hardware/mt761740)

[**KSAUDIO\_PACKETSIZE\_PROCESSINGMODE\_制約**](https://msdn.microsoft.com/library/windows/hardware/dn965562)

[**KSAUDIO\_位置**](https://msdn.microsoft.com/library/windows/hardware/ff537091)

[**KSAUDIO\_POSITIONEX**](https://msdn.microsoft.com/library/windows/hardware/ff537092)

[**KSAUDIO\_優先\_状態**](https://msdn.microsoft.com/library/windows/hardware/ff537093)

[**KSAUDIO\_プレゼンテーション\_位置**](https://msdn.microsoft.com/library/windows/hardware/hh450865)

[**KSAUDIOENGINE\_バッファー\_サイズ\_範囲**](https://msdn.microsoft.com/library/windows/hardware/hh450864)

[**KSAUDIOENGINE\_記述子**](https://msdn.microsoft.com/library/windows/hardware/hh450862)

[**KSAUDIOENGINE\_VOLUMELEVEL**](https://msdn.microsoft.com/library/windows/hardware/hh831854)

[**KSDATAFORMAT\_DSOUND**](https://msdn.microsoft.com/library/windows/hardware/ff537094)

[**KSDATAFORMAT\_WAVEFORMATEX**](https://msdn.microsoft.com/library/windows/hardware/ff537095)

[**KSDATARANGE\_オーディオ**](https://msdn.microsoft.com/library/windows/hardware/ff537096)

[**KSDATARANGE\_音楽**](https://msdn.microsoft.com/library/windows/hardware/ff537097)

[**KSDRMAUDIOSTREAM\_CONTENTID**](https://msdn.microsoft.com/library/windows/hardware/ff537099)

[**KSDSOUND\_BUFFERDESC**](https://msdn.microsoft.com/library/windows/hardware/ff537121)

[**KSDS3D\_バッファー\_すべて**](https://msdn.microsoft.com/library/windows/hardware/ff537101)

[**KSDS3D\_バッファー\_CONE\_角度**](https://msdn.microsoft.com/library/windows/hardware/ff537103)

[**KSDS3D\_HRTF\_FILTER\_FORMAT\_MSG**](https://msdn.microsoft.com/library/windows/hardware/ff537104)

[**KSDS3D\_HRTF\_INIT\_メッセージ**](https://msdn.microsoft.com/library/windows/hardware/ff537106)

[**KSDS3D\_HRTF\_PARAMS\_メッセージ**](https://msdn.microsoft.com/library/windows/hardware/ff537108)

[**KSDS3D\_ITD\_PARAMS**](https://msdn.microsoft.com/library/windows/hardware/ff537110)

[**KSDS3D\_ITD\_PARAMS\_メッセージ**](https://msdn.microsoft.com/library/windows/hardware/ff537114)

[**KSDS3D\_リスナー\_すべて**](https://msdn.microsoft.com/library/windows/hardware/ff537116)

[**KSDS3D\_リスナー\_向き**](https://msdn.microsoft.com/library/windows/hardware/ff537119)

[**KSJACK\_の説明**](ksjack-description.md)

[**KSJACK\_DESCRIPTION2**](ksjack-description2.md)

[**KSJACK\_シンク\_情報**](https://msdn.microsoft.com/library/windows/hardware/ff537140)

[**KSMUSICFORMAT**](https://msdn.microsoft.com/library/windows/hardware/ff537142)

[**KSNODEPROPERTY**](https://msdn.microsoft.com/library/windows/hardware/ff537143)

[**KSNODEPROPERTY\_オーディオ\_チャネル**](https://msdn.microsoft.com/library/windows/hardware/ff537145)

[**KSP\_DRMAUDIOSTREAM\_CONTENTID**](https://msdn.microsoft.com/library/windows/hardware/ff537492)

[**KSP\_PINMODE**](https://msdn.microsoft.com/library/windows/hardware/dn457711)

[KSRTAUDIO 構造体](https://msdn.microsoft.com/library/windows/hardware/ff537500)

[**KSTELEPHONY\_CALLCONTROL**](https://msdn.microsoft.com/library/windows/hardware/mt169883)

[**KSTELEPHONY\_CALLINFO**](https://msdn.microsoft.com/library/windows/hardware/mt169884)

[**KSTELEPHONY\_PROVIDERCHANGE**](https://msdn.microsoft.com/library/windows/hardware/mt169885)

[**KSTOPOLOGY\_ENDPOINTID**](https://msdn.microsoft.com/library/windows/hardware/mt169886)

[**KSTOPOLOGY\_ENDPOINTIDPAIR**](https://msdn.microsoft.com/library/windows/hardware/mt169887)

[**LOOPEDSTREAMING\_位置\_イベント\_データ**](https://msdn.microsoft.com/library/windows/hardware/ff537505)

[**MDEVICECAPSEX**](https://docs.microsoft.com/windows/desktop/api/mmddk/ns-mmddk-mdevicecapsex)

[**MIDIOPENDESC**](https://msdn.microsoft.com/library/windows/hardware/ff537518)

[**RTAUDIO\_GETREADPACKET\_情報**](https://msdn.microsoft.com/library/windows/hardware/mt169891)

[**RTAUDIO\_SETWRITEPACKET\_INFO**](https://msdn.microsoft.com/library/windows/hardware/mt169892)

[**SOUNDDETECTOR\_PATTERNHEADER**](https://msdn.microsoft.com/library/windows/hardware/dn957513)

[**シンセサイザー\_バッファー**](https://msdn.microsoft.com/library/windows/hardware/ff538460)

[**シンセサイザー\_PORTPARAMS**](https://msdn.microsoft.com/library/windows/hardware/ff538467)

[**シンセサイザー\_STATS**](https://msdn.microsoft.com/library/windows/hardware/ff538473)

[**SYNTHCAPS**](https://msdn.microsoft.com/library/windows/hardware/ff538424)

[**SYNTHDOWNLOAD**](https://msdn.microsoft.com/library/windows/hardware/ff538429)

[**SYNTHVOICEPRIORITY\_インスタンス**](https://msdn.microsoft.com/library/windows/hardware/ff538452)

[**SYSAUDIO\_アタッチ\_仮想\_ソース**](https://msdn.microsoft.com/library/windows/hardware/ff538480)

[**SYSAUDIO\_作成\_仮想\_ソース**](https://msdn.microsoft.com/library/windows/hardware/ff538485)

[**SYSAUDIO\_インスタンス\_情報**](https://msdn.microsoft.com/library/windows/hardware/ff538490)

[**SYSAUDIO\_選択\_グラフ**](https://msdn.microsoft.com/library/windows/hardware/ff538500)

[**UNCOMPRESSEDAUDIOFORMAT**](https://msdn.microsoft.com/library/windows/hardware/ff538640)

[**WAVEFORMATEX**](https://msdn.microsoft.com/library/windows/hardware/ff538799)

[**WAVEFORMATEXTENSIBLE**](https://msdn.microsoft.com/library/windows/hardware/ff538802)

 

 





