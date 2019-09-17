---
title: Microsoft 定義の Bluetooth HCI のコマンドとイベント
description: Bluetooth ホストコントローラーインターフェイス (HCI) は、ホストと Bluetooth ラジオコントローラーの間のすべての通信を指定します。
ms.assetid: 68E34B92-155B-401E-8D90-5BD1AF036B4D
ms.date: 02/07/2018
ms.localizationpriority: medium
ms.openlocfilehash: 400fdb42155f468a03c2570cfa295f269334f44c
ms.sourcegitcommit: 2c3b8e0ea0e75b72067d2e22dc530390bc19b11e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2019
ms.locfileid: "63328224"
---
# <a name="microsoft-defined-bluetooth-hci-extensions"></a>Microsoft が定義した Bluetooth HCI 拡張機能

Bluetooth ホストコントローラーインターフェイス (HCI) は、ホストと Bluetooth ラジオコントローラーの間のすべての通信を指定します。 Bluetooth 仕様では、ベンダー定義の HCI コマンドとイベントを使用して、ホストとコントローラーの間で標準化されていない対話を有効にすることができます。 Microsoft では、Windows によって使用されるベンダー固有の HCI コマンドとイベントを定義しています。 Bluetooth コントローラーの実装者は、これらの拡張機能を使用して特別な機能を実装できます。

## <a name="requirements"></a>要件

Windows 10 のデスクトップエディション (Home、Pro、Enterprise、および教育)、Windows 10 Mobile、およびそれ以降のバージョンでサポートされています。

## <a name="microsoft-defined-hci-commands"></a>Microsoft 定義の HCI コマンド

Bluetooth HCI コマンドは、16ビットのコマンドコードによって識別されます。 Bluetooth 組織は、0x0000 から0xFBFF までの範囲の値を定義します。 ベンダーは、0xFC00 ~ 0xFFFF の範囲の値を定義します。これにより、1024のベンダーによって割り当てられたコマンドコードを使用できます。

ベンダーは、Microsoft 定義のコマンドコードの値を選択する必要があります。 Microsoft では、コマンドコードを選択することはできません。また、競合する目的でコードを他のベンダーが使用しないことを前提としています。 ベンダー固有のコマンドを発行することは安全ではありません。また、コマンドが認識されない場合は、コントローラーに依存してコマンドを拒否します。 コントローラーは、コントローラーのファームウェアの更新などの破壊的な操作として、コマンドを解釈することができます。

ベンダーは、コントローラー以外のメソッドを使用して、選択された値を通信する必要があります。 Microsoft では、選択したコードを取得する方法を指定していません。

