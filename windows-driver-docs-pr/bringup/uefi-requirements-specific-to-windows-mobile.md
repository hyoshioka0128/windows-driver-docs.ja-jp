---
title: Windows 10 Mobile の UEFI 要件
description: UEFI 要件に加えて Windows のすべてのエディションに適用される、Windows 10 Mobile デバイスは、このトピックで説明する追加の要件を満たす必要があります。
ms.assetid: 12a03f5b-1717-4daf-90ef-5e530f72b19e
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1c5bac94d5be12ec499ca5638f6885de5cd55f7b
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56556672"
---
# <a name="uefi-requirements-for-windows-10-mobile"></a>Windows 10 Mobile の UEFI 要件


UEFI 要件だけでなく[Windows のすべてのエディションに適用される UEFI 要件](uefi-requirements-that-apply-to-all-windows-platforms.md)、Windows 10 Mobile を実行しているデバイスは、このトピックで説明する追加の要件を満たすも必要があります。

## <a name="requirements-that-expand-on-the-general-uefi-requirements-for-all-windows-editions"></a>すべての Windows エディションの一般の UEFI 要件の展開要件


次の表で説明されているこれらの要件で展開する Windows 10 Mobile の UEFI 要件[Windows のすべてのエディションに適用される UEFI 要件](uefi-requirements-that-apply-to-all-windows-platforms.md)します。

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
<td>GPT</td>
<td>デバイスは、GUID パーティション テーブル (GPT) からを起動できる必要があります。 さらに、デバイスがプライマリの両方を含める必要があり、5.3 のセクションで説明したようバックアップ GPT UEFI 仕様の「GUID パーティション テーブル ディスク レイアウト」のタイトルします。</td>
</tr>
<tr class="even">
<td>変数サービス</td>
<td>変数サービスは、Microsoft で使用するため、64 KB 以上の非揮発性ストレージを提供する必要があります。 さらに、記憶域のマーク付きの場所でこれらの変数サービスを実装しなければなりません。 この要件は、キーと点滅して新しい変数を全体の記憶域を許可して、全体の記憶域が点滅しているときにこれらの変数の除外を許可する、セキュア ブートの他のパラメーターを格納するための十分な領域がある必要があります。 Microsoft では、BOM のコストとハードウェアの複雑さを減らすためには、変数のサービスがデバイスに余分なフラッシュのパーツの追加によって実装されていませんする必要がありますが必要です。</td>
</tr>
<tr class="odd">
<td>単純なテキスト入力プロトコル</td>
<td><p>次の物理的なキーは、次の関数にマップされます。</p>
<ul>
<li>音量を上げる:上方向キー</li>
<li>音量を上げる:下方向キー</li>
<li>カメラ:以下に</li>
<li>電源ボタンをクリックします。中断</li>
</ul></td>
</tr>
<tr class="even">
<td>メモリのサービス</td>
<td>GetMemoryMap() 関数は、物理メモリのセクション 6.2 で指定したとおり、プラットフォームの完全な範囲を返す必要があります&quot;メモリ サービス&quot;UEFI 仕様の。</td>
</tr>
<tr class="odd">
<td>EFI ブロック I/O プロトコル</td>
<td>EFI ブロック I/O プロトコルでは、ネイティブのセクター サイズに基づいて、記憶域デバイスのサイズを報告する必要があります。 たとえば、4 KB セクター デバイス必要がありますと報告していない 512 バイト セクター デバイス。</td>
</tr>
</tbody>
</table>



## <a name="requirements-specific-to-windows-10-mobile"></a>Windows 10 Mobile に固有の要件


