---
title: AVStream コーデックの動的形式変更のサポート
description: AVStream コーデックの動的形式変更のサポート
ms.assetid: ae222512-fd19-404a-aaf8-6fbfa2a3349e
keywords:
- ハードウェアコーデックのサポート WDK AVStream、動的な形式の変更
- 動的形式変更 WDK AVStream のサポート
- 動的な形式変更 WDK AVStream
- AVStream ハードウェアコーデックサポート WDK、動的な形式変更
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: bc5beaad8ab5fa95cbde4823680775446ff6d8ca
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72837665"
---
# <a name="supporting-dynamic-format-changes-in-avstream-codecs"></a>AVStream コーデックの動的形式変更のサポート


実行中のメディアストリームで動的な形式の変更が発生すると、システムによって提供される Devproxy モジュールはキャプチャ pin とネゴシエートし、新しい形式が許容されるかどうかを判断します。

次の一連のイベントは、メディアソースから動的な形式の変更が行われた場合に発生します。

1.  ドライバーは、入力 KS pin が新しいメディアの種類をサポートしているかどうかを判断するために、 [**PROPOSEDATAFORMAT 要求\_Ksk プロパティ\_接続**](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-connection-proposedataformat)します。 ドライバーは、このプロパティをサポートする必要があります。

2.  入力ピンが新しいメディアの種類をサポートしている場合は、PROPOSEDATAFORMAT ハンドラーの KSK プロパティ\_接続\_handler が成功のステータス\_を返す必要があります。 次に、ドライバーは、提案された入力を現在選択されている出力メディアの種類と共に使用して、ストリームを再開できるかどうかを判断します。 Yes の場合、ストリームは再開されます。

3.  入力ピンが新しく提案されたメディアの種類をサポートしていない場合は、PROPOSEDATAFORMAT ハンドラーの KSK プロパティ\_接続\_handler がエラーを返す必要があります。 次に、HW MFT は、接続されたコンポーネントでメディアの種類を再度ネゴシエートします。

4.  入力ピンが新しいメディア入力の種類をサポートしているが、KS フィルタで別の出力メディアの種類が必要な場合、ドライバーは、このトピックで後述するように、このトピックの後半で説明するように、 [**KSEVENT\_動的\_フォーマット\_変更**](https://docs.microsoft.com/windows-hardware/drivers/stream/ksevent-dynamic-format-change)イベントを生成して、HW MFT に通知する必要があります。メディアの種類の変更について。

5.  HW MFT は、KSEVENT 通知を受信すると、出力ピンを**ksk\_状態**から ksk 状態\_停止に移行します。

6.  次に、HW MFT はドライバーに対して、使用可能なメディアの種類を照会します。これは、ドライバーの[*AVStrMiniIntersectHandlerEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/nc-ks-pfnksintersecthandlerex)の交差ハンドラーの呼び出しに変換されます。 ドライバーは、優先される出力メディアの種類を優先順位に従って報告する必要があります。

7.  ユーザーモードクライアントは、メディアの種類を選択し、HW MFT の出力ピンに新しいメディアの種類を設定します。 その結果、ドライバーの[*AVStrMiniPinSetDataFormat*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/nc-ks-pfnkspinsetdataformat)ディスパッチルーチンが呼び出されます。 ドライバーが状態\_SUCCESS を返すことによって形式を受け入れる場合、ストリーミングは新しいメディアの種類で再開されます。 呼び出しが失敗した場合、形式の変更に関係するコンポーネントは、メディアの種類を再ネゴシエーションする必要があります。

8.  HW MFT は、接続されたメディアに何らかの変更があるかどうかを確認します。 変更がない場合は、選択したメディアの種類を pin に設定し、それを KSK 状態に\_実行します。 接続されたメディアに変更がある場合、HW MFT は pin を破棄し、新しく選択されたメディアの種類とメディアを使用して pin を再作成します。 その後、MFT によって、pin が KSK 状態になり\_実行されます。

9.  ストリーミングが再開されます。

場合によっては、メディアソースによって形式の変更が検出されないことがあります。 たとえば、MPEG2 デコーダーでは、すべての形式の変更を見つけるために各パケットをデコードする必要があります。

このような場合、ドライバーが形式の変更を検出すると、ハードウェアドライバーは動的な形式の変更 KSEVENT を生成する必要があります。 その後、HW MFT は、サポートされているメディアの種類の pin を照会します。 Pin は優先順位に従って優先メディアの種類を返します。 次に、ハードウェア MFT は、前のセクションの手順 4. ~ 9. で説明した一連のイベントに従います。

ドライバーがこのような形式の変更を処理できない場合は、ストリーミングエラーが返されます。これは、MF に反映されます。

次のコード例は、KSEVENT を使用して、動的な形式の新しい変更を定義する方法を示しています。

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

各 pin は、pin 記述子でこのイベントを公開する必要があります。 イベントの種類は、KSEVENTF\_EVENT\_HANDLE です。

ドライバーは、このイベントを生成する前に、現在選択されている入力メディアの種類に基づいて、KS pin に優先するメディアの種類を設定する必要があります。 これを行うには、pin の記述子に対して[ **\_KsEdit**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/nf-ks-_ksedit)関数を使用します。

イベントを生成するには、ドライバーは[**Ksk Generateevents**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/nf-ks-ksgenerateevents)を呼び出す必要があります。

 

 