|HCI コマンド|説明|
|---|---|
|[HCI_VS_MSFT_Read_Supported_Features](#hci_vs_msft_read_supported_features) | HCI_VS_MSFT_Read_Supported_Features は、コントローラーがサポートする Microsoft 定義の機能を説明するビットマップを提供し、コントローラーによって返される Microsoft 定義のイベントのプレフィックスを指定します。|
|[HCI_VS_MSFT_Monitor_Rssi](#hci_vs_msft_monitor_rssi) | HCI_VS_MSFT_Monitor_Rssi は、指定された接続の測定されたリンク RSSI の監視をコントローラーが開始するように要求し、接続の測定されたリンク RSSI が指定された境界の外側に移動したときにイベントを生成します。|
|[HCI_VS_MSFT_Cancel_Monitor_Rssi](#hci_vs_msft_cancel_monitor_rssi) |HCI_VS_MSFT_Cancel_Monitor_Rssi は、以前に発行された HCI_VS_MSFT_Monitor_Rssi コマンドをキャンセルします。|
|[HCI_VS_MSFT_LE_Monitor_Advertisement](#hci_vs_msft_le_monitor_advertisement) | HCI_VS_MSFT_LE_Monitor_Advertisement は、指定された RSSI 範囲内にある提供情報の監視をコントローラーが開始し、他の要件を満たすことを要求します。|
|[HCI_VS_MSFT_LE_Cancel_Monitor_Advertisement](#hci_vs_msft_le_cancel_monitor_advertisement) | HCI_VS_MSFT_LE_Cancel_Monitor_Advertisement は、以前に発行された HCI_VS_MSFT_LE_Monitor_Advertisement コマンドをキャンセルします。|
[HCI_VS_MSFT_LE_Set_Advertisement_Filter_Enable](#hci_vs_msft_le_set_advertisement_filter_enable) | HCI_VS_MSFT_LE_Set_Advertisement_Filter_Enable は、提供情報フィルターの状態を設定します。|
|[HCI_VS_MSFT_Read_Absolute_RSSI](#hci_vs_msft_read_absolute_rssi) | HCI_VS_MSFT_Read_Absolute_RSSI は、コントローラーからの BR/EDR 接続について、受信した信号強度 (RSSI) の絶対値を読み取ります。|

### <a name="notifying-windows-bluetooth-stack-of-the-vendor-specific-command-code"></a>ベンダー固有のコマンドコードの Windows Bluetooth スタックへの通知

Windows Bluetooth スタックは、ベンダー固有のコマンドコードをレジストリキーから読み取ります。

VsMsftOpCode レジストリキーの種類は REG_DWORD で、キーデータはベンダー固有のオペコードです。

VsMsftOpCode キーへのレジストリパスは次のとおりです。

HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Enum\<デバイスインスタンスパス > \Device Parameters\VsMsftOpCode

次のコマンド例では、コマンドラインからレジストリ値を追加します。

```cpp
REG ADD "HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Enum\<Device instance path>\Device Parameters" /v VsMsftOpCode /t REG_DWORD /d <Vendor specific command code>
```

### <a name="using-inf-to-set-the-vsmsftopcode-registry-key"></a>INF を使用した VsMsftOpCode レジストリキーの設定

ベンダー固有のコマンドコードは、INF ファイルを使用して追加することもできます。 このサンプルでは、ベンダー固有のコマンドコードを追加してレジストリに自動的に追加されるようにする方法と場所を示します。

```cpp
[radio.NTamd64.HW]
AddReg=radio.NTamd64.HW.AddReg
[radio.NTamd64.HW.AddReg]
HKR,,"VsMsftOpCode",0x00010001,<Vendor Specific Opcode>
```

### <a name="microsoft-defined-hci-command-and-subcommands"></a>Microsoft 定義の HCI コマンドとサブコマンド

コントローラーは、Microsoft 固有の HCI コマンドが1つだけであることを認識します。 Microsoft 固有のコマンドセットは、オペコードを使用して拡張されます。 Microsoft 定義の HCI コマンドの最初のコマンドパラメーターは、サブコマンドを指定するオペコードです。

他の Microsoft HCI サブコマンドをサポートするために、コントローラーは[HCI_VS_MSFT_Read_Supported_Features](#hci_vs_msft_read_supported_features)をサポートする必要があります。 その他のコマンドのサポートは省略可能であり、HCI_VS_MSFT_Read_Supported_Features によって返される値によって異なります。 Windows では、コントローラーが HCI_VS_MSFT_Read_Supported_Features への応答を通じてサブコマンドのサポートを示す場合を除き、Microsoft が定義したサブコマンドは送信されません。

### <a name="hci_vs_msft_read_supported_features"></a>HCI_VS_MSFT_Read_Supported_Features

HCI_VS_MSFT_Read_Supported_Features は、コントローラーがサポートする Microsoft 定義の機能を説明するビットマップを提供し、コントローラーによって返される Microsoft 定義のイベントのプレフィックスを指定します。

コントローラーは、コマンド完了イベントを使用して、常にこのコマンドを実行する必要があります。

<table>
  <thead>
    <tr>
    <th>コマンド</th>
    <th>コード</th>
    <th>コマンドパラメーター</th>
    <th>戻りパラメーター</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>HCI_VS_MSFT_Read_Supported_Features</td>
      <td>選択された基本コード </td>
      <td>Subcommand_opcode</td>
      <td>
        <ul>
          <li>状況</li>
          <li>Subcommand_opcode</li>
          <li>Supported_features</li>
          <li>Microsoft_event_prefix_length</li>
          <li>Microsoft_event_prefix</li>
        </ul>
      </td>
    </tr>
  </tbody>
</table>

#### <a name="command_parameters"></a>Command_parameters

**Subcommand_opcode**(1 オクテット):

| Value  |  パラメーターの説明 |
|---|---|
|0x00   |  HCI_VS_MSFT_Read_Supported_Features のサブコマンドオペコード。|

#### <a name="return_parameters"></a>Return_parameters

**状態**(1 オクテット):

| Value  |  パラメーターの説明 |
|---|---|
|  0x00 |  コマンドが正常に実行されました。 |
| 0x01&#160;-&#160;0xFF  |  コマンドが失敗しました。 詳細については、「Bluetooth Core の仕様」の「_エラーコード_」を参照してください。 |

**Subcommand_opcode**(1 オクテット):

| Value  |  パラメーターの説明 |
|---|---|
|0x00   |  [HCI_VS_MSFT_Read_Supported_Features](#hci_vs_msft_read_supported_features)のサブコマンドオペコード。|

**Supported_features**(8 オクテット):

| Value  |  パラメーターの説明 |
|---|---|
|0x00000000&#160;00000001  |コントローラーは、BR/EDR 接続の RSSI Monitoring 機能をサポートしています。 さらに、このコントローラーは、BR/EDR 接続の絶対 RSSI メトリックを読み取るために[HCI_VS_MSFT_Read_Absolute_RSSI](#hci_vs_msft_read_absolute_rssi)をサポートしています。 |
|0x00000000&#160;00000002  |コントローラーは、LE 接続の RSSI Monitoring 機能をサポートしています。 |
|0x00000000&#160;00000004  |コントローラーでは、LE 広告の RSSI 監視がサポートされています。 |
|0x00000000&#160;00000008|コントローラーは、LE 広告の監視をサポートしています。|
|0x00000000&#160;00000010 |コントローラーは、P-192 と P-256 のセキュリティで保護された単純なペアリングプロセス中に、曲線上のパブリック X 座標と Y 座標の有効性を検証することをサポートしています。 <br/>詳細については、「 [Bluetooth Core Specification Erratum 10734](https://www.bluetooth.org/docman/handlers/downloaddoc.ashx?doc_id=447440)」を参照してください。|
|0x00000000 00000020|コントローラーは、他のラジオアクティビティと同時に実行される LE 広告の継続的な広告監視をサポートします。|
|0xFFFFFFFF&#160;FFFFFFF0|将来の定義用に予約されているビット。 0にする必要があります。|

**Microsoft_event_prefix_length**(1 オクテット):

| Value  |  パラメーターの説明 |
|---|---|
|0x00&#160;-&#160;0x20|返された_Microsoft_event_prefix_で指定された Microsoft イベントプレフィックスフィールドのバイト数。 これは、Microsoft が指定したすべての HCI イベントの先頭にある、定数情報のバイト数です。|

**Microsoft_event_prefix**(可変長):

| Value  |  パラメーターの説明 |
|---|---|
|イベント&#160;プレフィックス&#160;値| 各 Microsoft 定義イベントの先頭で予想される定数情報。 この情報は、Microsoft が定義したイベントを他のカスタムイベントと区別するために使用されます。|

### <a name="hci_vs_msft_monitor_rssi"></a>HCI_VS_MSFT_Monitor_Rssi

HCI_VS_MSFT_Monitor_Rssi は、指定された接続の測定されたリンク RSSI の監視をコントローラーが開始するように要求し、接続の測定されたリンク RSSI が指定された境界の外側に移動したときにイベントを生成します。

|コマンド|コード|コマンドパラメーター|戻りパラメーター|
|---|---|---|---|
|HCI_VS_MSFT_Read_Supported_Features|選択された基本コード |<ul><li>Subcommand_opcode</li><li>Connection_handle</li><li>RSSI_threshold_high</li><li>RSSI_threshold_low</li><li>RSSI_threshold_low_time_interval</li><li>RSSI_sampling_period</li></ul>|<ul><li>状況</li><li>Subcommand_opcode</ul>|

コントローラーは、 _RSSI_sampling_period_に基づいて、定期的に生成されたイベントを使用して RSSI 値のホストに通知する必要があります。 測定されたリンク RSSI は、その BR/EDR 接続について、dBm の**絶対**レシーバーシグナルの強さの値である必要があります。
コントローラーは、HCI_VS_MSFT_Monitor_Rssi コマンドに応答して、ステータスが0のコマンド完了イベントを生成する必要があります。コントローラーが監視を開始できる場合は0、それ以外の場合は0以外の状態になります。 Status 値が0以外の場合、コントローラーは、このコマンドに応答して[HCI_VS_MSFT_Rssi_Event](#hci_vs_msft_rssi_event)を生成しません。
同じ_Connection_handle_を持つ別の HCI_VS_MSFT_Monitor_Rssi コマンドが未解決の場合、または指定された接続ハンドルが無効である場合、コントローラーはコマンドを拒否します。 コントローラーは、リソース枯渇などの他の理由でコマンドを拒否することもできます。

#### <a name="state_diagram"></a>State_diagram

この状態の図は、接続の RSSI を監視する場合のコントローラーの遷移状態を示しています。HCI_VS_MSFT_Monitor_Rssi の状態ダイアグラムは、受信した Rssi が指定された_RSSI_threshold_high_以上の場合に、[HCI_VS_MSFT_Rssi_Event](#hci_vs_msft_rssi_event) を生成する必要があります。![](images/HCI_VS_MSFT_Monitor_Rssi_State_Diagram.png) このイベントが生成された後、コントローラーは、RSSI が下回っ _たことを指定する HCI_VS_MSFT_Rssi_Event を生成するまで RSSI_threshold_high が超過したことを指定する新しい HCI_VS_MSFT_Rssi_Event を生成しません。RSSI_threshold_low_。

このコントローラーは、受信した RSSI が、指定された_RSSI_threshold_low_time_interval_で指定された_RSSI_threshold_low_に等しいか下回った場合に、HCI_VS_MSFT_Rssi_Event を生成する必要があります。 このイベントが生成された後、コントローラーは、HCI_VS_MSFT_Rssi_Event イベントが生成されるまで RSSI が_RSSI_threshold_low_を下回ったことを指定する新しい HCI_VS_MSFT_Rssi_Event を生成しないようにして、RSSI_ を指定します。 _threshold_high_に達したか、それを超えています。

_RSSI_sampling_period_が0X01 と0xfe の間にある場合、コントローラーは_RSSI_sampling_period_ごとに HCI_VS_MSFT_Rssi_Event を定期的に生成する必要があります。 このイベントには、 _RSSI_sampling_period_に対して計算された RSSI の平均が含まれます。
_RSSI_sampling_period_が0x00 または0xff の場合、コントローラーはホストに定期的に HCI_VS_MSFT_Rssi_Event を通知し**ません**。

#### <a name="command_parameters"></a>Command_parameters

Subcommand_opcode (1 オクテット):

| Value  |  パラメーターの説明 |
|---|---|
|0x01   |  HCI_VS_MSFT_Monitor_Rssi のサブコマンドオペコード。|

Connection_handle (2 オクテット):

| Value  |  パラメーターの説明 |
|---|---|
|0Xxxxx (_l)   |  RSSI を監視する必要がある接続のハンドル。|

RSSI_threshold_high (1 オクテット):

| Value  |  パラメーターの説明 |
|---|---|
|N_ = High&#160;RSSI threshold&#160;の値 |  予想される最大 RSSI 値。 監視対象の RSSI がこの値以上になると、コントローラーはイベントを生成します。 BR/EDR の場合: <ul><li>範囲:-128 &lt; =  N&lt;= 127 (符号付き整数)</li><li>Unit: dBm</li></ul>LE の場合:<ul><li>範囲:-127 ~ 20 (符号付き整数)</li><li>Unit: dBm</li></ul>|

RSSI_threshold_low (1 オクテット):

| Value  |  パラメーターの説明 |
|---|---|
|N_ = 低&#160;RSSI しきい&#160;値|予想される最小 RSSI 値。 監視対象の RSSI がこの値以下になると、コントローラーはイベントを生成します。 BR/EDR の場合:<ul><li>範囲:-128 &lt; =  N&lt;= 127 (符号付き整数)</li><li>Unit: dBm</li></ul>LE の場合:<ul><li>範囲:-127 ~ 20 (符号付き整数)</li><li>Unit: dBm</li></ul>|

RSSI_threshold_low_time_interval (1 オクテット):

| Value  |  パラメーターの説明 |
|---|---|
|0x00|予約済みの値。|
|N_&#160;=&#160;0x01&#160;-&#160;0x3C|期間 = _N_ * 1 は、 [HCI_VS_MSFT_Rssi_Event](#hci_vs_msft_rssi_event)が生成される前に、RSSI 値が_RSSI_threshold_low_未満になるまでの時間を秒単位で示します。

RSSI_sampling_period (1 オクテット):

| Value  |  パラメーターの説明 |
|---|---|
|0x00|予約済みの値。|
|_N_&#160;=&#160;0x01&#160;-&#160;0xfe|期間 = _N_ * 100 millisecondsThe サンプリング間隔 (ミリ秒単位)。|
|0xFF|予約済みの値。|

#### <a name="return_parameters"></a>Return_parameters

状態 (1 オクテット):

| Value  |  パラメーターの説明 |
|---|---|
|  0x00 |  コマンドが正常に実行されました。 |
| 0x01&#160;-&#160;0xFF  |  コマンドが失敗しました。 詳細については、「Bluetooth Core の仕様」の「_エラーコード_」を参照してください。 |
|0x07|コマンドを処理するのに十分なメモリがない場合、コントローラーは_メモリ容量を超え_たことを返します。|
|_エラー&#160;コード_| コマンドが失敗しました。 詳細については、「Bluetooth Core の仕様」の「_エラーコード_」を参照してください。|

Subcommand_opcod (1 オクテット):

| Value  |  パラメーターの説明 |
|---|---|
|0x01|HCI_VS_MSFT_Monitor_Rssi のサブコマンドオペコード。|

#### <a name="events_generated__unless_masked_away"></a>Events_generated__unless_masked_away

コントローラーは、HCI_VS_MSFT_Monitor_Rssi コマンドを受信したときに、直ちにコマンド完了イベントを生成する必要があります。 コマンド完了イベントによってステータス0が返された場合、次のいずれかが発生すると、コントローラーは[HCI_VS_MSFT_Rssi_Event](#hci_vs_msft_rssi_event)を生成します。

- デバイスの観測された RSSI が_RSSI_threshold_low_time_interval_を超えると、指定した_RSSI_threshold_low_値以下になります。

- デバイスの観測された RSSI が、指定された_RSSI_threshold_high_値以上になっています。

- _RSSI_sampling_period_は有効で、サンプリング期間は終了します。

コントローラーは、指定されたデバイスとの接続が失われた場合に必要なすべてのクリーンアップを実行します。 この場合、 [HCI_VS_MSFT_Cancel_Monitor_Rssi](#hci_vs_msft_cancel_monitor_rssi)コマンドはコントローラーに送信されません。

### <a name="hci_vs_msft_cancel_monitor_rssi"></a>HCI_VS_MSFT_Cancel_Monitor_Rssi

HCI_VS_MSFT_Cancel_Monitor_Rssi は、以前に発行された[HCI_VS_MSFT_Monitor_Rssi](#hci_vs_msft_monitor_rssi)コマンドをキャンセルします。
コントローラーは、このコマンドに応答して、コマンドの完了イベントを即座に生成する必要があります。

|コマンド|コード|コマンドパラメーター|戻りパラメーター|
|---|---|---|---|
|HCI_VS_MSFT_Cancel_Monitor_Rssi|選択された基本コード |<ul><li>Subcommand_opcode</li><li>Connection_handle</li>|<ul><li>状況</li><li>Subcommand_opcode</ul>|

#### <a name="command_parameters"></a>Command_parameters

Subcommand_opcode (1 オクテット):

| Value  |  パラメーターの説明 |
|---|---|
|0x02   |  HCI_VS_MSFT_Cancel_Monitor_Rssi のサブコマンドオペコード。|

Connection_handle (1 オクテット):

| Value  |  パラメーターの説明 |
|---|---|
|0Xxxxx (_l)   |  RSSI をキャンセルする必要がある接続のハンドル。|

#### <a name="return_parameters"></a>Return_parameters

状態 (1 オクテット):

| Value  |  パラメーターの説明 |
|---|---|
|  0x00 |  コマンドが正常に実行されました。 |
| 0x01&#160;-&#160;0xFF  |  コマンドが失敗しました。 詳細については、「Bluetooth Core の仕様」の「_エラーコード_」を参照してください。 |

Subcommand_opcod (1 オクテット):

| Value  |  パラメーターの説明 |
|---|---|
|0x02|HCI_VS_MSFT_Cancel_Monitor_Rssi のサブコマンドオペコード。|

#### <a name="events_generated__unless_masked_away"></a>Events_generated__unless_masked_away

HCI_VS_MSFT_Cancel_Monitor_RSSI コマンドを受信すると、コントローラーはコマンド完了イベントを生成する必要があります。

### <a name="hci_vs_msft_le_monitor_advertisement"></a>HCI_VS_MSFT_LE_Monitor_Advertisement

HCI_VS_MSFT_LE_Monitor_Advertisement は、指定された RSSI 範囲内にある提供情報の監視をコントローラーが開始するように要求します。また、次のいずれかの条件を満たします。

- 指定されたパターンは、受信した提供情報パケットと照合できます。
- 指定された UUID は、受信した提供情報 packe と照合できます。
- 指定された Id 解決キー (IRK) を使用して、提供情報パケットの送信元のデバイスのプライベートアドレスを解決できます。
- 指定された Bluetooth アドレスは、受信した提供情報パケットと照合できます。

|コマンド|コード|コマンドパラメーター|戻りパラメーター|
|---|---|---|---|
|HCI_VS_MSFT_LE_Monitor_Advertisement|選択された基本コード |<ul><li>Subcommand_opcode</li><li>Connection_handle</li>|<ul><li>状況</li><li>Subcommand_opcode<li>Monitor_handle</li></ul>|

コントローラーは、このコマンドに応答してコマンド完了イベントを生成する必要があります。 コントローラーが監視を開始できる場合は status 値を0に設定し、それ以外の場合は0以外の状態を設定する必要があります。
コントローラーが LE 広告の RSSI monitoring をサポートしていない場合、 _RSSI_threshold_high_、 _RSSI_threshold_low_、 _RSSI_threshold_low_time_interval_、および_RSSI_sampling_period_の各パラメーター値は無視されます.

#### <a name="state_diagram"></a>State_diagram

この状態の図は、提供情報の RSSI を監視するときのコントローラーの遷移状態を示しています。 ![HCI_VS_MSFT_LE_Monitor_Advertisement](images/HCI_VS_MSFT_LE_Monitor_Advertisement_State_Diagram.png)の状態ダイアグラム。 このコントローラーは、受信した RSSI が特定のデバイスの_RSSI_threshold_high_以上である場合にのみ、最初のアドバタイズパケットをホストに伝達する必要があります。 コントローラーは、コントローラーが監視していることをホストに通知するために、 _Monitor_state_を1に設定し、 _Monitor_handle_をこの_条件_のハンドルに設定して、 [HCI_VS_MSFT_LE_Monitor_Device_Event](#hci_vs_msft_le_monitor_device_event)を生成する必要があります。_条件_の特定のデバイス。
受信した提供情報の RSSI が特定のデバイスの_RSSI_threshold_low_interval_ _を超えて_いるか下回っている場合、コントローラーは_状態_の監視を停止します。 コントローラーは、 _Monitor_state_を0に設定して[HCI_VS_MSFT_LE_Monitor_Device_Event](#hci_vs_msft_le_monitor_device_event)を生成し、その_条件_の特定のデバイスの監視がコントローラーによって停止されたことをホストに通知します。 コントローラーは、 _Monitor_state_が0に設定されている HCI_VS_MSFT_LE_Monitor_Device_Event を指定した後、コントローラーによって、RSSI がホストに通知されるまで、デバイスのホストに対してより多くのアドバタイズパケットを送信することを許可しません。では、特定のデバイスの_条件_に対して、特定のデバイスの_RSSI_threshold_high_以上が発生しています。
さらに、コントローラーは_Monitor_state_を0に設定して[HCI_VS_MSFT_LE_Monitor_Device_Event](#hci_vs_msft_le_monitor_device_event)を生成し、指定された RSSI_ が_条件_に対してデバイスの監視を停止したことをホストに通知します。 _threshold_low_time_interval_は、デバイスから広告パケットを受信しなくても有効期限が切れます。 コントローラーが特定の状態のデバイスを監視している場合は、次のステートメントが当てはまります。

- RSSI_sampling_period_ が0xFF に設定されている場合、コントローラーは、特定のデバイスの RSSI が _下回ったことをホストに通知するまで、そのデバイスのホストに対して、さらに情報提供パケットをフローすることを許可しません。_ この_条件_に対する特定のデバイスの_RSSI_threshold_low_time_interval_の RSSI_threshold_low。 この通知は、 _Monitor_state_を0に設定して[HCI_VS_MSFT_LE_Monitor_Device_Event](#hci_vs_msft_le_monitor_device_event)を生成することによって行われます。
- _RSSI_sampling_period_が0x0 に設定されている場合、コントローラーは、以前に [HCI_VS_MSFT_LE_Set_Advertisement_Filter_Enable](#hci_vs_msft_le_set_advertisement_filter_enable) を受信し_ていない_限り、受信したすべての提供情報パケットをデバイスのホストに伝達します。_Enable_を0x00 に設定してコマンドを実行します。 この _ために特定のデバイスで RSSI_threshold_low_time_interval が期限切れになっていない限り、受信した RSSI が RSSI_threshold_low 以下の場合でも、コントローラーは提供情報パケットをホストに伝達する必要があります。条件_。 この提供情報パケットの RSSI 値は、受信した提供情報の RSSI 値である必要があります。

_RSSI_sampling_period_が0X01 と0xfe の間にある場合、コントローラーは、前に [HCI_VS_MSFT_LE_Set_Advertisement_Filter_Enable](#hci_vs_msft_le_set_advertisement_filter_enable) を受け取っていない限り、指定された_RSSI_sampling_period_ごとに提供情報パケットをホストに伝達します。_Enable_を0x00 に設定してコマンドを実行します。 提供情報に指定された RSSI 値は、このサンプリング間隔中に受信した RSSI 値の平均値である必要があります。 サンプリング期間中に、提供情報パケットを受信しなかった場合は、ホストに提供情報が伝達されません。 _RSSI_sampling_period_が_RSSI_threshold_low_time_interval_よりも小さく、 _RSSI_sampling_period_中に受信したすべての提供情報が_RSSI_threshold_low_の下に RSSI を持っている可能性があります。 コントローラーは、このサンプリング間隔中に受信した RSSI 値の平均値を使用して提供情報を伝達する必要があります。

コントローラーが、 _Enable_を0x00 に設定して[HCI_VS_MSFT_LE_Set_Advertisement_Filter_Enable](#hci_vs_msft_le_set_advertisement_filter_enable)コマンドを受信した場合、サンプリング期間タイマーは停止されません。 例を参照してください。詳細については、サンプリング期間付きフィルターに関する HCI_VS_MSFT_LE_Set_Advertisement_Filter_Enable を参照してください。
同じデバイスから重複しない広告パケットを受信した場合、コントローラーに格納されている条件に対して、各公開通知パケットが一致している必要があります。

コントローラーが、複数の条件に一致するデバイスから提供情報パケットを受信した場合、コントローラーは、一致した各_条件_に対して_Monitor_handle_を使用して[HCI_VS_MSFT_LE_Monitor_Device_Event](#hci_vs_msft_le_monitor_device_event)を生成する必要があります。に一致した_条件_を設定します。

コントローラーが_条件_に一致する範囲内のすべてのデバイスの RSSI 値を監視できない場合、監視はできるだけ多くのデバイスで実行されます。 監視する必要があるデバイスの決定は、受信した提供情報の RSSI 値によって異なります。 コントローラーは、信号の強度が高いデバイスを監視する必要があります。

コントローラーが特定のデバイス (_a_) についてホストに通知し、ハードウェアの最大容量でデバイスを監視していて、別のデバイス (_B_) に RSSI 値が高い範囲内にある場合、コントローラーはホストに通知する必要があります。は、 _Monitor_state_を0に設定して[HCI_VS_MSFT_LE_Monitor_Device_Event](#hci_vs_msft_le_monitor_device_event)を生成することによって、デバイス (_A_) の監視を停止しました。 また、コントローラーは_Monitor_state_を1に設定して HCI_VS_MSFT_LE_Monitor_Device_Event を生成し、デバイス (_B_) が現在監視されていることをホストに通知します。

#### <a name="condition_type_and_condition_parameters"></a>Condition_type_and_Condition_parameters

_Condition_type_パラメーターでは、 _Condition_パラメーターで pattern、UUID、IRK、または BD_ADDR を指定するかどうかを指定します。
_Condition_type_パラメーターでパターンが_指定され_ている場合、条件には、_条件_内に存在するパターンの数とパターンデータを含む2つのセクションが含まれます。パターン条件データレイアウト](images/HCI_VS_MSFT_LE_Monitor_Advertisement_Conditions.png)
_パターンの数_は、照合する必要があるパターンの数を指定します。 ![

_パターンデータ_の形式は次のとおりです。

- _長さ_このパターンの長さには、パターンのデータ型と開始バイトを指定します。
- _Ad の種類_ad 型フィールドを指定します。
- _パターンの開始_は、AD 型の直後に続くパターンの開始バイト位置を指定します。
- _パターン_のサイズは (_長さ_は 0x2) で、指定された開始バイトから提供情報パケット内の指定された広告の種類と照合されるパターンです。

複数のパターンが指定されている場合、コントローラーは、少なくとも1つのパターンが受信した提供情報と一致することを保証する必要があります。

_Condition_type_パラメーターで uuid が指定されている場合、 _Condition_パラメーターには uuid 型と uuid が含まれます。 Uuid 型は、UUID が16ビット、32ビット、または128ビットのどちらであるかを指定します。 コントローラーは、指定された UUID を確認するために、提供情報パケットのサービス UUID を解析する必要があります。 UUID 型が0x01 として定義されている場合、コントローラーは、サービス UUID AD 型で指定されている16ビットサービス uuid の完全なリストと、すべての16ビットサービス uuid を解析する必要があります。 UUID 型が0x02 として定義されている場合、コントローラーは、32ビットサービス Uuid の不完全なリストと、サービス UUID AD 型で指定されている32ビット Uuid の完全な一覧を解析する必要があります。 指定された UUID の種類が0x03 の場合、コントローラーは、128ビットサービス Uuid の不完全なリストと、サービス UUID AD 型で指定された128ビットサービス Uuid の完全な一覧を解析する必要があります。

_Condition_type_パラメーターで irk が指定されている場合、 _Condition_パラメーターには irk が含まれます。

_Condition_type_パラメーターで Bluetooth アドレスを指定する場合、 _Condition_パラメーターにはアドレスの種類と BD_ADDR が含まれます。

スキャン (アクティブまたはパッシブ) が有効になっている場合でも、コントローラーは条件に基づいて監視を維持する必要があります。
アクティブスキャンが有効になっている場合、フィルターに一致する提供情報のスキャン応答をホストに反映する必要があります。

フィルターが無効になっているときにコントローラーが HCI_VS_MSFT_LE_Monitor_Advertisement コマンドを受信した場合 ( _Enable_が0x00 に設定された[HCI_VS_MSFT_LE_Set_Advertisement_Filter_Enable](#hci_vs_msft_le_set_advertisement_filter_enable)コマンドが既に受信されているため)、コントローラーはは、許可されている場合はコマンドを受け入れますが、無効の状態に設定します。
コントローラーは、リソース枯渇などの他の理由でコマンドを拒否することもできます。

#### <a name="command_parameters"></a>Command_parameters

Subcommand_opcode (1 オクテット):

| Value  |  パラメーターの説明 |
|---|---|
|0x03   |  HCI_VS_MSFT_LE_Monitor_Advertisement のサブコマンドオペコード。|

RSSI_threshold_high (1 オクテット):

| Value  |  パラメーターの説明 |
|---|---|
|High RSSI threshold 値|  予想される最大 RSSI 値。 監視対象の RSSI がこの値以上になると、コントローラーはイベントを生成します。 LE の場合:<ul><li>範囲:-127 ~ 20 (符号付き整数)</li><li>Unit: dBm</li></ul>|

RSSI_threshold_low (1 オクテット):

| Value  |  パラメーターの説明 |
|---|---|
|低 RSSI しきい値|予想される最小 RSSI 値。 監視対象の RSSI がこの値以下になると、コントローラーはイベントを生成します。 LE の場合:<ul><li>範囲:-127 ~ 20 (符号付き整数)</li><li>Unit: dBm</li></ul>|

RSSI_threshold_low_time_interval (1 オクテット):

| Value  |  パラメーターの説明 |
|---|---|
|0x00|予約済みの値。|
|N_&#160;=&#160;0x01&#160;-&#160;0x3C|期間 = _N_ * 1 秒。 [HCI_VS_MSFT_Rssi_Event](#hci_vs_msft_rssi_event)が生成される前に、RSSI 値が_RSSI_threshold_low_未満になるまでの時間 (秒単位)。

RSSI_sampling_period (1 オクテット):

| Value  |  パラメーターの説明 |
|---|---|
|0x00|予約済みの値。|
|_N_&#160;=&#160;0x01&#160;-&#160;0xfe|期間 = _N_ * 100 ミリ秒。 サンプリング間隔 (ミリ秒単位)。|
|0xFF|コントローラーは、受信した提供情報をホストに伝達することはできません。|

Condition_type (1 オクテット):

| Value  |  パラメーターの説明 |
|---|---|
|0x01|条件は、提供情報に対して照合する必要があるパターンです。|
|0x02|条件は UUID 型と UUID です。|
|0x03|この条件は IRK の解決策です。|
|0x04|条件は、Bluetooth アドレスです。|

フィルター条件に適用できるフィールドは、Condition_type の値によって異なります。 詳細については、「Condition_type and Condition parameters」セクションを参照してください。

Number_of_patterns (1 オクテット):

|Value | パラメーターの説明|
|---|---|
|0xXX| Pattern_data パラメーター内で指定されたパターンの数。|

Pattern_data (> 3 オクテット):

|Value | パラメーターの説明|
|---|---|
|長さ|このパターンの長さ。|
|データの種類| 提供情報セクションのデータ型。 値は、Bluetooth の割り当て番号に関するドキュメントに記載されています。|
|開始バイト| 指定されたデータ型と照合されるパターンの開始位置。|
|[パターン]| 照合するパターン (長さのサイズ–0x2 バイト)。|

UUID_type (1 オクテット):

|Value | パラメーターの説明|
|---|---|
|0x01| UUID は16ビットサービスです。|
|0x02| UUID は32ビットサービスです。|
|0x03| UUID は128ビットサービスです。|

UUID (2、4、または16オクテット):

|Value | パラメーターの説明|
|---|---|
|0xXXXX| <p>UUID_type が0x01 の場合は2バイト。<p><p>UUID_type が0x02 の場合は4バイトです。</p><p>UUID_type が0x03 の場合は16バイトです。</p>|

IRK (16 オクテット):

| Value  |  パラメーターの説明 |
|---|---|
|<p>0xXXXXXXXX XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX</p><p>XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX</p>|プライベートアドレスを解決するために使用される IRK。|

Address_type (1 オクテット):

| Value  |  パラメーターの説明 |
|---|---|
|0x00| パブリックデバイスアドレス。|
|0x01| ランダムデバイスアドレス。|
|0x02-0xFF| 将来使用するために予約された値。|

Address_type (1 オクテット):

| Value  |  パラメーターの説明 |
|---|---|
|0xXXXXXXXXXXXX 場合|監視するデバイスの Bluetooth アドレス。|

#### <a name="return_parameters"></a>Return_parameters

状態 (1 オクテット):

| Value  |  パラメーターの説明 |
|---|---|
|  0x00 |  コマンドが正常に実行されました。 |
|0x07|コマンドを処理するのに十分なメモリがない場合、コントローラーはメモリ容量を超えたことを返します。|
| エラー コード  |  コマンドが失敗しました。 詳細については、「Bluetooth Core の仕様」の「_エラーコード_」を参照してください。 |

Subcommand_opcode (1 オクテット):

| Value  |  パラメーターの説明 |
|---|---|
|0x03| HCI_VS_MSFT_LE_Monitor_Advertisement のサブコマンドオペコード。 |

Monitor_handle (1 オクテット):

| Value  |  パラメーターの説明 |
|---|---|
|0x00 ~ 0xFF|この規則へのハンドル。 このハンドルは、提供情報の監視をキャンセルする HCI_VS_MSFT_LE_Cancel_Monitor_Advertisement のパラメーターとして使用されます。 このパラメーターは、Status が0x00 の場合にのみ有効です。|

#### <a name="events_generated__unless_masked_away"></a>Events_generated__unless_masked_away

HCI_VS_MSFT_LE_Monitor_Advertisement コマンドを受信すると、コントローラーはコマンド完了イベントを生成する必要があります。

### <a name="hci_vs_msft_le_cancel_monitor_advertisement"></a>HCI_VS_MSFT_LE_Cancel_Monitor_Advertisement

HCI_VS_MSFT_LE_Cancel_Monitor_Advertisement は、以前に発行された[HCI_VS_MSFT_LE_Monitor_Advertisement](#hci_vs_msft_le_monitor_advertisement)コマンドをキャンセルします。

|コマンド|コード|コマンドパラメーター|戻りパラメーター|
|---|---|---|---|
|HCI_VS_MSFT_LE_Cancel_Monitor_Advertisement|選択された基本コード |<ul><li>Subcommand_opcode</li><li>Monitor_handle</li>|<ul><li>状況</li><li>Subcommand_opcode</ul>|

コントローラーは、このコマンドに応答して、コマンドの完了イベントを即座に生成する必要があります。

#### <a name="command_parameters"></a>Command_parameters

Subcommand_opcode (1 オクテット):

| Value  |  パラメーターの説明 |
|---|---|
|0x04   |  HCI_VS_MSFT_LE_Cancel_Monitor_Advertisement のサブコマンドオペコード。|

Connection_handle (1 オクテット):

| Value  |  パラメーターの説明 |
|---|---|
|0xXX| キャンセルされるフィルターへのハンドル。|

#### <a name="return_parameters"></a>Return_parameters

状態 (1 オクテット):

| Value  |  パラメーターの説明 |
|---|---|
|  0x00 |  コマンドが正常に実行されました。 |
|0x07|コマンドを処理するのに十分なメモリがない場合、コントローラーはメモリ容量を超えたことを返します。|
| エラー コード  |  コマンドが失敗しました。 詳細については、「Bluetooth Core の仕様」の「_エラーコード_」を参照してください。 |

Subcommand_opcode (1 オクテット):

| Value  |  パラメーターの説明 |
|---|---|
|0x04| HCI_VS_MSFT_LE_Cancel_Monitor_Adver のサブコマンドオペコード。 |

#### <a name="events_generated__unless_masked_away"></a>Events_generated__unless_masked_away

HCI_VS_MSFT_LE_Cancel_Monitor_Advertisement コマンドを受信すると、コントローラーはコマンド完了イベントを生成する必要があります。

### <a name="hci_vs_msft_le_set_advertisement_filter_enable"></a>HCI_VS_MSFT_LE_Set_Advertisement_Filter_Enable

HCI_VS_MSFT_LE_Set_Advertisement_Filter_Enable は、提供情報フィルターの状態を設定します。

|コマンド|コード|コマンドパラメーター|戻りパラメーター|
|---|---|---|---|
|HCI_VS_MSFT_LE_Set_Advertisement_Filter_Enable|選択された基本コード |<ul><li>Subcommand_opcode</li><li>Enable</li>|<ul><li>状況</li><li>Subcommand_opcode</ul>|

_Enable_が0x00 に設定されている場合、コントローラーは、既存のホワイトリストの設定に基づいて、受信した提供情報をホストに伝達します。 コントローラーは、現在監視されているデバイスの監視を続行し、デバイスが監視されなくなった場合は_Monitor_state_を0に設定して[HCI_VS_MSFT_LE_Monitor_Device_Event](#hci_vs_msft_le_monitor_device_event)を生成します。 新しいデバイスが監視されている場合、コントローラーは_Monitor_state_を1に設定して HCI_VS_MSFT_LE_Monitor_Device_Event を生成する必要があります。 ホストは、 _Enable_を0x01 に設定して HCI_VS_MSFT_LE_Set_Advertisement_Filter_Enable を発行し、すべてのフィルター条件を再度有効にすることができます。

_Enable_を0x01 に設定した場合、このコマンドは、以前に発行された[HCI_VS_MSFT_LE_Monitor_Advertisement](#hci_vs_msft_le_monitor_advertisement)コマンドで設定されたすべてのフィルターを有効にします。 フィルターの状態を切り替えない場合、コントローラーは HCI_VS_MSFT_LE_Set_Advertisement_Filter_Enable コマンドを拒否します。

- _Enable_が0x01 に設定された HCI_VS_MSFT_LE_Set_Advertisement_Filter_Enable コマンドを以前に受信した場合は、 _enable_が0x01 に設定されている HCI_VS_MSFT_LE_Set_Advertisement_Filter_Enable コマンドをコントローラーが拒否する必要があります。
- _Enable が0x00 に設定さ_れた HCI_VS_MSFT_LE_Set_Advertisement_Filter_Enable コマンドを_以前に受信_した場合、コントローラーは HCI_VS_MSFT_LE_Set_Advertisement_Filter_Enable コマンドを拒否します。

提供情報フィルターの既定の状態は off にする必要があります。 この状態は、 _Enable_が0x00 に設定された HCI_VS_MSFT_LE_Set_Advertisement_Filter_Enable コマンドを以前に受信したコントローラーに相当します。
コントローラーは、このコマンドに応答して、コマンドの完了イベントを即座に生成する必要があります。

#### <a name="command_parameters"></a>Command_parameters

Subcommand_opcode (1 オクテット):

| Value  |  パラメーターの説明 |
|---|---|
|0x05|  HCI_VS_MSFT_LE_Set_Advertisement_Filter_Enable のサブコマンドオペコード。|

有効 (1 オクテット):

| Value  |  パラメーターの説明 |
|---|---|
|0x00| 現在のホワイトリストの動作に戻しますが、 [HCI_VS_MSFT_LE_Monitor_Advertisement](#hci_vs_msft_le_monitor_advertisement)コマンドからのデバイスの監視を続行します。|
|0x01|コントローラーで発行されたすべての HCI_VS_MSFT_LE_Monitor_Advertisement コマンドを有効にします。|

#### <a name="return_parameter"></a>Return_parameter

状態 (1 オクテット):

|Value|パラメーターの説明|
|---|---|
|0x00|コマンドが正常に実行されました。|
|0x0C|コントローラーがコマンドを拒否した場合、コントローラーは許可されていない_コマンド_を返します。これは、 _Enable_がこのコマンドと同じ値に設定された HCI_VS_MSFT_LE_Set_Advertisement_Filter_Enable コマンドを以前に確認したためです。|
|エラー&#160;コード|コマンドが失敗しました。 詳細については、「Bluetooth Core の仕様」の「_エラーコード_」を参照してください。|

Subcommand_opcode (1 オクテット):

|Value|パラメーターの説明|
|---|---|
|0x05|HCI_VS_MSFT_LE_Set_Advertisement_Filter_Enable のサブコマンドオペコード。|

#### <a name="events_generated__unless_masked_away"></a>Events_generated__unless_masked_away

HCI_VS_MSFT_LE_Set_Advertisement_Filter_Enable コマンドを受信すると、コントローラーはコマンド完了イベントを生成する必要があります。

#### <a name="hci_vs_msft_read_absolute_rssi"></a>HCI_VS_MSFT_Read_Absolute_RSSI

HCI_VS_MSFT_Read_Absolute_RSSI は、コントローラーからの BR/EDR 接続について、受信した信号強度 (RSSI) の**絶対**値を読み取ります。

|コマンド|コード|コマンドパラメーター|戻りパラメーター|
|---|---|---|---|
|HCI_VS_MSFT_Read_Absolute_RSSI|選択された基本コード |<ul><li>Subcommand_opcode</li><li>ハンドル</li>|<ul><li>状況</li><li>Subcommand_opcode</li><li>ハンドル</li><li>RSSI</li></ul>|

接続ハンドルは、RSSI が読み取られている ACL 接続を識別するために、コマンドと戻りパラメーターの両方として提供されます。 RSSI メトリックは、dBm と± 6 dB 精度の**絶対**レシーバー信号強度です。 RSSI を読み取ることができない場合は、RSSI メトリックを127に設定する必要があります。
コントローラーは、コマンド完了イベントを使用して、常にこのコマンドを実行する必要があります。

#### <a name="command_parameters"></a>Command_parameters

Subcommand_opcode (1 オクテット):

| Value  |  パラメーターの説明 |
|---|---|
|0x06|  HCI_VS_MSFT_Read_Absolute_RSSI のサブコマンドオペコード。|

ハンドル (2 オクテット):

| Value  |  パラメーターの説明 |
|---|---|
|0x_XXXX_|RSSI を読み取る必要がある BR/EDR 接続のハンドル。|

#### <a name="return_parameters"></a>Return_parameters

状態 (1 オクテット):

|Value|パラメーターの説明|
|---|---|
|0x00|コマンドが正常に実行されました。|
|0x01-0xFF|コマンドが失敗しました。 詳細については、「Bluetooth Core の仕様」の「_エラーコード_」を参照してください。|

Subcommand_opcode (1 オクテット):

|Value|パラメーターの説明|
|---|---|
|0x06|HCI_VS_MSFT_Read_Absolute_RSSI のサブコマンドオペコード。|

ハンドル (2 オクテット):

|Value|パラメーターの説明|
|---|---|
|0xXXXX| RSSI が読み取られた BR/EDR 接続のハンドル。|

RSSI (1 オクテット):

|     Value      |                                                  パラメーターの説明                                                   |
|----------------|--------------------------------------------------------------------------------------------------------------------------|
| N = RSSI 値 | BR/EDR 接続の RSSI 値。<ul><li>範囲:-128 &lt; =  N&lt;= 127 (符号付き整数)</li><li>Unit: dBm</li> |

#### <a name="events_generated__unless_masked_away"></a>Events_generated__unless_masked_away

HCI_VS_MSFT_Read_Absolute_RSSI コマンドが完了すると、コントローラーはコマンド完了イベントを生成する必要があります。

## <a name="microsoft-defined-bluetooth-hci-events"></a>Microsoft が定義した Bluetooth HCI イベント

Microsoft が定義したすべての Bluetooth HCI イベントは、ベンダー定義のイベントで、イベントコード0xFF を使用します。 Microsoft イベントのイベントデータは、他のベンダー定義イベントと Microsoft 定義のイベントを区別するために、常に一定のバイトの文字列で開始されます。 定数文字列の長さと値は、コントローラーの実装者によって定義され、 [HCI_VS_MSFT_Read_Supported_Features](#hci_vs_msft_read_supported_features)への応答として返されます。

|HCI イベント|説明|
|---|---|
|[HCI_VS_MSFT_Rssi_Event](#hci_vs_msft_rssi_event)|HCI_VS_MSFT_RSSI_Event は、 [HCI_VS_MSFT_Monitor_Rssi](#hci_vs_msft_monitor_rssi)コマンドが完了したことを示します。|
|[HCI_VS_MSFT_LE_Monitor_Device_Event](#hci_vs_msft_le_monitor_device_event)|HCI_VS_MSFT_LE_Monitor_Device_Event は、コントローラーが Bluetooth LE デバイスの監視を開始または停止したことを示します。|

### <a name="hci_vs_msft_rssi_event"></a>HCI_VS_MSFT_RSSI_Event

HCI_VS_MSFT_RSSI_Event は、 [HCI_VS_MSFT_Monitor_Rssi](#hci_vs_msft_monitor_rssi)コマンドが完了したことを示します。
_Status_パラメーターが0の場合、リモートデバイスの RSSI 値が指定された範囲外の値に変更されたため、コマンドが完了します。 _Status_パラメーターが0以外の場合、接続の RSSI 値を監視できなくなったため、コマンドは完了しました。

|イベント|イベントコード|Microsoft イベントコード|イベントパラメーター|
|---|---|---|---|
|HCI_VS_MSFT_RSSI_Event|0xFF|0x01|<p>Event_prefix</p><p>Microsoft_event_code</p><p>状況</p><p>Connection_handle</p><p>RSSI</p>

#### <a name="event_parameters"></a>Event_parameters

Event_prefix (可変サイズ):

|Value|パラメーターの説明|
|---|---|
|イベントプレフィックス|このイベントに Microsoft 定義としてフラグを設定するイベントプレフィックス。 サイズと値は、 [HCI_VS_MSFT_Read_Supported_Features](#hci_vs_msft_read_supported_features)コマンドによって返されます。|

Microsoft_event_code (1 オクテット):

|Value|パラメーターの説明|
|---|---|
|0x01|HCI_VS_MSFT_RSSI_Event のイベントコード。|

状態 (1 オクテット):

|Value|パラメーターの説明|
|---|---|
|0x00|成功。 接続の RSSI 値が次のいずれかの条件を満たしています。<ul><li>RSSI が_RSSI_threshold_high_に達したか、それを超えました。</li><li>RSSI が_RSSI_threshold_low_time_interval_秒を超えて_RSSI_threshold_low_より下に達したか、削除されました。</li><li>_RSSI_sampling_period_の有効期限が切れました。このイベントは、RSSI の値をホストに通知するために生成されました。</li></ul>|
|0x01&#160;-&#160;0xFF|不具合. 接続の RSSI 値を監視できなくなりました。 エラーコードは、通常、基になる ACL 接続が失われた理由を示すコードの1つです。|

Connection_handle (2 オクテット):

|Value|パラメーターの説明|
|---|---|
|0x_XXXX_|RSSI を監視する接続のハンドル。|

RSSI (1 オクテット):

|Value|パラメーターの説明|
|---|---|
|N = _RSSI&#160;値_|接続の測定されたリンク RSSI 値。 BR/EDR の場合:<ul><li>範囲:-128 &lt; =  N&lt;= 127 (符号付き整数)</li><li>Unit: dBm</li></ul>LE の場合:<ul><li>範囲:-127 ~ 20 (符号付き整数)</li><li>Unit: dBm</li></ul>|

### <a name="hci_vs_msft_le_monitor_device_event"></a>HCI_VS_MSFT_LE_Monitor_Device_Event

HCI_VS_MSFT_LE_Monitor_Device_Event は、コントローラーが Bluetooth LE デバイスの監視を開始または停止したことを示します。

_Monitor_state_パラメーターの値が1の場合、コントローラーは、指定された BD_ADDR を使用して Bluetooth デバイスの監視を開始します。 _Monitor_state_パラメーターの値が0の場合、コントローラーは、指定された BD_ADDR で Bluetooth デバイスの監視を停止します。

|イベント|イベントコード|Microsoft イベントコード|イベントパラメーター|
|---|---|---|---|
|HCI_VS_MSFT_LE_Monitor_Device_Event|0xFF|0x02|<p>Event_prefix</p><p>Microsoft_event_code</p><p>Address_type</p><p>BD_ADDR</p><p>Monitor_handle</p><p>Monitor_state</p>

_Monitor_state_が1に設定されている HCI_VS_MSFT_LE_Monitor_Device_Event がまだ生成されていない場合、コントローラーは_Monitor_state_パラメーターを0に設定して HCI_VS_MSFT_LE_Monitor_Device_Event を生成しません。

#### <a name="event_parameters"></a>Event_parameters

Event_prefix (可変サイズ):

|Value|パラメーターの説明|
|---|---|
|イベントプレフィックス|このイベントに Microsoft 定義としてフラグを設定するイベントプレフィックス。 サイズと値は、 [HCI_VS_MSFT_Read_Supported_Features](#hci_vs_msft_read_supported_features)コマンドによって返されます。

Microsoft_event_code (1 オクテット):

|Value|パラメーターの説明|
|---|---|
|0x02|HCI_VS_MSFT_LE_Monitor_Device_Event のイベントコード。|

Address_type (1 オクテット):

|Value|パラメーターの説明|
|---|---|
|0x00|パブリックデバイスアドレス。|
|0x01|ランダムデバイスアドレス。|
|0x02&#160;-&#160;0xFF|将来使用するために予約された値。|

BD_ADDR (6 オクテット):

|Value|パラメーターの説明|
|---|---|
|0x_XXXXXXXXXXXX_|デバイスの Bluetooth アドレス。|

Monitor_handle (1 オクテット):

|Value|パラメーターの説明|
|---|---|
|0Xxx_|[HCI_VS_MSFT_LE_Monitor_Advertisement](#hci_vs_msft_le_monitor_advertisement)コマンドに対して指定されたフィルターへのハンドル。|

Monitor_state (1 オクテット):

|Value|パラメーターの説明|
|---|---|
|0x00|コントローラーは、 _BD_ADDR_および_Monitor_handle_によって指定されたデバイスの監視を停止しました。|
|0x01|コントローラーは、 _BD_ADDR_および_Monitor_handle_によって指定されたデバイスの監視を開始しました。|
