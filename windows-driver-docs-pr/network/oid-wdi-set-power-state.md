---
title: OID_WDI_SET_POWER_STATE
description: OID_WDI_SET_POWER_STATE では、デバイスの電源の状態を設定します。
ms.assetid: f1453ace-5e36-464e-96f0-e578890cdf3f
ms.date: 07/18/2017
keywords:
- OID_WDI_SET_POWER_STATE ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 982326f8e938b8549b395365997e22f29d54f4c9
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56532466"
---
# <a name="oidwdisetpowerstate"></a>OID\_WDI\_設定\_POWER\_状態


OID\_WDI\_設定\_POWER\_状態は、デバイスの電源状態を設定します。

| Scope   | タスクでシリアル化された設定します。 | 通常の実行時間 (秒) |
|---------|--------------------------|---------------------------------|
| アダプタ | 〇                      | 10                              |

 

NIC は、D0 で (デバイスの電源を完全に)、システムの起動時またはシステムへ NIC が接続されたとき。 条件が適切な場合 (AOAC プラットフォームでは、これは NIC アクティブな参照が NIC での 0 の場合)、オペレーティング システムを準備および D0 に NIC を格納します。 ユーザーが存在しない場合は、ホストは、電力を節約する低電力状態に移動します。 ホストは、NIC が自律的に、ホストの接続を維持できる低電力状態に NIC を設定することがあります。 NIC は、外部イベントを表すホストに関心ホストによって起動します。

OID\_WDI\_設定\_POWER\_D0、D1、d2 に切り替わり、および D3 に状態が、デバイスを設定します。 D の状態は、デバイス クラスとプラットフォーム固有です。 Wi-fi の NIC には、通常の状態のサブセットのみがサポートされています。 たとえば、SD バス上のデバイスを Wi-fi、サポートされているセットが D0、d2 に切り替わり、D3 で構成されます。 D2 や D3 の意味を特定のデバイスも同様です。 SDIO バス上の Wi-fi NIC、D2 からの復帰できるように定義されているが、D3 の NIC は停止されます。

PCIe バス NIC は、D0 と D3、D3Hot または D3Cold D3 を使用できる場所をサポートします。 ホスト ソフトウェア スタックには、D3 のみです。 D3hot または D3Cold は、ホストのシナリオと基になるプラットフォームのサポートに依存します。 コネクテッド スタンバイのシナリオではなどでホストがウェイク イベント、NIC にオフロードし、プラットフォームをサポートできるように、ホストの外部イベントの NIC を確認できますを利用した NIC を保持する D3hot は D3 に NIC を設定します。 休止状態のシナリオでは、ホストは、D3 に NIC を設定し、プラットフォームは、NIC は、電力を使用しないように、NIC に電源をオフにします。

休止状態をサポートする AOAC システムの場合、次は、重要なシステム電源の状態の概要を示します。 AOAC システムでは、システムのスリープ状態は、接続されたスタンバイ状態です。 これは、状態の省電力 (SDBus Nic の D2、PCIe Nic の D3) に Nic が設定される場所であり、スリープ解除を入手できます。 ハード ドライブにドライバーが中断されている場合、ドライバーは、もう一度再初期化を通過しません、ファームウェアの状態を再開するドライバーの責任は (たとえば、DriverEntry は呼び出されません)。

<table>
<colgroup>
<col width="20%" />
<col width="20%" />
<col width="20%" />
<col width="20%" />
<col width="20%" />
</colgroup>
<thead>
<tr class="header">
<th></th>
<th>スリープ</th>
<th>休止状態</th>
<th>ハイブリッドのシャット ダウン</th>
<th>完全にシャット ダウン</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>によって要求します。</td>
<td><p>[電源] ボタン (既定値)</p></td>
<td><p>shutdown /h</p></td>
<td><p>shutdown /s /hybrid</p></td>
<td><p>shutdown /s</p></td>
</tr>
<tr class="even">
<td>UI</td>
<td><p><strong>開始</strong> &gt; <strong>Power</strong> &gt; <strong>スリープ</strong></p></td>
<td><p>--</p></td>
<td><p><strong>開始</strong> &gt; <strong>Power</strong> &gt; <strong>シャット ダウン</strong></p></td>
<td><p>--</p></td>
</tr>
<tr class="odd">
<td>システム状態</td>
<td><p>コネクト スタンバイ</p></td>
<td><p>休止状態</p></td>
<td><p>ハイブリッドのシャット ダウン</p></td>
<td><p>電源オフ</p></td>
</tr>
<tr class="even">
<td>ドライバーの状態</td>
<td><p>有効 - 腕スリープ解除するには</p></td>
<td><p>ハード ドライブに中断します。</p></td>
<td><p>ハード ドライブに中断します。</p></td>
<td><p>電源オフ</p></td>
</tr>
</tbody>
</table>

 

