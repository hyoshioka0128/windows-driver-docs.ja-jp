---
title: USB Audio 2.0 のドライバー
description: Windows 10 以降のリリース1703では、USB Audio 2.0 ドライバーが Windows に付属しています。 このドライバーは、基本的な機能を提供します。
ms.date: 12/19/2019
ms.localizationpriority: medium
ms.topic: article
ms.custom:
- CI 111498
- CSSTroubleshooting
ms.openlocfilehash: fde47d6a24609de53ef16e6eddbe893192aaf4fb
ms.sourcegitcommit: 7a69c2e0abf91a57407b13a30faf24925f677970
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/01/2020
ms.locfileid: "85829039"
---
# <a name="usb-audio-20-drivers"></a>USB Audio 2.0 のドライバー

Windows 10 以降のリリース1703では、USB Audio 2.0 ドライバーが Windows に付属しています。 USB オーディオ2.0 デバイスクラスをサポートするように設計されています。 ドライバーは、WaveRT audio port クラスのミニポートです。 USB オーディオ2.0 デバイスクラスの詳細については、「」を参照してください [https://www.usb.org/documents?search=&type%5B0%5D=55&items_per_page=50](https://www.usb.org/documents?search=&type%5B0%5D=55&items_per_page=50) 。

ドライバーの名前は_usbaudio2.sys_であり、関連付けられている inf ファイルは_usbaudio2_です。

ドライバーは、デバイスマネージャーで "USB オーディオクラス2デバイス" として識別します。 この名前は、使用可能な場合は、USB 製品文字列で上書きされます。

互換性のあるデバイスがシステムに接続されている場合、ドライバーは自動的に有効になります。 ただし、サードパーティ製のドライバーがシステムまたは Windows Update に存在する場合は、そのドライバーがインストールされ、クラスドライバーが上書きされます。

## <a name="architecture"></a>アーキテクチャ

USBAudio.Sys、以下に示すように、Windows USB オーディオの広範なアーキテクチャに適しています。 

![上部に Kmixer.sys と USB オーディオデバイスが下部に表示されているスタック図](images/usb-2-0-audio-arch.png)

## <a name="related-usb-specifications"></a>関連する USB 仕様

次の USB 仕様は、USB オーディオを定義し、このトピックで参照されています。

- USB-2 は、ユニバーサルシリアルバス仕様、リビジョン2.0 を指します。
- ADC-2 は、オーディオデバイス (リリース 2.0) の USB デバイスクラス定義を指します。
- FMT-2 は、オーディオデータ形式の仕様である Release 2.0 を参照します。

USB-IF は、 [Usb 仕様](https://www.usb.org/documents)、テスト仕様、およびツールを公式に管理する特別なグループです。

## <a name="audio-formats"></a>オーディオの形式

ドライバーは、以下の形式をサポートしています。 FMT-2 で定義された別の形式または不明な形式を指定する別の設定は無視されます。

タイプ I 形式 (FMT-2 2.3.1):

- 8.. 32 ビットの PCM 形式 (サンプルあたり) (FMT20 2.3.1.7.1)
- PCM8 形式 (FMT-2 2.3.1.7.2)
- IEEE_FLOAT 形式 (FMT-2 2.3.1.7.3)

型 III 形式 (FMT-2 2.3.3 and A. 2.3):

- IEC61937_AC-3
- IEC61937_MPEG-2_AAC_ADTS
- IEC61937_DTS-I
- IEC61937_DTS-II
- IEC61937_DTS-III
- TYPE_III_WMA

## <a name="feature-descriptions"></a>機能の説明

ここでは、USB Audio 2.0 ドライバーのの機能について説明します。

### <a name="audio-function-topology"></a>オーディオ機能のトポロジ

このドライバーは、ADC 3.13 で定義されているすべてのエンティティ型をサポートしています。

各ターミナルエンティティには、互換性のある USB Audio 2.0 ハードウェアでの有効なクロック接続が必要です。 クロックパスには、必要に応じて、クロック乗数とクロックセレクターユニットを含めることができ、クロックソースエンティティで終了する必要があります。

ドライバーは、1つのクロックソースのみをサポートします。 デバイスに複数のクロックソースエンティティとクロックセレクターが実装されている場合、ドライバーは既定で選択されているクロックソースを使用し、クロックセレクターの位置は変更されません。

複数の入力ピンがある処理ユニット (ADC-2 3.13.9) はサポートされていません。

複数の入力 pin を持つ拡張装置 (ADC-2 3.13.10) はサポートされていません。

トポロジ内の循環パスは許可されていません。

### <a name="audio-streaming"></a>オーディオストリーミング

このドライバーでは、次のエンドポイント同期の種類がサポートされています (USB 2 5.12.4.1)。

- 非同期の送受信
- 同期のインとアウト
- アダプティブインとアウト

非同期の場合、ドライバーは明示的なフィードバックのみをサポートします。 フィードバックエンドポイントは、AS インターフェイスのそれぞれの代替設定で実装する必要があります。 ドライバーは、暗黙的なフィードバックをサポートしていません。

現在、複数のエンドポイントで共有クロックを使用しているデバイスのサポートは限られています。 

アダプティブの場合、ドライバーは、フィードフォワードエンドポイントをサポートしていません。 このようなエンドポイントが代替設定に存在する場合は、無視されます。 ドライバーは、ストリーム内の非同期と同じ方法でアダプティブストリームを処理します。

デバイスによって作成されるアイソクロナスパケットのサイズは、FMT-2.0 セクション2.3.1.1 に指定されている制限内である必要があります。 これは、公称サイズからの実際のパケットサイズの偏差が +/1 オーディオスロット (オーディオスロット = チャネル数のサンプル) を超えないようにすることを意味します。

## <a name="descriptors"></a>記述子

オーディオ関数は、1つの AudioControl インターフェイス記述子 (ADC-2 4.7) と1つ以上の Audiocontrol Interface 記述子 (ADC-2 4.9) を厳密に実装する必要があります。 オーディオコントロールインターフェイスはありますが、ストリーミングインターフェイスがない関数はサポートされていません。

ドライバーは、ADC20 セクション4で定義されているすべての記述子の種類をサポートしています。 次のサブセクションでは、特定の記述子の種類に関するコメントを提供します。

### <a name="class-specific-as-interface-descriptor"></a>クラス固有 (インターフェイス記述子として)

この仕様の詳細については、「ADC-2 4.9.2」を参照してください。

AS インターフェイス記述子は、エンドポイントなしの別の設定 0 (帯域幅使用なし) で開始する必要があります。また、互換性のある USB Audio 2.0 ハードウェアで、より詳細な代替設定を昇順に指定する必要があります。

ドライバーでサポートされていない形式の代替設定は無視されます。

0以外のそれぞれの代替設定では、アイソクロナスデータエンドポイントと、必要に応じてフィードバックエンドポイントを指定する必要があります。 エンドポイントなしの0以外の代替設定はサポートされていません。

Bターミナルリンクフィールドは、トポロジ内のターミナルエンティティを参照する必要があり、その値は AS インターフェイスのすべての代替設定で同一である必要があります。

AS インターフェイス記述子の bFormatType フィールドは、形式の型記述子 (FMT-2 2.3.1.6) で指定された bFormatType と同じである必要があります。

型 I 形式では、AS インターフェイス記述子の bmFormats フィールドで1つのビットを1に設定する必要があります。 それ以外の場合、形式はドライバーによって無視されます。

バス帯域幅を節約するために、1つのインターフェイスとして、同じ形式 (bNrChannels と形式の型記述子) を持つ複数の代替設定を実装できますが、アイソクロナスデータエンドポイント記述子の wMaxPacketSize 値は異なります。 特定のサンプルレートでは、ドライバーはデータ速度の要件を満たす最小の wMaxPacketSize で代替設定を選択します。

### <a name="type-i-format-type-descriptor"></a>型の型記述子を書式設定します。

この仕様の詳細については、「FMT-2 2.3.1.6」を参照してください。

次の制限事項が適用されます。

|Format                      |サブスロットサイズ            |ビット解像度                 |
|----|----|----|
| 入力 I PCM 形式:         | 1 <= bSubslotSize <= 4 |     8 <= bBitResolution <= 32 |
| 「I PCM8 format」と入力します。        | bSubslotSize = = 1      |     bBitResolution = = 8       |
| IEEE_FLOAT 形式で入力します。  | bSubslotSize = = 4      |     bBitResolution = = 32      |
| 種類 III IEC61937 形式: | bSubslotSize = = 2      |     bBitResolution = = 16      |

### <a name="class-specific-as-isochronous-audio-data-endpoint-descriptor"></a>クラス固有 (アイソクロナスオーディオデータエンドポイント記述子) 

この仕様の詳細については、「ADC-2 4.10.1.2」を参照してください。

BmAttributes フィールドの MaxPacketsOnly フラグはサポートされていないため、無視されます。

フィールド bmControls、bLockDelayUnits、および wLockDelay は無視されます。

## <a name="class-requests-and-interrupt-data-messages"></a>クラス要求と割り込みデータメッセージ

このドライバーは、一部のコントロールに対して、ADC 2 のセクション5.2 で定義された制御要求のサブセットをサポートし、割り込みデータメッセージ (ADC-2 6.1) をサポートしています。 次の表は、ドライバーに実装されているサブセットを示しています。

| Entity           | コントロール                    | その他のものを取得する | その他の設定 | 範囲の取得 | 妨害 |
|------------------|----------------------------|---------|---------|-----------|-----------|
| クロックソース     | サンプリング頻度の制御 | x       | x       | x         |           |
| クロックセレクター   | クロックセレクターコントロール     | x       |         |           |           |
| クロック乗数 | 分子コントロール          | x       |         |           |           |
|                  | 分母コントロール        | x       |         |           |           |
| ターミナル         | コネクタコントロール          | x       |         |           | x         |
| ミキサーユニット       | ミキサーコントロール              | x       | x       | x         |           |
| セレクターユニット    | セレクターコントロール           | x       | x       |           |           |
| 機能ユニット     | ミュートコントロール               | x       | x       |           | x         |
|                  | ボリュームコントロール             | x       | x       | x         | x         |
|                  | 自動ゲイン制御     | x       | x       |           |           |
| 効果の単位      | –                          |         |         |           |           |
| 処理ユニット  | –                          |         |         |           |           |
| 拡張機能ユニット   | –                          |         |         |           |           |

コントロールと要求の詳細については、次のサブセクションを参照してください。

### <a name="clock-source-entity"></a>クロックソースエンティティ

この仕様の詳細については、「ADC-2 5.2.5.1」を参照してください。

少なくとも、クロックソースエンティティは、互換性のある USB Audio 2.0 ハードウェアでサンプリング頻度制御の GET RANGE と GET 5.2.5.1.1 requests (ADC-2) を実装する必要があります。

サンプリング頻度制御 GET RANGE 要求では、部分範囲のリスト (ADC-2 5.2.1) が返されます。 各サブ範囲は、離散周波数または頻度の範囲を表します。 個別のサンプリング頻度は、MIN フィールドと MAX フィールドをそれぞれの頻度に、RES を0に設定して表す必要があります。 個々の部分範囲を重複させることはできません。 サブ範囲が前のサブ範囲と重なっている場合は、ドライバーによって無視されます。

1つの固定頻度だけを実装するクロックソースエンティティでは、サンプリング頻度コントロールセットの設定が同じである必要はありません。 これは、固定頻度を返す GET の動作を実装し、1つの個別の頻度を報告する GET RANGE を実装します。

### <a name="clock-selector-entity"></a>クロックセレクターエンティティ

この仕様の詳細については、「ADC-2 5.2.5.2」を参照してください。

USB Audio 2.0 ドライバーは、時刻の選択をサポートしていません。 ドライバーは、既定で選択されているクロックソースエンティティを使用します。これは、クロックセレクターコントロールセットの同一要求を発行しません。 クロックセレクターコントロール GET の同一要求 (ADC-2 5.2.5.2.1) は、互換性のある USB Audio 2.0 ハードウェアに実装する必要があります。

### <a name="feature-unit"></a>機能ユニット

この仕様の詳細については、「ADC-2 5.2.5.7」を参照してください。

ドライバーは、1つのボリューム範囲のみをサポートします。 ボリューム制御の範囲取得要求で複数の範囲が返された場合、後続の範囲は無視されます。

[最小] および [最大] の各フィールドで表されるボリューム間隔は、[RES] フィールドで指定されたステップサイズの倍数の整数である必要があります。

機能ユニットがミュートまたはボリュームのマスタコントロールだけでなく、シングルチャネルコントロールを実装している場合、ドライバーは1つのチャネルコントロールを使用し、マスターコントロールを無視します。

## <a name="additional-information-for-oem-and-ihvs"></a>OEM および Ihv 向けの追加情報

Oem と Ihv は、指定されたインボックスドライバーに対して既存のデバイスと新しいデバイスをテストする必要があります。

インボックス USB Audio 2.0 ドライバーに関連付けられている特定のパートナーカスタマイズはありません。

この INF ファイルエントリ (Windows Release 1703 の更新プログラムで提供されます) は、インボックスドライバーが汎用デバイスドライバーであることを識別するために使用されます。

```inf
GenericDriverInstalled,,,,1
```

インボックスドライバーは、usbaudio2 と互換性のある次の Id を登録します。

```inf
USB\Class_01&SubClass_00&Prot_20
USB\Class_01&SubClass_01&Prot_20
USB\Class_01&SubClass_02&Prot_20
USB\Class_01&SubClass_03&Prot_20
```

サブクラス型については、USB audio 2.0 仕様を参照してください。

MIDI を搭載した USB オーディオ2.0 デバイス (上のサブクラス 0x03) は、usbaudio.sys (USB Audio 1.0 driver) が読み込まれた別のマルチ機能デバイスとして MIDI 関数を列挙します。

USB Audio 1.0 クラスドライバーは、この互換性のある ID を wdma_usb に登録します。

```inf
USB\Class_01
```

とには次の除外があります。

```inf
USB\Class_01&SubClass_00&Prot_20
USB\Class_01&SubClass_01&Prot_20
USB\Class_01&SubClass_02&Prot_20
USB\Class_01&SubClass_03&Prot_20
```

Windows オーディオスタックの制限により、共有モードでは、任意の数 (8 を超える) のチャネルはサポートされません。

## <a name="ihv-usb-audio-20-drivers-and-updates"></a>IHV USB Audio 2.0 ドライバーおよび更新プログラム

IHV がサードパーティ製のドライバーの USB オーディオ2.0 ドライバーを提供する場合、この動作を明示的にオーバーライドし、インボックスドライバーを使用するようにドライバーを更新しない限り、これらのドライバーはデバイスに対してインボックスドライバーを使用して引き続き優先されます。 

## <a name="audio-jack-registry-descriptions"></a>オーディオジャックのレジストリの説明

Windows 10 release 1703 以降、1つ以上のジャックを持つ USB オーディオクラス2.0 デバイスを作成する Ihv は、これらのジャックをインボックスオーディオクラス2.0 ドライバーに記述する機能を備えています。 インボックスドライバーは、このデバイスの KSPROPERTY_JACK_DESCRIPTION を処理するときに、指定されたジャック情報を使用します。

ジャック情報は、デバイスインスタンスキー (HW キー) のレジストリに格納されます。

次に、レジストリのオーディオジャック情報設定について説明します。

```text
REG_DWORD  T<tid>_NrJacks                 # of the jack on this device
REG_DWORD  T<tid>_J<n>_ChannelMapping     Channel mask. The value is defined in ksmedia.h. e.g. SPEAKER_FRONT_RIGHT or KSAUDIO_SPEAKER_5POINT1_SURROUND
REG_DWORD  T<tid>_J<n>_ConnectorType      The enum value is define in EPcxConnectionType. 
REG_DWORD  T<tid>_J<n>_GeoLocation        The enum value is define in EPcxGeoLocation.
REG_DWORD  T<tid>_J<n>_GenLocation        The enum value is define in EPcxGenLocation.
REG_DWORD  T<tid>_J<n>_PortConnection     The enum value is define in EPxcPortConnection.
REG_DWORD  T<tid>_J<n>_Color              The color needs to be represent by RGB like this: 0x00RRGGBB (NOT a COLORREF).
```

\<tid\>= ターミナル ID (記述子で定義)
  
\<n\>= ジャック番号 (1 ~ n)。 

およびの \<tid\> 規則 \<n\> は次のとおりです。

- Base 10 (8, 9, 10, 8, 9, a)
- 先頭に0を含まない
- n は1から始まる (最初のジャックは、ジャック0ではなくジャック 1)

次に例を示します。

T1_NrJacks、T1_J2_ChannelMapping、T1_J2_ConnectorType

その他のオーディオジャック情報については、「 [KSJACK_DESCRIPTION 構造](https://docs.microsoft.com/windows-hardware/drivers/audio/ksjack-description)」を参照してください。

これらのレジストリ値は、さまざまな方法で設定できます。

- カスタム Inf を使用して、これらの値を設定するために、ボックス内の INF をラップします。

- USB デバイス用の Microsoft OS 記述子を使用して h/w デバイスによって直接 (次の例を参照)。 これらの記述子の作成の詳細については、「 [USB デバイス用の MICROSOFT OS 記述子](https://docs.microsoft.com/windows-hardware/drivers/usbcon/microsoft-defined-usb-descriptors)」を参照してください。

### <a name="microsoft-os-descriptors-for-usb-example"></a>USB 用 Microsoft OS 記述子の例

次の USB 用 OS 記述子の例には、1つのジャックのチャネルマッピングと色が含まれています。 この例は、単一の特徴記述子を持つ非複合デバイス用です。

IHV ベンダは、ジャックの説明に関する他の情報を含めるように、それを拡張する必要があります。

```text
UCHAR Example2_MSOS20DescriptorSetForUAC2 [0x76] = {
    //
    // Microsoft OS 2.0 Descriptor Set Header
    //
    0x0A, 0x00,             // wLength - 10 bytes
    0x00, 0x00,             // MSOS20_SET_HEADER_DESCRIPTOR
    0x00, 0x00, 0x0?, 0x06, // dwWindowsVersion – 0x060?0000 for future Windows version
    0x76, 0x00,             // wTotalLength – 118 bytes // update later

    //
    // Microsoft OS 2.0 Registry Value Feature Descriptor
    //
    0x42, 0x00,             // bLength - 66 bytes
    0x04, 0x00,             // wDescriptorType – 5 for Registry Property
    0x04, 0x00,             // wPropertyDataType - 4 for REG_DWORD
    0x34, 0x00,             // wPropertyNameLength – 52 bytes
    0x54, 0x00, 0x30, 0x00, // Property Name - “T01_J01_ChannelMapping”
    0x31, 0x00, 0x5f, 0x00,
    0x4a, 0x00, 0x30, 0x00,
    0x31, 0x00, 0x5f, 0x00,
    0x43, 0x00, 0x68, 0x00,
    0x61, 0x00, 0x6e, 0x00,
    0x6e, 0x00, 0x65, 0x00,
    0x6c, 0x00, 0x4d, 0x00,
    0x61, 0x00, 0x70, 0x00,
    0x70, 0x00, 0x69, 0x00,
    0x6e, 0x00, 0x67, 0x00,
    0x00, 0x00
    0x04, 0x00,                       // wPropertyDataLength – 4 bytes
    0x02, 0x00, 0x00, 0x00  // PropertyData - SPEAKER_FRONT_RIGHT

    //
    // Microsoft OS 2.0 Registry Value Feature Descriptor
    //
    0x2A, 0x00,             // bLength - 42 bytes
    0x04, 0x00,             // wDescriptorType – 5 for Registry Property
    0x04, 0x00,             // wPropertyDataType - 4 for REG_DWORD
    0x1C, 0x00,             // wPropertyNameLength – 28 bytes
    0x54, 0x00, 0x30, 0x00, // Property Name - “T01_J01_Color”
    0x31, 0x00, 0x5f, 0x00,
    0x4a, 0x00, 0x30, 0x00,
    0x31, 0x00, 0x5f, 0x00,
    0x43, 0x00, 0x6f, 0x00,
    0x6c, 0x00, 0x6f, 0x00,
    0x72, 0x00, 0x00, 0x00,
    0x04, 0x00,             // wPropertyDataLength – 4 bytes
    0x00, 0x00, 0xff, 0x00  // PropertyData - 0xff0000 - RED }
```

## <a name="troubleshooting"></a>トラブルシューティング

ドライバーが起動しない場合は、システムイベントログを確認する必要があります。 ドライバーは、エラーの原因を示すイベントをログに記録します。 同様に、[このブログエントリ](https://matthewvaneerde.wordpress.com/2017/01/09/collecting-audio-logs-the-old-fashioned-way/)に記載されている手順に従って、オーディオログを手動で収集することもできます。 ドライバーの問題を示している可能性がある場合は、以下で説明するフィードバックハブを使用して報告し、ログを含めてください。

追加の TMF ファイルを使用して USB Audio 2.0 クラスドライバーのログを読み取る方法については、こちらの[ブログエントリ](https://matthewvaneerde.wordpress.com/2016/09/26/report-problems-with-logs-and-suggest-features-with-the-feedback-hub//)を参照してください。 TMF ファイルの操作に関する一般的な情報については、「 [TMF ファイルを使用したトレースログの表示](https://docs.microsoft.com/windows-hardware/drivers/devtest/displaying-a-trace-log-with-a-tmf-file)」を参照してください。

Windows 10 バージョン1703で "オーディオサービスが応答しません" エラーと USB オーディオデバイスが動作しない場合の詳細については、「 [Usb オーディオが再生されない](usb-audio-not-playing.md)」を参照してください。

## <a name="feedback-hub"></a>フィードバック Hub

このドライバーで問題が発生した場合は、オーディオログを収集し、[このブログエントリ](https://blogs.msdn.microsoft.com/matthew_van_eerde/2016/09/26/report-problems-with-logs-and-suggest-features-with-the-feedback-hub/)に記載されている手順に従って、フィードバックハブを使用して注意を促します。

## <a name="driver-development"></a>ドライバーの開発

この USB Audio 2.0 クラスドライバーは、Microsoft によってサポートされています。

### <a name="see-also"></a>関連項目

[Windows Driver Model (WDM)](https://docs.microsoft.com/windows-hardware/drivers/kernel/windows-driver-model)

[オーディオドライバーの概要](https://docs.microsoft.com/windows-hardware/drivers/audio/getting-started-with-wdm-audio-drivers)

[WaveRT ポート ドライバー](https://docs.microsoft.com/windows-hardware/drivers/audio/introducing-the-wavert-port-driver)

[低待機時間オーディオ](https://docs.microsoft.com/windows-hardware/drivers/audio/low-latency-audio)
