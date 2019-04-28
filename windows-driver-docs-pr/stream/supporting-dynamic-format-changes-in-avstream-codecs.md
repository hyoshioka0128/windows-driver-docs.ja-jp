---
title: AVStream コーデックの動的形式変更のサポート
description: AVStream コーデックの動的形式変更のサポート
ms.assetid: ae222512-fd19-404a-aaf8-6fbfa2a3349e
keywords:
- ハードウェアのコーデック サポート WDK AVStream、動的形式の変更
- 動的形式変更 WDK AVStream のサポート
- WDK AVStream 動的形式の変更
- AVStream ハードウェア コーデック サポート WDK、動的形式の変更をサポートしています。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 030d22c07134ede6ea81131f30d783c3bbc452e5
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63371838"
---
# <a name="supporting-dynamic-format-changes-in-avstream-codecs"></a>AVStream コーデックの動的形式変更のサポート


実行中のメディア ストリームの動的形式の変更が発生したときにキャプチャ pin に新しい形式が許容されるかどうかを判断するシステム提供の Devproxy モジュールをネゴシエートします。

メディア ソースから動的形式変更の発生元と、次の一連のイベントが発生します。

1.  ドライバーが受信、 [ **KSPROPERTY\_接続\_PROPOSEDATAFORMAT** ](https://msdn.microsoft.com/library/windows/hardware/ff565107)入力 KS 暗証番号 (pin) が、新しいメディアの種類をサポートしているかどうかを判断する要求。 ドライバーは、このプロパティをサポートする必要があります。

2.  入力ピンが新しいメディアの種類、KSPROPERTY をサポートしているか\_接続\_PROPOSEDATAFORMAT ハンドラーは、状態を返す必要があります\_成功します。 ドライバーでは、現在選択されている出力メディアの種類と提案された入力を使用して、ストリームを再開できるかどうかを決定します。 場合は、ストリームを再開します。

3.  入力ピンに新しく提案されたメディアの種類、KSPROPERTY、サポートされていない場合\_接続\_PROPOSEDATAFORMAT ハンドラーがエラーを返す必要があります。 HW MFT には、メディアの種類で、接続されているコンポーネントから、再度ネゴシエートします。

4.  入力ピンには、新しいメディア入力の種類がサポートしている場合は、KS フィルターには、別の出力の種類のメディアが必要なドライバーを生成する必要があります、 [ **KSEVENT\_動的\_形式\_変更**](https://msdn.microsoft.com/library/windows/hardware/ff561849)イベント、メディアの種類の変更に関する HW MFT に通知する、このトピックの後半で詳しく説明します。

5.  HW MFT KSEVENT 通知を受け取ると、出力ピンが移行**KSSTATE\_実行**KSSTATE に\_を停止します。

6.  HW MFT は、これは、ドライバーの呼び出しに変換されます。 使用可能なメディアの種類、ドライバーを照会し[ *AVStrMiniIntersectHandlerEx* ](https://msdn.microsoft.com/library/windows/hardware/ff556326)交差ハンドラー。 ドライバーは、優先順位の順序の優先出力メディアの種類を報告する必要があります。

7.  ユーザー モードのクライアントは、メディアの種類を選択し、HW MFT の出力ピンに新しいメディアの種類を設定します。 これは、結果、ドライバーの呼び出しで[ *AVStrMiniPinSetDataFormat* ](https://msdn.microsoft.com/library/windows/hardware/ff556355)ルーチンをディスパッチします。 状態を返すことによって、ドライバーが、形式を受け入れる場合\_成功すると、新しいメディアの種類と再開をストリーミングします。 呼び出しが失敗した場合、形式の変更に関連するコンポーネントにメディアの種類が再ネゴシエートする必要があります。

8.  HW MFT は、接続されたメディアに変更があるかどうかを確認します。 選択したメディアの種類、暗証番号 (pin) を設定し、KSSTATE に配置の変更がない場合は、\_を実行します。 接続されたメディアに変更がある場合、HW MFT は、暗証番号 (pin) を破棄し、新しく選択されたメディアの種類とメディアを再作成します。 MFT は KSSTATE に、暗証番号 (pin) を格納する、\_を実行します。

9.  再開をストリーミングします。

特定の状況でメディア ソースの形式変更、検出可能性があります。 など、MPEG2 デコーダーは、任意の形式の変更を検索するには、各パケットをデコードする必要があります。

このような場合は、ドライバー形式の変更を検出した場合、ハードウェア ドライバーが生成されます KSEVENT 動的形式の変更。 HW MFT は、サポートされているメディアの種類の暗証番号 (pin) を照会します。 Pin では、優先順位の順序の優先されるメディアの種類を返す必要があります。 HW MFT は、手順 4 ~ 9 の前のセクションで説明されているイベントのシーケンスをしに従います。

ドライバーは、このような形式の変更を処理できない場合は、MF に伝達し、ストリーミングのエラーを返します。

次のコード例を KSEVENT を使用して、新しい動的形式の変更を定義する方法を示します。

```cpp
// {162AC456-83D7-4239-96DF-C75FFA138BC6}
#define STATIC_KSEVENTSETID_DynamicFormatChange\
    0x162ac456, 0x83d7, 0x4239, 0x96, 0xdf, 0xc7, 0x5f, 0xfa, 0x13, 0x8b, 0xc6 DEFINE_GUIDSTRUCT("162AC456-83D7-4239-96DF-C75FFA138BC6", KSEVENTSETID_ DynamicFormatChange);
#define KSEVENTSETID_DynamicFormatChange DEFINE_GUIDNAMED(KSEVENTSETID_ DynamicFormatChange)

typedef enum {
KSEVENT_DYNAMIC_FORMAT_CHANGE = 0
};

DEFINE_KSEVENT_TABLE(DynamicFormatChangeEventTable) {
    DEFINE_KSEVENT_ITEM
    (
        KSEVENT_DYNAMIC_FORMAT_CHANGE,
        sizeof(KSEVENTDATA),
        0,   
        NULL,
        NULL,
        NULL
    )
};

KSEVENT_SET PinEventTable[] =
{
    DEFINE_KSEVENT_SET
    (
        &KSEVENTSETID_DynamicFormatChange,
        SIZEOF_ARRAY(DynamicFormatChangeEventTable),
        DynamicFormatChangeEventTable
    )
};
```

各ピンには、その pin 記述子では、このイベントを公開する必要があります。 イベントは型 KSEVENTF\_イベント\_を処理します。

ドライバーは、このイベントを生成、前に、優先のメディアの種類、現在選択されている入力メディアの種類に基づいて、KS pin の設定があります。 使用してこれを行う、 [  **\_KsEdit** ](https://msdn.microsoft.com/library/windows/hardware/ff568796)暗証番号 (pin) の記述子の関数。

イベントを生成するドライバーを呼び出す必要があります[ **KsGenerateEvents**](https://msdn.microsoft.com/library/windows/hardware/ff562597)します。

 

 




