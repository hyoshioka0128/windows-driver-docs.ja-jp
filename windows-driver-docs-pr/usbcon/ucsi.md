---
Description: Microsoft では、USB Type-C コネクタ システム ソフトウェア インターフェイス (UCSI) 仕様に準拠したドライバーを提供しています。
title: USB Type-C Connector System Software Interface (UCSI) ドライバー
ms.date: 04/20/2017
ms.localizationpriority: High
ms.openlocfilehash: d2301377daf1057a90220785404b459182499f86
ms.sourcegitcommit: 1d531bf9d02653fdf9ad728126d68b8acb86182e
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/29/2020
ms.locfileid: "87402271"
---
# <a name="usb-type-c-connector-system-software-interface-ucsi-driver"></a>USB Type-C Connector System Software Interface (UCSI) ドライバー


**要約**

-   Microsoft が提供する、組み込みコントローラーを備えた USB Type-C システム用のインボックス UCSI ドライバー。

**最終更新日**

-   2018 年 10 月

**Windows バージョン**

-   Windows 10 デスクトップ エディション (Home、Pro、Enterprise、Education)
-   Windows 10 Mobile

**公式の仕様**

-   [Intel BIOS Implementation of UCSI](https://go.microsoft.com/fwlink/p/?LinkId=760658)
-   [USB Type-C Connector System Software Interface Specification](https://go.microsoft.com/fwlink/p/?LinkId=703713)
-   [ハードウェアの設計:埋め込みコントローラーを備えたシステム用 USB Type-C コンポーネント](hardware-design-of-a-usb-type-c-system.md#emb)


Microsoft では、ACPI トランスポート用の USB Type-C コネクタ システム ソフトウェア インターフェイス (UCSI) 仕様に準拠したドライバーを提供しています。 設計に ACPI トランスポートがある組み込みのコントローラーが含まれている場合は、システムの BIOS/EC に UCSI を実装し、インボックス UCSI ドライバー (UcmUcsiCx.sys および UcmUcsiAcpiClient.sys) を読み込みます。

UCSI 準拠のハードウェアが ACPI 以外のトランスポートを使用している場合は、[UCSI クライアント ドライバー](write-a-ucsi-driver.md)を作成する必要があります。

## <a name="drivers-for-supporting-usb-type-c-components-for-systems-with-embedded-controllers"></a>埋め込みコントローラーを備えたシステム用 USB Type-C コンポーネントをサポートするためのドライバー

埋め込みコントローラーを備えたシステムの例を次に示します。

![USB Type-C ソフトウェア コンポーネント](images/ucsiarch.png)

上記の例では、USB ロール スイッチはシステムのファームウェアで処理され、USB Role Switch ドライバー スタックは読み込まれていません。 別のシステムでは、デュアル ロールがサポートされていないため、ドライバー スタックが読み込まれない可能性があります。

上の図において、

-   **USB デバイス側ドライバー**

    [USB デバイス側ドライバー](usb-device-side-drivers-in-windows.md)は、機能、デバイス、周辺機器に対応します。 USB 関数コントローラーのクラス拡張機能は、MTP (メディア転送プロトコル)、および BC 1.2 充電器を使用した充電に対応しています。 Microsoft では、Synopsys USB 3.0 および ChipIdea USB 2.0 コントローラー用のインボックス クライアント ドライバーが提供されています。 [USB 関数コントローラー クライアント ドライバーのプログラミング インターフェイス](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/mt188010(v=vs.85))を使用して、関数コントローラー用のカスタム クライアント ドライバーを作成できます。 詳細については、[USB 関数コントローラー用 Windows ドライバーの開発](developing-windows-drivers-for-usb-function-controllers.md)に関する記事を参照してください。

    SoC ベンダーは、充電器検出用の USB 関数の下位フィルター ドライバーを提供している場合があります。 インボックス Synopsys USB 3.0 または ChipIdea USB 2.0 クライアント ドライバーを使用している場合は、独自のフィルター ドライバーを実装できます。

-   **USB ホスト側ドライバー**

    USB ホスト側ドライバーは、EHCI または XHCI 準拠の USB ホスト コントローラーで動作する一連のドライバーです。 ドライバーは、ロール スイッチ ドライバーがホストのロールを列挙した場合に読み込まれます。 ホスト コントローラーが仕様に準拠していない場合は、[USB ホスト コントローラー 拡張 (UCX) プログラミング インターフェイス](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/mt188009(v=vs.85))を使用して、カスタム ドライバーを作成できます。 詳細については、[USB ホスト コントローラー用 Windows ドライバーの開発](developing-windows-drivers-for-usb-host-controllers.md)に関する記事を参照してください。

    **注**  [すべての USB デバイス クラス](supported-usb-classes.md)が Windows 10 Mobile でサポートされているわけではありません。

     

-   **USB コネクタ マネージャー**

    Microsoft では、[USB Type-C コネクタ システム ソフトウェア インターフェイス仕様](https://go.microsoft.com/fwlink/p/?LinkId=703713)で定義されている機能を実装する Windows (UcmUcsiCx.sys) を備えた UCSI インボックス ドライバーを提供しています。 この仕様では、UCSI の機能、およびハードウェア コンポーネント デザイナー、システム ビルダー、およびデバイス ドライバーの開発者向けにレジスタとデータ構造について説明します。

    このドライバーは、埋め込みコントローラーを備えたシステムを対象としています。 このドライバーは、Microsoft が提供する USB コネクタ マネージャーのクラス拡張機能ドライバー (Ucmcx.sys) のクライアントです。 ドライバーでは、ファームウェアへの要求を開始してデータまたは電源ロールを変更し、ユーザーにトラブルシューティング メッセージを提供するために必要な情報を取得するなどのタスクが処理されます。

## <a name="ucsi-commands-required-by-windows"></a>Windows で必要な UCSI コマンド


すべての UCSI 実装で "Required" (必須) になっているコマンドについては、UCSI の仕様を参照してください。

"Required" とマークされているコマンドの他に、Windows では次のコマンドが必須です。

-   GET\_ALTERNATE\_MODES
-   GET\_CAM\_SUPPORTED
-   GET\_PDOS
-   SET\_NOTIFICATION\_ENABLE:システムまたはコントローラーでは、SET\_NOTIFICATION\_ENABLE の次の通知がサポートされている必要があります。
    -   Supported Provider Capabilities Change (サポートされているプロバイダー機能の変更)
    -   Negotiated Power Level Change (ネゴシエートされる電源レベルの変更)
-   GET\_CONNECTOR\_STATUS:システムまたはコントローラーでは、GET\_CONNECTOR\_STATUS のコネクタの状態の変更がサポートされている必要があります。
    -   Supported Provider Capabilities Change (サポートされているプロバイダー機能の変更)
    -   Negotiated Power Level Change (ネゴシエートされる電源レベルの変更)

BIOS で UCSI を実装するために必要なタスクの詳細については、「[Intel BIOS Implementation of UCSI](https://go.microsoft.com/fwlink/p/?LinkId=760658)」を参照してください。

## <a name="example-flow-for-ucsi"></a>UCSI のフローの例


このセクションで示す例では、USB Type-C ハードウェアまたはファームウェア、UCSI ドライバー、およびオペレーティング システム間の相互作用について説明します。

### <a name="drp-role-detection"></a>DRP ロールの検出

1.  USB Type-C ハードウェアまたはファームウェアでデバイス アタッチ イベントが検出され、最初に Windows 10 システムの DRP システムが UFP ロールになります。
    1.  ファームウェアで、コネクタが変更されたことを示す通知が送信されます。
    2.  UCSI ドライバーにより、GET\_CONNECTOR\_STATUS 要求が送信されます。
    3.  ファームウェアによって、Connect Status = 1 および Connector Partner Type = DFP という応答が返されます。 
2.  USB 関数スタック内のドライバーが、列挙に応答します。
3.  USB コネクタ マネージャーのクラス拡張機能で、USB 関数スタックが読み込まれたことによりシステムの状態が正しくないことが認識されます。 これは、Set USB Operation Role 要求および Set Power Direction Role 要求をファームウェアに送信するように UCSI ドライバーに指示します。
4.  USB Type-C ハードウェアまたはファームウェアで、DFP を使用してロールスワップ操作が開始されます。

### <a name="detecting-a-charger-mismatch-error-condition"></a><a name="detecting-a-charger-mismatch-error--condition"></a>充電器の不一致エラー条件の検出

1.  USB Type-C ハードウェアまたはファームウェアで充電器が接続されていることが検出され、既定の電源コントラクトのネゴシエーションが開始されます。 また、充電器からシステムに十分な電力が供給されていないことが確認されます。
2.  USB Type-C ハードウェアまたはファームウェアにより、低速充電されている部分が設定されます。
    1.  ファームウェアで、コネクタが変更されたことを示す通知が送信されます。
    2.  UCSI ドライバーにより、GET\_CONNECTOR\_STATUS 要求が送信されます。
    3.  ファームウェアによって、Connect Status = 1、Connector Partner Type = DFP、および Battery Charging Status = Slow/Trickle という応答が返されます。
    
3.  充電器の不一致のトラブルシューティング メッセージを表示するため、USB コネクタ マネージャーのクラス拡張機能によって UI に通知が送信されます。

## <a name="how-to-test-ucsi"></a>UCSI のテスト方法


UCSI 実装をテストするには、いくつかの方法があります。 UCSI BIOS/EC 実装で個々のコマンドをテストするには、[MUTT Software Pack](mutt-software-package.md) で提供されている UCSIControl.exe を使用します。 完全な UCSI の実装をテストするには、Windows Hardware Lab Kit (HLK) に含まれている UCSI テストと、[Type-C の手動での相互運用機能の手順](https://docs.microsoft.com/windows-hardware/drivers/usbcon/)に関する記事に記載されている手順を使用します。

**UCSIControl.exe**

UCSIControl.exe を使用して、UCSI BIOS/EC 実装で個々のコマンドをテストできます。 このツールを使用すると、UCSI ドライバーを使用して、UCSI コマンドをファームウェアに送信できます。 ドライバーが読み込まれて実行されていること、およびドライバーのテスト インターフェイスが有効になっていることが必要です。 このインターフェイスはリテール システムの承認されていないユーザーがアクセスできないよう、既定では有効になっていません。

1.  **UCSI USB コネクタ マネージャー**という名前のデバイス マネージャー (devmgmt.msc) でデバイス ノードを見つけます。 ノードは **[ユニバーサル シリアル バス コントローラー]** カテゴリにあります。
2.  デバイスを右クリックし、 **[プロパティ]** を選択して、 **[詳細]** タブを開きます。
3.  ドロップダウンから **[デバイス インスタンス パス]** を選択し、プロパティの値を書き留めます。
4.  レジストリ エディター (regedit.exe) を開きます。
5.  このキーの配下にあるデバイス インスタンス パスに移動します。

    HKEY\_LOCAL\_MACHINE\\System\\CurrentControlSet\\Enum\\&lt;device-instance-path&gt;\\Device Parameters

6.  **TestInterfaceEnabled** という名前の DWORD 値を作成し、値を 0x1 に設定します。
7.  デバイス マネージャーのデバイス ノードで **[無効]** オプションを選択してから **[有効]** 選択し、デバイスを再起動します。 または、単に PC を再起動することもできます。

ヘルプを表示するには、**UcsiControl.exe /?** を実行します。

一般的なコマンドを次に示します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>UCSI コマンド</th>
<th>UcsiControl.exe コマンド</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>PPM Reset</td>
<td><strong>UcsiControl.exe Send 0 1</strong></td>
</tr>
<tr class="even">
<td>Connector Reset</td>
<td><p>ソフト リセット:<strong>UcsiControl.exe Send 0 10003</strong></p>
<p>ハード リセット:<strong>UcsiControl.exe Send 0 810003</strong></p></td>
</tr>
<tr class="odd">
<td>Set Notification Enable</td>
<td><p>すべての通知:<strong>UcsiControl.exe Send 0 ffff0005</strong></p>
<p>コマンドの完了のみ:<strong>UcsiControl.exe Send 0 00010005</strong></p>
<p>通知なし:<strong>UcsiControl.exe Send 0 00000005</strong></p></td>
</tr>
<tr class="even">
<td>Get Capability</td>
<td><strong>UcsiControl.exe Send 0 6</strong></td>
</tr>
<tr class="odd">
<td>Get Connector Capability</td>
<td><strong>UcsiControl.exe Send 0 10007</strong></td>
</tr>
<tr class="even">
<td>Set UOM</td>
<td><p><strong>DFP:UcsiControl.exe Send 0 810008</strong></p>
<p><strong>UFP:UcsiControl.exe Send 0 1010008</strong></p>
<p><strong>DRP:UcsiControl.exe Send 0 2010008</strong></p></td>
</tr>
<tr class="odd">
<td>Set UOR</td>
<td><p><strong>DFP:UcsiControl.exe Send 0 810009</strong></p>
<p><strong>UFP:UcsiControl.exe Send 0 1010009</strong></p>
<p><strong>許可:UcsiControl.exe Send 0 2010009</strong></p></td>
</tr>
<tr class="even">
<td>Set PDR</td>
<td><p><strong>プロバイダー:UcsiControl.exe Send 0 81000B</strong></p>
<p><strong>コンシューマー:UcsiControl.exe Send 0 101000B</strong></p>
<p><strong>許可:UcsiControl.exe Send 0 201000B</strong></p></td>
</tr>
<tr class="odd">
<td>Get PDOs</td>
<td><p><strong>ローカル ソース:UcsiControl.exe Send 7 00010010</strong></p>
<p><strong>ローカル シンク:UcsiControl.exe Send 3 00010010</strong></p>
<p><strong>リモート ソース:UcsiControl.exe Send 7 00810010</strong></p>
<p><strong>リモート シンク:UcsiControl.exe Send 3 00810010</strong></p></td>
</tr>
<tr class="even">
<td>Get Connector Status</td>
<td><strong>UcsiControl.exe Send 0 010012</strong></td>
</tr>
<tr class="odd">
<td>Get Error Status</td>
<td><strong>UcsiControl.exe Send 0 13</strong></td>
</tr>
</tbody>
</table>

 

## <a name="related-topics"></a>関連トピック
[アーキテクチャ:Windows システム向け USB Type-C デザイン](architecture--usb-type-c-in-a-windows-system.md)  



