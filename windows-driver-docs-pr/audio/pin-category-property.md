---
title: ピン カテゴリのプロパティ
description: ピン カテゴリのプロパティ
ms.assetid: fd4a4afd-2c17-4002-87ae-21501b1d75c1
keywords:
- WDK、ピンのオーディオのプロパティ
- WDM オーディオ プロパティ WDK、ピン
- ピン WDK のオーディオ、カテゴリ
- WDK オーディオの入力ターミナル識別子
- 出力ターミナル識別子 WDK オーディオ
- 双方向ターミナル識別子 WDK オーディオ
- テレフォニー ターミナル識別子 WDK オーディオ
- 外部ターミナル識別子 WDK オーディオ
- 関数の埋め込みターミナル識別子 WDK オーディオ
- ターミナル識別子 WDK オーディオ
- Guid の WDK オーディオ
- カテゴリの Guid の WDK オーディオ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5909bf2de298ed4e3a1eee9de3121dc4d4e14e4b
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56574571"
---
# <a name="pin-category-property"></a>ピン カテゴリのプロパティ


## <span id="pin_category_property"></span><span id="PIN_CATEGORY_PROPERTY"></span>


USB オーディオ デバイス、IEEE 1394 オーディオ デバイス、およびすべての内部のバス上のオーディオ デバイス用の Microsoft Windows Driver Model (WDM) オーディオ ドライバーでは、KS ピン フィルターとして自分のデバイスを表します。 1 つは、WDM オーディオ ドライバーは[ **KSPIN\_記述子**](https://msdn.microsoft.com/library/windows/hardware/ff563533)でサポートされる各ピンの型の構造体。 この構造内でドライバーを格納、 [KSPROPSETID\_Pin](https://msdn.microsoft.com/library/windows/hardware/ff566584)暗証番号 (pin) の型のプロパティ。 これらのプロパティの中では、 [ **KSPROPERTY\_PIN\_カテゴリ**](https://msdn.microsoft.com/library/windows/hardware/ff565192)プロパティ。 このプロパティの要求を KS 暗証番号 (pin) カテゴリの GUID を取得しますから、 **KSPIN\_記述子**構造体の**カテゴリ**メンバー。 この GUID は、暗証番号 (pin) によって提供される機能の一般カテゴリを示します。 たとえば、特定のピン カテゴリの GUID、KSNODETYPE\_ヘッドホン、として、出力ジャックにヘッドホン、暗証番号 (pin) を識別します。

内部バス (たとえば、PCI など) で wave オーディオ デバイスの場合は、PortCls ミニポート ドライバーには、デバイスを表すフィルターに暗証番号 (pin) の型を記述の暗証番号 (pin) の記述子の配列が含まれています。 各ピンの記述子が、 [ **PCPIN\_記述子**](https://msdn.microsoft.com/library/windows/hardware/ff537721)埋め込みを含む構造体[ **KSPIN\_記述子**](https://msdn.microsoft.com/library/windows/hardware/ff563533)暗証番号 (pin) カテゴリの GUID を含む構造体。 受信すると、 [ **KSPROPERTY\_PIN\_カテゴリ**](https://msdn.microsoft.com/library/windows/hardware/ff565192)プロパティをクライアント要求ポート ドライバー、ミニポート ドライバーの暗証番号 (pin) の記述子からピン留めするカテゴリの GUID を取得します指定した pin の種類。 暗証番号 (pin) の記述子の詳細については、次を参照してください。 [Pin ファクトリ](pin-factories.md)します。

USB オーディオ デバイスが、いくつかの端末、ストリームのデジタルおよびアナログ信号入力して、デバイスを終了します。 USB オーディオ デバイスを表す KS フィルターを作成するときに、 [USBAudio クラスのシステム ドライバー](kernel-mode-wdm-audio-components.md#usbaudio_class_system_driver)フィルターのピンに、デバイスで終端要素を変換します。 Ksmedia.h ヘッダー ファイルでは、KS 暗証番号 (pin) カテゴリの GUID を各 USB 端末の種類の識別子のマッピングを定義します。 次の 6 つのテーブルでは、端末の種類の識別子と、対応するピン留めするカテゴリの Guid を表示します。

### <a name="span-idinputterminaltypesspanspan-idinputterminaltypesspan-input-terminal-types"></a><span id="input_terminal_types"></span><span id="INPUT_TERMINAL_TYPES"></span> 入力の種類の端末

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">USB の端末 ID</th>
<th align="left">KS Pin カテゴリ GUID</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>0x0201</p></td>
<td align="left"><p>KSNODETYPE_MICROPHONE</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x0202</p></td>
<td align="left"><p>KSNODETYPE_DESKTOP_MICROPHONE</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x0203</p></td>
<td align="left"><p>KSNODETYPE_PERSONAL_MICROPHONE</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x0204</p></td>
<td align="left"><p>KSNODETYPE_OMNI_DIRECTIONAL_MICROPHONE</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x0205</p></td>
<td align="left"><p>KSNODETYPE_MICROPHONE_ARRAY</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x0206</p></td>
<td align="left"><p>KSNODETYPE_PROCESSING_MICROPHONE_ARRAY</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idoutputterminaltypesspanspan-idoutputterminaltypesspan-output-terminal-types"></a><span id="output_terminal_types"></span><span id="OUTPUT_TERMINAL_TYPES"></span> 出力ターミナルの種類

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">USB の端末 ID</th>
<th align="left">KS Pin カテゴリ GUID</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>0x0301</p></td>
<td align="left"><p>KSNODETYPE_SPEAKER</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x0302</p></td>
<td align="left"><p>KSNODETYPE_HEADPHONES</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x0303</p></td>
<td align="left"><p>KSNODETYPE_HEAD_MOUNTED_DISPLAY_AUDIO</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x0304</p></td>
<td align="left"><p>KSNODETYPE_DESKTOP_SPEAKER</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x0305</p></td>
<td align="left"><p>KSNODETYPE_ROOM_SPEAKER</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x0306</p></td>
<td align="left"><p>KSNODETYPE_COMMUNICATION_SPEAKER</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x0307</p></td>
<td align="left"><p>KSNODETYPE_LOW_FREQUENCY_EFFECTS_SPEAKER</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idbidirectionalterminaltypesspanspan-idbidirectionalterminaltypesspan-bidirectional-terminal-types"></a><span id="bidirectional_terminal_types"></span><span id="BIDIRECTIONAL_TERMINAL_TYPES"></span> 双方向の端末の種類

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">USB の端末 ID</th>
<th align="left">KS Pin カテゴリ GUID</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>0x0401</p></td>
<td align="left"><p>KSNODETYPE_HANDSET</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x0402</p></td>
<td align="left"><p>KSNODETYPE_HEADSET</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x0403</p></td>
<td align="left"><p>KSNODETYPE_SPEAKERPHONE_NO_ECHO_REDUCTION</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x0404</p></td>
<td align="left"><p>KSNODETYPE_ECHO_SUPPRESSING_SPEAKERPHONE</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x0405</p></td>
<td align="left"><p>KSNODETYPE_ECHO_CANCELING_SPEAKERPHONE</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idtelephonyterminaltypesspanspan-idtelephonyterminaltypesspan-telephony-terminal-types"></a><span id="telephony_terminal_types"></span><span id="TELEPHONY_TERMINAL_TYPES"></span> テレフォニー端末の種類

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">USB の端末 ID</th>
<th align="left">KS Pin カテゴリ GUID</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>0x0501</p></td>
<td align="left"><p>KSNODETYPE_PHONE_LINE</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x0502</p></td>
<td align="left"><p>KSNODETYPE_TELEPHONE</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x0503</p></td>
<td align="left"><p>KSNODETYPE_DOWN_LINE_PHONE</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idexternalterminaltypesspanspan-idexternalterminaltypesspan-external-terminal-types"></a><span id="external_terminal_types"></span><span id="EXTERNAL_TERMINAL_TYPES"></span> 外部の端末の種類

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">USB の端末 ID</th>
<th align="left">KS Pin カテゴリ GUID</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>0x0601</p></td>
<td align="left"><p>KSNODETYPE_ANALOG_CONNECTOR</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x0602</p></td>
<td align="left"><p>KSNODETYPE_DIGITAL_AUDIO_INTERFACE</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x0603</p></td>
<td align="left"><p>KSNODETYPE_LINE_CONNECTOR</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x0604</p></td>
<td align="left"><p>KSNODETYPE_LEGACY_AUDIO_CONNECTOR</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x0605</p></td>
<td align="left"><p>KSNODETYPE_SPDIF_INTERFACE</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x0606</p></td>
<td align="left"><p>KSNODETYPE_1394_DA_STREAM</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x0607</p></td>
<td align="left"><p>KSNODETYPE_1394_DV_STREAM_SOUNDTRACK</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idembeddedfunctionterminaltypesspanspan-idembeddedfunctionterminaltypesspan-embedded-function-terminal-types"></a><span id="embedded_function_terminal_types"></span><span id="EMBEDDED_FUNCTION_TERMINAL_TYPES"></span> 種類の端末埋め込み関数

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">USB の端末 ID</th>
<th align="left">KS Pin カテゴリ GUID</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>0x0701</p></td>
<td align="left"><p>KSNODETYPE_LEVEL_CALIBRATION_NOISE_SOURCE</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x0702</p></td>
<td align="left"><p>KSNODETYPE_EQUALIZATION_NOISE</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x0703</p></td>
<td align="left"><p>KSNODETYPE_CD_PLAYER</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x0704</p></td>
<td align="left"><p>KSNODETYPE_DAT_IO_DIGITAL_AUDIO_TAPE</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x0705</p></td>
<td align="left"><p>KSNODETYPE_DCC_IO_DIGITAL_COMPACT_CASSETTE</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x0706</p></td>
<td align="left"><p>KSNODETYPE_MINIDISK</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x0707</p></td>
<td align="left"><p>KSNODETYPE_ANALOG_TAPE</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x0708</p></td>
<td align="left"><p>KSNODETYPE_PHONOGRAPH</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x0709</p></td>
<td align="left"><p>KSNODETYPE_VCR_AUDIO</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x070A</p></td>
<td align="left"><p>KSNODETYPE_VIDEO_DISC_AUDIO</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x070B</p></td>
<td align="left"><p>KSNODETYPE_DVD_AUDIO</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x070C</p></td>
<td align="left"><p>KSNODETYPE_TV_TUNER_AUDIO</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x070D</p></td>
<td align="left"><p>KSNODETYPE_SATELLITE_RECEIVER_AUDIO</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x070E</p></td>
<td align="left"><p>KSNODETYPE_CABLE_TUNER_AUDIO</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x070F</p></td>
<td align="left"><p>KSNODETYPE_DSS_AUDIO</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x0710</p></td>
<td align="left"><p>KSNODETYPE_RADIO_RECEIVER</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x0711</p></td>
<td align="left"><p>KSNODETYPE_RADIO_TRANSMITTER</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x0712</p></td>
<td align="left"><p>KSNODETYPE_MULTITRACK_RECORDER</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x0713</p></td>
<td align="left"><p>KSNODETYPE_SYNTHESIZER</p></td>
</tr>
</tbody>
</table>

 

USB 端末の種類の識別子の詳細については、次を参照してください、*ユニバーサル シリアル バス デバイス クラス定義の種類の端末*(リリース 1.0)、これは、 [USB Implementers Forum](https://go.microsoft.com/fwlink/p/?linkid=8780) 。web サイト。

上記の表ですべての暗証番号 (pin) のカテゴリの Guid がフォーム KSNODETYPE のパラメーターの名前を持つ\_*XXX*します。 KS ノード タイプの Guid も KSNODETYPE があることに注意してください\_*XXX*パラメーター名。 この名前付け規則は、暗証番号 (pin) カテゴリの Guid とノードの種類の Guid との混乱が発生する可能性を作成します。 さいわい、ほぼすべて KSNODETYPE\_*XXX* pin カテゴリまたはノードの種類のいずれかがパラメーターを識別します。 ルールの 1 つの例外は[ **KSNODETYPE\_シンセサイザー**](https://msdn.microsoft.com/library/windows/hardware/ff537203)、暗証番号 (pin) のカテゴリまたはコンテキストに応じて、ノードの種類のいずれかを識別することができます。 ノード タイプの Guid の一覧は、次を参照してください。[オーディオ トポロジ ノード](https://msdn.microsoft.com/library/windows/hardware/ff536219)します。

USB オーディオ デバイスをインスタンス化すると、USBAudio クラスのシステム ドライバーは、端末などの内部のトポロジについては、デバイスを照会します。 この情報により、USBAudio ドライバーは、デバイスの表示にフィルターを構築し、変換、フィルターに対応するピンの各ターミナルします。 このプロセス中には、ドライバーは各 USB 端末の種類の識別子を対応する KS pin カテゴリ GUID では、上記の表で Guid のいずれかに変換します。 ドライバーの構成要素を[ **KSPIN\_記述子**](https://msdn.microsoft.com/library/windows/hardware/ff563533) pin を記述する構造体し、構造体にピン留めするカテゴリの GUID を書き込みます。

PortCls ミニポート ドライバーは、前の 6 つのテーブルに表示される Guid のカテゴリのみを必ずしも使用しません。 たとえば、ドライバーは定義し、ピン留めするカスタム カテゴリの GUID を使用して、テーブル内のカテゴリの機能のカテゴリが含まれていないピンの型を記述する可能性があります。 当然ながら、独自の pin カテゴリ GUID は、GUID を認識するクライアントにのみ便利です。

オーディオのサブシステムでは、暗証番号 (pin) カテゴリの Guid の一覧と、システム レジストリで、関連付けられているフレンドリ名を保持します。 Guid とフレンドリ名が HKLM レジストリ パスに格納されている\\システム\\CurrentControlSet\\コントロール\\MediaCategories します。 Media クラスのインストーラーがメインの Windows フォルダーの Inf サブフォルダーにある Ks.inf ファイルからレジストリに GUID 名のペアをコピー (たとえば、c:\\Windows\\Inf\\Ks.inf)。

Windows Vista 以降では、オペレーティング システムは、フレンドリ名をエンドポイントのオーディオ デバイスに関連付ける暗証番号 (pin) のカテゴリを使用します。 フレンドリ名をエンドポイントのオーディオ デバイスに関連付ける方法の詳細については、次を参照してください。[エンドポイント、オーディオ デバイスのフレンドリ名](friendly-names-for-audio-endpoint-devices.md)します。

Windows XP、Windows 2000、および Windows Millennium Edition では、オペレーティング システム、暗証番号 (pin) カテゴリの制限のみを使用します。 [WDMAud システム ドライバー](user-mode-wdm-audio-components.md#wdmaud_system_driver)ミキサー MIXERLINE 暗証番号 (pin) カテゴリの Guid に変換する API の代わりに機能します\_COMPONENTTYPE\_*XXX*クライアント アプリケーションによって使用される値。 WDMAud では、前の 6 つのテーブルに表示される Guid の暗証番号 (pin) カテゴリのサブセットのみを認識します。 さらに、歴史的な理由から、WDMAud 認識、2 つのピン留めするカテゴリ Guid、KSCATEGORY\_オーディオおよび PINNAME\_キャプチャでは、テーブルに表示されません。 ミキサーの行にピン留めするカテゴリの翻訳の詳細については、次を参照してください。[トポロジ ピン](topology-pins.md)します。 ミキサー API については、Windows SDK のドキュメントを参照してください。

 

 




