---
title: KSPROPSETID\_SoundDetector2
description: KSPROPSETID_SoundDetector2 プロパティセットには、検出もサポートするオーディオキャプチャデバイスのフィルターを登録するために使用されるプロパティが含まれています。
ms.assetid: FC4A354B-D42C-4199-B613-1E1B75A600C7
ms.date: 09/25/2019
ms.localizationpriority: medium
ms.openlocfilehash: 025fa4aeb052308a69752770c55d05fce1df1fa4
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72830471"
---
# <a name="kspropsetid_sounddetector2"></a>KSPROPSETID\_SoundDetector2

`KSPROPSETID_SoundDetector2` プロパティセットには、検出もサポートするオーディオキャプチャデバイスのフィルターを登録するために使用されるプロパティが含まれています。 このフィルターには、pin カテゴリ[KSNODETYPE\_AUDIO\_KEYWORDDETECTOR](ksnodetype-audio-keyworddetector.md)を持つ KS pin ファクトリがあります。 特定の KS フィルターインスタンスで、この KS ピンカテゴリを持つ複数の pin ファクトリを指定することはできません。

`KSPROPSETID_SoundDetector2` は、Windows 10 バージョン1903以降でサポートされています。 KSPROPSETID_SoundDetector2 プロパティセットは、複数の音声エージェントをサポートするために使用されます。 詳細については、「[複数の音声アシスタント](voice-activation-mva.md)」を参照してください。  [Kspropsetid\_SoundDetector](kspropsetid-sounddetector.md)プロパティセットは、Cortana だけをサポートするシステムで使用されます。  

`KSPROPSETID_SoundDetector2` は、KSPROPERTY の代わりに[KSSOUNDDETECTORPROPERTY](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-kssounddetectorproperty)構造体を使用します。

``` syntax
typedef struct {
    KSPROPERTY  Property;
    GUID        EventId;
} KSSOUNDDETECTORPROPERTY, *PKSSOUNDDETECTORPROPERTY;
```

すべての KSPROPSETID_SoundDetector2 プロパティは、 [KSSOUNDDETECTORPROPERTY](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-kssounddetectorproperty)データ構造体を使用して呼び出されます。 このデータ構造には、KSK プロパティと、設定、リセット、検出などを行うキーワードのイベント id が含まれています。

ヘッダーファイルでは、次のように**Ksk Propsetid\_SoundDetector2**プロパティセットが定義されています。

``` syntax
#define STATIC_KSPROPSETID_SoundDetector2\
    0xfe07e322, 0x450c, 0x4bd5, 0x84, 0xca, 0xa9, 0x48, 0x50, 0xe, 0xa6, 0xaa
DEFINE_GUIDSTRUCT("FE07E322-450C-4BD5-84CA-A948500EA6AA", KSPROPSETID_SoundDetector2);
```

`KSPROPSETID_SoundDetector2` プロパティセットには、次のプロパティが含まれています。

- [Ksproperty\_sounddetector\_SUPPORTEDPATTERNS](ksproperty-sounddetector-supportedpatterns.md)の場合、このプロパティは、検出されるキーワードを構成するためにオペレーティングシステムによって設定されます。

- [Ksk プロパティ\_SOUNDDETECTOR\_パターン](ksproperty-sounddetector-patterns.md)-ドライバーの KS フィルターは、この読み取り/書き込みプロパティをサポートしています。 OS は、このプロパティを設定して、検出されるキーワードを構成します。

- [Ksk プロパティ\_SOUNDDETECTOR\_](ksproperty-sounddetector-armed.md)がある-この読み取り/書き込みプロパティは、検出可能かどうかを示す単純なブール値です。 OS は、キーワード検出機能を利用するようにこれを設定します。 OS はこれをオフにしてオフにできます。 キーワードパターンが設定され、キーワードが検出された後に、ドライバーによって自動的にクリアされます。 (OS は rearm する必要があります)。

- [Ksk プロパティ\_SOUNDDETECTOR\_リセット](ksproperty-sounddetector-reset.md)-パターンが設定されていない unarmed 状態に検出をリセットします。

- [Ksk プロパティ\_SOUNDINGSUPPORT\_のサウンド検出機能](ksproperty-sounddetector-streamingsupport.md)では、将来使用します。 プロパティがサポートされていないか成功したことを示すこの要求を失敗とし、他のすべてのドライバーに対して true を返します。

キーワード検出時には、KSNOTIFICATIONID_SoundDetector を含む PNP 通知が送信されます。 注: これは KSEvent ではなく、 [IoReportTargetDeviceChangeAsynchronous](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioreporttargetdevicechangeasynchronous)を介してペイロードと共に送信される PNP イベントです。
