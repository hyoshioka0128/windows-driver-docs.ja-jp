---
title: ドライバーの検証ツールのオプション
description: ドライバーの検証ツールのオプションと規則クラス
ms.assetid: f251fe07-e68e-4d93-9aa5-9a0bc818756d
keywords:
- Driver Verifier WDK、オプションの一覧
- エラー WDK ドライバーの検証ツール
ms.date: 04/02/2020
ms.localizationpriority: medium
ms.openlocfilehash: 95f9bec69d0bfa4d54f1dadce31c5db2cfb55b38
ms.sourcegitcommit: 84be9e06fd0886598df77dffcbc75632d613c8f3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/11/2020
ms.locfileid: "81208135"
---
# <a name="driver-verifier-options-and-rule-classes"></a>ドライバーの検証ツールのオプションと規則クラス


このトピックでは、ドライバー検証ツール内のオプションの機能および規則クラスについて説明します。 標準設定を使用する場合に含まれるオプションの一覧については、「[標準設定](#standard-settings)」を参照してください。

> [!NOTE]
> どのオプションが選択されているかに関係なく、検証されるドライバーに対しては、[自動チェック](automatic-checks.md)が常に実行されます。 ドライバーが不適切な IRQL でメモリを使用している場合、スピンロックやメモリ割り当てを不適切に呼び出すか解放したり、スタックを不適切に切り替えたり、最初にタイマーを削除せずにメモリプールを解放したりすると、ドライバー検証ツールはこの動作を検出します。 ドライバーがアンロードされると、ドライバーの検証ツールは、そのリソースが正しく解放されたことを確認します。

## <a name="enabling-rule-classes-with-ruleclasses"></a>/Ruleclasses を使用したルールクラスの有効化

Windows 10 以降のバージョン17627以降では、次の構文を使用してルールクラスを有効にすることができます。

`/ruleclasses or /rc [<ruleclass_1> <ruleclass_2> ... <ruleclass_k>]`

(下の正の10進整数で表される) 複数のクラスを有効にする場合は、各整数を空白文字で区切ります。 

これらの規則クラスの説明については、以下を参照してください。

### <a name="standard-rule-classes"></a>標準規則クラス

| Rule クラス | 10進数 ID |
| -- | -- |
| 特別なプール        | 1 |
| 強制 IRQL 検査 | 2 |
| プールのトラック       | 4 |
| I/O の検証    | 5 |
| デッドロックの検出  | 6 |
| DMA チェック | 8 |
| セキュリティの検査 | 9 |
| その他の検査 | 12 |
| DDI 準拠の検査 | 18 |
| WDF の検証 | 34 |

### <a name="additional-rule-classes"></a>追加の規則クラス

これらの規則クラスは、特定のシナリオのテストを目的としています。 規則クラスは、(\*) に設定されており、自動的に有効になる i/o 検証 (5) が必要です。 (\**) でマークされたフラグは、個々のルールを無効にすることをサポートします。

| Rule クラス | 10進数 ID |
| -- | -- |
| ランダム化した低リソースシミュレーション        | 3 |
| 強制的に保留中の i/o 要求 (*) | 10 |
| IRP ログ       | 11 |
| スタックに対する不変の MDL チェック (*)    | 14 |
| ドライバーに対する不変の MDL チェック (*)  | 15 |
| Power framework 遅延ファジー | 16 |
| ポート/ミニポート インターフェイス チェック | 17 |
| 体系的な低リソースのシミュレーション | 19 |
| DDI 準拠の確認 (追加) | 20 |
| カーネル同期遅延ファジー テスト | 24 |
| VM スイッチ検証 | 25 |
| コードの整合性チェック | 26 |
| 追加の IRQL チェック | 35 |

## <a name="optional-feature-and-rule-class-descriptions"></a>オプションの機能とルールクラスの説明

[特別なプール](special-pool.md)

このオプションが有効になっている場合、ドライバーの検証ツールは、ドライバーのメモリ要求の大部分を特別なプールから割り当てます。 この特別なプールでは、メモリ オーバーラン、メモリ アンダーラン、既に解放されたメモリへのアクセスが監視されます。

[強制 IRQL チェック](force-irql-checking.md)

このオプションが有効になっている場合、ドライバーの検証ツールは、ページング可能なコードを無効にすることで、ドライバーに極端なメモリ負荷をかけます。 ドライバーが不適切な IRQL で、またはスピン ロックを保持したままでページ メモリにアクセスしようとすると、ドライバーの検証ツールはこの動作を検出します。

[低リソースシミュレーション](low-resources-simulation.md)(Windows 8.1 でランダム化された*低リソースシミュレーション*と呼ばれます)

このオプションが有効になっていると、ドライバーの検証ツールは、プール割り当て要求やその他のリソース要求をランダムに失敗させることができます。 システムでこれらの割り当てエラーを引き起こすことで、ドライバーの検証ツールはリソース不足の状況でのドライバーの能力をテストします。

[プールの追跡](pool-tracking.md)

このオプションが有効になっている場合、ドライバーの検証ツールは、ドライバーがアンロードされるときにすべてのメモリ割り当てが解放されたかどうかを確認します。 これによってメモリ リークが明らかになります。

[I/o の検証](i-o-verification.md)

このオプションが有効になっている場合、ドライバーの検証ツールは、特殊なプールからドライバーの Irp を割り当て、ドライバーの i/o 処理を監視します。 これによって、I/O ルーチンの不適切な使用や不整合な使用が検出されます。

[デッドロック検出](deadlock-detection.md)

(Windows XP 以降)このオプションがアクティブになっている場合、ドライバーの検証ツールは、ドライバーによるスピンロック、ミューテックス、および高速ミューテックスの使用を監視します。 これにより、ドライバーのコードに、ある時点でデッドロックが発生する可能性があるかどうかが検出されます。

[強化された i/o 検証](enhanced-i-o-verification.md)

(Windows XP 以降)このオプションが有効になっている場合、ドライバーの検証ツールは、複数の i/o マネージャールーチンの呼び出しを監視し、PnP Irp、停電、および WMI Irp のストレステストを実行します。 Windows 7 以降のバージョンの Windows オペレーティングシステムでは、拡張 i/o 検証のすべての機能が[I/o 検証](i-o-verification.md)の一部として含まれています。また、ドライバー検証マネージャーまたはコマンドラインでこのオプションを選択する必要もありません。

[DMA の検証](dma-verification.md)

(Windows XP 以降)このオプションがアクティブになっている場合、ドライバーの検証ツールはドライバーの DMA ルーチンの使用を監視します。 これによって、DMA バッファー、アダプター、マップ レジスタの不適切な使用が検出されます。

[セキュリティチェック](security-checks.md)

(Windows Vista 以降)このオプションが有効になっている場合、ドライバーの検証ツールは、カーネルモードルーチンによるユーザーモードアドレスへの参照など、セキュリティ上の脆弱性につながる可能性がある一般的なエラーを検索します。

[その他のチェック](miscellaneous-checks.md)

(Windows Vista 以降)このオプションがアクティブになっている場合、ドライバーの検証ツールは、解放されたメモリの mishandling など、ドライバーのクラッシュの一般的な原因を探します。

[保留中の I/O 要求を強制する](force-pending-i-o-requests.md)

(Windows Vista 以降)このオプションが有効になっている場合、ドライバーの検証ツールは、 [**IoCallDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocalldriver)へのランダムな呼び出しの状態\_pending を返すことによって、ドライバーの状態\_保留中の戻り値をテストします。

[IRP ログ](irp-logging.md)

(Windows Server 2003 以降)このオプションが有効になっている場合、ドライバーの検証ツールはドライバーの Irp の使用を監視し、IRP の使用のログを作成します。

[ディスクの整合性チェック](disk-integrity-checking.md)

(Windows Server 2003 で導入されました。 Windows 7 以降では使用できません。)このオプションがアクティブになっている場合、ドライバー検証ツールはハードディスクのアクセスを監視し、ディスクのデータが正しく保持されているかどうかを検出します。

[SCSI 検証](scsi-verification.md)

(Windows XP 以降)このオプションが有効になっている場合、ドライバーの検証ツールは SCSI ミニポートドライバーを監視して、エクスポートされた SCSI ポートルーチン、過剰な遅延、および SCSI 要求の不適切な処理を使用します。

[Storport 検証](dv-storport-verification.md)

(Windows Vista 以降)このオプションが有効になっている場合、ドライバーの検証ツールは、Storport ミニポートドライバーを監視して、エクスポートされた Storport ルーチン、過度の遅延、および Storport 要求の不適切な処理を使用します。

[Power Framework 遅延ファジー](concurrency-stress-test.md)

(Windows 8 以降)このオプションがアクティブになっている場合、ドライバーの検証ツールは、[電源管理フレームワーク (PoFx)](https://docs.microsoft.com/windows-hardware/drivers/kernel/overview-of-the-power-management-framework)を使用するドライバーの同時実行エラーをフラッシュするのを防ぐために、スレッドのスケジュールをランダム化します。 このオプションは、電源管理フレームワーク (PoFx) を直接利用しないドライバーには推奨されません。

[DDI のコンプライアンスチェック](ddi-compliance-checking.md)

(Windows 8 以降)このオプションが有効になっている場合、ドライバーの検証ツールは、ドライバーとオペレーティングシステムのカーネルインターフェイスとの間の適切な対話を確認する一連のデバイスドライバーインターフェイス (DDI) 規則を適用します。

[不変な MDL のスタック用検査](invariant-mdl-checking-for-stack.md)

(Windows 8 以降)[インバリアントな Mdl チェックスタック](invariant-mdl-checking-for-stack.md)オプションは、ドライバーがドライバースタック全体で不変の mdl バッファーを処理する方法を監視します。 不変の MDL バッファーに対する無効な改変が、ドライバーの検証ツールによって検出されます。 このオプションを使うには、少なくとも 1 つのドライバーで I/O の検証を有効にする必要があります。

[不変な MDL のドライバー用検査](invariant-mdl-checking-for-driver.md)

(Windows 8 以降)[インバリアントな Mdl チェックドライバー](invariant-mdl-checking-for-driver.md)オプションは、ドライバーがドライバー単位で不変の mdl バッファーを処理する方法を監視します。 不変の MDL バッファーに対する無効な改変が、このオプションによって検出されます。 このオプションを使うには、少なくとも 1 つのドライバーで I/O の検証を有効にする必要があります。

[スタックベースのエラー挿入](stack-based-failure-injection.md)

(Windows 8 および WDK 8 でのみ使用可能)[スタックベースのエラー挿入](stack-based-failure-injection.md)オプションにより、カーネルモードドライバーにリソースエラーが挿入されます。 このオプションは、特別なドライバーである KmAutoFail.sys と[ドライバー検証ツール](driver-verifier.md)を使って、ドライバーのエラー処理パスに入り込みます。

[体系的な低リソースシミュレーション](systematic-low-resource-simulation.md)

(Windows 8.1 以降)[体系的な低リソースシミュレーション](systematic-low-resource-simulation.md)オプションは、カーネルモードドライバーにリソースエラーを挿入します。

[NDIS/WIFI の検証](ndis-wifi-verification.md)

(Windows 8.1 以降)このオプションが有効になっている場合、ドライバーの検証ツールは、NDIS ミニポートドライバーとオペレーティングシステムカーネルの間の適切な対話を確認する NDIS およびワイヤレス LAN (WIFI) 規則のセットを適用します。

[カーネル同期遅延ファジー](kernel-synchronization-delay-fuzzing.md)

(Windows 8.1 以降)このオプションは、ドライバーの同時実行のバグを検出するために、スレッドのスケジュールをランダムにします。

[VM スイッチの検証](vm-switch-verification.md)

(Windows 8.1 以降)このオプションは、 [Hyper-v 拡張可能スイッチ](https://docs.microsoft.com/windows-hardware/drivers/network/hyper-v-extensible-switch)内で実行されるフィルタードライバー (*拡張可能なスイッチ拡張機能*) を監視します。

[ポート/ミニポートインターフェイスのチェック](port-miniport-interface-checking.md)

ポート/ミニポートのチェックにより、ドライバーの検証ツールは、PortCls とそのオーディオミニポートドライバーの間の DDI インターフェイスと、ks およびその AVStream のミニポートドライバーを調べることができます。 「AVStream ドライバーの規則」および「オーディオドライバーの規則」を参照してください。

[コードの整合性チェック](code-integrity-checking.md)

仮想化ベースのセキュリティを使用してコードの整合性を分離する場合、カーネルメモリを実行可能ファイルにする唯一の方法は、コードの整合性を検証することです。 そのため、カーネル メモリのページは決して書き込み可能または実行可能 (W+X) にならず、実行可能コードを直接変更することはできません。 コードの整合性チェックによって、これらのコード整合性規則の互換性が確保され、違反が検出されます。

[WDF の検証](wdf-verification.md)

WDF 検証では、カーネルモードドライバーがカーネルモードドライバーフレームワーク (KMDF) の要件に適切に従っているかどうかを確認します。

[追加の IRQL チェック]()

追加の IRQL チェックにより、PASSIVE_LEVEL に対して DDI 準拠チェックの IRQL 規則が強化されます。 次の2つの規則で構成されます。
- [IrqlIoRtlZwPassive](wdm-irqliortlzwpassive.md)規則は、ドライバーが IRQL = PASSIVE_LEVEL で実行されている場合にのみ、規則に記載されている DDIs を呼び出すように指定します。
- [Irqlntifsapcpassive](wdm-irqlntifsapcpassive.md)規則では、ドライバーが irql = PASSIVE_LEVEL または irql < = APC_LEVEL のいずれかで実行されている場合にのみ、規則に記載されている DDIs を呼び出すように指定します。

## <a name="standard-settings"></a>標準設定

<table>
<colgroup>
<col width="100%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">標準設定に含まれるオプション</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><a href="special-pool.md" data-raw-source="[Special Pool](special-pool.md)">特別なプール</a></p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="force-irql-checking.md" data-raw-source="[Force IRQL Checking](force-irql-checking.md)">強制 IRQL チェック</a></p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="pool-tracking.md" data-raw-source="[Pool Tracking](pool-tracking.md)">プールの追跡</a></p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="i-o-verification.md" data-raw-source="[I/O Verification](i-o-verification.md)">I/o の検証</a></p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="deadlock-detection.md" data-raw-source="[Deadlock Detection](deadlock-detection.md)">デッドロック検出</a>(Windows XP 以降)</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="enhanced-i-o-verification.md" data-raw-source="[Enhanced I/O Verification](enhanced-i-o-verification.md)">拡張 I/o 検証</a>(Windows 7 以降では、[i/o 検証] を選択すると、このオプションは自動的にアクティブ化されます)</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="dma-verification.md" data-raw-source="[DMA Verification](dma-verification.md)">DMA の検証</a>(Windows XP 以降)</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="security-checks.md" data-raw-source="[Security Checks](security-checks.md)">セキュリティチェック</a>(Windows XP 以降)</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="miscellaneous-checks.md" data-raw-source="[Miscellaneous Checks](miscellaneous-checks.md)">その他のチェック</a>(Windows Vista 以降)</p></td>
</tr>
<tr class="even">
<td align="left"><a href="ddi-compliance-checking.md" data-raw-source="[DDI compliance checking](ddi-compliance-checking.md)">DDI 準拠の確認</a>(Windows 8 以降)</td>
</tr>
</tbody>
</table>

## <a name="driver-verifier-options-that-require-io-verification"></a>I/o 検証を必要とするドライバーの検証ツールオプション

先に [I/O の検証](i-o-verification.md)を有効にする必要がある 4 つのオプションがあります。 I/O の検証が有効化されていない場合は、これらのオプションも有効になりません。

-   [保留中の I/O 要求を強制する](force-pending-i-o-requests.md)
-   [IRP ログ](irp-logging.md)
-   [不変な MDL のスタック用検査](invariant-mdl-checking-for-stack.md)
-   [不変な MDL のドライバー用検査](invariant-mdl-checking-for-driver.md)
