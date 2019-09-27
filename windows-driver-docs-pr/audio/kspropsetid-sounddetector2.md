---
title: Kspropsetid\_SoundDetector2
description: KSPROPSETID_SoundDetector2 プロパティセットには、検出もサポートするオーディオキャプチャデバイスのフィルターを登録するために使用されるプロパティが含まれています。
ms.assetid: FC4A354B-D42C-4199-B613-1E1B75A600C7
ms.date: 09/25/2019
ms.localizationpriority: medium
ms.openlocfilehash: cffc8d4764b8ba090e03fffff0034b9363fe358c
ms.sourcegitcommit: 8295a2b59212972b0f7457a748cc904b5417ad67
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71329468"
---
# <a name="kspropsetid_sounddetector2"></a>Kspropsetid\_SoundDetector2

プロパティ`KSPROPSETID_SoundDetector2`セットには、検出もサポートするオーディオキャプチャデバイスのフィルターを登録するために使用されるプロパティが含まれています。 このフィルターには、pin カテゴリ[\_KSNODETYPE AUDIO\_KEYWORDDETECTOR](ksnodetype-audio-keyworddetector.md)を持つ KS ピンファクトリがあります。 特定の KS フィルターインスタンスで、この KS ピンカテゴリを持つ複数の pin ファクトリを指定することはできません。

`KSPROPSETID_SoundDetector2`は、Windows 10 バージョン1903以降でサポートされています。 KSPROPSETID_SoundDetector2 プロパティセットは、複数の音声エージェントをサポートするために使用されます。 詳細については、「[複数の音声アシスタント](voice-activation-mva.md)」を参照してください。  [Kspropsetid\_sounddetector](kspropsetid-sounddetector.md)プロパティセットは、Cortana だけをサポートするシステムで使用されます。  

`KSPROPSETID_SoundDetector2`は、KSPROPERTY ではなく、 [KSSOUNDDETECTORPROPERTY](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-kssounddetectorproperty)構造体を使用します。

``` syntax
typedef struct {
    KSPROPERTY  Property;
    GUID        EventId;
} KSSOUNDDETECTORPROPERTY, *PKSSOUNDDETECTORPROPERTY;
```

すべての KSPROPSETID_SoundDetector2 プロパティは、 [KSSOUNDDETECTORPROPERTY](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-kssounddetectorproperty)データ構造体を使用して呼び出されます。 このデータ構造には、KSK プロパティと、設定、リセット、検出などを行うキーワードのイベント id が含まれています。

ヘッダーファイルでは、次のように**ksk propsetid\_SoundDetector2**プロパティセットが定義されています。

``` syntax
#define STATIC_KSPROPSETID_SoundDetector2\
    0xfe07e322, 0x450c, 0x4bd5, 0x84, 0xca, 0xa9, 0x48, 0x50, 0xe, 0xa6, 0xaa
DEFINE_GUIDSTRUCT("FE07E322-450C-4BD5-84CA-A948500EA6AA", KSPROPSETID_SoundDetector2);
```

プロパティ`KSPROPSETID_SoundDetector2`セットには、次のプロパティが含まれています。

- [Ksk プロパティ\_sounddetector\_supportedpatterns](ksproperty-sounddetector-supportedpatterns.md) -このプロパティは、検出されるキーワードを構成するためにオペレーティングシステムによって設定されます。

- [Ksk プロパティ\_の\_sounddetector パターン](ksproperty-sounddetector-patterns.md)-ドライバーの KS フィルターは、この読み取り/書き込みプロパティをサポートしています。 OS は、このプロパティを設定して、検出されるキーワードを構成します。

- [Ksk プロパティ\_のサウンド\_検出](ksproperty-sounddetector-armed.md)機能-この読み取り/書き込みプロパティは、検出されたかどうかを示す単純なブール値です。 OS は、キーワード検出機能を利用するようにこれを設定します。 OS はこれをオフにしてオフにできます。 キーワードパターンが設定され、キーワードが検出された後に、ドライバーによって自動的にクリアされます。 (OS は rearm する必要があります)。

- [Ksproperty\_sounddetector\_のリセット](ksproperty-sounddetector-reset.md)-パターンが設定されていない状態で、検出機能を unarmed 状態にリセットします。

- [Ksk プロパティ\_sounddetector\_の streamingsupport](ksproperty-sounddetector-streamingsupport.md) -今後使用する音声認識の検出機能のみです。 プロパティがサポートされていないか成功したことを示すこの要求を失敗とし、他のすべてのドライバーに対して true を返します。

キーワード検出時には、KSNOTIFICATIONID_SoundDetector を含む PNP 通知が送信されます。 注: これは KSEvent ではなく、 [IoReportTargetDeviceChangeAsynchronous](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ioreporttargetdevicechangeasynchronous)を介してペイロードと共に送信される PNP イベントです。
