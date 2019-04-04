---
title: マイクロソフトによって定義された Bluetooth HCI コマンドとイベント
description: Bluetooth ホスト コント ローラー インターフェイス (HCI) には、ホストと Bluetooth 無線コント ローラー間のすべての対話を指定します。
ms.assetid: 68E34B92-155B-401E-8D90-5BD1AF036B4D
ms.date: 02/07/2018
ms.localizationpriority: medium
ms.openlocfilehash: 8d78cc2a0abe156ae4df345e4b0349f887041adc
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56552799"
---
# <a name="microsoft-defined-bluetooth-hci-extensions"></a>マイクロソフトによって定義された Bluetooth HCI の拡張機能
Bluetooth ホスト コント ローラー インターフェイス (HCI) には、ホストと Bluetooth 無線コント ローラー間のすべての対話を指定します。 Bluetooth の仕様では、コント ローラーとホスト間での非標準の相互作用を有効にするには、HCI のベンダー定義コマンドおよびイベントを許可します。 Microsoft では、ベンダー固有 HCI コマンドと Windows で使用されるイベントを定義します。 Bluetooth コント ローラーの実装者は、特殊な機能を実装するために、これらの拡張機能を使用できます。

#### <a name="requirements"></a>要件
Windows 10 Mobile、およびそれ以降のバージョンのデスクトップ エディション (Home、Pro、Enterprise、および教育機関向け)、Windows 10 でサポート。

## <a name="microsoft-defined-hci-commands"></a>Microsoft による HCI コマンド 

Bluetooth HCI のコマンドは、16 ビットのコマンドのコードによって識別されます。 Bluetooth の組織では、0x0000 0xFBFF 経由の範囲の値を定義します。 ベンダーは、1024 異なる可能なベンダーが割り当てたコマンド コードの許可 0xFC00、0 xffff までの範囲の値を定義します。

仕入先には、コマンドの Microsoft によるコードの値を選択する必要があります。 Microsoft は、コマンドのコードを選択し、その他のベンダーの競合する目的は、コード使用しないと仮定ことはできません。 ベンダー固有のコマンドを発行し、認識しない場合、コマンドを拒否するコント ローラーに依存する安全ではありません。 コント ローラーは、コント ローラーのファームウェアの更新など、破壊的な操作として、コマンドを解釈できます。

仕入先は、コント ローラー以外の方法を選択した値を伝える必要があります。 Microsoft では、選択したコードを取得する方法を指定しません。

