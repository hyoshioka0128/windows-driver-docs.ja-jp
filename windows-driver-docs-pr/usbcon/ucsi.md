---
Description: Microsoft は、USB タイプの C コネクタシステムソフトウェアインターフェイス (UCSI) 仕様に準拠したドライバーを提供しています。
title: USB Type-C Connector System Software Interface (UCSI) ドライバー
ms.date: 04/20/2017
ms.localizationpriority: High
ms.openlocfilehash: bb4c1969370147e8298eabd32aef3befb2cee2e6
ms.sourcegitcommit: c73954a5909ec8c7e189f77fd5813f2eb749687c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/07/2019
ms.locfileid: "72007630"
---
# <a name="usb-type-c-connector-system-software-interface-ucsi-driver"></a>USB Type-C Connector System Software Interface (UCSI) ドライバー


**概要**

-   組み込みコントローラーを備えた USB タイプ C システム用の組み込みの UCSI ドライバー。

**最終更新日時**

-   2018 年 10 月

**Windows のバージョン**

-   Windows 10 デスクトップ エディション (Home、Pro、Enterprise、Education)
-   Windows 10 Mobile

**公式の仕様**

-   [UCSI の Intel BIOS 実装](https://go.microsoft.com/fwlink/p/?LinkId=760658)
-   [USB タイプ-C コネクタシステムソフトウェアインターフェイスの仕様](https://go.microsoft.com/fwlink/p/?LinkId=703713)
-   @no__t 0Hardware の設計:埋め込みコントローラー @ no__t を持つシステムの USB タイプ-C コンポーネント


Microsoft は、ACPI トランスポート用の USB タイプ C コネクタシステムソフトウェアインターフェイス (UCSI) 仕様準拠のドライバーを提供しています。 設計に ACPI トランスポートが組み込まれたコントローラーが含まれている場合は、システムの BIOS/EC に UCSI を実装し、インボックス UCSI ドライバー (UcmUcsiCx および UcmUcsiAcpiClient) を読み込みます。

UCSI 準拠のハードウェアが ACPI 以外のトランスポートを使用している場合は、 [ucsi クライアントドライバーを記述](write-a-ucsi-driver.md)する必要があります。

## <a name="drivers-for-supporting-usb-type-c-components-for-systems-with-embedded-controllers"></a>埋め込みコントローラーを備えたシステムの USB タイプ C コンポーネントをサポートするためのドライバー

コントローラーが埋め込まれているシステムの例を次に示します。

![usb タイプ-c ソフトウェアコンポーネント](images/ucsiarch.png)

前の例では、システムのファームウェアで USB 役割の切り替えが処理され、USB 役割スイッチドライバースタックが読み込まれていません。 別のシステムでは、デュアルロールがサポートされていないため、ドライバースタックが読み込まれない可能性があります。

上の図では、

-   **USB デバイス側ドライバー**

    [USB デバイス側ドライバー](usb-device-side-drivers-in-windows.md)は、機能/デバイス/周辺機器を処理します。 USB 関数コントローラークラス拡張は、MTP (メディア転送プロトコル) をサポートし、BC 1.2 充電器を使用して課金します。 Microsoft には、Synopsys USB 3.0 および ChipIdea USB 2.0 コントローラー用のインボックスクライアントドライバーが用意されています。 関数コントローラー用のカスタムクライアントドライバーは、 [USB 関数コントローラークライアントドライバーのプログラミングインターフェイス](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/mt188010(v=vs.85))を使用して作成できます。 詳細については、「 [USB 機能コントローラー用の Windows ドライバーの開発](developing-windows-drivers-for-usb-function-controllers.md)」を参照してください。

    SoC ベンダは、USB 機能であるチャージャー検出用の下位フィルタードライバーを提供する場合があります。 インボックス Synopsys USB 3.0 または ChipIdea USB 2.0 クライアントドライバーを使用している場合は、独自のフィルタードライバーを実装できます。

-   **USB ホスト側ドライバー**

    USB ホスト側ドライバーは、EHCI または XHCI 準拠の USB ホストコントローラーで動作するドライバーのセットです。 ドライバーは、役割スイッチドライバーがホストの役割を列挙した場合に読み込まれます。 ホストコントローラーが仕様に準拠していない場合は、 [USB ホストコントローラー拡張 (UCX) プログラミングインターフェイス](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/mt188009(v=vs.85))を使用してカスタムドライバーを作成できます。 詳細については、「 [USB ホストコントローラー用の Windows ドライバーの開発](developing-windows-drivers-for-usb-host-controllers.md)」を参照してください。

    **注**   Windows 10 Mobile では、[すべての USB デバイスクラス](supported-usb-classes.md)がサポートされているわけではありません。

     

-   **USB コネクタマネージャー**

    Microsoft では、[ここ](https://go.microsoft.com/fwlink/p/?LinkId=703713)で使用可能な ucsi 仕様で定義されている機能を実装する、Windows (UcmUcsiCx) を使用する ucsi インボックスドライバーを提供しています。 この仕様では、UCSI の機能について説明し、ハードウェアコンポーネントデザイナー、システムビルダー、およびデバイスドライバーの開発者のためのレジスタとデータ構造について説明します。

    このドライバーは、コントローラーが組み込まれているシステムを対象としています。 このドライバーは、Microsoft 提供の USB コネクタマネージャークラス拡張ドライバー (Ucmcx .sys) のクライアントです。 ドライバーは、ファームウェアへの要求を開始してデータまたは電源の役割を変更し、ユーザーにトラブルシューティングメッセージを提供するために必要な情報を取得するなどのタスクを処理します。

## <a name="ucsi-commands-required-by-windows"></a>Windows で必要な UCSI コマンド


すべての UCSI 実装で "必須" になっているコマンドについては、UCSI の仕様を参照してください。

"Required" とマークされているコマンドに加えて、Windows には次のコマンドが必要です。

-   GET @ NO__T-0ALTERNATE @ NO__T モード
-   GET @ NO__T-0CAM @ NO__T-1 SUPPORTED
-   GET @ NO__T-0PDOS
-   SET @ NO__T-0NOTIFICATION @ NO__T-1 ENABLE:システムまたはコントローラーは、SET @ no__t-0NOTIFICATION @ no__t-1ENABLE で次の通知をサポートする必要があります。
    -   サポートされているプロバイダーの機能の変更
    -   ネゴシエートされる電源レベルの変更
-   GET @ NO__T-0CONNECTOR @ NO__T-1STATUS:システムまたはコントローラーは、GET @ no__t-0CONNECTOR @ no__t-1STATUS でこれらのコネクタの状態の変更をサポートする必要があります。
    -   サポートされているプロバイダーの機能の変更
    -   ネゴシエートされる電源レベルの変更

BIOS で UCSI を実装するために必要なタスクの詳細については、「 [INTEL bios による ucsi の実装](https://go.microsoft.com/fwlink/p/?LinkId=760658)」を参照してください。

## <a name="example-flow-for-ucsi"></a>UCSI のフローの例


このセクションで示す例では、USB タイプ C ハードウェア/ファームウェア、UCSI ドライバー、およびオペレーティングシステム間の相互作用について説明します。

### <a name="drp-role-detection"></a>DRP ロールの検出

1.  USB タイプ-C ハードウェア/ファームウェアはデバイスアタッチイベントを検出し、最初に Windows 10 システムの DRP システムが UFP ロールになります。
    1.  ファームウェアは、コネクタが変更されたことを示す通知を送信します。
    2.  UCSI ドライバーは、GET @ no__t-0CONNECTOR @ no__t-1STATUS 要求を送信します。
    3.  ファームウェアによって、Connect Status = 1 および Connector Partner Type = DFP という応答が返されます。 
2.  USB 関数スタック内のドライバーは、列挙体に応答します。
3.  USB コネクタマネージャークラス拡張は、USB 関数スタックが読み込まれたことを認識しているため、システムの状態が正しくありません。 このメソッドは、設定された USB 操作の役割を送信し、電源の方向の役割要求をファームウェアに設定するように UCSI ドライバーに指示します。
4.  USB タイプ-C ハードウェア/ファームウェアは、DFP を使用してロールスワップ操作を開始します。

### <a name="detecting-a-charger-mismatch-error--condition"></a>チャージャーの不一致エラー条件の検出

1.  USB タイプ-C ハードウェア/ファームウェアは、チャージャーが接続されていることを検出し、既定の電源コントラクトをネゴシエートします。 また、チャージャーがシステムに十分な電力を供給していないことを観察します。
2.  USB タイプ-C ハードウェア/ファームウェアは、低速充電ビットを設定します。
    1.  ファームウェアは、コネクタが変更されたことを示す通知を送信します。
    2.  UCSI ドライバーは、GET @ no__t-0CONNECTOR @ no__t-1STATUS 要求を送信します。
    3.  ファームウェアは、Connect Status = 1、Connector Partner Type = DFP、およびバッテリの充電状態 = 低速/トリクルで応答します。
    
3.  USB コネクタマネージャークラス拡張は、充電の不一致のトラブルシューティングメッセージを表示するために、UI に通知を送信します。

## <a name="how-to-test-ucsi"></a>UCSI のテスト方法


UCSI 実装をテストするには、いくつかの方法があります。 UCSI BIOS/EC 実装で個々のコマンドをテストするには、 [MUTT ソフトウェアパック](mutt-software-package.md)に用意されている UCSIControl を使用します。 UCSI の完全実装をテストするには、Windows Hardware Lab Kit (HLK) に含まれている UCSI テストと、[タイプ C の手動による相互運用手順](https://docs.microsoft.com/windows-hardware/drivers/usbcon/)の手順を使用します。

**UCSIControl**

UCSIControl を使用して、UCSI BIOS/EC 実装で個々のコマンドをテストできます。 このツールを使用すると、ucsi ドライバーを使用して、UCSI コマンドをファームウェアに送信できます。 ドライバーが読み込まれ、実行されていること、およびドライバーのテストインターフェイスが有効になっていることが必要です。 既定では、このインターフェイスは有効になっていないため、リテールシステムの未承認ユーザーがアクセスできないようにします。

1.  **Ucsi USB コネクタマネージャー**という名前のデバイスノードをデバイスマネージャー (devmgmt.msc) に配置します。 ノードは、 **[ユニバーサルシリアルバスコントローラー]** カテゴリの下にあります。
2.  デバイスを右クリックし、 **[プロパティ]** をクリックして、 **[詳細]** タブを開きます。
3.  ドロップダウンから **[デバイスインスタンスのパス]** を選択し、プロパティの値をメモします。
4.  レジストリ エディター (regedit.exe) を開きます。
5.  このキーの下にあるデバイスインスタンスのパスに移動します。

    HKEY @ no__t-0LOCAL @ no__t-1MACHINE @ no__t-2System @ no__t-3CurrentControlSet @ no__t-4Enum @ no__t-5 @ no__t-6device--path @ no__t-7 @ no__t-8Device Parameters

6.  **Testinterfaceenabled**という名前の DWORD 値を作成し、値を0x1 に設定します。
7.  デバイスマネージャーのデバイスノードで **[無効]** オプションを選択し、 **[有効に]** する を選択して、デバイスを再起動します。 または、単に PC を再起動することもできます。

ヘルプを表示するには、 **UcsiControl/?** を実行します。

一般的なコマンドを次に示します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>UCSI コマンド</th>
<th>UcsiControl コマンド</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>PPM のリセット</td>
<td><strong>UcsiControl Send 0 1</strong></td>
</tr>
<tr class="even">
<td>コネクタのリセット</td>
<td><p>ソフトリセット:<strong>UcsiControl Send 0 10003</strong></p>
<p>ハードリセット:<strong>UcsiControl Send 0 810003</strong></p></td>
</tr>
<tr class="odd">
<td>通知の有効化の設定</td>
<td><p>すべての通知:<strong>UcsiControl Send 0 ffff0005</strong></p>
<p>コマンドの完了のみ:<strong>UcsiControl Send 0 00010005</strong></p>
<p>通知なし:<strong>UcsiControl Send 0 00000005</strong></p></td>
</tr>
<tr class="even">
<td>機能の取得</td>
<td><strong>UcsiControl Send 0 6</strong></td>
</tr>
<tr class="odd">
<td>コネクタ機能の取得</td>
<td><strong>UcsiControl Send 0 10007</strong></td>
</tr>
<tr class="even">
<td>UOM の設定</td>
<td><p>@NO__T-セーフ FP:UcsiControl Send 0 810008 @ no__t-0</p>
<p><strong>UFP:UcsiControl Send 0 1010008 @ no__t-0</p>
<p><strong>DRP:UcsiControl Send 0 2010008 @ no__t-0</p></td>
</tr>
<tr class="odd">
<td>UOR を設定する</td>
<td><p>@NO__T-セーフ FP:UcsiControl Send 0 810009 @ no__t-0</p>
<p><strong>UFP:UcsiControl Send 0 1010009 @ no__t-0</p>
<p><strong>Accept:UcsiControl Send 0 2010009 @ no__t-0</p></td>
</tr>
<tr class="even">
<td>民主共和国の設定</td>
<td><p><strong>Provider:UcsiControl Send 0 81000B @ no__t-0</p>
<p><strong>Consumer:UcsiControl Send 0 101000B @ no__t-0</p>
<p><strong>Accept:UcsiControl Send 0 201000B @ no__t-0</p></td>
</tr>
<tr class="odd">
<td>PDOs を取得する</td>
<td><p><strong>Local ソース:UcsiControl Send 7 00010010 @ no__t-0</p>
<p><strong>Local シンク:UcsiControl Send 3 00010010 @ no__t-0</p>
<p><strong>Remote Source:UcsiControl Send 7 00810010 @ no__t-0</p>
<p><strong>Remote Sink:UcsiControl Send 3 00810010 @ no__t-0</p></td>
</tr>
<tr class="even">
<td>コネクタの状態の取得</td>
<td><strong>UcsiControl Send 0 010012</strong></td>
</tr>
<tr class="odd">
<td>エラー状態の取得</td>
<td><strong>UcsiControl Send 0 13</strong></td>
</tr>
</tbody>
</table>

 

## <a name="related-topics"></a>関連トピック
[Architecture:Windows システムの USB タイプ-C の設計 @ no__t-0  



