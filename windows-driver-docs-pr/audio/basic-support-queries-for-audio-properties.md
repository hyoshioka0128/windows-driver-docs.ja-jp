---
title: オーディオのプロパティに対してサポートされる基本的なクエリ
description: オーディオのプロパティに対してサポートされる基本的なクエリ
ms.assetid: d08b6f86-e4fd-4b2c-bfaa-191bcbac3ff8
keywords:
- オーディオプロパティ WDK、基本サポートクエリ
- WDM オーディオプロパティ WDK、基本サポートクエリ
- basic-サポートクエリ WDK オーディオ
- set プロパティ WDK audio
- WDK audio の有効範囲
- 範囲値 WDK オーディオ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5b64b6cffc67b018e8ba684f3e4375cc6e691ad5
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72831261"
---
# <a name="basic-support-queries-for-audio-properties"></a>オーディオのプロパティに対してサポートされる基本的なクエリ


## <span id="basic_support_queries_for_audio_properties"></span><span id="BASIC_SUPPORT_QUERIES_FOR_AUDIO_PROPERTIES"></span>


フィルター、ピン、またはノードに対するプロパティの設定要求のデータを指定する場合、クライアントは、プロパティに対して指定された値または値の有効なデータ範囲を頻繁に認識する必要があります。 範囲はデバイスごとに異なり、場合によっては、同じデバイス内のノード間でも異なる可能性があります。

一部のプロパティは、セットプロパティの要求で範囲外の値を指定できるように定義されていますが、ミニポートドライバーは、これらの値をサポートされている範囲 (例: [**Ksk プロパティ\_AUDIO\_VOLUMELEVEL**](https://docs.microsoft.com/windows-hardware/drivers/audio/ksproperty-audio-volumelevel)) に自動的に固定します。 同じプロパティに対する後続の get 要求では、ドライバーの値の実際の設定が取得されます。これは、クライアントが設定要求で指定した値の固定バージョンである可能性があります。

ただし、クライアントは、単にミニポートドライバーに依存して範囲外の値を自動的にクランプするのではなく、プロパティ値の範囲を知る必要がある場合があります。 たとえば、オーディオデバイスのボリュームコントロールスライダーを表示するウィンドウアプリケーションでは、その範囲をスライダーの完全な長さにマップするために、デバイスのボリューム範囲を把握しておく必要がある場合があります。

特定のプロパティのドライバーのハンドラールーチンは、基本サポートプロパティ要求 (KSK プロパティ\_型\_BASICSUPPORT) に応答して範囲情報を提供できる必要があります。 基本サポートプロパティ要求をドライバーに送信すると、クライアントは、プロパティハンドラーが基本サポート情報を書き込むための値バッファーを提供します。この情報は、次のように指定される[**Ksk プロパティ\_DESCRIPTION**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksproperty_description)構造体で構成されます。プロパティ固有のデータ。 このデータは、通常、プロパティに応じて1つ以上のパラメーター範囲の仕様で構成されます。

一般に、クライアントはこの値バッファーの大きさを事前に把握しておらず、プロパティハンドラーに1つまたは2つの予備の要求を送信して値のサイズを決定する必要があります。 これらの暫定的な要求の形式は、適切に定義されています。 クライアントは、基本サポート要求を処理するときに、ドライバーが次の規則に従うことを想定しています。

-   要求で値のサイズが**sizeof**(ulong) として指定されている場合、プロパティハンドラーは、ksk プロパティ\_DESCRIPTION 構造体の**accessflags**メンバーの値を ulong サイズの値バッファーに書き込みます。 ハンドラーは、基本サポートのプロパティ要求をさらにサポートする場合に、\_型\_BASICSUPPORT flag bit を設定します。

-   要求で値のサイズが**sizeof**(ksk プロパティ\_DESCRIPTION) として指定されている場合、ハンドラーは ksk プロパティ\_description 構造体をデータバッファーに書き込む必要があります。 このハンドラーは、構造体のサイズに、構造体の後のデータバッファーへの読み込みに使用できる追加のプロパティ固有の情報すべてのサイズに加えて、構造体の**descriptionsize**フィールドを設定します。 これは、プロパティの基本サポート情報を格納するためにクライアントが割り当てる必要がある値バッファーのサイズです。

-   要求で、KSK プロパティ\_DESCRIPTION 構造体とプロパティ固有の情報の両方を格納するのに十分な大きさの値が指定されている場合、ハンドラーは KSK プロパティ\_DESCRIPTION 構造体をバッファーの先頭に書き込む必要があります。また、プロパティ固有の情報は、KSK プロパティ\_DESCRIPTION 構造体の末尾に続くデータバッファーの部分に書き込む必要があります。 KSK プロパティ\_DESCRIPTION 構造体を書き込むときは、ハンドラーが**descriptionsize**フィールドにその構造体のサイズに加えて、構造体に続くプロパティ固有の情報のサイズを設定する必要があります。

この要求で、この3つのケースのいずれにも一致しない値のサイズが指定されている場合、プロパティハンドラーは要求を拒否し、ステータスコードの状態\_バッファー\_\_小さすぎます。

ハンドラーが値バッファーに書き込むプロパティ固有の情報には、プロパティ値のデータ範囲が含まれている場合があります。 KSK プロパティの**Memberssize**メンバー\_MEMBERSSIZE は、データ範囲が含まれているかどうかを示します。

-   範囲が不要な場合、 **Memberssize**は0です。 たとえば、プロパティ値が BOOL 型の場合などです。

-   **Memberssize**\_MEMBERSSIZE 構造体の後に1つ以上のプロパティ値の範囲記述子が続いている場合は、0以外の値になります。

ブール型のプロパティ値の場合、範囲は暗黙的に**TRUE**と**FALSE**の値に制限されるため、範囲記述子は必要ありません。 ただし、整数型のプロパティ値の範囲を指定するには、範囲記述子が必要です。

たとえば、ボリュームノード ([**KSNODETYPE\_ボリューム**](https://docs.microsoft.com/windows-hardware/drivers/audio/ksnodetype-volume)) の[**KSK プロパティ\_AUDIO\_VOLUMELEVEL**](https://docs.microsoft.com/windows-hardware/drivers/audio/ksproperty-audio-volumelevel)プロパティに対する基本サポート要求では、そのノードの最小ボリューム設定と最大ボリューム設定が取得されます。 この場合、クライアントは、次の構造を格納するのに十分な大きさの値バッファーを割り当てる必要があります。

[**KSK プロパティ\_の説明**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksproperty_description)

[**KSK プロパティ\_メンバーのプロパティ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksproperty_memberslist)

[**KSK プロパティ\_ステップ実行\_長い**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksproperty_stepping_long)

上記の一覧に示されている順序で、3つの構造体がバッファー内の隣接する位置にパックされます。 要求を処理するときに、ミニポートドライバーは、\_の長い構造体\_、KSK プロパティの**境界**メンバーに最小ボリュームレベルと最大ボリュームレベルを書き込みます。

範囲記述子の配列を使用した基本的なサポート要求の例については、「[マルチチャネルノードを公開](exposing-multichannel-nodes.md)する」の図を参照してください。 基本サポートのプロパティ要求の詳細については、「 [KS のプロパティ](https://docs.microsoft.com/windows-hardware/drivers/stream/ks-properties)」を参照してください。 コード例については、Microsoft Windows Driver Kit (WDK) の[サンプルオーディオドライバー](sample-audio-drivers.md)のプロパティハンドラーの実装に関する記述を参照してください。

 

 




