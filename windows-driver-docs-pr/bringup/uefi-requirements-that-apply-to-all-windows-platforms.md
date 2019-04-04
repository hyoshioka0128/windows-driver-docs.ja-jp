---
title: SoC のプラットフォームで Windows の UEFI 要件
description: このトピックでは、デスクトップのエディション (Home、Pro、Enterprise、および Education) および Windows 10 Mobile、Windows 10 に適用される UEFI 要件について説明します。
ms.assetid: 7A0B901E-1252-4F8F-B1CB-BA1AB7B01112
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c32694d75dcdd948d93f0fda50674f7fdf3abc55
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56551533"
---
# <a name="uefi-requirements-for-windows-editions-on-soc-platforms"></a>SoC のプラットフォームでの Windows のエディションの UEFI 要件


このトピックでは、デスクトップのエディション (Home、Pro、Enterprise、および Education) および Windows 10 Mobile、Windows 10 に適用される UEFI 要件について説明します。 Windows 10 Mobile のみに適用される追加の要件では、[Windows 10 Mobile の UEFI 要件](uefi-requirements-specific-to-windows-mobile.md)を参照してください。

## <a name="summary-of-requirements"></a>要件の概要


次の表は、UEFI 仕様で定義されている UEFI 対応の現在のすべての要件を示します (UEFI 2.3.1 の 2.6 の仕様)。 このテーブルで、用語*Windows の明示的な要件*プロトコルまたは Windows コンポーネントによって直接呼び出されるサービスを識別します。 これらのサービスは、Windows によって使用されることが明示的に、表示されているサービスとプロトコルの他の必要があります暗黙的または明示的に core ファームウェアの実装、EFI ドライバー、開発とデプロイ ツール チェーン。

Microsoft では、フィードバックを歓迎し、この一連の要件の実装からコメントします。 OS またはファームウェアによって要求されるされません子機 UEFI コンプライアンス要件、デバイスのこのクラスの厳密でないこれらコンプライアンス要件を持つ UEFI.org を今回の目的です。

特定の要件の詳細については、表の後のセクションを参照してください。