AOAC システムを休止状態またはされていないために必要なサポート、ドライバーの電源状態の概要を示します。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th></th>
<th>スリープ</th>
<th>完全にシャット ダウン</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>によって要求します。</td>
<td><p>[電源] ボタン (既定値)</p></td>
<td><p>shutdown /s</p></td>
</tr>
<tr class="even">
<td>UI</td>
<td><p><strong>開始</strong> &gt; <strong>Power</strong> &gt; <strong>スリープ</strong></p></td>
<td><p><strong>開始</strong> &gt; <strong>Power</strong> &gt; <strong>シャット ダウン</strong></p></td>
</tr>
<tr class="odd">
<td>システム状態</td>
<td><p>コネクト スタンバイ</p></td>
<td><p>電源オフ</p></td>
</tr>
<tr class="even">
<td>ドライバーの状態</td>
<td><p>有効 - 腕スリープ解除するには</p></td>
<td><p>電源オフ</p></td>
</tr>
</tbody>
</table>

 

電源の set コマンドが失敗することはできません。 ファームウェアでは、このようなコマンドが失敗しない必要があります。 Microsoft コンポーネントによりがない未処理タスクまたはコマンドの set power コマンドを送信するとき。 セット power コマンドは、卓越したが、中に、Microsoft コンポーネントは、その他のコマンドやタスクには送信されません IHV コンポーネントも保証されます。

| 電源の状態                                            | 説明                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                |
|--------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| D0 (完全に利用)                                     | NIC が完全に供給され、コマンドを受信する準備ができて、します。 ホストは、決して低電力状態の間の変更を要求します。 たとえば、D3 に D2 からの NIC の電源状態を設定する場合、ホストは、最初設定電源の状態 D0、してから、D3 に。                                                                                                                                                                                                                                                            |
| D2 wake (SDBus Nic) の活用と                     | D2 に切り替わりで、ホストは決して設定 D0 コマンド以外のファームウェアに要求を送信します。 関連するフローのグラフは、このトピックで以降のセクションを参照してください。                                                                                                                                                                                                                                                                                                                                                                 |
| : D3 の電源をオフ (SDBus Nic)、ウェイク アップ (PCIe Nic) の有効活用 | SDBus nic の場合は、この状態を電源オフします。 PCIe バス Nic では、オペレーティング システムのスリープ状態の解除 (D3Hot) の Nic を arm 可能性があります。 または (D3Cold) の電源をオフにすることがあります。 ドライバー スタックの観点からは D3 状態のみに注意してください。 複数のコンポーネントが関連して D3Hot 状態は、ACPI テーブル、システム電源の NDIS エンドユーザーの作為または不作為、休止状態、接続の Standby、およびハイブリッドなどに応じて、オペレーティング システムから取得した Irp の処理などを有効にするにはシャット ダウンします。 |
| 既定以外のポートの Dx                               | Dx は D2 または D3 のいずれかです。 NIC は、既定以外のすべてのポートがリセット Dx に入れられます、Dx で既定以外のすべてのポートが切断されているを意味します。                                                                                                                                                                                                                                                                                                                                                              |

 

## <a name="set-property-parameters"></a>プロパティ パラメーターの設定


