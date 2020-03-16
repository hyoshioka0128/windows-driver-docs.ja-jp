---
title: Windows の UEFI 要件 (SoC プラットフォーム)
description: このトピックでは、Windows 10 for desktop エディション (Home、Pro、Enterprise、および教育) と Windows 10 Mobile に適用される UEFI の要件について説明します。
ms.assetid: 7A0B901E-1252-4F8F-B1CB-BA1AB7B01112
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c32694d75dcdd948d93f0fda50674f7fdf3abc55
ms.sourcegitcommit: b316c97bafade8b76d5d3c30d48496915709a9df
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/13/2020
ms.locfileid: "79242839"
---
# <a name="uefi-requirements-for-windows-editions-on-soc-platforms"></a>SoC プラットフォームでの Windows エディションの UEFI 要件


このトピックでは、Windows 10 for desktop エディション (Home、Pro、Enterprise、および教育) と Windows 10 Mobile に適用される UEFI の要件について説明します。 Windows 10 Mobile のみに適用されるその他の要件については、「 [windows 10 mobile の UEFI 要件](uefi-requirements-specific-to-windows-mobile.md)」を参照してください。

## <a name="summary-of-requirements"></a>要件の概要


次の表は、uefi 仕様 (UEFI 2.3.1 仕様のセクション 2.6) で定義されている UEFI コンプライアンスの現在の要件をすべて示しています。 この表では、*明示的な windows の要件*という用語は、windows コンポーネントによって直接呼び出されるプロトコルまたはサービスを識別します。 これらのサービスのみが Windows によって明示的に使用されますが、その他のサービスやプロトコルは、コアファームウェア実装、EFI デバイスドライバー、または開発および展開ツールチェーンによって暗黙的または明示的に要求される場合があります。

Microsoft は、この一連の要件について、実装からのフィードバックとコメントを歓迎します。 OS またはファームウェアによって要求されないと判断された UEFI 準拠の要件については、UEFI.org を使用して、このクラスのデバイスに対してこれらのコンプライアンス要件を緩和することを目的としています。

特定の要件の詳細については、表の後のセクションを参照してください。

