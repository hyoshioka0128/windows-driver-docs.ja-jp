---
title: ラジオ チューナー付きビデオ キャプチャ デバイス
description: ラジオ チューナー付きビデオ キャプチャ デバイス
ms.assetid: 36e3ca98-cb1b-46cc-809a-8c9ad08a53c8
keywords:
- ラジオチューナー WDK ビデオキャプチャ
- PLL オフセット WDK ビデオキャプチャ
- 信号強度 WDK ビデオキャプチャ
- 手動ラジオのチューニング WDK ビデオキャプチャ
- FM チューナー WDK ビデオキャプチャ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3ee80453a2bfbb8dafb93b79a67ee9307fc68990
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844935"
---
# <a name="video-capture-devices-with-radio-tuners"></a>ラジオ チューナー付きビデオ キャプチャ デバイス


Microsoft Windows XP 以降、および Microsoft DirectX 8.1 以降では、FM ラジオチューナーを含むビデオキャプチャデバイスのサポートを提供しています。

FM チューナーを持つデバイスのビデオキャプチャミニドライバーでは、 [**Ksk プロパティ\_チューナー\_STATUS**](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-tuner-status)プロパティがサポートされている必要があります。 これにより、ユーザーモードのクライアントは、 [ **\_チューナー\_状態\_S**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_tuner_status_s)構造体を取得して、チューニング操作の進行状況を示すことができます。

ミニドライバーは、次の3つのチューニング戦略のいずれかをサポートできます。

1.  **PLL オフセットによるチューニング。**

    FM チューナーハードウェアで PLL オフセットを使用したチューニングがサポートされている場合は、ミニドライバー[**チューナー\_モード\_CAPS\_S 構造体\_、Ksk プロパティ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_tuner_mode_caps_s)の**戦略**メンバーを KS\_チューナー\_戦略に設定する必要があり @no__t9_ PLL (_S)

    FM チューナーハードウェアで PLL サポートが提供されていない場合、ミニドライバーは、ネイティブ信号強度インジケーターを使用して PLL サポートをエミュレートする必要があります。 *KsTvTune.ax*のシステム提供の FM チューニングロジックは、ミニドライバーが**KS\_チューナー\_戦略\_pll**戦略をサポートしていることを指定した場合にのみ有効になります。

2.  **シグナルの強さによるチューニング。**

    ミニドライバーが KSK プロパティの**戦略**メンバーを設定している場合\_チューナー\_モード\_CAPS\_S 構造体を KS\_チューナーに\_信号\_強度、 *KsTvTune.ax*は引き続きを使用しようとします。KSK プロパティの**Plloffset**メンバー\_チューナー\_STATUS\_S 構造体。 そのため、これは将来の互換性のための有効なオプションではありません。

    また、ミニドライバーは、使用可能な頻度が現在選択されているかどうかに応じて、 [ **\_チューナー\_状態\_S**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_tuner_status_s)構造体の**signalstrength**メンバーを-1、0、または1に設定する必要があります。 ベンダーは、ベースライン電圧の上位または下限のレシーバー信号強度インジケーター (RSSI) またはデシベル millivolt (dBmV) レベルを決定します。

3.  **ミニドライバーによって手動で実行されるチューニング。**

    ミニドライバーでチューニングロジックを制御するには、 [**Ksk プロパティの\_チューナー\_モード\_CAPS\_S**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_tuner_mode_caps_s)構造体を**KS\_チューナー\_戦略\_** \_に**設定します**。

FM モードでは、 *KsTvTune.ax*は、ミニドライバーで指定された\_\_プロパティの**tuninggranularity 度**メンバー [ **\_CAPS\_S を使用して、周波数 (両側の 100 khz) を中心として 200-khz バンドをステップ実行します。** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_tuner_mode_caps_s)ステップサイズとしての構造体。 検索は、 *KsTvTune.ax*が 200 kHz のバンド全体を検索したとき、またはミニドライバーが適切な信号が検出されたことを確認したときに停止します (どちらか早い方)。

ミニドライバーが常に-1 または1の**Plloffset**値を指定すると、チューニングにかかる時間が大幅に長くなります。 この場合、 *KsTvTune.ax*のチューニングロジックによって、頻度の範囲が重複して再試行されます。 ミニドライバーでは、最初**のチューニング**要求でのみ-1 または1を指定する必要があります。または、チューナーが最高の信号の8ステップ以内である場合にのみ指定する必要があります。 チューニング要求の詳細について[は、「最初のチューニング要求を認識する](recognizing-the-first-tuning-request.md)」を参照してください。

チューニングプロセスは、アプリケーションによって要求されたときに常にセンターの頻度で開始され、中央の上の 100 kHz を超えてステップアップします。 ただし、 **Plloffset**が上位 100-khz の上限に達すると、チューニングロジックは 100 khz の帯域を超えて処理されます。

チューニングプロセスで、上限の範囲内に許容される信号が見つからない場合は、中央の周波数の下に達し、中央の下にある 100 kHz を超えていることを確認し、それでも許容される信号が見つからない場合はセンターの周波数で終了します。 ここでも、 **Plloffset**が中心の周波数付近に1になると、最終的に戻る前に中心の周波数を超えてステップがチューニングされます。

最初のチューニング要求で**Plloffset**メンバー値-1 または1を指定すると、 *KsTvTune.ax*が微調整モードになります。 微調整モードは、 [**Ksk プロパティ\_\_\_\_チューナー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_tuner_mode_caps_s)の**tuninggranularity 度**メンバーによって指定されたステップ間隔で、要求を迅速に連続してチューニングすることで構成されます。**Plloffset**。

*KsTvTune.ax*は、周波数を増減することによって、8つの微調整の手順が失敗した場合に、そのチューニングの試行を停止します。 *KsTvTune.ax*が微調整モードになった後、 **plloffset**が-1 から1、または1から-1 の方向に変更した場合、または0になった場合、チューニング要求は成功したと見なされます。 微調整と 200 kHz バンドの検索は、その時点で停止します。

ただし、 **Plloffset**が1より大きいか、または-1 より小さい場合は、微調整が開始されないか、または破棄されます。 微調整モードは、中心の周波数を中心とした 200 kHz バンドの検索には依存しませんが、どちらも**Tuninggranularity 度**で指定されたステップサイズを使用します (したがって、常に-1 の**plloffset**を返すことに注意してください)。

 

 




