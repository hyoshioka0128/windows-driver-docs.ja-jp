---
title: ドライバーの検証ツールのオプション
description: Driver Verifier のオプションとルール クラス
ms.assetid: f251fe07-e68e-4d93-9aa5-9a0bc818756d
keywords:
- Driver Verifier の WDK、オプションの一覧
- WDK の Driver Verifier のエラー
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1c7c76a18706ffebe56c74d189e4c9a3297c1c42
ms.sourcegitcommit: 179f9119b6c7888ea18281f6d5d11d62ac45b58d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/22/2019
ms.locfileid: "66035120"
---
# <a name="driver-verifier-options-and-rule-classes"></a>Driver Verifier のオプションとルール クラス


このトピックでは、Driver Verifier 内のルール クラス、省略可能な機能について説明します。 参照してください[標準設定](#standard-settings)標準設定を使用するときに含まれるオプションの一覧についてはします。

> [!NOTE]
> いくつか[自動チェック](automatic-checks.md)ドライバーに対しては検証されている、選択したオプションに関係なく、常に実行されます。 ドライバー不適切な IRQL でメモリを使用して、不適切な呼び出しまたはスピン ロックとメモリの割り当てを解放、不適切なスタックの切り替え、または最初の削除タイマーなしのメモリ プールを解放、Driver Verifier はこの動作を検出します。 ドライバーが読み込まれると、Driver Verifier はそのリソースが解放が正しくことを確認します。

## <a name="enabling-rule-classes-with-ruleclasses"></a>/Ruleclasses ルール クラスを有効にします。

Windows 10、17627 以降のバージョン以降、次の構文と規則クラスを有効にできます。

`/ruleclasses or /rc [<ruleclass_1> <ruleclass_2> ... <ruleclass_k>]`

注意してください (下正の 10 進整数で表される) 複数のクラスを有効にする場合、各整数を空白文字で区切ります。 

以下は、これらのルール クラスの説明を確認できます。

### <a name="standard-rule-classes"></a>標準の規則クラス

| ルール クラス | 10 進数の ID |
| -- | -- |
| 特別なプール        | 1 |
| 強制 IRQL 検査 | 2 |
| プールのトラック       | 4 |
| I/O の検証    | 5 |
| デッドロックの検出  | 6 |
| DMA のチェック | 8 |
| セキュリティの検査 | 9 |
| その他の検査 | 12 |
| DDI 準拠の検査 | 18 |
| WDF の検証 | 34 |

### <a name="additional-rule-classes"></a>追加の規則クラス

これらのルール クラスは、特定のシナリオをテストします。 ルール クラスでマークされます (\*) I/O の検証 (5) に自動的に有効にする必要があります。 フラグが付いた (\**) 個々 のルールの無効化をサポートします。

| ルール クラス | 10 進数の ID |
| -- | -- |
| ランダム化された低リソース シミュレーション        | 3 |
| 強制的に保留中の I/O 要求 (*) | 10 |
| IRP ログ       | 11 |
| 不変の MDL スタック (*) のチェック    | 14 |
| 不変の MDL ドライバー (*) のチェック  | 15 |
| Power framework 遅延ファジー テスト | 16 |
| ポート/ミニポート インターフェイス チェック | 17 |
| 体系的な低リソースのシミュレーション | 19 |
| DDI 準拠のチェック (追加) | 20 |
| カーネル同期遅延ファジー テスト | 24 |
| VM スイッチ検証 | 25 |
| コードの整合性チェック | 26 |

## <a name="optional-feature-and-rule-class-descriptions"></a>省略可能な機能とルール クラスの説明 

[特別なプール](special-pool.md)
    
このオプションを有効にすると、ドライバーの検証ツールは、特別なプールからほとんどのドライバーのメモリ要求を割り当てます。 この特別なプールでは、メモリ オーバーラン、メモリ アンダーラン、既に解放されたメモリへのアクセスが監視されます。

[強制 IRQL 検査](force-irql-checking.md)

このオプションを有効にすると、ドライバーの検証ツールは、ページング可能なコードを無効にすること、ドライバーでメモリ不足状態を配置します。 ドライバーが不適切な IRQL で、またはスピン ロックを保持したままでページ メモリにアクセスしようとすると、ドライバーの検証ツールはこの動作を検出します。

[低リソース シミュレーション](low-resources-simulation.md)(と呼ばれる*低リソース シミュレーションをランダム化*で Windows 8.1)

このオプションを有効にすると、ドライバーの検証ツールは、プールの割り当て要求およびその他のリソース要求にランダムに失敗します。 システムでこれらの割り当てエラーを引き起こすことで、ドライバーの検証ツールはリソース不足の状況でのドライバーの能力をテストします。

[プールの追跡](pool-tracking.md)

このオプションを有効にすると、ドライバーの検証ツールがアンロードされるときに、ドライバーがそのすべてのメモリ割り当てを解放してかどうかを確認します。 これによってメモリ リークが明らかになります。

[I/O の検証](i-o-verification.md)

このオプションがアクティブで、Driver Verifier はから特別なプールの場合は、ドライバーの Irp を割り当てますおよびドライバーの I/O 処理を監視します。 これによって、I/O ルーチンの不適切な使用や不整合な使用が検出されます。

[デッドロックの検出](deadlock-detection.md)

(Windows XP 以降)このオプションがアクティブで、Driver Verifier は、スピン ロック、ミュー テックス、および高速なミュー テックスのドライバーの使用を監視します。 これを検出したかどうか、ドライバーのコードには、ある時点で、デッドロックを発生させる可能性が。

[強化された I/O の検証](enhanced-i-o-verification.md)

(Windows XP 以降)このオプションがアクティブな場合は、Driver Verifier は複数の I/O マネージャー ルーチンの呼び出しを監視し、PnP Irp、電源 Irp および WMI の Irp のストレスのテストを実行します。 Windows 7 および Windows オペレーティング システムの以降のバージョンでは、強化された I/O の検証のすべての機能はの一部として含める[I/O の検証](i-o-verification.md)使用可能なもドライバーの検証ツールでこのオプションを選択するために必要ではありませんマネージャーまたはコマンドラインから。

[DMA の検証](dma-verification.md)

(Windows XP 以降)このオプションがアクティブで、Driver Verifier は、DMA ルーチンのドライバーの使用を監視します。 これによって、DMA バッファー、アダプター、マップ レジスタの不適切な使用が検出されます。

[セキュリティ チェック](security-checks.md)

(Windows Vista 以降)このオプションがアクティブで、Driver Verifier は、カーネル モードのルーチンによってユーザー モード アドレスへの参照などのセキュリティの脆弱性につながる一般的なエラーを検索します。

[その他の検査](miscellaneous-checks.md)

(Windows Vista 以降)このオプションがアクティブな場合は、Driver Verifier は、解放されたメモリの取り扱いミスなどのドライバー クラッシュの一般的な原因を探します。

[保留中の I/O 要求を強制する](force-pending-i-o-requests.md)

(Windows Vista 以降)Driver Verifier テスト状態へのドライバーの応答でこのオプションがアクティブで\_保留の状態を返すことによって値を返す\_ランダムの呼び出しに対して保留[**保留**](https://msdn.microsoft.com/library/windows/hardware/ff548336).

[IRP ログ](irp-logging.md)

(Windows Server 2003 以降)このオプションがアクティブで、Driver Verifier は Irp のドライバーの使用を監視し、IRP の使用のログを作成します。

[ディスクの整合性チェック](disk-integrity-checking.md)

(Windows Server 2003 で導入されました。 いない Windows 7 で使用できる以降。)このオプションがアクティブな場合は、Driver Verifier は、ハード ディスク アクセスを監視し、ディスクがそのデータを正しく保持するかどうかを検出します。

[SCSI の検証](scsi-verification.md)

(Windows XP 以降)このオプションがアクティブな場合は、Driver Verifier は、SCSI ミニポート ドライバーのエクスポートされた SCSI ポート ルーチン、過剰な遅延は、不適切な使用を監視し、SCSI の不適切な処理を要求します。

[Storport の検証](dv-storport-verification.md)

(Windows Vista 以降)このオプションがアクティブな場合は、Driver Verifier は、エクスポートされた Storport ルーチン、過剰な遅延、および Storport の要求の不適切な処理の不適切な使用の Storport ミニポート ドライバーを監視します。

[Power Framework 遅延ファジー テスト](concurrency-stress-test.md)

(Windows 8 以降)Driver Verifier を使用するドライバーの同時実行エラーをフラッシュ スレッドのスケジュールをランダムにこのオプションがアクティブの場合、[電源管理フレームワーク (PoFx)](https://msdn.microsoft.com/library/windows/hardware/hh406637)します。 電源管理フレームワーク (PoFx) を直接利用しないドライバーでは、このオプションはお勧めできません.

[DDI 準拠の確認](ddi-compliance-checking.md)

(Windows 8 以降)このオプションがアクティブで、Driver Verifier には、一連のドライバーとオペレーティング システムのカーネル インターフェイスの適切な相互作用をチェックするデバイス ドライバー インターフェイス (DDI) ルールが適用されます。

[不変な MDL のスタック用検査](invariant-mdl-checking-for-stack.md)

(Windows 8 以降)[不変な Mdl のスタック](invariant-mdl-checking-for-stack.md)オプションは、ドライバーがドライバー スタック間で不変の MDL バッファーを処理する方法を監視します。 不変の MDL バッファーに対する無効な改変が、ドライバーの検証ツールによって検出されます。 このオプションを使うには、少なくとも 1 つのドライバーで I/O の検証を有効にする必要があります。

[不変な MDL のドライバー用検査](invariant-mdl-checking-for-driver.md)

(Windows 8 以降)[不変な Mdl のドライバー](invariant-mdl-checking-for-driver.md)オプションは、ドライバーがドライバーごとの単位で不変の MDL バッファーを処理する方法を監視します。 不変の MDL バッファーに対する無効な改変が、このオプションによって検出されます。 このオプションを使うには、少なくとも 1 つのドライバーで I/O の検証を有効にする必要があります。

[スタック ベースのエラー挿入](stack-based-failure-injection.md)

(Windows 8 および WDK 8 でのみ使用可能)[スタック ベースのエラー挿入](stack-based-failure-injection.md)オプションは、カーネル モード ドライバーにリソース エラーを挿入します。 このオプションは、特別なドライバーである KmAutoFail.sys と[ドライバー検証ツール](driver-verifier.md)を使って、ドライバーのエラー処理パスに入り込みます。

[体系的な低リソース シミュレーション](systematic-low-resource-simulation.md)

(Windows 8.1 以降)[体系的な低リソース シミュレーション](systematic-low-resource-simulation.md)オプションは、カーネル モード ドライバーにリソース エラーを挿入します。

[NDIS/WIFI の検証](ndis-wifi-verification.md)

(Windows 8.1 以降)このオプションがアクティブで、Driver Verifier には、一連の NDIS および NDIS ミニポート ドライバーと、オペレーティング システムのカーネルと適切な相互作用をチェックするワイヤレス LAN (WIFI) 規則が適用されます。

[カーネル同期遅延ファジー テスト](kernel-synchronization-delay-fuzzing.md)

(Windows 8.1 以降)このオプションでは、ドライバーで同時実行のバグを検出するためにスレッド スケジュールはランダム化します。

[VM スイッチの確認](vm-switch-verification.md)

(Windows 8.1 以降)このオプションは、フィルター ドライバーを監視します。 (*拡張可能スイッチの拡張機能*) 内で実行される、 [Hyper-v 拡張可能スイッチ](https://msdn.microsoft.com/library/windows/hardware/hh598161)します。

[ポート/ミニポート インターフェイスのチェック](port-miniport-interface-checking.md)

ポート/ミニポート インターフェイスのチェックには、Driver Verifier PortCls.sys やオーディオのミニポート ドライバーは、ks.sys AVStream ミニポート ドライバーとの間の DDI インターフェイスの検査を有効になります。 オーディオ ドライバーの AVStream ドライバーのルールおよびルールを参照してください。

[コードの整合性チェック](code-integrity-checking.md)

仮想化ベースのセキュリティを使用して、コードの整合性を分離する、カーネル メモリは、実行可能になることができますのみの方法は、コードの整合性の検証です。 そのため、カーネル メモリのページは決して書き込み可能または実行可能 (W+X) にならず、実行可能コードを直接変更することはできません。 コードの整合性チェックは、これらのコードの整合性の規則の互換性を確保し、違反を検出します。

[WDF の検証](wdf-verification.md)

WDF の検証は、カーネル モード ドライバーが正しく、カーネル モード ドライバー フレームワーク (KMDF) の要件に従ってがかどうかを確認します。 


## <a name="standard-settings"></a>標準の設定

<table>
<colgroup>
<col width="100%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">標準の設定に含まれるオプション</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><a href="special-pool.md" data-raw-source="[Special Pool](special-pool.md)">特別なプール</a></p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="force-irql-checking.md" data-raw-source="[Force IRQL Checking](force-irql-checking.md)">強制 IRQL 検査</a></p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="pool-tracking.md" data-raw-source="[Pool Tracking](pool-tracking.md)">プールの追跡</a></p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="i-o-verification.md" data-raw-source="[I/O Verification](i-o-verification.md)">I/O の検証</a></p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="deadlock-detection.md" data-raw-source="[Deadlock Detection](deadlock-detection.md)">デッドロックの検出</a>(Windows XP 以降)</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="enhanced-i-o-verification.md" data-raw-source="[Enhanced I/O Verification](enhanced-i-o-verification.md)">I/O の検証の強化</a>(Windows 7 以降、このオプションは自動的にアクティブ化 I/O の検証を選択すると)</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="dma-verification.md" data-raw-source="[DMA Verification](dma-verification.md)">DMA の検証</a>(Windows XP 以降)</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="security-checks.md" data-raw-source="[Security Checks](security-checks.md)">セキュリティ チェック</a>(Windows XP 以降)</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="miscellaneous-checks.md" data-raw-source="[Miscellaneous Checks](miscellaneous-checks.md)">その他の検査</a>(Windows Vista 以降)</p></td>
</tr>
<tr class="even">
<td align="left"><a href="ddi-compliance-checking.md" data-raw-source="[DDI compliance checking](ddi-compliance-checking.md)">DDI 準拠の検査</a>(Windows 8 以降)</td>
</tr>
</tbody>
</table>

 

## <a name="driver-verifier-options-that-require-io-verification"></a>I/O の検証が必要なドライバーの検証オプション


先に [I/O の検証](i-o-verification.md)を有効にする必要がある 4 つのオプションがあります。 I/O の検証が有効化されていない場合は、これらのオプションも有効になりません。

-   [保留中の I/O 要求を強制する](force-pending-i-o-requests.md)
-   [IRP ログ](irp-logging.md)
-   [不変な MDL のスタック用検査](invariant-mdl-checking-for-stack.md)
-   [不変な MDL のドライバー用検査](invariant-mdl-checking-for-driver.md)

 

 