次の表では、Windows 10 Mobile に固有の要件について説明します。

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
<td>UEFI ドライバー</td>
<td>UEFI ドライバーは、UEFI ファームウェアに埋め込む必要があります。</td>
</tr>
<tr class="even">
<td>USB 関数プロトコル</td>
<td>UEFI ファームウェアでは、UEFI USB 関数のプロトコルに準拠したドライバーを含める必要があります。 詳細については、次を参照してください。 <a href="uefi-usb-function-protocol.md" data-raw-source="[UEFI USB function protocol](uefi-usb-function-protocol.md)">UEFI USB 関数プロトコル</a>します。 UEFI で USB 列挙は、Microsoft コードによってのみ処理されるものとします。</td>
</tr>
<tr class="odd">
<td>バッテリの充電プロトコル</td>
<td><p>デバイスで Microsoft UEFI バッテリの充電中のアプリケーションを使用する場合、UEFI ファームウェアは、UEFI バッテリを充電プロトコルを実装するドライバーを含める必要があります。 デバイスが準拠する必要があります、デバイスは、Microsoft UEFI バッテリが充電ソフトウェアに渡し、前に、 <em>USB バッテリの充電 v1.2 仕様</em>します。 詳細については、次を参照してください。 <a href="uefi-battery-charging-protocol.md" data-raw-source="[UEFI battery charging protocol](uefi-battery-charging-protocol.md)">UEFI バッテリの充電プロトコル</a>と<a href="battery-charging-in-the-boot-environment.md" data-raw-source="[Battery charging in the boot environment](battery-charging-in-the-boot-environment.md)">ブート環境でバッテリが充電中</a>します。</p>
<div class="alert">
<strong>重要な</strong>この要件は、デバイスが Microsoft UEFI バッテリが充電アプリケーションを使用している場合にのみ適用されます。 デバイスは、Microsoft から提供されたアプリケーションではなくカスタム UEFI バッテリの充電アプリケーションを使用している場合、UEFI バッテリの充電ドライバーする必要があります、UEFI バッテリを充電プロトコルを実装していません。
</div>
<div>

</div></td>
</tr>
<tr class="even">
<td>電源状態のプロトコルを表示します。</td>
<td><p>デバイスで Microsoft UEFI バッテリが充電アプリケーションを使用する場合、UEFI ファームウェアは、UEFI ディスプレイの電源状態のプロトコルを実装するドライバーを含める必要があります。 画面をオンにし、もう一度 UEFI 環境での充電中にバックライトをオフにして、このプロトコルが使用されます。 このプロトコルの詳細については、次を参照してください。 <a href="uefi-display-power-state-protocol.md" data-raw-source="[UEFI display power state protocol](uefi-display-power-state-protocol.md)">UEFI 電源状態のプロトコルを表示する</a>します。 UEFI バッテリが充電アプリケーションでこのプロトコルの使用方法の詳細については、次を参照してください。 <a href="architecture-of-the-uefi-battery-charging-application.md" data-raw-source="[Architecture of the UEFI battery charging application](architecture-of-the-uefi-battery-charging-application.md)">UEFI バッテリが充電アプリケーションのアーキテクチャ</a>します。</p>
<div class="alert">
<strong>重要な</strong>この要件は、デバイスが Microsoft UEFI バッテリが充電アプリケーションを使用している場合にのみ適用されます。 デバイスは、カスタム UEFI バッテリが充電、Microsoft が提供するアプリケーションではなくアプリケーションを使用している場合、UEFI バッテリの充電ドライバーする必要があります UEFI ディスプレイの電源状態プロトコルを実装していません。
</div>
<div>

