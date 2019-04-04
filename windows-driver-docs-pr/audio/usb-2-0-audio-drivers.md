---
title: USB 2.0 のオーディオ ドライバー
description: 1703 のリリース以降、Windows 10 では、USB オーディオ 2.0 ドライバーが Windows に含まれます。 このドライバーは、基本的な機能を提供します。
ms.date: 10/23/2018
ms.localizationpriority: medium
ms.openlocfilehash: fcdf5f1a141a94257ded52be6616ba068164912f
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56551212"
---
# <a name="usb-audio-20-drivers"></a>USB 2.0 のオーディオ ドライバー

1703 のリリース以降、Windows 10 では、USB オーディオ 2.0 ドライバーが Windows に含まれます。 USB オーディオ 2.0 デバイス クラスをサポートするために設計されています。 ドライバーは、WaveRT オーディオ ポート クラス ミニポートです。 USB オーディオ 2.0 デバイス クラスの詳細については、[ https://www.usb.org/developers/docs/devclass_docs/](https://www.usb.org/developers/docs/devclass_docs/)を参照してください。 

ドライバーの名前は: _usbaudio2.sys_と関連付けられている inf ファイルは_usbaudio2.inf_します。

ドライバーは、デバイス マネージャーで「USB オーディオ クラス 2 デバイス」として識別されます。 この名前は、使用できる場合、USB 製品の文字列で上書きされます。

互換性のあるデバイスがシステムに関連付けられている場合、ドライバーが自動的に有効にします。 ただし、システムまたは Windows Update でサード パーティ製のドライバーが存在する場合、そのドライバーがインストールされ、クラス ドライバーをオーバーライドします。 

 
## <a name="architecture"></a>Architecture

USBAudio.Sys に示すように、Windows USB オーディオの広いアーキテクチャ内に収まります。 

![Kmixer.sys 上部と下部にある USB オーディオ デバイスで表示して、スタックの図](images/usb-2-0-audio-arch.png)

## <a name="related-usb-specifications"></a>関連する USB 仕様

次の USB 仕様は、USB オーディオを定義し、このトピックで参照されます。

-   USB 2 仕様を参照、ユニバーサル シリアル バス、リビジョン 2.0
-   ADC 2 は、オーディオ デバイス、リリース 2.0 の USB デバイスのクラス定義を参照します。
-   FMT 2 は、Release 2.0 にオーディオ データ形式の仕様を参照します。

USB のかどうかは、特別な関心のグループを保持する、[公式の USB 仕様](https://www.usb.org/developers/docs/)仕様書、およびツールをテストします。 


## <a name="audio-formats"></a>オーディオ形式の設定
ドライバーは、次の形式をサポートします。 FMT 2、または不明な形式で定義されている別の形式を指定する代替の設定は無視されます。

私の書式設定 (FMT 2 2.3.1) の種類:
-   サンプルあたりのビット数 8..32 PCM 形式 (FMT20 2.3.1.7.1)
-   PCM8 形式 (FMT 2 2.3.1.7.2)
-   IEEE_FLOAT 形式 (FMT 2 2.3.1.7.3)

III 形式 (FMT 2 2.3.3 および A.2.3) を入力します。
-   IEC61937_AC-3
-   IEC61937_MPEG-2_AAC_ADTS
-   IEC61937_DTS-I
-   IEC61937_DTS-II
-   IEC61937_DTS-III
-   TYPE_III_WMA


## <a name="feature-descriptions"></a>機能の説明

このセクションの機能を説明する、USB オーディオ 2.0 ドライバーの。 

### <a name="audio-function-topology"></a>オーディオの関数のトポロジ

ドライバーは、ADC 2 3.13 で定義されたすべてのエンティティ型をサポートします。

各ターミナル エンティティは、互換性のある USB オーディオ 2.0 ハードウェア クロックの有効な接続が必要です。 クロック パスでは、乗数の時計と時計セレクターのユニットを含めることができます必要に応じてと、クロック ソース エンティティ内で終了する必要があります。

ドライバーは、1 つの単一のクロック ソースのみをサポートします。 デバイスは、複数のクロック ソース エンティティとクロック セレクターを実装する場合、ドライバーはクロック ソースは既定で選択を使用し、クロック セレクターの位置は変更されません。

1 つ以上の入力ピンと処理ユニット (ADC 2 3.13.9) がサポートされていません。

1 つ以上の入力ピンと拡張機能単位 (ADC 2 3.13.10) がサポートされていません。

トポロジ内の循環のパスを指定することはできません。


### <a name="audio-streaming"></a>オーディオ ストリーミング

ドライバーには、次のエンドポイントの同期の種類 (USB 2 5.12.4.1) がサポートされています。

 -  非同期 IN および OUT
 -  同期 IN および OUT
 -  アダプティブ IN および OUT

ケースを非同期には、ドライバーは、明示的なフィードバックのみをサポートします。 AS インターフェイスのそれぞれの代替設定では、フィードバックのエンドポイントを実装する必要があります。 ドライバーは、暗黙的なフィードバックをサポートしていません。

共有のクロックを複数のエンドポイントを使用してデバイスの現在の制限付きサポートがあります。 

適応型の場合、ドライバーは feedforward エンドポイントをサポートしていません。 このようなエンドポイントが別の設定に存在する場合は、これは無視されます。 ドライバーは、非同期でストリームと同じ方法でアダプティブのストリームを処理します。

デバイスによって作成された isochronous パケットのサイズは、FMT 2.0 2.3.1.1 セクションで指定された制限内である必要があります。 つまり、オーディオの 1 つのスロットの +/-公称サイズから実際のパケット サイズの偏差を超えないこと (オーディオ スロット = チャネル数のサンプル)。


## <a name="descriptors"></a>記述子

オーディオの関数には、1 つだけ AudioControl インターフェイス記述子 (ADC 2 4.7) と 1 つまたは複数の AudioStreaming インターフェイス記述子 (ADC 2 4.9) を実装する必要があります。 オーディオ コントロール インターフェイスがないストリーミング インターフェイスを持つ関数がサポートされていません。

ドライバーは、ADC20、セクション 4 で定義されているすべての記述子の種類をサポートします。 次のサブセクションでは、いくつかの具体的な記述子の種類のコメントを提供します。

### <a name="class-specific-as-interface-descriptor"></a>特定のクラスとインターフェイスの記述子 

詳細については、この仕様は、ADC 2 4.9.2 を参照してください。

AS インターフェイスの記述子を先頭に 0 (帯域幅の消費しない) エンドポイントがないと設定の代替は、互換性のある USB オーディオ 2.0 ハードウェアで昇順にさらに代替設定を指定する必要があります。

ドライバーによってサポートされていない形式で別の設定は無視されます。

各 0 以外の代替設定には、データ アイソクロナス エンドポイント、および必要に応じてフィードバックのエンドポイントを指定する必要があります。 任意のエンドポイントなしの 0 以外の代替設定がサポートされていません。

BTerminalLink フィールドが、トポロジ内のターミナル エンティティを参照する必要があり、その値は、AS インターフェイスのすべての代替設定が同じである必要があります。

BFormatType AS インターフェイスの記述子フィールドは、bFormatType 形式の型記述子 (FMT 2 2.3.1.6) で指定されたのと同じである必要があります。

Type I 形式 AS インターフェイス記述子の bmFormats フィールドのいずれかに正確に 1 つのビットを設定する必要があります。 それ以外の場合、形式は、ドライバーによって無視されます。

バスの帯域幅を節約するには、AS インターフェイスを 1 つが、データ アイソクロナス エンドポイント記述子で (bNrChannels および AS 形式の型記述子) に関する同じ形式が異なる wMaxPacketSize 値で複数の代替設定を実装できます。 指定されたサンプル レートでは、ドライバーは、データ レートの要件を満たすことができますが、最小 wMaxPacketSize の代替設定を選択します。

### <a name="type-i-format-type-descriptor"></a>型記述子を書式設定の種類

詳細については、この仕様は、FMT 2 2.3.1.6 を参照してください。

次の制限が適用されます。

|                            |                        |                               |
|----------------------------|------------------------|-------------------------------|
| タイプ I PCM 形式。         | 1 < = bSubslotSize < = 4 |     8 < bBitResolution を = < = 32 |
| タイプ I PCM8 形式。        | bSubslotSize 1 = =      |     bBitResolution 8 = =       |
| タイプ I IEEE_FLOAT 形式。  | bSubslotSize == 4      |     bBitResolution 32 = =      | 
| III IEC61937 形式を入力します。 | bSubslotSize 2 = =      |     bBitResolution 16 = =      |


### <a name="class-specific-as-isochronous-audio-data-endpoint-descriptor"></a>クラスに固有の AS isochronous オーディオ データのエンドポイント記述子 

詳細については、この仕様は、ADC 2 4.10.1.2 を参照してください。

BmAttributes フィールドで MaxPacketsOnly フラグは、サポートされていませんは無視されます。

フィールド bmControls、bLockDelayUnits および wLockDelay は無視されます。


## <a name="class-requests-and-interrupt-data-messages"></a>クラスの要求およびデータ メッセージの割り込み

ドライバーは、ADC 2 のセクション 5.2 で定義されている制御要求のサブセットをサポートし、サポートが一部のコントロール データ メッセージ (ADC 2 6.1) を中断します。 次の表では、ドライバーに実装されているサブセットを示します。

| エンティティ           | コントロール                    | CUR を取得します。 | セット CUR | GET 範囲 | 割り込み |
|------------------|----------------------------|---------|---------|-----------|-----------|
| クロック ソース     | サンプリング頻度コントロール | ○       | ○       | ○         |           |
| クロックのセレクター   | クロック セレクター コントロール     | ○       |         |           |           |
| クロックの乗数 | 分子コントロール          | ○       |         |           |           |
|                  | コントロールの分母        | ○       |         |           |           |
| ターミナル         | コネクタの制御          | ○       |         |           | ○         |
| Mixer 単位       | Mixer コントロール              | ○       | ○       | ○         |           |
| セレクターの単位    | セレクター コントロール           | ○       | ○       |           |           |
| 機能単位     | ミュート用のコントロール               | ○       | ○       |           | ○         |
|                  | ボリューム コントロール             | ○       | ○       | ○         | ○         |
|                  | 自動ゲイン制御     | ○       | ○       |           |           |
| 効果の単位      | –                          |         |         |           |           |
| 処理ユニット  | –                          |         |         |           |           |
| 拡張ユニット   | –                          |         |         |           |           |


コントロールと要求の詳細については、次のサブセクションでは。

### <a name="clock-source-entity"></a>クロック ソース エンティティ 

詳細については、この仕様は、ADC 2 5.2.5.1 を参照してください。

少なくとも、クロックのソース エンティティは、互換性のある USB オーディオ 2.0 ハードウェアでサンプリング頻度コントロール GET 範囲と異なる文字の取得要求 (ADC 2 5.2.5.1.1) を実装する必要があります。

サンプリング頻度コントロール GET 範囲の要求は、部分範囲 (ADC 2 5.2.1) の一覧を返します。 各サブ範囲には、不連続の頻度、または周波数範囲について説明します。 0 に該当する周波数を RES MIN と MAX のフィールドを設定して不連続サンプリング頻度を表す必要があります。 個々 の部分範囲が重複しない必要があります。 対象となる範囲には、前の 1 つが重なっている場合、ドライバーによって無視されます。

1 つの 1 つの固定周波数を実装しているクロック ソース エンティティはのみ、サンプリング周波数コントロール設定 CUR を実装する必要はありません。 固定の頻度を返す GET CUR を実装し、1 つの 1 つの独立した頻度を報告する GET 範囲を実装します。

### <a name="clock-selector-entity"></a>クロック セレクター エンティティ 

詳細については、この仕様は、ADC 2 5.2.5.2 を参照してください。

USB オーディオ 2.0 ドライバーは、クロック選択をサポートしていません。 ドライバーは、これが既定で選択されているし、クロック セレクター コントロール設定 CUR 要求を問題はありませんクロック ソース エンティティを使用します。 USB オーディオ 2.0 の互換性のあるハードウェアでは、クロック セレクター コントロール取得 CUR 要求 (ADC 2 5.2.5.2.1) を実装する必要があります。 


### <a name="feature-unit"></a>機能単位 

詳細については、この仕様は、ADC 2 5.2.5.7 を参照してください。

ドライバーでは、1 つの 1 つのボリュームの範囲でのみサポートしています。 ボリューム コントロール GET 範囲の要求には、1 つ以上の範囲が返された場合は後続の範囲は無視されます。

MIN と MAX のフィールドで表されるボリュームの間隔は、整数、RES フィールドで指定されたステップ サイズの倍数です。

機能ユニットは、ミュートまたはボリュームにマスター コントロールと同様に 1 つのチャネルのコントロールを実装する場合は、ドライバーが 1 つのチャネル コントロールを使用して、マスターのコントロールを無視します。



## <a name="additional-information-for-oem-and-ihvs"></a>OEM および ihv 向けの追加情報

Oem および ihv 側は、指定されたインボックス ドライバーに対して、既存および新規のデバイスをテストする必要があります。

ボックスで USB オーディオ 2.0 ドライバーに関連付けられている、特定のパートナーのカスタマイズはありません。

(Windows リリース 1703 に、更新プログラムで提供される) この INF ファイル エントリを使用して、インボックス ドライバーが汎用デバイス ドライバーを識別します。 

```inf
GenericDriverInstalled,,,,1
```


インボックス ドライバー usbaudio2.inf で次の互換性のある id を登録します。

```inf
USB\Class_01&SubClass_00&Prot_20
USB\Class_01&SubClass_01&Prot_20
USB\Class_01&SubClass_02&Prot_20
USB\Class_01&SubClass_03&Prot_20
```

サブクラスの種類の USB オーディオ 2.0 の仕様を参照してください。

Midi (0x03 上記のサブクラス)、USB オーディオ 2.0 デバイス ロード usbaudio.sys (USB オーディオ 1.0 ドライバー) とは別の多機能デバイスとして、MIDI 関数が列挙されます。 

USB オーディオ 1.0 クラス ドライバーは、この互換性のある ID を wdma_usb.inf に登録します。
 
```inf
USB\Class_01
```
 
これらの除外あり。
 
```inf
USB\Class_01&SubClass_00&Prot_20
USB\Class_01&SubClass_01&Prot_20
USB\Class_01&SubClass_02&Prot_20
USB\Class_01&SubClass_03&Prot_20
```

チャネル (8 より大きい) の任意の数は、Windows オーディオ スタックの制限により、共有モードではサポートされていません。


## <a name="ihv-usb-audio-20-drivers-and-updates"></a>IHV USB オーディオ 2.0 ドライバーと更新プログラム
IHV が提供されているサード パーティ製ドライバー USB オーディオ 2.0 ドライバーでは、それらのドライバーにするのには、デバイスの優先、インボックス ドライバーを明示的にこの動作をオーバーライドし、インボックス ドライバーを使用して、ドライバーを更新しない限り、引き続きします。 

## <a name="audio-jack-registry-descriptions"></a>オーディオ ジャック レジストリの説明

1 つまたは複数のジャックを持つデバイスに Windows 10 以降のリリース 1703、USB オーディオ クラス 2.0 作成 Ihv インボックス クラス 2.0 のオーディオ ドライバーにこれらのジャックを記述する機能があります。 インボックス ドライバーは、このデバイスの KSPROPERTY_JACK_DESCRIPTION を処理するときに、指定された回線のモジュラー ジャック情報を使用します。

回線のモジュラー ジャック情報は、デバイスのインスタンス キー (HW キー) でレジストリに格納されます。

レジストリでのオーディオ ジャック情報の設定を次に示します。

```text
REG_DWORD  T<tid>_NrJacks                 # of the jack on this device
REG_DWORD  T<tid>_J<n>_ChannelMapping     Channel mask. The value is defined in ksmedia.h. e.g. SPEAKER_FRONT_RIGHT or KSAUDIO_SPEAKER_5POINT1_SURROUND
REG_DWORD  T<tid>_J<n>_ConnectorType      The enum value is define in EPcxConnectionType. 
REG_DWORD  T<tid>_J<n>_GeoLocation        The enum value is define in EPcxGeoLocation.
REG_DWORD  T<tid>_J<n>_GenLocation        The enum value is define in EPcxGenLocation.
REG_DWORD  T<tid>_J<n>_PortConnection     The enum value is define in EPxcPortConnection.
REG_DWORD  T<tid>_J<n>_Color              The color needs to be represent by RGB like this: 0x00RRGGBB (NOT a COLORREF).
```

\<tid\> (記述子で定義) された端末 ID を =
  
\<n\>ジャック数 = (1 ~ n)。 

規約\<tid\>と\<n\>は。

- 底が 10 (8、9、10 ではなく 8、9 を)
- 先行ゼロなし
- n は 1 から始まります (ジャック 0 ではなく、ジャック 1 は、最初のジャック)

次に、例を示します。 

T1_NrJacks、T1_J2_ChannelMapping、T1_J2_ConnectorType

その他のオーディオ ジャックについては、[KSJACK_DESCRIPTION 構造](https://docs.microsoft.com/windows-hardware/drivers/audio/ksjack-description)を参照してください。

さまざまな方法では、これらのレジストリ値を設定できます。 

- これらの値を設定する目的のためのインボックス INF をラップするカスタムの Inf を使用します。

- H または w は、Microsoft OS ディスクリプターを使用して (次の例を参照してください)、USB デバイスのデバイスによって直接。 これらの記述子を作成する方法の詳細については、[USB デバイスの Microsoft OS ディスクリプター](https://docs.microsoft.com/windows-hardware/drivers/usbcon/microsoft-defined-usb-descriptors)を参照してください。

### <a name="microsoft-os-descriptors-for-usb-example"></a>USB の例については、Microsoft OS ディスクリプター

USB の例については、次の Microsoft OS ディスクリプターには、チャネルのマッピングとジャックの 1 つの色が含まれています。 例では、1 つの機能の記述子を使用して非複合デバイスです。 

IHV ベンダーを拡張ジャックの説明の他の情報を格納する必要があります。 


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
ドライバーが起動しない場合、システム イベント ログをチェックする必要があります。 ドライバーは、失敗の理由を示すイベントを記録します。 同様に、オーディオ ログ手動で収集できるで説明されている手順に従って[このブログ エントリ](https://blogs.msdn.microsoft.com/matthew_van_eerde/2017/01/09/collecting-audio-logs-the-old-fashioned-way/)します。 場合は、エラーは、ドライバーの問題を示している可能性がありますは、以下に示すフィードバック Hub を使用して報告して、ログが含まれます。

補足 TMF ファイルを使用して USB オーディオ 2.0 クラス ドライバーのログを読み取る方法については、[このブログ エントリ](https://blogs.msdn.microsoft.com/matthew_van_eerde/2017/10/23/how-to-gather-and-read-logs-for-microsofts-usb-audio-2-0-class-driver/)を参照してください。 TMF ファイルの使用の概要については、[TMF ファイルでトレース ログを表示する](https://docs.microsoft.com/windows-hardware/drivers/devtest/displaying-a-trace-log-with-a-tmf-file)を参照してください。

## <a name="feedback-hub"></a>フィードバック Hub
このドライバーに問題が発生した場合は、オーディオのログを収集してくださいに記載されている手順を実行して[このブログ エントリ](https://blogs.msdn.microsoft.com/matthew_van_eerde/2016/09/26/report-problems-with-logs-and-suggest-features-with-the-feedback-hub/)フィードバック Hub 経由で注目にします。


## <a name="driver-development"></a>ドライバーの開発 

このオーディオ 2.0 の USB クラス ドライバーは Thesycon によって開発され、は Microsoft によってサポートします。


### <a name="see-also"></a>関連項目

[Windows Driver Model (WDM)](https://msdn.microsoft.com/library/windows/hardware/ff565698)

[オーディオ ドライバーの概要](https://docs.microsoft.com/windows-hardware/drivers/audio/getting-started-with-wdm-audio-drivers)

[WaveRT ポート ドライバー](https://docs.microsoft.com/windows-hardware/drivers/audio/introducing-the-wavert-port-driver)

[低待機時間のオーディオ](https://docs.microsoft.com/windows-hardware/drivers/audio/low-latency-audio)