| 要件                               | UEFI 仕様のセクション | 説明                          |
|-------------------------------------------|----------------------------|--------------------------------|
| **EFI システム テーブル**                      | 4.3                        | Windows の明示的な要件   |
| **EFI ブート サービス**                     | 6.0                        |                                |
|   イベント、タイマー タスクのサービス          | 6.1                        |                                |
|   メモリのサービス                         | 6.2                        | Windows の明示的な要件\` |
|   プロトコル ハンドラーのサービス               | 6.3                        | Windows の明示的な要件   |
|   イメージ サービス                          | 6.4                        | Windows の明示的な要件   |
|   その他のサービス                  | 6.5                        | Windows の明示的な要件   |
| **EFI ランタイム サービス**                  | 7.0                        |                                |
|   タイム サービス                           | 7.3                        | Windows の明示的な要件   |
|   変数サービス                       | 7.2                        | Windows の明示的な要件   |
|   その他のサービス                  | 7.5                        | Windows の明示的な要件   |
| **UEFI の必要なプロトコル**               |                            |                                |
|   読み込まれる EFI のイメージのプロトコル               | 8.1                        |                                |
|   EFI に読み込まれたイメージ デバイス パス プロトコル   | 8.2                        |                                |
|   EFI デバイス パス プロトコル                | 9.2                        | Windows の明示的な要件   |
|   EFI デバイス パス ユーティリティ プロトコル      | 9.5                        |                                |
|   EFI プロトコルを圧縮解除します。                 | 18.5                       |                                |
|   EBC インタープリター プロトコル                | 20.11                      |                                |
| **必要な条件付きでの UEFI プロトコル** |                            |                                |
|   EFI 単純なテキスト入力プロトコル          | 11.3                       | Windows の明示的な要件   |
|   プロトコル EX EFI 単純なテキスト入力       | 11.2                       |                                |
|   EFI 単純なテキスト出力プロトコル         | 11.4                       |                                |
|   EFI グラフィックスの出力プロトコル            | 11.9                       | Windows の明示的な要件   |
|   EFI EDID プロトコルの検出            | 11.9.1                     |                                |
|   EFI EDID active プロトコル                | 11.9.1                     |                                |
|   EFI ブロック IO のプロトコル                   | 12.8                       | Windows の明示的な要件   |
|   EFI ディスク IO のプロトコル                    | 12.7                       |                                |
|   EFI 単純なファイル システム プロトコル         | 12.4                       |                                |
|   EFI Unicode 照合順序のプロトコル          | 12.10                      |                                |
|   単純なネットワーク プロトコルの EFI             | 21.1                       |                                |
|   EFI PXE ベースのコードのプロトコル              | 21.3                       |                                |
|   EFI ブート整合性サービス プロトコル    | 21.5                       |                                |
|   EFI シリアル IO プロトコルです。                  | 11.8                       |                                |
|   UEFI の ARM のバインド                        | 2.3.5                      | Windows の明示的な要件   |
| **セキュリティ要件**                 |                            |                                |
|   セキュア ブート                             | 27.0                       | Windows の明示的な要件   |
|   ブート マネージャーの要件               | 3.1, 3.3                   | Windows の明示的な要件   |

 

## <a name="efi-system-table-requirements"></a>EFI システム テーブルの要件


EFI システム テーブルは、実装レベルのリビジョンで標準定義に従っている必要があります。 EFI システム テーブルによって示される構成テーブルには、2 つの Guid と、次の表で説明されている、関連付けられたポインターを含める必要があります。

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
<td><p>この GUID は、プラットフォームの ACPI システムのルートの説明のポインター (RSDP) をポイントする必要があります。</p></td>
</tr>
<tr class="even">
<td>SMBIOS_Table GUID</td>
<td><p>この GUID は、SMBIOS エントリ ポイント構造体を指す必要があります。</p>
<p>Windows では、2.4 以降のリビジョン レベルでの SMBIOS 仕様が必要です。 セクション 3.2、「必要な構造およびデータ」、および 4、「準拠ガイドライン」が必要です。 Windows の SMBIOS 互換性テストは使用できます。</p></td>
</tr>
</tbody>
</table>

 

## <a name="efi-boot-services-requirements"></a>EFI ブート サービスの要件


次の表では、Windows を EFI ブート サービスの要件を示します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>EFI ブート サービス</th>
<th>要件</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>メモリのサービス</td>
<td>Windows では、すべてのメモリ サービスが必要です。</td>
</tr>
<tr class="even">
<td>プロトコル ハンドラーのサービス</td>
<td><p>Windows では、次のプロトコル ハンドラー サービスが必要です。</p>
<ul>
<li><p>OpenProtocol()</p></li>
<li><p>CloseProtocol()</p></li>
<li><p>LocateDevicePath()</p></li>
<li><p>LocateHandle()</p></li>
</ul></td>
</tr>
<tr class="odd">
<td>イメージ サービス</td>
<td><p>Windows では、次のイメージのサービスが必要です。</p>
<ul>
<li><p>ExitBootServices()</p></li>
</ul></td>
</tr>
<tr class="even">
<td>その他のブート サービス</td>
<td><p>Windows では、次の他のブート サービスが必要です。</p>
<ul>
<li><p>Stall()</p></li>
</ul>
<div class="alert">
<strong>注</strong>  決定論的 (反復可能) エラーがあるエラーの修正や取り消しを確実に実行されることができるようにする、Stall() 実装が必要です。
</div>
<div>
 
</div></td>
</tr>
</tbody>
</table>

 

## <a name="efi-runtime-services-requirements"></a>EFI ランタイム サービスの要件


次の表では、Windows を EFI ランタイム サービスの要件を示します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>EFI ランタイム サービス</th>
<th>要件</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>タイム サービス</td>
<td><p>Windows では、次の時間のサービスが必要です。</p>
<ul>
<li><p>GetTime()</p></li>
<li><p>SetTime()</p>
<div class="alert">
<strong>注</strong>  時のサービス (プラットフォームの時刻のハードウェアにアクセスするための ExitBootServices()) 前に、の起動中にのみ呼び出されます。
</div>
<div>
 
</div></li>
</ul></td>
</tr>
<tr class="even">
<td>変数サービス</td>
<td><p>すべての UEFI 変数サービスは、複数のブート デバイスとシステムのターゲット クラスのセキュリティの変数を管理する必要があります。</p></td>
</tr>
<tr class="odd">
<td>その他のランタイム サービス</td>
<td><p>Windows では、次の他のランタイム サービスが必要です。</p>
<ul>
<li><p>ResetSystem()</p>
<div class="alert">
<strong>注</strong>  ResetSystem() 実装は、リセットとシャット ダウンの両方のオプションをサポートする必要があります。
</div>
<div>
 
</div></li>
</ul></td>
</tr>
</tbody>
</table>

 

## <a name="protocol-requirements"></a>プロトコルの要件


次の表で Windows を起動中に特定の機能を実現するために必要な UEFI プロトコルについて説明します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>プロトコル</th>
<th>要件</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>グラフィックスの出力プロトコル</td>
<td><p>Windows では、グラフィックスの出力プロトコル (GOP) が必要です。 特定のフレーム バッファーの要件は次のとおりです。</p>
<ul>
<li><p>統合のディスプレイの<em>HorizontalResolution</em>と<em>VerticalResoluton</em>パネルのネイティブの解像度である必要があります。</p></li>
<li><p>外部ディスプレイ、 <em>HorizontalResolution</em>と<em>VerticalResoluton</em>ある必要があります、ディスプレイのネイティブの解像度、サポートされていない場合、ビデオの両方でサポートされている最高値アダプターおよび接続されている表示します。</p></li>
<li><p><em>PixelsPerScanLine</em>に等しくなければ<em>HorizontalResolution</em>します。</p></li>
<li><p><em>PixelFormat</em>あります<em>PixelBlueGreenRedReserved8BitPerColor</em>します。 物理フレーム バッファーが必要なことに注意してください。<em>PixelBltOnly</em>はサポートされていません。</p></li>
</ul>
<p>UEFI ブート アプリケーションの実行が引き渡さファームウェア ブート マネージャとファームウェアによって目的を問わず、フレーム バッファーをしない使用する必要があります。 フレーム バッファーは、ブート サービスが終了した後にスキャンを続ける必要があります。</p></td>
</tr>
<tr class="even">
<td>別の表示の出力</td>
<td><p>UEFI ファームウェアでは、ハードウェアでサポートされている表示コネクタを使用しての起動をサポートする必要があります。 内部のパネルが接続されていると表示されている内部パネルを使用する必要があります。 表示を物理的に接続されているすべての出力には、起動画面を表示する必要があります。 接続が表示されたら、UEFI ファームウェア必要があります。</p>
<ul>
<li><p>ネイティブの解像度を特定できる場合は、表示のネイティブ モードで出力を初期化します。</p></li>
<li><p>ネイティブ モードが使用できない場合は、最高の互換性のあるモードに初期化する必要があります。</p></li>
<li><p>表示機能を決定できない場合、限り (通常は 640 x 480 または 1024 x 768、60 hz) 同数のモニターと互換性のあることがわかっているモードで接続されているモニターを初期化する必要があります。</p></li>
</ul></td>
</tr>
<tr class="odd">
<td>ブート時に入力します。</td>
<td><p>EFI の単純なテキスト入力プロトコルは、組み込みキーボードがあるか、キーボードが接続されているシステムでブート選択やその他のメニューの選択を行う必要があります。 キーボードのないシステムでは、3 つのボタンは、ブート環境で推奨されます。</p>
<ul>
<li><p>[スタート] ボタン</p></li>
<li><p>Volume Up ボタン</p></li>
<li><p>Volume Down ボタン</p></li>
</ul>
<p>ボタンを押すようは、次のキーボードのキーにそれぞれマップ EFI の単純なテキスト入力プロトコルを使って報告する必要があります。</p>
<ul>
<li><p>Windows キー</p></li>
<li><p>上方向キー</p></li>
<li><p>下方向キー</p></li>
</ul></td>
</tr>
<tr class="even">
<td>ローカル ストレージのブート</td>
<td><p>Windows では、I/O のプロトコルをブロックし、デバイス パスのプロトコルを EFI システム パーティションと Windows OS のパーティションを含む記憶域ソリューションのサポートが必要です。 Wear 負荷平準化/その他のフラッシュの管理が必要なフラッシュ記憶域から起動すると、これは (UEFI アプリケーション) ではなく、ファームウェアで実装する必要があります。</p></td>
</tr>
</tbody>
</table>

 

## <a name="security-requirements"></a>セキュリティ要件


Windows では、セキュア ブート、メジャー ブート、暗号化、およびデータ保護の分野におけるセキュリティの要件があります。 次の表では、これらの要件が詳しく説明します。 さらに、どの SoC ハードウェアを防ぎます (TPM、RTC など) は、既存の標準に準拠してこれらの領域の他の要件を開発しています。 これらは、テーブルの最後に説明します。

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
<td>全般的な情報</td>
<td><ul>
<li><p>要件 1:必須。 プラットフォームは、このセクションで指定されたすべての要件を準拠している必要があります。</p></li>
<li><p>要件 2:必須。 プラットフォームは、UEFI クラス 3 つインストールされているか、インストール可能ななしの互換性サポート モジュールでなければいけない。 BIOS のエミュレーションと従来の PC/ブートでは無効する必要があります。</p></li>
</ul></td>
</tr>
<tr class="even">
<td>UEFI セキュア ブート</td>
<td><ul>
<li><p>要件 3:必須。 定義されている UEFI v2.3.1 セクション 27 とセキュア ブートを有効になっている出荷する必要があり、マシンを安全に起動するために必要な署名データベース (EFI_IMAGE_SECURITY_DATABASE) でプロビジョニング済み。 署名のデータベースの初期コンテンツはに基づいて決定されます、OEM によって必要なサード パーティの UEFI ドライバー、リカバリーのニーズと、コンピューターにインストールされている OS ブート ローダーが Microsoft から提供された EFI_CERT_X509 署名に指定されます。 存在するものと追加のシグネチャはありません。</p></li>
<li><p>要件 4:必須。 UEFI の「許可されていない」署名データベース (EFI_IMAGE_SECURITY_DATABASE1) の存在が必要です。</p></li>
<li><p>要件 5:必須。 Microsoft 提供の UEFI KEK は、UEFI KEK データベースで記載するものとします。 存在するものと追加の Kek はありません。 Microsoft では、EFI_CERT_X509 署名の形式で KEK を提供します。</p></li>
<li><p>要件 6:必須。 A PK<em><sub>pub</sub></em> 存在し、ファームウェアのフラッシュに格納されているキーがあるものとします。</p>
<div class="alert">
<strong>注</strong>  ため PK<em><sub>priv</sub> </em> (PK に秘密キーの対応する<em><sub>pub</sub></em>) セキュア ブートの制御PK でプロビジョニングされたすべてのデバイスのポリシーを<em><sub>pub</sub></em>、保護操作と使用する必要がありますは厳密に保護します。
</div>
<div>
 
</div></li>
<li><p>要件 7:必須。 最初の署名データベースは、フラッシュのファームウェアに格納して、OEM で署名されたファームウェア更新でのみ、または UEFI 変数書き込みの認証を更新することがあります。</p></li>
<li><p>要件 8:必須。 署名の検証に失敗したブート パス内のイメージを実行する必要がないと失敗の理由は、EFI_IMAGE_EXECUTION_TABLE に追加する必要があります。 さらに、このような状況で推奨されるアプローチでは、UEFI ブート マネージャーが、OEM 固有の戦略に従って回復を開始します。</p></li>
<li><p>要件 9:必須。 ユーザー オーバーライドを物理的に存在する必要がありますの署名の検証に失敗したイメージを UEFI できません。</p></li>
<li><p>要件 10:省略可能。 OEM は PK へのアクセスをいずれかでセキュア ブートをオフに物理的に存在するユーザーの機能を実装できます<em><sub>priv</sub></em> またはファームウェア設定を使用して物理的な操作です。 プラットフォーム固有の方法 (管理者パスワード、スマート カード、静的な構成など) でファームウェアのセットアップへのアクセスを保護することがあります。</p></li>
<li><p>要件 11:要件 10 が実装されている場合は必須です。 セキュア ブートが無効になっている場合、すべての既存の UEFI 変数はアクセスできません。</p></li>
<li><p>要件 12:省略可能。 OEM は、物理的に存在するユーザーの間でファームウェアのセットアップで 2 つのセキュア ブート モードを選択する機能を実装できます。"Custom"と"Standard"。 カスタム モードではより柔軟として次のように指定できます。</p></li>
<li><p>13 の要件:要件 12 が実装されている場合は必須です。 特定の所有者を設定して、カスタム モードでは無効になっているセキュア ブートを再度有効にできるものと<em>PK</em>します。 UEFI 仕様の v2.3.1 の 27.5 セクションで定義されている、管理が続行されます。ファームウェア OS/キーの交換します。 カスタム モードで、デバイスの所有者は、署名データベースでの署名が選択したを設定できます。</p></li>
<li><p>14 の要件:要件 12 が実装されている場合は必須です。 ファームウェア セットアップには、セキュア ブートがオンの場合、これは標準またはカスタム モードで運用されている場合を示すものとします。 ファームウェアのセットアップでは、カスタムから標準モードに戻すためのオプションが提供されます。</p></li>
<li><p>15 の要件:必須。 ファームウェアの設定は、出荷時設定にリセットされます、すべてのカスタム セット保護されている変数が消去され、元の PK<em><sub>pub</sub></em> 元と共にが再確立されている必要があります製造元から提供された署名データベース。</p></li>
<li><p>16 の要件:必須。 ドライバーの署名は Authenticode オプション (WIN_CERT_TYPE_PKCS_SIGNED_DATA) を使用します。</p></li>
<li><p>17 の要件:必須。 (作成および開始するか、ブート時に開始されていないイメージに関する情報の格納) EFI_IMAGE_EXECUTION_INFO_TABLE をサポートします。</p></li>
<li><p>18 の要件:必須。 (承認および署名データベースは禁止されています) EFI_IMAGE_SECURITY_DATABASE の GetVariable() をサポートします。</p></li>
<li><p>19 の要件:必須。 (承認両方および署名データベースは禁止されています)、EFI_IMAGE_SECURITY_DATABASE のサポートの SetVariable() を Microsoft KEK を使用して認証します。</p></li>
<li><p>20 の要件:必須。 EFI_HASH_SERVICE_BINDING_PROTOCOL:サービスのサポート:CreateChild()、DestroyChild() します。</p></li>
<li><p>21 の要件:必須。 EFI_HASH_PROTOCOL します。 サービスのサポート:Hash() します。 SHA_1 と sha-256 ハッシュ アルゴリズムをサポートします。 長いメッセージを少なくとも 10 バイトの引き渡しはサポートする必要があります。</p></li>
</ul></td>
</tr>
<tr class="odd">
<td>メジャー ブートの UEFI</td>
<td><p>次の要件は、TCG TPM の実装の必要性を意味しません影響を受ける領域の同等の機能が必要であるはただし意味します。</p>
<p>プラットフォームのサポートは、セキュリティで保護された実行環境で実行する、暗号化の高速化エンジンの上に階層化および分離ストレージを利用して、TPM のファームウェアの実装によって提供されます。 Microsoft は、参照のソフトウェア ベンダーで使用するため、このような TPM 実装を提供することができます。 さらに議論の対象になります。</p>
<ul>
<li><p>22 の要件:必須。 プラットフォームはで指定された EFI プロトコルに準拠している、 <a href="https://go.microsoft.com/fwlink/p/?LinkId=528536" data-raw-source="[UEFI Trusted Execution Environment EFI Protocol](https://go.microsoft.com/fwlink/p/?LinkId=528536)">UEFI 信頼できる実行環境の EFI プロトコル</a>します。</p></li>
<li><p>23 の要件:必須。 プラットフォームは、TCG EFI プラットフォームの仕様を加え、次に従わなければいけない。</p>
<ul>
<li><p>ツリーの EFI プロトコル、PK のダイジェストで定義されているインターフェイスをサポートするプラットフォームで<em><sub>pub</sub></em>  EV_EFI_VARIABLE_CONFIG イベントとしての TPM PCR [03] に拡張されます。</p></li>
<li><p>EV_EFI_VARIABLE_CONFIG イベントとしてメジャー ブートでの承認済み署名データベース (UEFI 仕様の v2.3.1 の高は 27.8」セクションを参照) の一覧のコンテンツのダイジェストを拡張する必要があります。 拡張操作は、TPM PCR [03] になります。</p></li>
<li><p>UEFI クライアントに読み取りおよび EFI_IMAGE_SECURITY_DATABASE 変数を使用して証明書の一覧を解析および拡張の値に対してダイジェストを検証することはできます。</p></li>
<li><p>TCG_PCR_EVENT ダイジェスト値は、sha-256、not SHA 1 でなければいけない。</p></li>
</ul></li>
<li><p>24 の要件:必須。 プラットフォームで定義されている MemoryOverwriteRequestControl を実装する必要があります、 <a href="https://go.microsoft.com/fwlink/p/?LinkId=528539" data-raw-source="[TCG Platform Reset Attack Mitigation Specification](https://go.microsoft.com/fwlink/p/?LinkId=528539)">TCG プラットフォーム リセット攻撃の軽減策仕様</a>します。</p></li>
</ul></td>
</tr>
<tr class="even">
<td>暗号化</td>
<td><ul>
<li><p>25 の要件:必須。 プラットフォームは、暗号化ハッシュ操作のオフロード用 EFI_HASH_PROTOCOL (UEFI v2.3.1 セクション 27.4) を提供するものとします。 Sha-256 をサポートする必要があります。</p></li>
<li><p>26 の要件:必須。 プラットフォームは Microsoft によるサポート<a href="uefi-entropy-gathering-protocol.md" data-raw-source="[EFI_RNG_PROTOCOL](uefi-entropy-gathering-protocol.md)">EFI_RNG_PROTOCOL</a>のエントロピの os 起動前の読み取り。</p></li>
</ul></td>
</tr>
<tr class="odd">
<td>データ保護</td>
<td><ul>
<li><p>27 の要件:必須。 プラットフォームには、次の UEFI 変数の属性セットの任意の組み合わせで EFI 変数をサポートする必要があります。</p>
<ul>
<li><p>EFI_VARIABLE_BOOTSERVICE_ACCESS</p></li>
<li><p>EFI_VARIABLE_NON_VOLATILE</p></li>
<li><p>EFI_VARIABLE_AUTHENTICATED_WRITE_ACCESS</p></li>
</ul></li>
</ul></td>
</tr>
<tr class="even">
<td>その他のセキュリティ要件</td>
<td><p>Windows では、SoC プラットフォームで、次の追加要件が必要です。</p>
<ul>
<li><p>Microsoft では、UEFI のプラットフォームからエントロピを収集するためのプロトコルを定義します。 UEFI 要件ではありません、中にこのプロトコルは SoC プラットフォーム上で Windows に必要です。 このプロトコルの詳細については、<a href="uefi-entropy-gathering-protocol.md" data-raw-source="[UEFI entropy gathering protocol](uefi-entropy-gathering-protocol.md)">プロトコルを収集する UEFI エントロピ</a>を参照してください。</p></li>
<li><p>UEFI 署名データベースの更新。 認証済みの変数を更新する新しいメカニズムは UEFI 2.3.1 のセクション 27 で採用されています。 このメカニズムは、Windows で必要です。</p></li>
<li><p>信頼できる実行環境。 Microsoft は、信頼できる実行環境 (ツリー) Trusted Computing Group (TCG) トラステッド プラットフォーム モジュール (TPM) のサブセットと似た機能を操作する EFI プロトコルを開発しました。 EFI プロトコルは、大規模な程度、「TCG EFI プロトコル」、バージョン 1.2 改訂 1.00、2006 年 6 月 9 日、Trusted Computing Group 者を活用します。</p>
<p>詳細については、 <a href="https://go.microsoft.com/fwlink/p/?LinkId=528536" data-raw-source="[UEFI Trusted Execution Environment EFI Protocol](https://go.microsoft.com/fwlink/p/?LinkId=528536)">UEFI 信頼できる実行環境の EFI プロトコル</a>します。</p></li>
</ul></td>
</tr>
</tbody>
</table>

 

## <a name="firmware-boot-manager-requirements"></a>ファームウェア ブート マネージャーの要件


ファームウェア ブート マネージャーでは、仕様のセクション 3.3 で定義されている既定のブートの動作をサポートする必要があります。 さらに、複数のブートのサポート、グローバルに定義されている変数と仕様のセクション 3.1 のブート マネージャーの要件が必要です。

## <a name="uefi-arm-binding-requirements"></a>UEFI ARM バインディング要件


UEFI ARM バインドには、UEFI 仕様に準拠するために必要な ARM プラットフォームに固有の要件が含まれています。 Windows では、ARMv7 に適用される ARM バインド内のすべてが必要です。 Windows では、ARMv7 より前の何もサポートしていない、ため ARMv6k と下に固有の要件、バインドでは省略可能です。

バインディングは、たとえば、MMU が構成、および物理メモリをする方法をマップする必要がありますを指定します。 バインディングには、こと UEFI プロトコルへの呼び出しであり、サービス実行 ARM ISA のみで Thumb2 またはつまみで実行されているソフトウェアは UEFI 関数を呼び出す前に、ARM モードに切り替えるしなければを意味も指定します。

## <a name="uefi-arm-multiprocessor-startup-requirements"></a>UEFI ARM マルチプロセッサのスタートアップの要件


Microsoft では、マルチプロセッサ UEFI プラットフォームで複数の ARM コアを開始するためのプロトコルを開発しました。 このプロトコルがサポートしていない ARM プラットフォームで Windows に必要な[電源状態の調整インターフェイス (PSCI)](https://go.microsoft.com/fwlink/p/?LinkId=528534)します。 PSCI をサポートしているプラットフォームでは、このプロトコルは使用しないでください。 このプロトコルの詳細については、次を参照してください。、 [UEFI ARM ベースのプラットフォームでマルチプロセッサ スタートアップ](https://go.microsoft.com/fwlink/p/?LinkId=528533)ACPI コンポーネント アーキテクチャ (ACPICA) の Web サイト上のドキュメント。

## <a name="platform-setup-requirements"></a>プラットフォームのセットアップ要件


ファームウェアが、OS ローダーを処理する前に明確に定義された状態にシステムのハードウェアを配置する責任を負います。 次の表では、関連するプラットフォームのセットアップ要件を定義します。

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
<td>ブート パス</td>
<td>ファームウェアでは、Windows の UEFI を使用して、ブート デバイスにアクセスして、カーネルを読み込むことがポイントするプラットフォームを初期化する必要があります。 ブート デバイスからの読み取り、階層に関係する任意のデバイスは、出勤、パフォーマンスと電源に関する考慮事項を指定した、妥当なレートでの電源をする必要があります。 自体ベースのプロセッサ コアを出勤も、電源、妥当な速度をシステムが、バッテリを使ったりすることがなく、適切なタイミングで起動できるようにする必要があります。</td>
</tr>
<tr class="even">
<td>コアのシステム リソース</td>
<td><p>ACPI テーブルを使用して OS に公開されているコアのシステム リソースを電源オンになり出勤している必要があります。 コアのシステム リソースは、割り込みコント ローラー、タイマーおよび DMA コント ローラー、OS で管理する必要があります。</p>
<p>さらに、OS に関連するデバイス ドライバに対してマスクを解除し、デバイスの割り込みを再度有効にするまでは、割り込みを ExitBootServices() への呼び出しによってマスクする必要があります。 ブート サービス中には、割り込みが有効になって、ファームウェアがそれらを管理することと見なされます。</p></td>
</tr>
<tr class="odd">
<td>デバッグ</td>
<td>Windows ホスト (XHCI)、USB 2 ホスト (EHCI) 1、IEEE 1394、シリアル、USB 3 経由でデバッグをサポートし、USB 関数インターフェイス (だけでなく PCI イーサネット アダプター)。 これらの少なくとも 1 つあり必要がありますの電源、出勤して OS ハンドオフする前に、ファームウェアによって初期化します。 どちらのオプションが提供される、デバッグ目的で、公開されているポートが必要になりますし、コント ローラーがメモリ マップする必要がありますまたは専用 (非共有) の周辺機器バスによって接続されるようにします。</td>
</tr>
<tr class="even">
<td>その他のプラットフォームのセットアップ要件</td>
<td>OS ローダーに処理を制御する前に、ファームウェアでは、pin 多重化とパッドの構成を完了する必要があります。</td>
</tr>
</tbody>
</table>

 

## <a name="installation-requirements"></a>インストール要件


Windows では、OS のパーティションの GPT パーティションのストレージ ソリューションに存在する必要があります。 MBR パーティションのストレージは、データ ストレージとして使用できます。 UEFI 仕様で定義されている、UEFI プラットフォーム専用のシステム パーティションが必要です。 Windows が必要な専用のシステム パーティション、EFI システム パーティション (ESP) と呼ばれます。

## <a name="hardware-security-test-interface-hsti-requirement"></a>ハードウェア セキュリティ テスト インターフェイス (HSTI) の要件


プラットフォームは、ハードウェア セキュリティ テスト インターフェイスを実装する必要があり、プラットフォームがドキュメントとで指定されているツールを共有するために必要な[ハードウェア セキュリティ テストの容易性の仕様](https://docs.microsoft.com/windows-hardware/test/hlk/testref/hardware-security-testability-specification)します。

## <a name="related-topics"></a>関連トピック

[SoC のプラットフォームで Windows の最小の UEFI 要件](minimum-uefi-requirements-for-windows-on-soc-platforms.md)  

[Windows 10 Mobile の UEFI 要件](uefi-requirements-specific-to-windows-mobile.md)  

[USB サポートが点滅の UEFI 要件](uefi-requirements-for-usb-flashing-support.md)  