| 要件                               | UEFI 仕様セクション | 説明                          |
|-------------------------------------------|----------------------------|--------------------------------|
| **EFI システムテーブル**                      | 4.3                        | 明示的な Windows 要件   |
| **EFI ブートサービス**                     | 6.0                        |                                |
|   イベント、タイマー、タスクのサービス          | 6.1                        |                                |
|   メモリサービス                         | 6.2                        | 明示的な Windows 要件\` |
|   プロトコルハンドラーサービス               | 6.3                        | 明示的な Windows 要件   |
|   イメージサービス                          | 6.4                        | 明示的な Windows 要件   |
|   その他のサービス                  | 6.5                        | 明示的な Windows 要件   |
| **EFI ランタイムサービス**                  | 7.0                        |                                |
|   タイムサービス                           | 7.3                        | 明示的な Windows 要件   |
|   変数サービス                       | 7.2                        | 明示的な Windows 要件   |
|   その他のサービス                  | 7.5                        | 明示的な Windows 要件   |
| **必要な UEFI プロトコル**               |                            |                                |
|   EFI 読み込まれたイメージプロトコル               | 8.1                        |                                |
|   EFI 読み込まれたイメージデバイスパスプロトコル   | 8.2                        |                                |
|   EFI デバイスパスプロトコル                | 9.2                        | 明示的な Windows 要件   |
|   EFI デバイスパスユーティリティプロトコル      | 9.5                        |                                |
|   EFI 圧縮解除プロトコル                 | 18.5                       |                                |
|   EBC インタープリタープロトコル                | 20.11                      |                                |
| **条件付きで UEFI プロトコルを必要とする** |                            |                                |
|   EFI simple text 入力プロトコル          | 11.3                       | 明示的な Windows 要件   |
|   EFI simple text input EX プロトコル       | 11.2                       |                                |
|   EFI シンプルテキスト出力プロトコル         | 11.4                       |                                |
|   EFI グラフィックス出力プロトコル            | 11.9                       | 明示的な Windows 要件   |
|   EFI EDID 検出プロトコル            | 11.9.1                     |                                |
|   EFI EDID のアクティブなプロトコル                | 11.9.1                     |                                |
|   EFI ブロック IO プロトコル                   | 12.8                       | 明示的な Windows 要件   |
|   EFI ディスク IO プロトコル                    | 12.7                       |                                |
|   EFI simple ファイルシステムプロトコル         | 12.4                       |                                |
|   EFI Unicode 照合順序プロトコル          | 12.10                      |                                |
|   EFI simple ネットワークプロトコル             | 21.1                       |                                |
|   EFI PXE ベースコードプロトコル              | 21.3                       |                                |
|   EFI ブート整合性サービスプロトコル    | 21.5                       |                                |
|   EFI シリアル IO プロトコル                  | 11.8                       |                                |
|   UEFI ARM バインド                        | 2.3.5                      | 明示的な Windows 要件   |
| **セキュリティ要件**                 |                            |                                |
|   セキュアブート                             | 27.0                       | 明示的な Windows 要件   |
|   ブートマネージャーの要件               | 3.1、3.3                   | 明示的な Windows 要件   |

 

## <a name="efi-system-table-requirements"></a>EFI システムテーブルの要件


EFI システムテーブルは、実装されているリビジョンレベルの標準定義に準拠している必要があります。 EFI システムテーブルによってポイントされる構成テーブルには、次の表で説明する2つの Guid とそれに関連するポインターが含まれている必要があります。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>GUID</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>EFI_ACPI_Table GUID</td>
<td><p>この GUID は、プラットフォームの ACPI ルートシステム記述ポインター (RSDP) を指す必要があります。</p></td>
</tr>
<tr class="even">
<td>SMBIOS_Table GUID</td>
<td><p>この GUID は、SMBIOS エントリポイント構造体を指す必要があります。</p>
<p>Windows では、2.4 以上のリビジョンレベルで SMBIOS 仕様が必要です。 セクション3.2、「必要な構造とデータ」、および「準拠のガイドライン」が必要です。 Windows の SMBIOS 互換性テストを使用できます。</p></td>
</tr>
</tbody>
</table>

 

## <a name="efi-boot-services-requirements"></a>EFI ブートサービスの要件


次の表は、Windows の EFI ブートサービス要件を示しています。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>EFI ブートサービス</th>
<th>要件</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>メモリサービス</td>
<td>Windows には、すべてのメモリサービスが必要です。</td>
</tr>
<tr class="even">
<td>プロトコルハンドラーサービス</td>
<td><p>Windows には、次のプロトコルハンドラーサービスが必要です。</p>
<ul>
<li><p>OpenProtocol ()</p></li>
<li><p>CloseProtocol ()</p></li>
<li><p>LocateDevicePath()</p></li>
<li><p>LocateHandle()</p></li>
</ul></td>
</tr>
<tr class="odd">
<td>イメージサービス</td>
<td><p>Windows では、次のイメージサービスが必要です。</p>
<ul>
<li><p>ExitBootServices ()</p></li>
</ul></td>
</tr>
<tr class="even">
<td>その他のブートサービス</td>
<td><p>Windows には、次のようなその他のブートサービスが必要です。</p>
<ul>
<li><p>ストール ()</p></li>
</ul>
<div class="alert">
<strong>  、</strong>エラーの修正やキャンセルを確実に実行できるように、決定的な (反復可能な) エラーを発生させるには、ストール () の実装が必要です。
</div>
<div>
 
</div></td>
</tr>
</tbody>
</table>

 

## <a name="efi-runtime-services-requirements"></a>EFI ランタイムサービスの要件


次の表に、Windows の EFI ランタイムサービスの要件を示します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>EFI ランタイムサービス</th>
<th>要件</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>タイムサービス</td>
<td><p>Windows には、次のタイムサービスが必要です。</p>
<ul>
<li><p>GetTime ()</p></li>
<li><p>SetTime ()</p>
<div class="alert">
<strong>注</strong>  タイムサービスは、プラットフォームの時間のハードウェアにアクセスするために (ExitBootServices () の前に) 起動中にのみ呼び出されます。
</div>
<div>
 
</div></li>
</ul></td>
</tr>
<tr class="even">
<td>変数サービス</td>
<td><p>複数のブートデバイスとセキュリティ変数をシステムのターゲットクラスで管理するには、すべての UEFI 変数サービスが必要です。</p></td>
</tr>
<tr class="odd">
<td>その他のランタイムサービス</td>
<td><p>Windows には、次のようなランタイムサービスが必要です。</p>
<ul>
<li><p>ResetSystem ()</p>
<div class="alert">ResetSystem () の実装では、reset オプションと shutdown オプションの両方がサポートされている必要
<strong>が  ます</strong>。
</div>
<div>
 
</div></li>
</ul></td>
</tr>
</tbody>
</table>

 

## <a name="protocol-requirements"></a>プロトコルの要件


次の表では、ブート中に特定の機能を実行するために Windows に必要な UEFI プロトコルについて説明します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>[プロトコル]</th>
<th>要件</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>グラフィックス出力プロトコル</td>
<td><p>Windows では、グラフィックス出力プロトコル (GOP) が必要です。 特定のフレームバッファー要件は次のとおりです。</p>
<ul>
<li><p>統合ディスプレイの場合、<em>水平解像度</em>と<em>VerticalResoluton</em>はパネルのネイティブ解像度である必要があります。</p></li>
<li><p>外部ディスプレイの場合、<em>水平解像度</em>と<em>VerticalResoluton</em>はディスプレイのネイティブ解像度である必要があります。サポートされていない場合は、ビデオアダプターと接続されているディスプレイの両方でサポートされる最大値になります。</p></li>
<li><p><em>ピクセル</em>の値は、<em>水平解像度</em>と同じでなければなりません。</p></li>
<li><p><em>ピクセル形式</em>は<em>PixelBlueGreenRedReserved8BitPerColor</em>でなければなりません。 物理フレームバッファーが必要であることに注意してください。<em>ピクセルの Bltonly</em>はサポートされていません。</p></li>
</ul>
<p>実行が UEFI ブートアプリケーションに渡された場合、ファームウェアブートマネージャーとファームウェアは、フレームバッファーを使用しないようにする必要があります。 ブートサービスが終了した後も、フレームバッファーは引き続きスキャンされる必要があります。</p></td>
</tr>
<tr class="even">
<td>代替表示出力</td>
<td><p>UEFI ファームウェアは、ハードウェアでサポートされているディスプレイコネクタを使用した起動をサポートしている必要があります。 内部パネルが接続されて表示されている場合は、内部パネルを使用する必要があります。 物理的に接続しているすべての出力には、ブート画面が表示されます。 接続されたディスプレイの場合、UEFI ファームウェアは次のことを行う必要があります。</p>
<ul>
<li><p>ネイティブの解像度を決定できる場合は、表示のネイティブモードで出力を初期化します。</p></li>
<li><p>ネイティブモードを使用できない場合は、最も互換性の高いモードに初期化する必要があります。</p></li>
<li><p>表示機能を特定できない場合は、接続されたディスプレイを、可能な限り多くのモニターと互換性があるとわかっているモードで初期化する必要があります (通常、解像度は480、1024x768 は 60Hz)。</p></li>
</ul></td>
</tr>
<tr class="odd">
<td>起動時の入力</td>
<td><p>EFI Simple Text 入力プロトコルは、ブートを選択したり、キーボードまたは接続されたキーボードが組み込まれているシステムでメニューを選択したりするために必要です。 キーボードレスシステムの場合は、ブート環境で次の3つのボタンを使用することをお勧めします。</p>
<ul>
<li><p>[スタート] ボタン</p></li>
<li><p>音量アップボタン</p></li>
<li><p>音量ダウンボタン</p></li>
</ul>
<p>ボタンの押下は、EFI Simple Text 入力プロトコルを使用して、それぞれ次のキーボードキーにマップすることによって報告する必要があります。</p>
<ul>
<li><p>Windows キー</p></li>
<li><p>↑キー</p></li>
<li><p>下方向キー</p></li>
</ul></td>
</tr>
<tr class="even">
<td>ローカルストレージブート</td>
<td><p>Windows では、EFI システムパーティションと Windows OS パーティションを含む記憶域ソリューションに対して、ブロック i/o プロトコルとデバイスパスプロトコルがサポートされている必要があります。 劣化の平準化やその他のフラッシュ管理を必要とするフラッシュストレージから起動する場合は、(UEFI アプリケーションではなく) ファームウェアに実装する必要があります。</p></td>
</tr>
</tbody>
</table>

 

## <a name="security-requirements"></a>セキュリティ要件


Windows では、セキュアブート、メジャーブート、暗号化、およびデータ保護の領域にセキュリティ要件があります。 これらの要件については、次の表で詳しく説明します。 さらに、SoC ハードウェアが既存の標準 (TPM、RTC など) に準拠していない領域については、追加の要件があります。 これらの詳細については、表の最後を参照してください。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>エリア</th>
<th>要件</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>全般</td>
<td><ul>
<li><p>要件 1: 必須。 このプラットフォームは、このセクションで指定されているすべての要件に準拠している必要があります。</p></li>
<li><p>要件 2: 必須。 プラットフォームは、互換性サポートモジュールがインストールまたはインストールされていない UEFI クラス3である必要があります。 BIOS エミュレーションとレガシ PC/起動時ブートを無効にする必要があります。</p></li>
</ul></td>
</tr>
<tr class="even">
<td>UEFI セキュアブート</td>
<td><ul>
<li><p>要件 3: 必須。 UEFI v 2.3.1 section 27 で定義されているセキュアブートでは、有効なと、コンピューターを安全に事前プロビジョニングするために必要な署名データベース (EFI_IMAGE_SECURITY_DATABASE) が有効になっている必要があります。 署名データベースの初期コンテンツは、必要なサードパーティの UEFI ドライバー、回復のニーズ、およびコンピューターにインストールされている OS ブートローダーに基づき、OEM によって決定されますが、Microsoft が提供する EFI_CERT_X509 署名が含まれている必要があります。 追加の署名は存在しません。</p></li>
<li><p>要件 4: 必須。 UEFI の "許可されていない" 署名データベース (EFI_IMAGE_SECURITY_DATABASE1) の存在が必要です。</p></li>
<li><p>要件 5: 必須。 Microsoft が提供する UEFI KEK は、UEFI KEK データベースに含まれている必要があります。 追加の KEKs は存在しません。 Microsoft は、KEK を EFI_CERT_X509 署名の形式で提供します。</p></li>
<li><p>要件 6: 必須。 PK<em><sub>pub</sub></em>キーが存在し、ファームウェアフラッシュに格納されている必要があります。</p>
<div class="alert">  に
<strong>注意</strong>してください。 pk<em><sub>priv</sub></em> (秘密キーは pk<em><sub>pub</sub></em>に相当する) では、pk<em><sub>Pub</sub></em>によってプロビジョニングされたすべてのデバイスでセキュアブートポリシーを制御します。そのため、その保護と使用は厳重に保護されている必要があります。
</div>
<div>
 
</div></li>
<li><p>要件 7: 必須。 初期署名データベースは、ファームウェアフラッシュに格納されている必要があり、OEM 署名済みのファームウェア更新プログラム、または UEFI で認証された変数の書き込みによってのみ更新される可能性があります。</p></li>
<li><p>要件 8: 必須。 署名の検証に失敗したブートパス内のイメージを実行することはできません。また、エラーの原因を EFI_IMAGE_EXECUTION_TABLE に追加する必要があります。 また、このような状況で推奨されるアプローチは、UEFI ブートマネージャーが OEM 固有の戦略に従って回復を開始することです。</p></li>
<li><p>要件 9: 必須。 署名の検証に失敗した UEFI イメージでは、物理的に存在するユーザーの上書きを許可しないでください。</p></li>
<li><p>要件 10: 省略可能。 OEM は、物理的に存在するユーザーが、PK<em><sub>priv</sub></em>にアクセスするか、ファームウェアセットアップを使用して物理プレゼンスを使用して、セキュアブートを無効にする機能を実装する場合があります。 ファームウェアのセットアップへのアクセスは、プラットフォーム固有の手段 (管理者パスワード、スマートカード、静的構成など) によって保護されている場合があります。</p></li>
<li><p>要件 11: 要件10が実装されている場合は必須。 セキュアブートがオフになっている場合、既存の UEFI 変数にはアクセスできません。</p></li>
<li><p>要件 12: 省略可能。 OEM は、物理的に存在するユーザーが、ファームウェアセットアップの "カスタム" と "標準" の2つのセキュアブートモードのどちらかを選択する機能を実装できます。 カスタムモードでは、次のように指定した場合の柔軟性が向上します。</p></li>
<li><p>要件 13: 要件12が実装されている場合は必須。 所有者固有の<em>PK</em>を設定することにより、カスタムモードで無効になっているセキュアブートを再度有効にすることができます。 管理は、UEFI 仕様のセクション27.5 の定義に従って続行する必要があります: ファームウェア/OS キー交換。 カスタムモードでは、デバイスの所有者が署名データベースで選択した署名を設定できます。</p></li>
<li><p>要件 14: 要件12が実装されている場合は必須。 ファームウェアのセットアップでは、セキュアブートが有効になっているかどうか、および標準モードまたはカスタムモードで動作しているかどうかが示されます。 ファームウェアのセットアップには、カスタムから標準モードに戻すオプションが用意されています。</p></li>
<li><p>要件 15: 必須。 ファームウェア設定が工場出荷時の既定値にリセットされた場合、すべてのカスタムセット保護変数は消去されます。元の PK<em><sub>pub</sub></em>は、元の製造元がプロビジョニングした署名データベースと共に再確立されます。</p></li>
<li><p>要件 16: 必須。 ドライバーの署名では、Authenticode オプション (WIN_CERT_TYPE_PKCS_SIGNED_DATA) を使用する必要があります。</p></li>
<li><p>要件 17: 必須。 EFI_IMAGE_EXECUTION_INFO_TABLE のサポート (起動時に開始または開始されたイメージに関する情報の作成と保存)。</p></li>
<li><p>要件 18: 必須。 EFI_IMAGE_SECURITY_DATABASE に対して GetVariable () をサポートします (承認された署名データベースと禁止された署名データベースの両方)。</p></li>
<li><p>要件 19: 必須。 Microsoft KEK を認証に使用して、EFI_IMAGE_SECURITY_DATABASE (承認された署名データベースと禁止された署名データベースの両方) の SetVariable () をサポートします。</p></li>
<li><p>要件 20: 必須。 EFI_HASH_SERVICE_BINDING_PROTOCOL: サービスのサポート: CreateChild ()、DestroyChild ()。</p></li>
<li><p>要件 21: 必須。 EFI_HASH_PROTOCOL。 サービスサポート: Hash ()。 SHA_1 と SHA-256 ハッシュアルゴリズムのサポート。 は、少なくとも 10 Mb の長さのメッセージを渡すことをサポートする必要があります。</p></li>
</ul></td>
</tr>
<tr class="odd">
<td>UEFI メジャーブート</td>
<td><p>次の要件は、TCG TPM 実装の必要性を意味するものではありません。ただし、影響を受ける領域に対して同等の機能が必要であることを意味します。</p>
<p>プラットフォームのサポートは、セキュリティで保護された実行環境で実行されている TPM のファームウェア実装によって提供され、暗号化アクセラレーションエンジンの上にレイヤーが配置され、分離ストレージが活用されます。 Microsoft は、このような TPM 実装に対して、ベンダーが使用するための参照ソフトウェアを提供できる場合があります。 これについては、さらに詳しく説明します。</p>
<ul>
<li><p>要件 22: 必須。 プラットフォームは、 <a href="https://go.microsoft.com/fwlink/p/?LinkId=528536" data-raw-source="[UEFI Trusted Execution Environment EFI Protocol](https://go.microsoft.com/fwlink/p/?LinkId=528536)">UEFI の信頼できる実行環境の Efi プロトコル</a>に指定されている efi プロトコルに準拠している必要があります。</p></li>
<li><p>要件 23: 必須。 このプラットフォームは、次の追加機能を備えた TCG EFI プラットフォーム仕様に準拠している必要があります。</p>
<ul>
<li><p>TrEE EFI プロトコルで定義されているインターフェイスをサポートするプラットフォームでは、PK<em><sub>pub</sub></em>のダイジェストは、EV_EFI_VARIABLE_CONFIG イベントとして TPM PCR [03] に拡張する必要があります。</p></li>
<li><p>認証された署名データベースの内容のダイジェスト (UEFI specification v1.0 のセクション27.8 を参照) は、EV_EFI_VARIABLE_CONFIG イベントとして測定されたブートで拡張する必要があります。 拡張操作は、TPM PCR [03] にする必要があります。</p></li>
<li><p>UEFI クライアントは、EFI_IMAGE_SECURITY_DATABASE 変数を使用して証明書の一覧を読み取って解析し、その拡張値に対してダイジェストを検証することができます。</p></li>
<li><p>TCG_PCR_EVENT のダイジェスト値は、sha-1 ではなく、SHA-256 である必要があります。</p></li>
</ul></li>
<li><p>要件 24: 必須。 このプラットフォームでは、 <a href="https://go.microsoft.com/fwlink/p/?LinkId=528539" data-raw-source="[TCG Platform Reset Attack Mitigation Specification](https://go.microsoft.com/fwlink/p/?LinkId=528539)">TCG プラットフォームリセット攻撃の緩和の仕様</a>で定義されている MemoryOverwriteRequestControl を実装する必要があります。</p></li>
</ul></td>
</tr>
<tr class="even">
<td>暗号化</td>
<td><ul>
<li><p>要件 25: 必須。 このプラットフォームでは、暗号化ハッシュ操作のオフロードに EFI_HASH_PROTOCOL (UEFI v 2.3.1 セクション 27.4) を提供する必要があります。 SHA-256 がサポートされている必要があります。</p></li>
<li><p>要件 26: 必須。 プラットフォームは、エントロピを OS で読み取るために、Microsoft によって定義された<a href="uefi-entropy-gathering-protocol.md" data-raw-source="[EFI_RNG_PROTOCOL](uefi-entropy-gathering-protocol.md)">EFI_RNG_PROTOCOL</a>をサポートする必要があります。</p></li>
</ul></td>
</tr>
<tr class="odd">
<td>データ保護</td>
<td><ul>
<li><p>要件 27: 必須。 このプラットフォームでは、次の UEFI 変数属性セットの任意の組み合わせで EFI 変数をサポートする必要があります。</p>
<ul>
<li><p>EFI_VARIABLE_BOOTSERVICE_ACCESS</p></li>
<li><p>EFI_VARIABLE_NON_VOLATILE</p></li>
<li><p>EFI_VARIABLE_AUTHENTICATED_WRITE_ACCESS</p></li>
</ul></li>
</ul></td>
</tr>
<tr class="even">
<td>その他のセキュリティ要件</td>
<td><p>SoC プラットフォームの Windows では、次の追加要件が必要です。</p>
<ul>
<li><p>Microsoft では、UEFI プラットフォームからエントロピを収集するためのプロトコルが定義されています。 UEFI の要件ではありませんが、SoC プラットフォームの Windows ではこのプロトコルが必要です。 このプロトコルの詳細については、「 <a href="uefi-entropy-gathering-protocol.md" data-raw-source="[UEFI entropy gathering protocol](uefi-entropy-gathering-protocol.md)">UEFI エントロピ収集プロトコル</a>」を参照してください。</p></li>
<li><p>UEFI 署名データベースの更新。 認証済み変数を更新するための新しいメカニズムは、UEFI 2.3.1 のセクション27で採用されています。 このメカニズムは、Windows で必要です。</p></li>
<li><p>信頼された実行環境。 Microsoft は、信頼できる実行環境 (ツリー) と対話するための EFI プロトコルを開発しています。これは、Trusted Computing Group (TCG) トラステッドプラットフォームモジュール (TCG) のサブセットに似ています。 EFI プロトコルは、Trusted Computing Group によって、"TCG EFI Protocol" バージョン1.2 リビジョン 1.00, June 9, 2006 を利用しています。</p>
<p>詳細については、 <a href="https://go.microsoft.com/fwlink/p/?LinkId=528536" data-raw-source="[UEFI Trusted Execution Environment EFI Protocol](https://go.microsoft.com/fwlink/p/?LinkId=528536)">UEFI の信頼された実行環境 EFI プロトコル</a>に関する説明を参照してください。</p></li>
</ul></td>
</tr>
</tbody>
</table>

 

## <a name="firmware-boot-manager-requirements"></a>ファームウェアブートマネージャーの要件


ファームウェアブートマネージャーは、仕様のセクション3.3 で定義されている既定のブート動作をサポートしている必要があります。 さらに、マルチブートをサポートするために、グローバルに定義された変数と、仕様のセクション3.1 のブートマネージャーの要件が必要です。

## <a name="uefi-arm-binding-requirements"></a>UEFI ARM のバインド要件


UEFI ARM バインドには、UEFI 仕様に準拠するために必要な ARM プラットフォームに固有の要件が含まれています。 Windows では、ARMv7 に適用される ARM バインド内のすべてが必要です。 Windows では ARMv7 より前のものはサポートされていないため、ARMv6k 以下に固有のバインドの要件は省略可能です。

バインドでは、MMU の構成方法や物理メモリのマッピング方法などを指定します。 また、バインドでは、UEFI プロトコルとサービスへの呼び出しを ARM ISA のみで行うように指定します。つまり、Thumb2 または Thumb で実行されているソフトウェアは、UEFI 関数を呼び出す前に ARM モードに戻す必要があります。

## <a name="uefi-arm-multiprocessor-startup-requirements"></a>UEFI ARM マルチプロセッサのスタートアップ要件


Microsoft は、マルチプロセッサの UEFI プラットフォームで複数の ARM コアを開始するためのプロトコルを開発しました。 このプロトコルは、[電源状態調整インターフェイス (PSCI)](https://go.microsoft.com/fwlink/p/?LinkId=528534)をサポートしていない ARM プラットフォームの Windows で必要です。 PSCI をサポートするプラットフォームでは、このプロトコルを使用できません。 このプロトコルの詳細については、「ACPI コンポーネントアーキテクチャ (ACPICA)」 Web サイトの「 [UEFI ARM ベースのプラットフォームでのマルチプロセッサの起動](https://go.microsoft.com/fwlink/p/?LinkId=528533)」を参照してください。

## <a name="platform-setup-requirements"></a>プラットフォームのセットアップ要件


ファームウェアは、OS ローダーに渡す前に、システムハードウェアを適切に定義された状態にする役割を担います。 次の表は、関連するプラットフォームのセットアップ要件を定義しています。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>要件</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>ブートパス</td>
<td>ファームウェアは、Windows が UEFI 経由でブートデバイスにアクセスでき、カーネルを読み込むポイントにプラットフォームを初期化する必要があります。 ブートデバイスから読み取るために階層に関係するすべてのデバイスは、パフォーマンスと電源に関する考慮事項により、適切な速度で稼働している必要があります。 また、基本プロセッサコア自体は、クロックを適切なレートで電源にする必要があります。これにより、システムがバッテリを使用しなくても適時に起動できるようになります。</td>
</tr>
<tr class="even">
<td>コアシステムリソース</td>
<td><p>ACPI テーブルを介して OS に公開されているコアシステムリソースには、電源が入っていて、クロックが必要です。 コアシステムリソースには、OS によって管理される必要がある割り込みコントローラー、タイマー、DMA コントローラーが含まれます。</p>
<p>さらに、OS 内の関連付けられたデバイスドライバーによってデバイスの割り込みが解除されるまで、ExitBootServices () への呼び出しによって割り込みがマスクされる必要があります。 ブートサービス中に割り込みが有効になっている場合は、ファームウェアによってその割り込みが管理されることを前提としています。</p></td>
</tr>
<tr class="odd">
<td>デバッグ</td>
<td>Windows は、USB 3 ホスト (XHCI)、USB 2 ホスト (EHCI) 1、IEEE 1394、シリアルおよび USB の機能インターフェイス (および PCI イーサネットアダプター) を使用したデバッグをサポートしています。 これらのうち少なくとも1つは、OS ハンドオフの前に、ファームウェアによって電源がオンになっている必要があります。 どちらのオプションを指定する場合でも、デバッグのために公開されたポートが必要です。また、コントローラーはメモリにマップされているか、専用の (共有されていない) 周辺機器バスを介して接続されている必要があります。</td>
</tr>
<tr class="even">
<td>その他のプラットフォームのセットアップ要件</td>
<td>OS ローダーに制御を渡す前に、ファームウェアで pin の多重化およびパッドの構成を完了しておく必要があります。</td>
</tr>
</tbody>
</table>

 

## <a name="installation-requirements"></a>インストール要件


Windows では、OS パーティションが GPT パーティション分割されたストレージソリューションに存在している必要があります。 MBR パーティション分割ストレージは、データストレージとして使用できます。 Uefi 仕様で定義されているように、UEFI プラットフォームには専用のシステムパーティションが必要です。 Windows では、この専用システムパーティションが必要です。これは、EFI システムパーティション (ESP) と呼ばれています。

## <a name="hardware-security-test-interface-hsti-requirement"></a>ハードウェアセキュリティテストインターフェイス (HSTI) の要件


プラットフォームは、ハードウェアセキュリティテストインターフェイスを実装する必要があります。プラットフォームは、[ハードウェアセキュリティ](https://docs.microsoft.com/windows-hardware/test/hlk/testref/hardware-security-testability-specification)のテストの容易性の仕様で指定されているドキュメントやツールを共有するために必要です。

## <a name="related-topics"></a>関連トピック

[SoC プラットフォーム上の Windows の最小 UEFI 要件](minimum-uefi-requirements-for-windows-on-soc-platforms.md)  

[Windows 10 Mobile の UEFI 要件](uefi-requirements-specific-to-windows-mobile.md)  

[USB フラッシュのサポートに関する UEFI の要件](uefi-requirements-for-usb-flashing-support.md)  