<table>
<colgroup>
<col width="25%" />
<col width="25%" />
<col width="25%" />
<col width="25%" />
</colgroup>
<thead>
<tr class="header">
<th>TLV</th>
<th>許可されている複数の TLV インスタンス</th>
<th>省略可能</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/dn898040" data-raw-source="[&lt;strong&gt;WDI_TLV_POWER_STATE&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/dn898040)"><strong>WDI_TLV_POWER_STATE</strong></a></p></td>
<td></td>
<td></td>
<td><p>電源の状態。 これは、プライマリのポートに適用されます。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/dn926303" data-raw-source="[&lt;strong&gt;WDI_TLV_ENABLE_WAKE_EVENTS&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/dn926303)"><strong>WDI_TLV_ENABLE_WAKE_EVENTS</strong></a></p></td>
<td></td>
<td>X</td>
<td><p>このフィールドは可能性があります、NIC が省電力に配置されていると (SD IO で D2) などの指定したイベントのいずれかのスリープ解除されている場合にのみ表示されます。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/dn898060" data-raw-source="[&lt;strong&gt;WDI_TLV_SET_POWER_DX_REASON&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/dn898060)"><strong>WDI_TLV_SET_POWER_DX_REASON</strong></a></p></td>
<td></td>
<td>X</td>
<td><p>セットの電力理由です。</p></td>
</tr>
</tbody>
</table>

 

## <a name="set-property-results"></a>セットのプロパティの結果