</div></td>
</tr>
<tr class="odd">
<td>電力の最適化</td>
<td>電力の過剰使用に電源が最適化されたを UEFI 環境があることをお勧めします。 これにより、デバイスが起動中にできるだけ小さな電源として使用する (UEFI で課金) 場合は、できるだけ早く課金できます。</td>
</tr>
<tr class="even">
<td>予約済みのハードウェア ボタン</td>
<td><p>ブート プロセス中には、Microsoft をスタンドアロン押したとき、power、ボリュームを定義し、下向きの矢印ボタンをトリガーとしてボリュームは、いくつかの Microsoft 提供の UEFI アプリケーションを起動するために使用できます。 電源のボリュームまたはボリューム ダウンする必要があります、Oem をオーバー ロードしないカスタム アクションを実行または他の UEFI アプリケーションを開始する起動中にボタンをクリックします。</p>
<p>Microsoft 提供の UEFI アプリケーションは、これらのボタンによって開始されたを次に示します。</p>
<ul>
<li>音量を上げる:Microsoft が提供 UEFI アプリケーションを点滅します。</li>
<li>音量を下げる:Microsoft 提供の UEFI デバイスは、アプリケーションをリセットします。</li>
<li>電源。開発者が Microsoft から提供された boot メニュー アプリケーション。</li>
</ul>
<div class="alert">
<strong>注:</strong><br/><p>Oem する必要がありますもいることを確認するボリュームとボリューム ダウン ボタンの上向き矢印のように関数および下矢印キーはそれぞれ、UEFI 環境でします。</p>
</div>
<div>

</div></td>
</tr>
<tr class="odd">
<td>OEM の UEFI アプリケーション</td>
<td><p>Oem は、製造とデバイスのサービスで支援する UEFI アプリケーションを追加できます。 これらのアプリケーションでは、次の制限があります。</p>
<ul>
<li><p>UEFI アプリケーションでは、起動時には影響はありません。</p></li>
<li><p>UEFI アプリケーションは、許可されている署名データベース (db) の UEFI 変数内にある証明書で署名する必要があります。</p></li>
<li><p>UEFI アプリケーションは、次の方法のいずれかで動作する必要があります。</p>
<ul>
<li><p>必要があります<em>決して</em>メイン OS をブート時に実行または OS を更新します。</p>
<p>- または -</p></li>
<li><p>必要があります<em>常に</em>メインの OS のブート時に実行または OS を更新します。</p></li>
</ul></li>
</ul>
<p>UEFI アプリケーション<em>は許可されません</em>場合があります実行されないことがありましたメイン OS を起動中に実行や OS を更新します。 デバイスの暗号化を有効にすると、トラステッド プラットフォーム モジュール (TPM)、ブート シーケンスを格納して、デバイスの暗号化が有効にした後に変更できません。 たとえば、ブート シーケンス<em>UEFI ファームウェア</em> &gt; <em>アプリケーション A</em> &gt; bootarm.efi、削除してから削除<em>アプリケーション A</em> 、ブートからシーケンスは、TPM の開封に失敗した場合になります。</p>
<p>さらに、複数の UEFI アプリケーションがある場合は、ファームウェアによって必要があります、アプリケーションの一貫した順序を確認します。 たとえば、ブート シーケンス<em>UEFI ファームウェア</em> &gt; <em>アプリケーション A</em> &gt; <em>アプリケーション B</em> &gt; bootarm.efi しブート シーケンスを変更する<em>UEFI ファームウェア</em> &gt; <em>アプリケーション B</em> &gt; <em>アプリケーション A</em> &gt; bootarm.efiTPM は、A と B のアプリケーションは、db 内の異なるエントリにチェーンする場合の開封に失敗した場合の考えられる原因。</p>
<p>ブート アプリケーションの署名証明書の更新は、TPM の問題は発生しません。 ただし、UEFI アプリケーションは、db では、別のエントリにチェーンするために再署名は場合、しこれもにより、TPM の開封に失敗した場合します。</p></td>
</tr>
</tbody>
</table>



## <a name="related-topics"></a>関連トピック
[SoC のプラットフォームで Windows の最小の UEFI 要件](minimum-uefi-requirements-for-windows-on-soc-platforms.md)  
[すべての Windows エディションに適用される UEFI 要件](uefi-requirements-that-apply-to-all-windows-platforms.md)  
[USB サポートが点滅の UEFI 要件](uefi-requirements-for-usb-flashing-support.md)  