|HCI コマンド|説明|
|---|---|
|[HCI_VS_MSFT_Read_Supported_Features](#hcivsmsftreadsupportedfeatures) | HCI_VS_MSFT_Read_Supported_Features を説明するビットマップを提供する Microsoft 定義、コント ローラーの機能をサポートしているし、コント ローラーによって返される Microsoft 定義のイベントのプレフィックスを指定します。|
|[HCI_VS_MSFT_Monitor_Rssi](#hcivsmsftmonitorrssi) | HCI_VS_MSFT_Monitor_Rssi を要求コント ローラーが指定された接続に対して測定リンク RSSI の監視を開始し、接続の測定リンク RSSI が指定された範囲外になると、イベントが生成されます。|
|[HCI_VS_MSFT_Cancel_Monitor_Rssi](#hcivsmsftcancelmonitorrssi) |HCI_VS_MSFT_Cancel_Monitor_Rssi は、HCI_VS_MSFT_Monitor_Rssi 以前に発行されたコマンドをキャンセルします。|
|[HCI_VS_MSFT_LE_Monitor_Advertisement](#hcivsmsftlemonitoradvertisement) | HCI_VS_MSFT_LE_Monitor_Advertisement を要求コント ローラーは、指定 RSSI 範囲内し、もその他の要件を満たしている提供情報の監視を開始します。|
|[HCI_VS_MSFT_LE_Cancel_Monitor_Advertisement](#hcivsmsftlecancelmonitoradvertisement) | HCI_VS_MSFT_LE_Cancel_Monitor_Advertisement は、HCI_VS_MSFT_LE_Monitor_Advertisement 以前に発行されたコマンドをキャンセルします。|
[HCI_VS_MSFT_LE_Set_Advertisement_Filter_Enable](#hcivsmsftlesetadvertisementfilterenable) | HCI_VS_MSFT_LE_Set_Advertisement_Filter_Enable では、提供情報のフィルターの状態を設定します。|
|[HCI_VS_MSFT_Read_Absolute_RSSI](#hcivsmsftreadabsoluterssi) | HCI_VS_MSFT_Read_Absolute_RSSI は、コント ローラーから BR EDR/接続の絶対受信信号の強さを示す値 (RSSI) 値を読み取ります。|



### <a name="notifying-windows-bluetooth-stack-of-the-vendor-specific-command-code"></a>ベンダー固有のコマンドのコードの Windows Bluetooth スタックを通知します。
Windows の Bluetooth スタックは、レジストリ キーからベンダー固有のコマンドのコードを読み取ります。

VsMsftOpCode のレジストリ キーは REG_DWORD の一種を備え、キーのデータは、ベンダー固有のオペコードにします。

VsMsftOpCode キーにレジストリ パスになります。

探します\<デバイス インスタンスのパス > \Device Parameters\VsMsftOpCode

このコマンドの例では、コマンドラインからレジストリ値を追加します。

```cpp
REG ADD "HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Enum\<Device instance path>\Device Parameters" /v VsMsftOpCode /t REG_DWORD /d <Vendor specific command code>
```

### <a name="using-inf-to-set-the-vsmsftopcode-registry-key"></a>INF を使用して VsMsftOpCode レジストリ キーを設定するには
INF ファイルを使用して、ベンダー固有のコマンドのコードを追加することもできます。 このサンプルの表示方法と場所がレジストリに自動的に追加できるように、ベンダ固有のコマンドのコードを追加します。

```cpp
[radio.NTamd64.HW]
AddReg=radio.NTamd64.HW.AddReg
[radio.NTamd64.HW.AddReg]
HKR,,"VsMsftOpCode",0x00010001,<Vendor Specific Opcode>
```
### <a name="microsoft-defined-hci-command-and-subcommands"></a>Microsoft による HCI コマンドとサブコマンド

コント ローラーは、1 つだけの Microsoft 固有 HCI コマンドが認識しています。 オペコードを使用して、Microsoft 固有のコマンド セットが拡張されます。 Microsoft による HCI コマンドの最初のコマンド パラメーターは、オペコード、サブコマンドを指定します。

コント ローラーをサポートする必要があります[HCI_VS_MSFT_Read_Supported_Features](#hcivsmsftreadsupportedfeatures)他の Microsoft HCI のサブコマンドをサポートするためにします。 その他のコマンドのサポートは省略可能で、HCI_VS_MSFT_Read_Supported_Features によって返される値によって異なります。 Windows では、コント ローラーが HCI_VS_MSFT_Read_Supported_Features への応答を通じて、サブコマンドのサポートを指定しない限り、任意の Microsoft によるサブコマンドは送信しません。

### <a name="hcivsmsftreadsupportedfeatures"></a>HCI_VS_MSFT_Read_Supported_Features

HCI_VS_MSFT_Read_Supported_Features を説明するビットマップを提供する Microsoft 定義、コント ローラーの機能をサポートしているし、コント ローラーによって返される Microsoft 定義のイベントのプレフィックスを指定します。

コント ローラーでは、コマンドの完了イベントをすぐにこのコマンドが完了常にものとします。


|コマンド|コード|コマンドのパラメーター|戻り値パラメーター|
|---|---|---|---|
|HCI_VS_MSFT_Read_Supported_Features|選択した基本コード |Subcommand_opcode|<ul><li>状況</li><li>Subcommand_opcode</li><li>Supported_features</li><li>Microsoft_event_prefix_length</li><li>Microsoft_event_prefix</li></ul>|


#### <a name="commandparameters"></a>Command_parameters

**Subcommand_opcode** (1 オクテット)。

| Value  |  パラメーターの説明 |
|---|---|
|0x00   |  HCI_VS_MSFT_Read_Supported_Features のサブコマンド オペコードです。|

#### <a name="returnparameters"></a>Return_parameters
**ステータス**(1 オクテット)。

| Value  |  パラメーターの説明 |
|---|---|
|  0x00 |  コマンドが成功しました。 |
| 0x01&#160;-&#160;0xFF  |  コマンドが失敗しました。 参照してください_エラーコード_詳細については、Bluetooth のコア仕様でします。 |

**Subcommand_opcode** (1 オクテット)。

| Value  |  パラメーターの説明 |
|---|---|
|0x00   |  サブコマンドのオペコード[HCI_VS_MSFT_Read_Supported_Features](#hcivsmsftreadsupportedfeatures)します。|

**Supported_features** (オクテットの 8)。

| Value  |  パラメーターの説明 |
|---|---|
|0x00000000&#160;00000001  |コント ローラーは、BR EDR/接続の RSSI 監視機能をサポートします。 さらに、コント ローラーがサポートしている[HCI_VS_MSFT_Read_Absolute_RSSI](#hcivsmsftreadabsoluterssi) BR EDR/接続の絶対 RSSI メトリックを読み取る。 |
|0x00000000&#160;00000002  |コント ローラーは、LE 接続 RSSI 監視機能をサポートします。 |
|0x00000000&#160;00000004  |コント ローラーには、LE の RSSI 監視の提供情報がサポートしています。 |
|0x00000000&#160;00000008|コント ローラーには、LE の広告の監視の提供情報がサポートしています。|
|0x00000000&#160;00000010 |コント ローラーのサポート、公開の有効性を確認する X 座標と Y 座標曲線の中にセキュリティで保護されたシンプル P-192 および P-256 のペアリング プロセス。 <p>詳細については、[Bluetooth のコア仕様 Erratum 10734](https://www.bluetooth.org/docman/handlers/downloaddoc.ashx?doc_id=447440)を参照してください。</p>|
|0x00000000 00000020|コント ローラーには、ラジオの他のアクティビティと同時実行の継続的な広告の監視の LE 提供情報がサポートしています。|
|0 xffffffff&#160;FFFFFFF0|ビットを今後の定義に予約されています。 0 にする必要があります。|

**Microsoft_event_prefix_length** (1 オクテット)。

| Value  |  パラメーターの説明 |
|---|---|
|0x00&#160;-&#160;0x20|返されたで指定されているマイクロソフト イベント プレフィックス フィールド内のバイト数_Microsoft_event_prefix_します。 これは、Microsoft が指定した HCI のすべてのイベントの先頭にある定数情報のバイト数です。|

**Microsoft_event_prefix** (可変長)。

| Value  |  パラメーターの説明 |
|---|---|
|イベント&#160;プレフィックス&#160;値| 各 Microsoft 定義のイベントの先頭に期待する定数の情報です。 この情報は、他のカスタム イベントから Microsoft 定義イベントを区別するために使用されます。|

 ### <a name="hcivsmsftmonitorrssi"></a>HCI_VS_MSFT_Monitor_Rssi

HCI_VS_MSFT_Monitor_Rssi を要求コント ローラーが指定された接続に対して測定リンク RSSI の監視を開始し、接続の測定リンク RSSI が指定された範囲外になると、イベントが生成されます。


|コマンド|コード|コマンドのパラメーター|戻り値パラメーター|
|---|---|---|---|
|HCI_VS_MSFT_Read_Supported_Features|選択した基本コード |<ul><li>Subcommand_opcode</li><li>Connection_handle</li><li>RSSI_threshold_high</li><li>RSSI_threshold_low</li><li>RSSI_threshold_low_time_interval</li><li>RSSI_sampling_period</li></ul>|<ul><li>状況</li><li>Subcommand_opcode</ul>|

コント ローラーが RSSI 値を定期的に生成されたイベントのホストに通知されます (に基づいて、 _RSSI_sampling_period_)。 RSSI は純益、測定されたリンク、**絶対**dbm BR EDR/接続の信号強度 受信側の値。
HCI_VS_MSFT_Monitor_Rssi コマンドへの応答、コント ローラーはイベントが生成コマンドの完了ステータスが、コント ローラーは、監視を開始できる場合は、0 を相当または 0 以外の状態のそれ以外の場合。 状態値が 0 以外の場合は、コント ローラーは生成されません、 [HCI_VS_MSFT_Rssi_Event](#hcivsmsftrssievent)このコマンドに応答します。
HCI_VS_MSFT_Monitor_Rssi のもう 1 つのコマンドと同じ場合、コント ローラーが、コマンドを拒否するものと_Connection_handle_が未解決か、指定された接続を処理する場合は無効です。 コント ローラーは、その他の理由から、リソースの枯渇などのコマンドを拒否もあります。

#### <a name="statediagram"></a>State_diagram

この状態の図では、接続 RSSI を監視するときに、コント ローラーの遷移状態を示します。![HCI_VS_MSFT_Monitor_Rssi の状態ダイアグラム](images/HCI_VS_MSFT_Monitor_Rssi_State_Diagram.png)コント ローラーを生成する、 [HCI_VS_MSFT_Rssi_Event](#hcivsmsftrssievent)受信 RSSI が、指定した以上の場合_RSSI_threshold_high_します。 このイベントが生成された後、コント ローラーはことを指定する新しい HCI_VS_MSFT_Rssi_Event を生成は、 _RSSI_threshold_high_ RSSI を指定する、HCI_VS_MSFT_Rssi_Event を生成するまでを超えています下回りました_RSSI_threshold_low_します。

受信した RSSI と等しいか、指定したを下回ったときに、コント ローラーは、HCI_VS_MSFT_Rssi_Event を生成は_RSSI_threshold_low_を指定した_RSSI_threshold_low_time_interval_します。 このイベントが生成された後、コント ローラーは、RSSI を下回ったことを指定する新しい HCI_VS_MSFT_Rssi_Event を生成は、 _RSSI_threshold_low_ HCI_VS_MSFT_Rssi_Event イベントが生成されますを指定するまで_RSSI_threshold_high_に達したか超えましたされています。

場合、 _RSSI_sampling_period_は 0x01 と 0 xfe、間、コント ローラーを生成する、HCI_VS_MSFT_Rssi_Event 定期的にすべて_RSSI_sampling_period_します。 このイベントを含むことにわたって計算された RSSI の平均値、 _RSSI_sampling_period_します。
場合、 _RSSI_sampling_period_は、コント ローラーは 0x00 または 0 xff の場合、**いない**HCI_VS_MSFT_Rssi_Event で定期的にホストに通知します。

#### <a name="commandparameters"></a>Command_parameters

Subcommand_opcode (1 オクテット)。

| Value  |  パラメーターの説明 |
|---|---|
|0x01   |  HCI_VS_MSFT_Monitor_Rssi のサブコマンド オペコードです。|

Connection_handle (2 つのオクテット)。

| Value  |  パラメーターの説明 |
|---|---|
|0x_XXXX   |  接続がある RSSI を監視する必要がありますのハンドル。|


RSSI_threshold_high (1 オクテット)。

| Value  |  パラメーターの説明 |
|---|---|
|待機 = _High&#160;RSSI しきい値&#160;値 |  最大値には、RSSI 値が必要です。 観察された RSSI は、この値以上になると、コント ローラー イベントが生成されます。 BR/EDR: の <ul><li>範囲:-128 &lt; =  _N_ &lt;= 127 (符号付き整数)</li><li>単位: dBm</li></ul>LE: の<ul><li>20 (符号付き整数) の範囲:-127</li><li>単位: dBm</li></ul>|

RSSI_threshold_low (1 オクテット)。

| Value  |  パラメーターの説明 |
|---|---|
|待機 = _Low&#160;RSSI しきい値&#160;値|最小値には、RSSI 値が必要です。 コント ローラー観測 RSSI になった場合、イベントが生成されますこの値未満です。 BR/EDR: の<ul><li>範囲:-128 &lt; =  _N_ &lt;= 127 (符号付き整数)</li><li>単位: dBm</li></ul>LE: の<ul><li>20 (符号付き整数) の範囲:-127</li><li>単位: dBm</li></ul>|

RSSI_threshold_low_time_interval (1 オクテット)。

| Value  |  パラメーターの説明 |
|---|---|
|0x00|予約済みの値。|
|N_&#160;=&#160;0x01&#160;-&#160;0x3C|期間 = _N_ * 未満でなければならない RSSI 値を秒単位で 1 回、secondThe _RSSI_threshold_low_する前に、 [HCI_VS_MSFT_Rssi_Event](#hcivsmsftrssievent)が生成されます。

RSSI_sampling_period (1 オクテット)。

| Value  |  パラメーターの説明 |
|---|---|
|0x00|予約済みの値。|
|_N_&#160;=&#160;0x01&#160;-&#160;0xFE|期間 = _N_ * 100 millisecondsThe サンプリング間隔 (ミリ秒)。|
|0 xff の場合|予約済みの値。|

#### <a name="returnparameters"></a>Return_parameters
状態 (1 オクテット):

| Value  |  パラメーターの説明 |
|---|---|
|  0x00 |  コマンドが成功しました。 |
| 0x01&#160;-&#160;0xFF  |  コマンドが失敗しました。 参照してください_エラーコード_詳細については、Bluetooth のコア仕様でします。 |
|0x07|コント ローラーを返す_メモリ容量を超えて_コマンドを処理するための十分なメモリがあるない場合。|
|_エラー&#160;コード_| コマンドが失敗しました。 参照してください_エラーコード_詳細については、Bluetooth のコア仕様でします。|

Subcommand_opcod (1 オクテット)。

| Value  |  パラメーターの説明 |
|---|---|
|0x01|HCI_VS_MSFT_Monitor_Rssi のサブコマンド オペコードです。| 

#### <a name="eventsgeneratedunlessmaskedaway"></a>Events_generated__unless_masked_away

コント ローラーは、HCI_VS_MSFT_Monitor_Rssi コマンドを受信したときに、コマンドの完了イベントを生成速やかにものとします。 コント ローラーを生成するコマンドの完了イベントが 0 の状態を返す場合、 [HCI_VS_MSFT_Rssi_Event](#hcivsmsftrssievent)次のいずれかに発生します。
-    経由でデバイスの監視対象の RSSI _RSSI_threshold_low_time_interval_が同じか、または指定したよりも小さい_RSSI_threshold_low_値。

-    デバイスの監視対象の RSSI が以上の値を指定した_RSSI_threshold_high_値。 

-    _RSSI_sampling_period_が有効では、サンプリング期間が終了するとします。

コント ローラーは、指定されたデバイスとの接続が失われた場合、すべての必要なクリーンアップを行う必要があります。 ここで、 [HCI_VS_MSFT_Cancel_Monitor_Rssi](#hcivsmsftcancelmonitorrssi)コマンドは、コント ローラーに送信されません。

### <a name="hcivsmsftcancelmonitorrssi"></a>HCI_VS_MSFT_Cancel_Monitor_Rssi

以前発行を取り消します HCI_VS_MSFT_Cancel_Monitor_Rssi [HCI_VS_MSFT_Monitor_Rssi](#hcivsmsftmonitorrssi)コマンド。
コント ローラーは、このコマンドに応答コマンドが完了イベントを生成するものと速やかに。


|コマンド|コード|コマンドのパラメーター|戻り値パラメーター|
|---|---|---|---|
|HCI_VS_MSFT_Cancel_Monitor_Rssi|選択した基本コード |<ul><li>Subcommand_opcode</li><li>Connection_handle</li>|<ul><li>状況</li><li>Subcommand_opcode</ul>|

#### <a name="commandparameters"></a>Command_parameters

Subcommand_opcode (1 オクテット)。

| Value  |  パラメーターの説明 |
|---|---|
|0x02   |  HCI_VS_MSFT_Cancel_Monitor_Rssi のサブコマンド オペコードです。|

Connection_handle (1 オクテット)。

| Value  |  パラメーターの説明 |
|---|---|
|0x_XXXX   |  キャンセルする必要がある RSSI 接続用のハンドル。|

#### <a name="returnparameters"></a>Return_parameters
状態 (1 オクテット):

| Value  |  パラメーターの説明 |
|---|---|
|  0x00 |  コマンドが成功しました。 |
| 0x01&#160;-&#160;0xFF  |  コマンドが失敗しました。 参照してください_エラーコード_詳細については、Bluetooth のコア仕様でします。 |

Subcommand_opcod (1 オクテット)。

| Value  |  パラメーターの説明 |
|---|---|
|0x02|HCI_VS_MSFT_Cancel_Monitor_Rssi のサブコマンド オペコードです。| 

#### <a name="eventsgeneratedunlessmaskedaway"></a>Events_generated__unless_masked_away

コント ローラー HCI_VS_MSFT_Cancel_Monitor_RSSI コマンドを受信したコマンドの完了イベントが生成されます。

### <a name="hcivsmsftlemonitoradvertisement"></a>HCI_VS_MSFT_LE_Monitor_Advertisement

コント ローラーがアドバタイズを指定した RSSI 範囲内し、も、次の条件のいずれかを満たす監視が開始される HCI_VS_MSFT_LE_Monitor_Advertisement が要求されます。

-    指定したパターンは、提供情報を受信したパケットを照合できます。
-    受信した提供情報 packe に指定された UUID を一致させることができます。
-    提供情報のパケットが元のデバイスのプライベート アドレスを解決するのには、指定の Id 解決キー (IRK) を使用できます。
-    Bluetooth の指定したアドレスは、提供情報を受信したパケットを照合できます。


|コマンド|コード|コマンドのパラメーター|戻り値パラメーター|
|---|---|---|---|
|HCI_VS_MSFT_LE_Monitor_Advertisement|選択した基本コード |<ul><li>Subcommand_opcode</li><li>Connection_handle</li>|<ul><li>状況</li><li>Subcommand_opcode<li>Monitor_handle</li></ul>|



コント ローラーは、このコマンドに応答、コマンドの完了イベントを生成するものとします。 Status の値は、それ以外の場合、コント ローラーは、の監視を開始できる場合は 0 または 0 以外の状態に設定する必要があります。
これを無視するものと、コント ローラーが RSSI が LE 提供情報の監視をサポートしていない場合、 _RSSI_threshold_high_、 _RSSI_threshold_low_、 _RSSI_threshold_low_time_interval_、および_RSSI_sampling_period_パラメーターの値。

##### <a name="statediagram"></a>State_diagram

この状態の図では、広告の RSSI を監視する場合に、コント ローラーの遷移状態を示します。 ![HCI_VS_MSFT_LE_Monitor_Advertisement の状態の図](images/HCI_VS_MSFT_LE_Monitor_Advertisement_State_Diagram.png)します。 受信した RSSI がより大きいまたは等しい場合にのみ、コント ローラーがホストに最初の提供情報のパケットを伝達は_RSSI_threshold_high_特定のデバイスにします。 コント ローラーを生成する、 [HCI_VS_MSFT_LE_Monitor_Device_Event](#hcivsmsftlemonitordeviceevent)で_Monitor_state_を 1 に設定し、 _Monitor_handle_こののハンドルに設定_条件_、コント ローラーがのこの特定のデバイスを監視しているホストに通知する_条件_します。
コント ローラーがの監視を停止するものと_条件_以上受信した提供情報の RSSI になると下回った_RSSI_threshold_low_経由で_RSSI_threshold_low_interval_特定のデバイス用です。 コント ローラーを生成する、 [HCI_VS_MSFT_LE_Monitor_Device_Event](#hcivsmsftlemonitordeviceevent)で_Monitor_state_コント ローラーが、の特定のデバイスの監視を停止しているホストに通知を0に設定_条件_します。 コント ローラーと HCI_VS_MSFT_LE_Monitor_Device_Event の指定後_Monitor_state_を 0 に設定すると、コント ローラーはできませんさらに、コント ローラーになるまで、デバイスのホストに流れるパケットが送信ホストを特定のデバイスに対して RSSI が増えた以上に通知を受け取る_RSSI_threshold_high_の特定のデバイスに対して、_条件_します。
さらに、コント ローラーを生成する必要、 [HCI_VS_MSFT_LE_Monitor_Device_Event](#hcivsmsftlemonitordeviceevent)で_Monitor_state_コント ローラーのデバイスの監視を停止しているホストに通知を 0 に設定します_条件_場合、指定した_RSSI_threshold_low_time_interval_有効期限が切れたデバイスからの広告のパケットを受信します。 コント ローラーは、特定の条件のデバイスを監視している場合、次のステートメントは true です。

-    RSSI_sampling_period_ は 0 xff に設定されている場合、コント ローラーものといないパケットを許可するさらに提供情報については、デバイスのホストにフローを_条件_コント ローラーは、ホストを通知が、特定のデバイスが RSSI のことまで下回りました_RSSI_threshold_low_の_RSSI_threshold_low_time_interval_この特定のデバイスに対して_条件_します。 この通知は生成することによって行われます、 [HCI_VS_MSFT_LE_Monitor_Device_Event](#hcivsmsftlemonitordeviceevent)で_Monitor_state_を 0 に設定します。
-    場合、 _RSSI_sampling_period_設定は 0x0、コント ローラーは、このデバイスのホストにすべての提供情報を受信したパケットを伝達は_条件_コント ローラーが以前に受信しない限り、[HCI_VS_MSFT_LE_Set_Advertisement_Filter_Enable](#hcivsmsftlesetadvertisementfilterenable)コマンドと_を有効にする_0x00 に設定します。 受信した RSSI と等しいまたはそれよりも小さい場合でも、コント ローラーがアドバタイズ パケットをホストするを伝達は_RSSI_threshold_low_限り_RSSI_threshold_low_time_interval_が切れていません。この特定のデバイスに対して_条件_します。 この提供情報のパケットの RSSI 値は、受信した提供情報の RSSI 値である必要があります。

場合_RSSI_sampling_period_は 0x01 と 0 xfe、間、コント ローラーがホストにパケットが送信を伝達はすべて_RSSI_sampling_period_しない限り、指定されたコント ローラーを以前受信した、 [HCI_VS_MSFT_LE_Set_Advertisement_Filter_Enable](#hcivsmsftlesetadvertisementfilterenable)コマンドと_を有効にする_0x00 に設定します。 提供情報の指定された RSSI 値をこのサンプリング間隔中に受信した RSSI 値の平均値となります。 コント ローラーがサンプリング期間中に、提供情報のパケットを受信しなかった場合それをホストに提供情報は反映されないものとします。 できますを_RSSI_sampling_period_がより小さい_RSSI_threshold_low_time_interval_中に受信したすべての提供情報と、 _RSSI_sampling_period_以下の RSSI がある_RSSI_threshold_low_します。 コント ローラーは、このサンプリング間隔中に受信した RSSI 値の平均値の提供情報を伝達まだものとします。

コント ローラーが以前に受信した場合、 [HCI_VS_MSFT_LE_Set_Advertisement_Filter_Enable](#hcivsmsftlesetadvertisementfilterenable)コマンドと_を有効にする_0x00 に設定すると、サンプリング期間タイマーは停止できません。 例を参照してください。詳細については、サンプリング期間でフィルターに HCI_VS_MSFT_LE_Set_Advertisement_Filter_Enable します。
コント ローラーは、同じデバイスから提供情報の重複していないパケットを受信する場合、コント ローラーに格納されている条件に対して各提供情報のパケットに一致する必要があります。

コント ローラーが複数の条件に一致するデバイスから提供情報パケットを受信し、コント ローラーを生成するかどうか、 [HCI_VS_MSFT_LE_Monitor_Device_Event](#hcivsmsftlemonitordeviceevent)各_条件_一致するに_Monitor_handle_に設定、_条件_に一致します。

コント ローラーは RSSI 値と一致する範囲内のすべてのデバイスを監視することがない場合、_条件_、可能な限り多くのデバイスが監視保持されます。 どのようなデバイスを監視するかについての判断は、受信した提供情報の RSSI 値によって異なります。 コント ローラーには、大きい受信信号強度を持つデバイスを監視ものとします。

コント ローラーが特定のデバイスについて、ホストの通知を受け取る場合 (_A_) デバイス ハードウェアの最大の容量では、監視と場合に別のデバイス (_B_) し、大きい RSSI 値を持つ範囲にはコント ローラーは、ホストを通知は、デバイスの監視が停止されている (_A_) 生成することによって、 [HCI_VS_MSFT_LE_Monitor_Device_Event](#hcivsmsftlemonitordeviceevent)で_Monitor_state_を 0 に設定します。 コント ローラーを生成することも、HCI_VS_MSFT_LE_Monitor_Device_Event で_Monitor_state_ホストに通知を 1 に設定するデバイス (_B_) が監視されているようになりました。

#### <a name="conditiontypeandconditionparameters"></a>Condition_type_and_Condition_parameters

_Condition_type_パラメーターを指定するかどうか、_条件_パラメーターは、パターン、UUID、IRK、または定義を指定します。
場合、 _Condition_type_パターンを指定するパラメーター、_条件_パターン内の番号を含む 2 つのセクションが含まれています、_条件_、およびデータのパターン。![パターン条件のデータ レイアウト](images/HCI_VS_MSFT_LE_Monitor_Advertisement_Conditions.png)
_番号のパターン_パターンと一致する必要がある数を指定します。

_データのパターンを_形式は、次のとおりです。

-    _長さ_このパターンの長さのデータ型を含めるし、パターンのバイトの開始を指定します。
-    _広告の種類_広告の種類フィールドを指定します。
-    _パターンの先頭_広告の種類の直後に続くパターンの開始バイト位置を指定します。
-    _パターン_のサイズ (_長さ_-0x2)、指定した開始バイトから提供情報のパケット内の指定した AD 型に関して照合されるパターンです。

指定された複数のパターンがある場合は、コント ローラーはその 1 つ以上のパターンに一致する受信した提供情報を確認します。

場合、 _Condition_type_ 、UUID を指定するパラメーター、_条件_UUID 型と、UUID、パラメーターが含まれます。 UUID 型では、16 ビット、32 ビットまたは 128 ビット UUID は、かどうかを指定します。 コント ローラーには、指定された UUID を確認する提供情報のパケットのサービス UUID を解析ものとします。 UUID の種類が 0x01 として定義される場合、コント ローラーは 16 ビット サービス Uuid の不完全なリストとサービス UUID 広告の種類で指定した 16 ビット サービス Uuid の完全な一覧を解析ものとします。 UUID の種類が 0x02 として定義される場合、コント ローラーは 32 ビット サービス Uuid の不完全なリストとサービス UUID 広告の種類で指定した 32 ビット Uuid の完全な一覧を解析ものとします。 指定された UUID 型が 0x03 である場合は、コント ローラーは 128 ビット サービス Uuid の不完全なリストとサービス UUID 広告の種類で指定された 128 ビット サービス Uuid の完全な一覧を解析ものとします。

場合、 _Condition_type_ 、IRK を指定するパラメーター、_条件_パラメーターには、IRK が含まれています。

場合、 _Condition_type_ Bluetooth のアドレスを指定するパラメーター、_条件_パラメーターには、アドレスの種類と定義が含まれています。

コント ローラーが保持されます (アクティブまたはパッシブ) のスキャンが有効になっている場合でも、条件に基づく監視します。
アクティブなスキャンを有効にすると、スキャンの応答をフィルターに一致する提供情報がホストに伝達は。

フィルターを無効にする、コント ローラーが HCI_VS_MSFT_LE_Monitor_Advertisement コマンドを受け取るかどうか (以前に受信したため[HCI_VS_MSFT_LE_Set_Advertisement_Filter_Enable](#hcivsmsftlesetadvertisementfilterenable)コマンドと_を有効にします。_ 0x00 に設定)、コント ローラーは、コマンドを受け入れるものとことができますが、無効な状態に設定します。
コント ローラーは、リソースの枯渇など他の理由により、コマンドを拒否もあります。


#### <a name="commandparameters"></a>Command_parameters

Subcommand_opcode (1 オクテット)。

| Value  |  パラメーターの説明 |
|---|---|
|0x03   |  HCI_VS_MSFT_LE_Monitor_Advertisement のサブコマンド オペコードです。|

RSSI_threshold_high (1 オクテット)。

| Value  |  パラメーターの説明 |
|---|---|
|高 RSSI しきい値|  最大値には、RSSI 値が必要です。 観察された RSSI は、この値以上になると、コント ローラー イベントが生成されます。 LE: の<ul><li>20 (符号付き整数) の範囲:-127</li><li>単位: dBm</li></ul>|

RSSI_threshold_low (1 オクテット)。

| Value  |  パラメーターの説明 |
|---|---|
|低 RSSI しきい値|最小値には、RSSI 値が必要です。 コント ローラー観測 RSSI になった場合、イベントが生成されますこの値未満です。 LE: の<ul><li>20 (符号付き整数) の範囲:-127</li><li>単位: dBm</li></ul>|

RSSI_threshold_low_time_interval (1 オクテット)。

| Value  |  パラメーターの説明 |
|---|---|
|0x00|予約済みの値。|
|N_&#160;=&#160;0x01&#160;-&#160;0x3C|期間 = _N_ * 1 秒です。 未満でなければならない RSSI 値を秒単位の時間_RSSI_threshold_low_する前に、 [HCI_VS_MSFT_Rssi_Event](#hcivsmsftrssievent)が生成されます。

RSSI_sampling_period (1 オクテット)。

| Value  |  パラメーターの説明 |
|---|---|
|0x00|予約済みの値。|
|_N_&#160;=&#160;0x01&#160;-&#160;0xFE|期間 = _N_ * 100 ミリ秒です。 サンプリング間隔 (ミリ秒単位)。|
|0 xff の場合|コント ローラーを使用して、任意のホストに受信した提供情報の伝達する必要がありますされません。|

Condition_type (1 オクテット)。

| Value  |  パラメーターの説明 |
|---|---|
|0x01|条件は、提供情報に一致する必要のあるパターンです。|
|0x02|条件は、UUID 型 UUID です。| 
|0x03|条件とは、IRK の解像度です。| 
|0x04|条件は、Bluetooth アドレスです。|

条件:条件に該当するフィールドは、Condition_type の値に依存します。 詳細については、Condition_type と条件のパラメーター セクションを参照してください。

Number_of_patterns (1 オクテット)。

|Value | パラメーターの説明| 
|---|---|
|0 xxx| Pattern_data パラメーター内で指定されたパターンの数。|

Pattern_data (> 3 オクテット)。

|Value | パラメーターの説明| 
|---|---|
|長さ|このパターンの長さ。|
|データの種類| 提供情報 セクションのデータ型。 値は、Bluetooth Assigned Numbers ドキュメントに表示されます。|
|バイトを開始します。| 指定したデータ型に関して照合されるパターンの開始位置。|
|[パターン]| パターンが (長さ – 0x2 バイトのサイズ) を照合します。|

UUID_type (1 オクテット)。

|Value | パラメーターの説明| 
|---|---|
|0x01| UUID は、16 ビット サービスです。|
|0x02| UUID は、32 ビット サービスです。| 
|0x03| UUID は、128 ビット サービスです。|

UUID (2、4、または 16 オクテット):

|Value | パラメーターの説明| 
|---|---|
|0xXXXX| <p>2 バイト UUID_type が 0x01 の場合。<p><p>4 バイト UUID_type は 0x02 場合。</p><p>16 バイト UUID_type が 0x03 場合。</p>|

(16 オクテット) を IRK:

| Value  |  パラメーターの説明 |
|---|---|
|<p>0xXXXXXXXX XXXXXXXX</p><p>XXXXXXXX XXXXXXXX</p>|プライベート アドレスの解決に使用する IRK します。|

Address_type (1 オクテット)。

| Value  |  パラメーターの説明 |
|---|---|
|0x00| デバイスのパブリック アドレスです。|
|0x01| ランダムなデバイスのアドレス。| 
|0x02 - 0 xff の場合| 将来使用するための予約済みの値。|

Address_type (1 オクテット)。

| Value  |  パラメーターの説明 |
|---|---|
|0xXXXXXXXXXXXX|監視対象となるデバイスの Bluetooth のアドレス。|

#### <a name="returnparameters"></a>Return_parameters
状態 (1 オクテット):

| Value  |  パラメーターの説明 |
|---|---|
|  0x00 |  コマンドが成功しました。 |
|0x07|コント ローラーは、コマンドを処理するのに十分なメモリがあるない場合は、メモリ容量を超えて返します。|
| エラー コード  |  コマンドが失敗しました。 参照してください_エラーコード_詳細については、Bluetooth のコア仕様でします。 |

Subcommand_opcode (1 オクテット)。

| Value  |  パラメーターの説明 |
|---|---|
|0x03| HCI_VS_MSFT_LE_Monitor_Advertisement のサブコマンド オペコードです。 |

Monitor_handle (1 オクテット)。

| Value  |  パラメーターの説明 |
|---|---|
|0x00 - 0 xff の場合|このルールに対するハンドル。 このハンドルは、提供情報の監視をキャンセルする HCI_VS_MSFT_LE_Cancel_Monitor_Advertisement のパラメーターとして使用されます。 このパラメーターでは、有効なは、ステータスが 0x00 である場合のみです。|

#### <a name="eventsgeneratedunlessmaskedaway"></a>Events_generated__unless_masked_away

HCI_VS_MSFT_LE_Monitor_Advertisement コマンドが受信したときに、コント ローラーは、コマンドの完了イベントを生成します。



### <a name="hcivsmsftlecancelmonitoradvertisement"></a>HCI_VS_MSFT_LE_Cancel_Monitor_Advertisement

以前発行を取り消します HCI_VS_MSFT_LE_Cancel_Monitor_Advertisement [HCI_VS_MSFT_LE_Monitor_Advertisement](#hcivsmsftlemonitoradvertisement)コマンド。


|コマンド|コード|コマンドのパラメーター|戻り値パラメーター|
|---|---|---|---|
|HCI_VS_MSFT_LE_Cancel_Monitor_Advertisement|選択した基本コード |<ul><li>Subcommand_opcode</li><li>Monitor_handle</li>|<ul><li>状況</li><li>Subcommand_opcode</ul>|

コント ローラーは、このコマンドに応答コマンドが完了イベントを生成するものと速やかに。

#### <a name="commandparameters"></a>Command_parameters

Subcommand_opcode (1 オクテット)。

| Value  |  パラメーターの説明 |
|---|---|
|0x04   |  HCI_VS_MSFT_LE_Cancel_Monitor_Advertisement のサブコマンド オペコードです。|

Connection_handle (1 オクテット)。

| Value  |  パラメーターの説明 |
|---|---|
|0 xxx| 取り消すフィルターへのハンドル。|


#### <a name="returnparameters"></a>Return_parameters

状態 (1 オクテット):

| Value  |  パラメーターの説明 |
|---|---|
|  0x00 |  コマンドが成功しました。 |
|0x07|コント ローラーは、コマンドを処理するのに十分なメモリがあるない場合は、メモリ容量を超えて返します。|
| エラー コード  |  コマンドが失敗しました。 参照してください_エラーコード_詳細については、Bluetooth のコア仕様でします。 |

Subcommand_opcode (1 オクテット)。

| Value  |  パラメーターの説明 |
|---|---|
|0x04| HCI_VS_MSFT_LE_Cancel_Monitor_Adver のサブコマンド オペコードです。 |


#### <a name="eventsgeneratedunlessmaskedaway"></a>Events_generated__unless_masked_away

コント ローラー HCI_VS_MSFT_LE_Cancel_Monitor_Advertisement コマンドを受信したコマンドの完了イベントが生成されます。


### <a name="hcivsmsftlesetadvertisementfilterenable"></a>HCI_VS_MSFT_LE_Set_Advertisement_Filter_Enable

HCI_VS_MSFT_LE_Set_Advertisement_Filter_Enable では、提供情報のフィルターの状態を設定します。

|コマンド|コード|コマンドのパラメーター|戻り値パラメーター|
|---|---|---|---|
|HCI_VS_MSFT_LE_Set_Advertisement_Filter_Enable|選択した基本コード |<ul><li>Subcommand_opcode</li><li>Enable</li>|<ul><li>状況</li><li>Subcommand_opcode</ul>|


場合_を有効にする_設定は、0x00、コント ローラーに既存のホワイト リスト設定に基づいて、ホストに受信した提供情報伝達されます。 コント ローラーが現在監視されていると、生成するデバイスの監視を継続するものと、 [HCI_VS_MSFT_LE_Monitor_Device_Event](#hcivsmsftlemonitordeviceevent)で_Monitor_state_デバイスが不要になった場合は 0 に設定監視されています。 コント ローラーを生成すると、HCI_VS_MSFT_LE_Monitor_Device_Event _Monitor_state_新しいデバイスが監視されている場合は 1 に設定します。 ホスト発行と HCI_VS_MSFT_LE_Set_Advertisement_Filter_Enable_を有効にする_0x01 に設定すると、すべてのフィルター条件を再度有効にします。

場合_を有効にする_設定されている 0x01 には、このコマンドは、以前に発行されたが設定されているすべてのフィルターを有効[HCI_VS_MSFT_LE_Monitor_Advertisement](#hcivsmsftlemonitoradvertisement)コマンド。 コント ローラーはフィルターの状態を切り替えることはない場合、HCI_VS_MSFT_LE_Set_Advertisement_Filter_Enable コマンドを拒否します。

-    コント ローラーは HCI_VS_MSFT_LE_Set_Advertisement_Filter_Enable コマンドを拒否_を有効にする_0x01 HCI_VS_MSFT_LE_Set_Advertisement_Filter_Enable コマンド以前受信した場合は設定_有効にする_0x01 に設定します。
- コント ローラーは HCI_VS_MSFT_LE_Set_Advertisement_Filter_Enable コマンドを元に戻す_を有効にする_HCI_VS_MSFT_LE_Set_Advertisement_Filter_Enable コマンド以前受信した場合は 0x00 に設定_有効にする_0x00 に設定します。

提供情報のフィルターの既定の状態がオフにされます。 この状態は、コント ローラーが以前に HCI_VS_MSFT_LE_Set_Advertisement_Filter_Enable コマンドの受信に相当_を有効にする_0x00 に設定します。
コント ローラーは、このコマンドに応答コマンドが完了イベントを生成するものと速やかに。

#### <a name="commandparameters"></a>Command_parameters

Subcommand_opcode (1 オクテット)。

| Value  |  パラメーターの説明 |
|---|---|
|0x05|  HCI_VS_MSFT_LE_Set_Advertisement_Filter_Enable のサブコマンド オペコードです。|

(1 オクテット) 有効にするには:

| Value  |  パラメーターの説明 |
|---|---|
|0x00| 現在、ホワイト リストの動作に戻すから _Condition_s に基づいてデバイスの監視はまだ[HCI_VS_MSFT_LE_Monitor_Advertisement](#hcivsmsftlemonitoradvertisement)コマンド。|
|0x01|コント ローラー上のすべての発行済みの HCI_VS_MSFT_LE_Monitor_Advertisement コマンドを有効にします。|

#### <a name="returnparameter"></a>Return_parameter

状態 (1 オクテット):

|Value|パラメーターの説明|
|---|---|
|0x00|コマンドが成功しました。|
|0x0C|コント ローラーを返す_コマンドが許可されていません_HCI_VS_MSFT_LE_Set_Advertisement_Filter_Enable コマンドを紹介したため、コント ローラーに、コマンドが拒否された場合_を有効にする_に設定しますこのコマンドと同じ値です。|
|エラー&#160;コード|コマンドが失敗しました。 参照してください_エラーコード_詳細については、Bluetooth のコア仕様でします。|

Subcommand_opcode (1 オクテット)。

|Value|パラメーターの説明|
|---|---|
|0x05|HCI_VS_MSFT_LE_Set_Advertisement_Filter_Enable のサブコマンド オペコードです。|

#### <a name="eventsgeneratedunlessmaskedaway"></a>Events_generated__unless_masked_away

コント ローラー HCI_VS_MSFT_LE_Set_Advertisement_Filter_Enable コマンドを受信したコマンドの完了イベントが生成されます。


#### <a name="hcivsmsftreadabsoluterssi"></a>HCI_VS_MSFT_Read_Absolute_RSSI

HCI_VS_MSFT_Read_Absolute_RSSI を読み取り、**絶対**コント ローラーから BR EDR/接続の受信信号の強さを示す値 (RSSI) 値。

|コマンド|コード|コマンドのパラメーター|戻り値パラメーター|
|---|---|---|---|
|HCI_VS_MSFT_Read_Absolute_RSSI|選択した基本コード |<ul><li>Subcommand_opcode</li><li>ハンドル</li>|<ul><li>状況</li><li>Subcommand_opcode</li><li>ハンドル</li><li>RSSI</li></ul>|


接続ハンドルは、コマンドと戻り値パラメーターの両方が RSSI が読み取られる ACL の接続を識別するために提供されます。 RSSI メトリックは、**絶対**± 6 dB 精度 dBm で信号強度を受信します。 RSSI が読み取れない場合は、127 に RSSI メトリックを設定する必要があります。
コント ローラーでは、コマンドの完了イベントをすぐにこのコマンドが完了常にものとします。

#### <a name="commandparameters"></a>Command_parameters

Subcommand_opcode (1 オクテット)。

| Value  |  パラメーターの説明 |
|---|---|
|0x06|  HCI_VS_MSFT_Read_Absolute_RSSI のサブコマンド オペコードです。|

ハンドル (2 つのオクテット):

| Value  |  パラメーターの説明 |
|---|---|
|0x_XXXX_|ある RSSI を読み取る必要があります BR EDR/接続のハンドル。|

#### <a name="returnparameters"></a>Return_parameters

状態 (1 オクテット):

|Value|パラメーターの説明|
|---|---|
|0x00|コマンドが成功しました。|
|0x01 - 0 xff の場合|コマンドが失敗しました。 参照してください_エラーコード_詳細については、Bluetooth のコア仕様でします。|

Subcommand_opcode (1 オクテット)。

|Value|パラメーターの説明|
|---|---|
|0x06|HCI_VS_MSFT_Read_Absolute_RSSI のサブコマンド オペコードです。|

ハンドル (2 つのオクテット):

|Value|パラメーターの説明|
|---|---|
|0xXXXX| ある RSSI が読み取られた BR EDR/接続のハンドル。|

RSSI (1 オクテット)。


|     Value      |                                                  パラメーターの説明                                                   |
|----------------|--------------------------------------------------------------------------------------------------------------------------|
| N = RSSI 値 | BR EDR/接続の RSSI 値。<ul><li>範囲:-128 &lt; =  *N* &lt;= 127 (符号付き整数)</li><li>単位: dBm</li> |

#### <a name="eventsgeneratedunlessmaskedaway"></a>Events_generated__unless_masked_away
コント ローラー HCI_VS_MSFT_Read_Absolute_RSSI コマンドが完了したらコマンドの完了イベントが生成されます。 

## <a name="microsoft-defined-bluetooth-hci-events"></a>マイクロソフトによって定義された Bluetooth HCI イベント

すべての Bluetooth HCI の Microsoft によるイベントは、ベンダー定義イベントし、0 xff までのイベント コードを使用します。 Microsoft イベントのイベント データは、常に、その他のベンダ定義イベントから、マイクロソフトによって定義されたイベントを区別するためにバイトの定数文字列で始まります。 長さと文字列定数の値はコント ローラーの実装者が定義されへの応答で返される[HCI_VS_MSFT_Read_Supported_Features](#hcivsmsftreadsupportedfeatures)します。

|HCI イベント|説明|
|---|---|
|[HCI_VS_MSFT_Rssi_Event](#hcivsmsftrssievent)|HCI_VS_MSFT_RSSI_Event をことを示します、 [HCI_VS_MSFT_Monitor_Rssi](#hcivsmsftmonitorrssi)コマンドが完了しました。|
|[HCI_VS_MSFT_LE_Monitor_Device_Event](#hcivsmsftlemonitordeviceevent)|HCI_VS_MSFT_LE_Monitor_Device_Event では、こと、コント ローラーが起動または Bluetooth LE デバイスの監視を停止することを示します。|

### <a name="hcivsmsftrssievent"></a>HCI_VS_MSFT_RSSI_Event

HCI_VS_MSFT_RSSI_Event をことを示します、 [HCI_VS_MSFT_Monitor_Rssi](#hcivsmsftmonitorrssi)コマンドが完了しました。
場合、_状態_パラメーターが 0 では、指定した範囲外の値をリモート デバイスの RSSI 値が変更されたために、完了コマンドです。 場合、_状態_パラメーターが 0 以外の場合、接続の RSSI の値を監視できなくできるため完了コマンド。


|イベント|イベント コード|Microsoft イベント コード|イベント パラメーター|
|---|---|---|---|
|HCI_VS_MSFT_RSSI_Event|0 xff の場合|0x01|<p>Event_prefix</p><p>Microsoft_event_code</p><p>状況</p><p>Connection_handle</p><p>RSSI</p>

#### <a name="eventparameters"></a>Event_parameters

Event_prefix (変数のサイズ):

|Value|パラメーターの説明|
|---|---|
|イベントのプレフィックス|このイベントは、Microsoft 定義としてフラグを設定するイベントのプレフィックス。 サイズと値がによって返される、 [HCI_VS_MSFT_Read_Supported_Features](#hcivsmsftreadsupportedfeatures)コマンド。|

Microsoft_event_code (1 オクテット)。

|Value|パラメーターの説明|
|---|---|
|0x01|HCI_VS_MSFT_RSSI_Event のイベント コード。|


状態 (1 オクテット):

|Value|パラメーターの説明|
|---|---|
|0x00|成功しました。 接続の RSSI の値は、次の条件のいずれかを満たします。<ul><li>RSSI に達したか超えました_RSSI_threshold_high_します。</li><li>RSSI に達したか、下にドロップ_RSSI_threshold_low_経由で_RSSI_threshold_low_time_interval_秒。</li><li>_RSSI_sampling_period_有効期限が切れた RSSI 値のホストに通知するイベントが生成されたとします。</li></ul>|
|0x01&#160;-&#160;0xFF|失敗しました。 接続の RSSI 値を監視することが不要になったことができます。 エラー コードは、通常は、基になる ACL の接続が失われた理由を説明するコードのいずれかです。|

Connection_handle (2 つのオクテット)。

|Value|パラメーターの説明|
|---|---|
|0x_XXXX_|監視対象となるが RSSI が接続のハンドル。|

RSSI (1 オクテット)。

|Value|パラメーターの説明|
|---|---|
|_N_ = _RSSI&#160;値_|測定のリンク接続の RSSI 値。 BR/EDR: の<ul><li>範囲:-128 &lt; =  _N_ &lt;= 127 (符号付き整数)</li><li>単位: dBm</li></ul>LE: の<ul><li>20 (符号付き整数) の範囲:-127</li><li>単位: dBm</li></ul>|

### <a name="hcivsmsftlemonitordeviceevent"></a>HCI_VS_MSFT_LE_Monitor_Device_Event

HCI_VS_MSFT_LE_Monitor_Device_Event では、こと、コント ローラーが起動または Bluetooth LE デバイスの監視を停止することを示します。 

場合、 _Monitor_state_パラメーターの値が 1 の場合、コント ローラーは、指定した定義での Bluetooth デバイスの監視を開始します。 場合、 _Monitor_state_パラメーターの値が 0 の場合、コント ローラーは、指定した定義での Bluetooth デバイスの監視を停止します。

|イベント|イベント コード|Microsoft イベント コード|イベント パラメーター|
|---|---|---|---|
|HCI_VS_MSFT_LE_Monitor_Device_Event|0 xff の場合|0x02|<p>Event_prefix</p><p>Microsoft_event_code</p><p>Address_type</p><p>定義</p><p>Monitor_handle</p><p>Monitor_state</p>

コント ローラーを生成する必要を HCI_VS_MSFT_LE_Monitor_Device_Event でない、 _Monitor_state_で、HCI_VS_MSFT_LE_Monitor_Device_Event が既に生成がない場合に、パラメーターが 0 に設定_Monitor_state_を 1 に設定します。

#### <a name="eventparameters"></a>Event_parameters

Event_prefix (変数のサイズ):

|Value|パラメーターの説明|
|---|---|
|イベントのプレフィックス|このイベントは、Microsoft 定義としてフラグを設定するイベントのプレフィックス。 サイズと値がによって返される、 [HCI_VS_MSFT_Read_Supported_Features](#hcivsmsftreadsupportedfeatures)コマンド。


Microsoft_event_code (1 オクテット)。

|Value|パラメーターの説明|
|---|---|
|0x02|HCI_VS_MSFT_LE_Monitor_Device_Event のイベント コード。|

Address_type (1 オクテット)。

|Value|パラメーターの説明|
|---|---|
|0x00|デバイスのパブリック アドレスです。|
|0x01|ランダムなデバイスのアドレス。|
|0x02&#160;-&#160;0xFF|将来使用するための予約済みの値。|


定義 (6、8 進数)。

|Value|パラメーターの説明|
|---|---|
|0x_XXXXXXXXXXXX_|デバイスの Bluetooth アドレス。|

Monitor_handle (1 オクテット)。

|Value|パラメーターの説明|
|---|---|
|0x_XX_|指定されたフィルターを識別するハンドル、 [HCI_VS_MSFT_LE_Monitor_Advertisement](#hcivsmsftlemonitoradvertisement)コマンド。|

Monitor_state (1 オクテット)。

|Value|パラメーターの説明|
|---|---|
|0x00|コント ローラーがで指定されたデバイスの監視を停止_定義_と_Monitor_handle_します。|
|0x01|指定されたデバイスの監視を開始して、コント ローラー_定義_と_Monitor_handle_します。|