| TLV                                                                                 | 許可されている複数の TLV インスタンス | 省略可能 | 説明                                                                                                                                                                                                                                                                                                                                               |
|-------------------------------------------------------------------------------------|--------------------------------|----------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| [**WDI\_TLV\_アダプター\_再開\_必要な作業**](https://msdn.microsoft.com/library/windows/hardware/dn926120) |                                | X        | 値が true の場合に通知、OS のファームウェアがそのコンテキストの再開中にアシスタンスを必要があること。 ストレージに、ドライバーが中断されている場合にのみ発生する必要があります。 IHV コンポーネントは、オペレーティング システムは、一連のファームウェア コンテキストおよび IHV コンポーネント コンテキストの最新の状態を表示する Wi-fi のコマンドを発行するため、ソフトウェアの状態をリセットする必要があります。 |

 

## <a name="enable-wake-events"></a>ウェイク イベントを有効にします。


NIC には、スタックをスリープ解除することを検出するイベントのセットを指定します。 サブセットまたは低電力のコマンドを使用して NIC にイベントの完全なセットをオペレーティング システムが組み込まれます。 ウェイク イベントのいくつかのパラメーターは、Dx コマンドよりもかなり以前に設定されます。 Dx コマンドの前に、ファームウェアに他のユーザー設定されます。 すべてのイベントは、Dx コマンドでのみ有効になります。

このインターフェイスでは、ダウンが有効に設定されているイベントを追加、省略可能な[ **WDI\_TLV\_を有効にする\_WAKE\_イベント**](https://msdn.microsoft.com/library/windows/hardware/dn926303) TLV の一部として、OID\_WDI\_設定\_Dx デバイスの電源状態の電源コマンド。 TLV がない場合、オペレーティング システムがスリープ解除する NIC を arm しない場合。

ファームウェアが持つ Dx コマンドを受信すると[ **WDI\_TLV\_を有効にする\_WAKE\_イベント**](https://msdn.microsoft.com/library/windows/hardware/dn926303)、検出、Dx を完了する前に、ウェイク イベントコマンド。 イベントのバッファー、コマンドの処理が完了、およびウェイク割り込みをアサートする必要があります。

NIC がスタックを解除する理由のウェイク アップの理由で、Wi-fi NIC によって各ウェイクに従ってください。 NIC は、アサートすることは通常、バスや ACPI メソッドによって処理されますが、ウェイク アップ割り込み行で、スタックを解除します。 メソッドは、ウェイク イベントを処理するには、CPU と必要なコンポーネントをスリープ解除し、Wi-fi 待機 Wake IRP スタックを完了します。 その後、オペレーティング システムでは、ドライバーとファームウェアを D0 要求を発行します。 この要求は、ドライバー、ファームウェアに D0 コマンドを送信するには、電源 OID です。 ファームウェアは、受け取って D0 コマンドが完了するまでに、ウェイク アップの理由を示す値を保持します。

**注**  NIC が何らかの理由で D0 コマンドを受信するかどうか (たとえば、NIC が解除されないホスト)、NIC がウェイク アップの理由を示していません。

 

## <a name="no-enabled-wake-events"></a>有効なウェイク イベントがありません。


存在する場合ありません[ **WDI\_TLV\_を有効にする\_WAKE\_イベント**](https://msdn.microsoft.com/library/windows/hardware/dn926303)存在する場合は、オペレーティング システムでは、省電力で実行するために Nic は必要はありません。 Nic が完全に電源がオフです。 ハード ドライブに中断されている場合は、ファームウェアのコンテキストで再開を再開する Nic ドライバーが必要です。

## <a name="power-state-interaction-and-transition-examples"></a>電源状態の相互作用と移行の例


次の図は、NIC の相互作用と D0 および Dx (D2 または D3) 間の遷移のシーケンスを表示します。 このコンテキストでは、「ミニポート」は、ホストまたは WDI に準拠したドライバーを表します。

### <a name="d0-to-dx-armed-to-wake"></a>Dx (wake を入手できます) に D0

![wdi d0 武装 dx 移行する](images/wdi-d0-to-dx-armed-to-wake.png)

-   停止\[DnIO |UpIO\]:DnIO は、下位層へのメッセージ (コントロールとデータ) です。 UpIO は、上位層へのメッセージです。

    -   レイヤー (高速では失敗します)、上記の新しい要求を拒否します。
    -   (この Dx コマンド) を除く、このレイヤーからの IO の開始を停止します。
    -   Dx に TXs を挿入する下位の層を使用できます。
    -   キューをフラッシュします。
-   AwaitInflight:進行中の DMA を含む戻るには、IO の呼び出しを待機しています。 キューをフラッシュします。

-   Dx は、任意の非 D0 状態です。 SDBus Wi-fi の D2 になります。 PCIe バスでは、これは D3Hot です。 ファームウェアは電源が失われないものとします。

### <a name="dx-armed-to-wake-to-d0-transition"></a>Dx (wake を入手できます) D0 移行する

![dx d0 遷移を入手できます。](images/wdi-dx-to-d0-armed-to-wake.png)

-   NIC はスリープ状態を解除すれば、D3Cold ことができません。 ファームウェアでは、Dx で実行を継続する必要があります。

### <a name="d0-to-d3-not-armed-to-wake-transition"></a>D0 D3 (スリープ解除するは取得されません) の移行

![d0 いない武装 d3 の移行](images/wdi-d0-to-d3-not-armed.png)

-   停止\[DnIO |UpIO\]:DnIO は、下位層へのメッセージ (コントロールとデータ) です。 UpIO は、上位層へのメッセージです。

    -   レイヤー (高速では失敗します)、上記の新しい要求を拒否します。
    -   (この Dx コマンド) を除く、このレイヤーからの IO の開始を停止します。
    -   Dx に TXs を挿入する下位の層を使用できます。
    -   キューをフラッシュします。
-   AwaitInflight:進行中の DMA を含む戻るには、IO の呼び出しを待機しています。 キューをフラッシュします。

-   D3 PmParameters なし。 NIC (D3Cold) は、電源オフ (たとえば、D0 デバイスと共有 power レール) 可能性がありますはありません。

### <a name="dx-not-armed-to-wake-to-d0-transition"></a>Dx (スリープ状態を解除しない武装) D0 移行する

![dx d0 遷移を入手できません。](images/wdi-dx-to-d0-not-armed.png)

-   D2 notArmToWake:保持している電力は、再初期化が必要ありません。
-   D3 notArmtoWake:ホット場合がありますまたはコールドします。 コールドは、そのコンテキストを復元する必要があります。

<a name="requirements"></a>要件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>サポートされている最小のクライアント</p></td>
<td><p>Windows 10</p></td>
</tr>
<tr class="even">
<td><p>サポートされている最小のサーバー</p></td>
<td><p>Windows Server 2016</p></td>
</tr>
<tr class="odd">
<td><p>Header</p></td>
<td>Dot11wdi.h</td>
</tr>
</tbody>
</table>

 

 




