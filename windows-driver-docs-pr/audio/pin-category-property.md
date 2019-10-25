---
title: ピン カテゴリのプロパティ
description: ピン カテゴリのプロパティ
ms.assetid: fd4a4afd-2c17-4002-87ae-21501b1d75c1
keywords:
- オーディオプロパティ WDK、pin
- WDM オーディオプロパティ WDK、pin
- WDK オーディオ、カテゴリをピン留めする
- 入力端末識別子 WDK オーディオ
- 出力端末識別子 WDK オーディオ
- 双方向ターミナル識別子 WDK オーディオ
- テレフォニーターミナル識別子 WDK オーディオ
- 外部ターミナル識別子 WDK オーディオ
- 埋め込み関数ターミナル識別子 WDK オーディオ
- ターミナル識別子 WDK オーディオ
- Guid WDK オーディオ
- カテゴリ Guid WDK オーディオ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6d7d6de7bd67a5fa5cad50a6f9ee13a7beeb5c60
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72830247"
---
# <a name="pin-category-property"></a>ピン カテゴリのプロパティ


## <span id="pin_category_property"></span><span id="PIN_CATEGORY_PROPERTY"></span>


USB オーディオデバイス用の Microsoft Windows Driver Model (WDM) オーディオドライバー、IEEE 1394 オーディオデバイス、内部バス上のオーディオデバイスはすべて、デバイスを、ピン付きの KS フィルターとして表します。 WDM オーディオドライバーは、サポートする各 pin の種類に対して1つの[**Kspin\_記述子**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-kspin_descriptor)構造を保持します。 この構造内では、ドライバーは、ピンの種類の[Ksk Propsetid\_pin](https://docs.microsoft.com/windows-hardware/drivers/stream/kspropsetid-pin)プロパティを格納します。 これらのプロパティの中には、 [ **\_CATEGORY プロパティ\_"Ksk" プロパティ**](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-pin-category)があります。 このプロパティの要求では、 **Kspin\_記述子**構造体の**カテゴリ**メンバーから KS pin カテゴリ GUID を取得します。 この GUID は、pin によって提供される機能の一般的なカテゴリを示します。 たとえば、特定のピンカテゴリ GUID (KSNODETYPE\_ヘッドホン) は、ヘッドホンの出力ジャックとして pin を識別します。

内部バス上の wave オーディオデバイス (PCI など) の場合、PortCls ミニポートドライバーにはピン記述子の配列が含まれており、それぞれがデバイスを表すフィルターのピンの種類を表します。 各 pin 記述子は、ピンカテゴリ GUID を持つ埋め込みの[**Kspin\_記述子**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-kspin_descriptor)構造を含む[**PCPIN\_記述子**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/ns-portcls-pcpin_descriptor)構造体です。 クライアントからの[ **\_CATEGORY**](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-pin-category)プロパティの要求を\_、ksk プロパティを受け取ると、ポートドライバーは、指定されたピンの種類について、ミニポートドライバーの pin 記述子から pin カテゴリの GUID を取得します。 ピン記述子の詳細については、「[ファクトリのピン留め](pin-factories.md)」を参照してください。

USB オーディオデバイスには、デジタルストリームとアナログ信号がデバイスを出入りできるいくつかの端末があります。 USB オーディオデバイスを表す KS フィルターを構築する場合、 [usbaudio クラスのシステムドライバー](kernel-mode-wdm-audio-components.md#usbaudio_class_system_driver)は、デバイス上のターミナルをフィルターのピンに変換します。 ヘッダーファイル Ksmedia. h は、各 USB ターミナルの種類の識別子の割り当てを、KS pin カテゴリの GUID に定義します。 次の6つの表は、ターミナルの種類の識別子とそれに対応する pin カテゴリの Guid を示しています。

### <a name="span-idinput_terminal_typesspanspan-idinput_terminal_typesspan-input-terminal-types"></a><span id="input_terminal_types"></span><span id="INPUT_TERMINAL_TYPES"></span>入力端末の種類

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">USB 端末 ID</th>
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

 

### <a name="span-idoutput_terminal_typesspanspan-idoutput_terminal_typesspan-output-terminal-types"></a><span id="output_terminal_types"></span><span id="OUTPUT_TERMINAL_TYPES"></span>出力端末の種類

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">USB 端末 ID</th>
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

 

### <a name="span-idbidirectional_terminal_typesspanspan-idbidirectional_terminal_typesspan-bidirectional-terminal-types"></a><span id="bidirectional_terminal_types"></span><span id="BIDIRECTIONAL_TERMINAL_TYPES"></span>双方向のターミナルの種類

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">USB 端末 ID</th>
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

 

### <a name="span-idtelephony_terminal_typesspanspan-idtelephony_terminal_typesspan-telephony-terminal-types"></a><span id="telephony_terminal_types"></span><span id="TELEPHONY_TERMINAL_TYPES"></span>テレフォニーターミナルの種類

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">USB 端末 ID</th>
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

 

### <a name="span-idexternal_terminal_typesspanspan-idexternal_terminal_typesspan-external-terminal-types"></a><span id="external_terminal_types"></span><span id="EXTERNAL_TERMINAL_TYPES"></span>外部ターミナルの種類

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">USB 端末 ID</th>
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

 

### <a name="span-idembedded_function_terminal_typesspanspan-idembedded_function_terminal_typesspan-embedded-function-terminal-types"></a><span id="embedded_function_terminal_types"></span><span id="EMBEDDED_FUNCTION_TERMINAL_TYPES"></span>埋め込み関数のターミナル型

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">USB 端末 ID</th>
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

 

USB ターミナルの種類の識別子の詳細については、「*ユニバーサルシリアルバスデバイスクラスのターミナルの種類の定義*(リリース 1.0)」を参照してください。このクラスは、 [Usb 実装者フォーラム](https://go.microsoft.com/fwlink/p/?linkid=8780)の web サイトから入手できます。

前の表のすべてのピンカテゴリ Guid には、KSNODETYPE\_*XXX*という形式のパラメーター名があります。 KS ノード型 Guid には、KSNODETYPE\_*XXX*パラメーター名も含まれることに注意してください。 この名前付け規則により、pin カテゴリの Guid とノードの種類の Guid が混同される可能性があります。 幸いにも、ほぼすべての KSNODETYPE\_*XXX*パラメーターでは、ピンカテゴリまたはノードの種類を識別しますが、両方は指定しません。 ルールの1つの例外は、 [**KSNODETYPE\_シンセサイザー**](https://docs.microsoft.com/windows-hardware/drivers/audio/ksnodetype-synthesizer)です。これは、コンテキストに応じて、ピンカテゴリまたはノードの種類のいずれかを識別できます。 ノードの種類の Guid の一覧については、「[オーディオトポロジノード](https://docs.microsoft.com/windows-hardware/drivers/audio/audio-topology-nodes)」を参照してください。

USB オーディオデバイスをインスタンス化する場合、USBAudio クラスシステムドライバーは、その端末を含む内部トポロジのデバイスを照会します。 この情報を使用すると、USBAudio ドライバーはデバイスを表すフィルターを構築し、各ターミナルをフィルターの対応するピンに変換します。 この処理中、ドライバーは各 USB 端末の種類の識別子を、前の表の Guid の1つである、対応する KS pin カテゴリ GUID に変換します。 ドライバーは、ピンを記述する[**Kspin\_記述子**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-kspin_descriptor)構造を構築し、ピンカテゴリ GUID を構造体に書き込みます。

PortCls ミニポートドライバーは、前の6つのテーブルに出現するカテゴリ Guid のみを使用するとは限りません。 たとえば、ドライバーはカスタム pin カテゴリ GUID を定義して使用し、機能カテゴリがテーブル内のカテゴリの外部にある pin の種類を表すことができます。 当然ながら、カスタム pin カテゴリ GUID は、GUID を認識するクライアントにのみ有効です。

オーディオサブシステムでは、システムレジストリにピンカテゴリ Guid とそれに関連付けられたフレンドリ名の一覧が保持されます。 Guid とフレンドリ名は、レジストリパス HKLM\\SYSTEM\\CurrentControlSet\\Control\\MediaCategories に格納されます。 Media クラスインストーラは、メインの Windows フォルダーの Inf サブフォルダーにある Ks ファイル (たとえば、C:\\Windows\\Inf\\Ks) から、GUID と名前のペアをレジストリにコピーします。

Windows Vista 以降では、オペレーティングシステムはピン留めカテゴリを使用して、フレンドリ名をオーディオエンドポイントデバイスに関連付けます。 フレンドリ名をオーディオエンドポイントデバイスに関連付ける方法の詳細については、「[オーディオエンドポイントデバイスのフレンドリ名](friendly-names-for-audio-endpoint-devices.md)」を参照してください。

Windows XP、Windows 2000、および Windows Millennium Edition では、オペレーティングシステムで pin カテゴリの使用が制限されています。 [WDMAud システムドライバー](user-mode-wdm-audio-components.md#wdmaud_system_driver)は、ミキサー API の代わりとして機能し、クライアントアプリケーションで使用するために、ピンカテゴリ GUID を MIXERLINE\_componenttype\_*XXX*値に変換します。 WDMAud は、前の6つのテーブルに出現するピンカテゴリの Guid のサブセットのみを認識します。 また、履歴上の理由により、WDMAud は、テーブルには表示されない2つのピンカテゴリ Guid、KSCATEGORY\_AUDIO および PINNAME\_CAPTURE を認識します。 ピン留めカテゴリをミキサー線に変換する方法の詳細については、「[トポロジピン](topology-pins.md)」を参照してください。 ミキサ API の詳細については、Windows SDK のドキュメントを参照してください。

 

 




