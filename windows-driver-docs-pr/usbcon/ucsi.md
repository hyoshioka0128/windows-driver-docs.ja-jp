---
Description: Microsoft では、USB 型 C コネクタ システム ソフトウェア インターフェイス (UCSI) 仕様準拠のドライバーを提供します。
title: USB Type-C Connector System Software Interface (UCSI) ドライバー
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 623a0fddd4f04d1d82a554924edc8354f15b9719
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63355204"
---
# <a name="usb-type-c-connector-system-software-interface-ucsi-driver"></a>USB Type-C Connector System Software Interface (UCSI) ドライバー


**要約**

-   Microsoft から提供されたインボックス UCSI システム用のドライバーを USB 型-C# 埋め込みコント ローラー。

**最終更新日**

-   2018 年 10 月

**Windows のバージョン**

-   Windows 10 デスクトップ エディション (Home、Pro、Enterprise、Education)
-   Windows 10 Mobile

**公式の仕様**

-   [UCSI の Intel BIOS の実装](https://go.microsoft.com/fwlink/p/?LinkId=760658)
-   [USB タイプ C コネクタ システム ソフトウェア インターフェイスの仕様](https://go.microsoft.com/fwlink/p/?LinkId=703713)
-   [ハードウェアの設計:システム埋め込みコント ローラーと USB 型-C# のコンポーネント](hardware-design-of-a-usb-type-c-system.md#emb)


Microsoft では、ACPI トランスポートの USB 型 C コネクタ システム ソフトウェア インターフェイス (UCSI) 仕様準拠のドライバーを提供します。 設計には、ACPI トランスポートを使用して埋め込みコント ローラーが含まれている場合は、EC/システムの BIOS で UCSI を実装し、(UcmUcsiCx.sys および UcmUcsiAcpiClient.sys) ボックスで UCSI ドライバーをロードします。

必要があります、UCSI 準拠のハードウェアは、ACPI 以外のトランスポートを使用している場合[UCSI クライアント ドライバーを書く](write-a-ucsi-driver.md)します。

## <a name="drivers-for-supporting-usb-type-c-components-for-systems-with-embedded-controllers"></a>システムの埋め込みコント ローラーと USB 型-C# のコンポーネントをサポートするためのドライバー

埋め込みコント ローラーのシステムの例を次に示します。

![usb タイプ c ソフトウェア コンポーネント](images/ucsiarch.png)

前の例では、システムのファームウェアで処理が USB 役割の交代と役割の交代の USB ドライバー スタックが読み込まれていません。 別のシステムでドライバー スタックが読み込まれないデュアル ロールがサポートされていないため。

上の図

-   **デバイス側の USB ドライバー**

    [デバイス側の USB ドライバー](usb-device-side-drivers-in-windows.md)関数デバイス/周辺機器のサービスを提供します。 USB 関数コント ローラー クラスの拡張サポート MTP (Media Transfer Protocol) と充電 BC 1.2 を使用しています。 Microsoft では、Synopsys USB 3.0、および ChipIdea USB 2.0 コント ローラーの組み込みのクライアント ドライバーを提供します。 使用して、関数のコント ローラーのカスタム クライアント ドライバーを記述する[USB 関数コント ローラー クライアント ドライバーのプログラミング インターフェイス](https://msdn.microsoft.com/library/windows/hardware/mt188010)します。 詳細については、次を参照してください。 [usb ドライバーを Windows の開発機能のコント ローラー](developing-windows-drivers-for-usb-function-controllers.md)します。

    SoC ベンダー可能性があります関数下位の USB フィルター ドライバーとの提供充電器の検出。 インボックス Synopsys USB 3.0 または ChipIdea USB 2.0 のクライアント ドライバーを使用している場合は、独自のフィルター ドライバーを実装できます。

-   **ホスト側の USB ドライバー**

    ホスト側の USB ドライバーでは、EHCI または XHCI 準拠の USB ホスト コント ローラーを使用するドライバーのセットです。 役割の交代ドライバー ホスト ロールを列挙する場合は、ドライバーが読み込まれます。 ホスト コント ローラーが仕様に準拠していないかどうかは、使用してカスタム ドライバーを記述する[USB ホスト コント ローラーの拡張機能 (UCX) プログラミング インターフェイス](https://msdn.microsoft.com/library/windows/hardware/mt188009)します。 詳しくは、次を参照してください。[開発 Windows ドライバーの USB ホスト コント ローラー](developing-windows-drivers-for-usb-host-controllers.md)します。

    **注**  いない[USB デバイスのすべてのクラス](supported-usb-classes.md)Windows 10 Mobile でサポートされます。

     

-   **USB コネクタ マネージャー**

    Microsoft Windows (UcmUcsiCx.sys) 使用可能な UCSI 仕様で定義されている機能を実装すると UCSI インボックス ドライバーを提供して[ここ](https://go.microsoft.com/fwlink/p/?LinkId=703713)します。 仕様では、UCSI の機能について説明し、ハードウェア コンポーネントの設計者、システム ビルダー、およびデバイス ドライバー開発者向けのレジスタとデータの構造を説明します。

    このドライバーは、埋め込みコント ローラーのシステムを対象としています。 このドライバーは、Microsoft 提供の USB コネクタ マネージャー クラスの拡張機能ドライバー (Ucmcx.sys) にクライアントです。 ドライバーは、データまたは電源のロールを変更するには、ファームウェアに要求を開始して、トラブルシューティング メッセージをユーザーに提供するために必要な情報の取得などのタスクを処理します。

## <a name="ucsi-commands-required-by-windows"></a>Windows で必要な UCSI コマンド


すべての UCSI 実装で「必要」なコマンドの UCSI 仕様を参照してください。

「必須」とマークされてコマンドだけでなく Windows には、これらのコマンドが必要です。

-   取得\_代替\_モード
-   取得\_CAM\_サポートされています。
-   取得\_PDO
-   設定\_通知\_を有効にします。システムまたはコント ローラーは、セット内の次の通知をサポートする必要があります\_通知\_を有効にします。
    -   サポートされているプロバイダーの機能の変更
    -   ネゴシエートされた電源レベルの変更
-   取得\_コネクタ\_状態。システムまたはコント ローラーは、GET 内でこれらのコネクタの状態変更をサポートする必要があります\_コネクタ\_状態。
    -   サポートされているプロバイダーの機能の変更
    -   ネゴシエートされた電源レベルの変更

BIOS で UCSI を実装するために必要なタスクについては、次を参照してください。 [Intel BIOS UCSI 実装](https://go.microsoft.com/fwlink/p/?LinkId=760658)します。

## <a name="example-flow-for-ucsi"></a>UCSI のフローの例


このセクションで示す例では、USB 型-C# のハードウェアまたはファームウェア、UCSI ドライバー、およびオペレーティング システム間の相互作用について説明します。

### <a name="drp-role-detection"></a>DRP ロールの検出

1.  USB タイプ-C/ハードウェアのファームウェアを検出した、デバイス接続イベントと、Windows 10 システム DRP システムが UFP ロールを最初になります。
    1.  ファームウェアでは、コネクタでの変更を示す通知を送信します。
    2.  UCSI ドライバーは GET を送信\_コネクタ\_状態要求。
    3.  ファームウェアの応答をその接続の状態 = 1 とパートナーの種類のコネクタ DFP を =。 
2.  USB 関数のスタック内のドライバーは、列挙体に応答します。
3.  USB コネクタ マネージャー クラス拡張は、USB 関数のスタックが読み込まれて、そのため、システムが正しくない状態を認識します。 UCSI ドライバー、ファームウェアに USB 操作ロールの設定と電源の方向のロールの設定の要求を送信するよう指示します。
4.  USB タイプ-C/ハードウェアのファームウェアは、DFP でロール スワップ操作を開始します。

### <a name="detecting-a-charger-mismatch-error--condition"></a>充電器の不一致エラー状態を検出

1.  USB タイプ-C/ハードウェアのファームウェアは、充電が接続され、既定の電源のコントラクトをネゴシエートを検出します。 また、充電器がシステムに十分な電力を提供しないことを監視します。
2.  USB タイプ-C/ハードウェアのファームウェア設定低速な充電ビット。
    1.  ファームウェアでは、コネクタでの変更を示す通知を送信します。
    2.  UCSI ドライバーは GET を送信\_コネクタ\_状態要求。
    3.  ファームウェアが接続状態で応答 = 1、コネクタのパートナーの種類 = DFP、およびバッテリの充電状態低速/トリクルを = です。
    
3.  USB コネクタ マネージャー クラスの拡張が充電器の不一致を表示する UI に通知を送信メッセージのトラブルシューティングを行います。

## <a name="how-to-test-ucsi"></a>UCSI をテストする方法


UCSI 実装をテストする方法を数多くあります。 UCSI BIOS/EC の実装で個々 のコマンドをテストするで提供されており、UCSIControl.exe を使用、 [MUTT ソフトウェア パック](mutt-software-package.md)します。 完全な UCSI 実装をテストするには、Windows ハードウェア ラボ キット (HLK) および」の手順ではありますが、両方の UCSI テストを使用して、[種類 C の相互運用機能のプロシージャを手動](https://msdn.microsoft.com/library/windows/hardware/mt422725)します。

**UCSIControl.exe**

UCSIControl.exe を使用して、EC/UCSI BIOS の実装で個々 のコマンドをテストすることができます。 このツールでは、UCSI ドライバー、ファームウェアに UCSI コマンドを送信することができます。 読み込まれ、実行されているとは、ドライバーを有効になっているテスト インターフェイスを持っているドライバーが必要です。 既定では、このインターフェイスは無効化に小売システムで承認されていないユーザーがアクセスできないようにするためです。

1.  デバイス マネージャーで (devmgmt.msc) という名前のデバイス ノードを検索**UCSI USB コネクタ マネージャー**します。 下のノードが、**ユニバーサル シリアル バス コント ローラー**カテゴリ。
2.  デバイスで、右クリックして**プロパティ**を開くと、**詳細**タブ。
3.  選択**デバイス インスタンス パス**ドロップダウン リストからプロパティ値を書き留めます。
4.  レジストリ エディター (regedit.exe) を開きます。
5.  このキーの下でデバイスのインスタンスのパスに移動します。

    HKEY\_ローカル\_マシン\\システム\\CurrentControlSet\\Enum\\&lt;デバイス-path インスタンス&gt;\\デバイス パラメーター

6.  という名前の DWORD 値を作成する**TestInterfaceEnabled**し、値を 0x1 に設定します。
7.  選択して、デバイスの再起動、**を無効にする**デバイス マネージャーで、[デバイス] ノードのオプションを選択し、**を有効にする**します。 または、PC を単に再開できます。

実行して、ヘルプを表示する**UcsiControl.exe/でしょうか。** します。

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
<td>PPM のリセット</td>
<td><strong>UcsiControl.exe 送信 0 1</strong></td>
</tr>
<tr class="even">
<td>コネクタのリセット</td>
<td><p>ソフト リセット:<strong>UcsiControl.exe 送信 0 10003</strong></p>
<p>ハード リセットを実行します。<strong>UcsiControl.exe 送信 0 810003</strong></p></td>
</tr>
<tr class="odd">
<td>通知の有効化を設定します。</td>
<td><p>すべての通知:<strong>UcsiControl.exe 送信 0 ffff0005</strong></p>
<p>コマンドの完了のみ<strong>UcsiControl.exe 送信 0 00010005</strong></p>
<p>通知されません。<strong>UcsiControl.exe 送信 0 00000005</strong></p></td>
</tr>
<tr class="even">
<td>機能を取得します。</td>
<td><strong>UcsiControl.exe 送信 0 6</strong></td>
</tr>
<tr class="odd">
<td>コネクタ機能を取得します。</td>
<td><strong>UcsiControl.exe 送信 0 10007</strong></td>
</tr>
<tr class="even">
<td>セット UOM</td>
<td><p><strong>DFP:UcsiControl.exe Send 0 810008</strong></p>
<p><strong>UFP:UcsiControl.exe Send 0 1010008</strong></p>
<p><strong>DRP:UcsiControl.exe Send 0 2010008</strong></p></td>
</tr>
<tr class="odd">
<td>UOR を設定します。</td>
<td><p><strong>DFP:UcsiControl.exe Send 0 810009</strong></p>
<p><strong>UFP:UcsiControl.exe Send 0 1010009</strong></p>
<p><strong>使用できます。UcsiControl.exe Send 0 2010009</strong></p></td>
</tr>
<tr class="even">
<td>民主共和国を設定します。</td>
<td><p><strong>プロバイダー:UcsiControl.exe 0 81000B を送信します。</strong></p>
<p><strong>コンシューマー:UcsiControl.exe 0 101000B を送信します。</strong></p>
<p><strong>使用できます。UcsiControl.exe 0 201000B を送信します。</strong></p></td>
</tr>
<tr class="odd">
<td>Pdo を取得します。</td>
<td><p><strong>ローカル ソース:UcsiControl.exe Send 7 00010010</strong></p>
<p><strong>ローカルのシンク。UcsiControl.exe Send 3 00010010</strong></p>
<p><strong>リモート ソース:UcsiControl.exe 送信 7 00810010</strong></p>
<p><strong>リモートのシンク。UcsiControl.exe 送信 3 00810010</strong></p></td>
</tr>
<tr class="even">
<td>コネクタの状態を取得します。</td>
<td><strong>UcsiControl.exe 送信 0 010012</strong></td>
</tr>
<tr class="odd">
<td>エラー状態を取得します。</td>
<td><strong>UcsiControl.exe 送信 0 13</strong></td>
</tr>
</tbody>
</table>

 

## <a name="related-topics"></a>関連トピック
[アーキテクチャ:Windows システムの USB 型-C# のデザイン](architecture--usb-type-c-in-a-windows-system.md)  



