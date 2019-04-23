---
title: Driver Verifier はの新機能
description: Driver Verifier は、Windows が Windows 2000 以降のすべてのバージョンで使用できます。 各バージョンでは、新機能と Windows のドライバーにバグを見つけるためのチェックが導入されています。 このセクションでは、変更内容をまとめたものですし、関連ドキュメントへのリンクを提供します。
ms.assetid: EAC30108-F8A2-4914-9218-2E0672982B7E
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c25056d883a4f56b27d2198e4f9ba2964943c347
ms.sourcegitcommit: d17b4c61af620694ffa1c70a2dc9d308fd7e5b2e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/22/2019
ms.locfileid: "59902456"
---
# <a name="driver-verifier-whats-new"></a>ドライバーの検証ツール: 新機能

[Driver Verifier](driver-verifier.md)は Windows 2000 以降の Windows のすべてのバージョンで使用できます。 各バージョンでは、新機能と Windows のドライバーにバグを見つけるためのチェックが導入されています。 このセクションでは、変更内容をまとめたものですし、関連ドキュメントへのリンクを提供します。

* [Windows 10 の driver Verifier](#driver-verifier-in-windows-10-updated-may-8-2018)
* [Windows 8.1 の driver Verifier](#driver-verifier-in-windows-8-1-updated-june-17-2013)
* [Windows 8 の driver Verifier](#driver-verifier-in-windows-8-updated-october-20-2012)
* [Windows 7 の driver Verifier](#driver-verifier-in-windows-7-updated-october-22-2012)
* [Windows Vista の driver Verifier](#driver-verifier-in-windows-vista-updated-february-9-2009)
* [Windows XP の driver Verifier](#driver-verifier-in-windows-xp-updated-december-4-2001)

## <a name="driver-verifier-in-windows10-updated-may-8-2018"></a>Windows 10 の driver Verifier (*更新します。2018 年 5 月 8 日*)

> [!IMPORTANT]
> 後は、Windows 10 1803 以降のバージョンでは、Driver Verifier を実行しているが自動的に行われなくを有効にする Windows Driver Framework (WDF) 検証します。 以下の点に注意してください。

* Driver Verifier の一環として WDF の検証を有効にできますも`/standard`フラグ。 参照してください[Driver Verifier のコマンド構文](https://docs.microsoft.com/windows-hardware/drivers/devtest/verifier-command-line)詳細についてはします。
* この変更は、影響する構文を使用して、DV を有効にする場合`/flags 0x209BB`WDF の検証が自動的に有効不要になったとします。

Windows 10 以降、ドライバーの検証ツールには、次のテクノロジ用の新しいドライバー検証規則が含まれています。

* 新しい[オーディオ ドライバーの規則](https://msdn.microsoft.com/library/windows/hardware/dn906757)
* 新しい [AVStream ドライバーの規則](https://msdn.microsoft.com/library/windows/hardware/dn906758)
* 4 つの新しい [KMDF ドライバーの規則](https://msdn.microsoft.com/library/windows/hardware/ff551709)
* 3 つの新しい [NDIS ドライバーの規則](https://msdn.microsoft.com/library/windows/hardware/ff551713)

## <a name="driver-verifier-in-windows-8-1-updated-june-17-2013"></a>Windows 8-1 の driver Verifier (*更新します。2013 年 6 月 17 日、*)

Windows 8.1 以降では、Driver Verifier には、エラーを検出するための 4 つの新しいオプションが導入されています。

* [NDIS/WIFI 検証](ndis-wifi-verification.md)オプションには、一連の NDIS および NDIS ミニポート ドライバーと、オペレーティング システムのカーネルと適切な相互作用をチェックするワイヤレス LAN ルールが適用されます。

* [体系的な低リソース シミュレーション](systematic-low-resource-simulation.md)オプションは、カーネル モード ドライバーにリソース エラーを挿入します。

* [カーネル同期遅延ファジー テスト](kernel-synchronization-delay-fuzzing.md)オプションは、ドライバーの同時実行のバグを検出するためにスレッド スケジュールをランダム化します。

* [VM switch 検証](vm-switch-verification.md)オプション内で実行されるフィルター ドライバー (拡張可能スイッチの拡張機能) の監視、 [HYPER-V 拡張可能スイッチ](https://msdn.microsoft.com/library/windows/hardware/hh598161)します。
* デバッガーの新しい拡張機能: [ **! ruleinfo**](https://msdn.microsoft.com/library/windows/hardware/dn265374)

## <a name="driver-verifier-in-windows-8-updated-october-20-2012"></a>Windows 8 の driver Verifier (*更新します。2012 年 10 月 20 日*)

Windows 8 以降、Driver Verifier には、エラーを検出するための 5 つの新しいオプションが導入されています。

* [Power Framework 遅延ファジー テスト](concurrency-stress-test.md)オプションは、電源管理フレームワーク (PoFx) を使用するドライバーの同時実行のバグを検出するためにランダムな実行の遅延を挿入します。 実行の遅延では、上限に制限があります。 このオプションは、電源管理フレームワーク (PoFx) を直接利用しないドライバーを使用しないでください。
* [DDI 準拠の検査](ddi-compliance-checking.md)オプションが適用される同じデバイス ドライバー インターフェイス (DDI) の使い方の規則を[Static Driver Verifier](static-driver-verifier.md)を使用して、ドライバーが適切な IRQL で関数呼び出しを行うことを確認します。関数。 DDI 準拠の確認は、標準の Driver Verifier のオプションの一部として実行されます。
* [[不変な MDL のスタック用検査]](invariant-mdl-checking-for-stack.md) は、不変の MDL バッファーがドライバーでどのように処理されているかをドライバー スタック全体を対象に監視するオプションです。
* [[不変な MDL のドライバー用検査]](invariant-mdl-checking-for-driver.md) は、不変の MDL バッファーがドライバーでどのように処理されているかをドライバー単位で監視するオプションです。
* [スタック ベースのエラー挿入](stack-based-failure-injection.md)オプションは、カーネル モード ドライバーでのリソース割り当てのエラーを挿入します。

ビルド、展開、および Visual Studio 2012 と Windows 8 の WDK を使用して、ドライバーをテストするときに、Driver Verifier テスト用にドライバーを展開するときに、テスト コンピューターで実行する構成もできます。

## <a name="driver-verifier-in-windows-7-updated-october-22-2012"></a>Windows 7 の driver Verifier (*更新します。2012 年 10 月 22 日*)

Windows 7 で追加された新機能については、ホワイト ペーパーを参照してください。 [Windows 7 の Driver Verifier]( https://go.microsoft.com/fwlink/p/?linkid=309793)します。

Windows 7 では、Driver Verifier を一般的なドライバーのバグのより多くのクラスを公開する機能と新しいテストとドライバーの検証ツールが強化されました。

* カーネル ドライバーからのユーザーへの参照が正しくない処理します。
* I/O の検証の機能強化
* 特別なプール、プールの追跡、および低リソース シミュレーションの機能強化
* 同期機構の不適切な使用方法
* 不正なオブジェクトの参照
* DPC ルーチンからプール クォータの料金
* システム シャット ダウンはブロックや遅延
* 保留中の I/O 要求の改善の強制

Windows 7 でドライバーの検証ツールでは、キューに置かれたスピン ロックのチェック、これらのチェックでは、Windows の以前のバージョンのスピンロックに提供されるようになります。 これらのチェックを以下に示します。

* などの操作、割り込み要求レベル (IRQL) を発生させる必要があります値を確認する[ **KeAcquireInStackQueuedSpinLock**](https://msdn.microsoft.com/library/windows/hardware/ff551899)、実際には、IRQL の値の削減はできません。

* などの操作を IRQL を削減する必要があります値を確認する[ **KeReleaseInStackQueuedSpinLock**](https://msdn.microsoft.com/library/windows/hardware/ff553130)は、IRQL の値は実際に発生していません。

* トリミングのシステム プロセスのワーキング セット場合、[強制 IRQL 検査](force-irql-checking.md)オプションが有効の IRQL をディスパッチする生成されている場合\_レベル以上に設定すると、中にページング可能なメモリへの参照を公開するために、ドライバーは、管理者特権での IRQL で行われています。

* デッドロック検出オプションが有効にすると、デッドロックの可能性を予測します。

* 同じ KSPIN を使用しようとしています。\_スピン ロックとスタックの両方のロックのデータ構造は、デッドロック検出オプションが有効にすると、スピン ロックをキューに登録します。

* スピン ロックのアドレスとして使用されるユーザー モード仮想アドレスなどの明らかに不適切なポインター値を確認しています。

* Driver Verifier の IRQL ログには、IRQL の遷移を記録します。 使用する場合、この情報が表示されます、 **! verifier 8** Windows デバッガーの拡張機能。 参照してください[ **! verifier**](https://msdn.microsoft.com/library/windows/hardware/ff565591)します。

## <a name="additional-debugging-information"></a>追加のデバッグ情報

Windows 7 では、Driver Verifier は、デバッグに役立つ次の追加情報を提供します。

最近の呼び出しの順にスタック トレースとログがある[ **KeEnterCriticalRegion** ](https://msdn.microsoft.com/library/windows/hardware/ff552021)と[ **KeLeaveCriticalRegion** ](https://msdn.microsoft.com/library/windows/hardware/ff552964)からドライバーを確認します。 使用して、ログの内容が表示されます、 **! verifier 0x200**デバッガー Windows デバッガーの拡張機能。 この情報は、スレッドが予期せずクリティカル領域で実行されているまたはクリティカル領域が既にままをしようとしてが理解する場合に便利です。

追加情報を表示することができます、 [Force 保留中の I/O 要求](force-pending-i-o-requests.md)ログを使用して、 **! verifier 0x40**デバッガー拡張機能。 Windows の以前のバージョンでは、ログには、Driver Verifier は、保留状態の場合に強制する各 IRP の 1 つのスタック トレースが含まれています。 これは、時間からスタック トレースと[ **IoCompleteRequest** ](https://msdn.microsoft.com/library/windows/hardware/ff548343)強制 IRP の保留中の最初に呼び出されました。 Windows 7 では、強制的に保留中の IRP ごとに 2 より可能性がある詳細は、少なくとも 2 つのログ エントリがあります。

* Driver Verifier が保留中に強制する IRP を選択するときにスタック トレース。 Driver Verifier がいくつかの確認済みのドライバーのいずれかを呼び出すと、保留中の強制する Irp [**保留**](https://msdn.microsoft.com/library/windows/hardware/ff548336)します。
* それぞれのスタック トレース[ **IoCompleteRequest** ](https://msdn.microsoft.com/library/windows/hardware/ff548343)が完成したら、検証済みのドライバーに達する前に、強制 IRP の保留中の呼び出し。 1 つ以上**IoCompleteRequest** 、ドライバーのいずれかその完了ルーチンからの完了を一時的に停止できして呼び出すことによって再開できるため、同じ IRP の呼び出しが存在できる**IoCompleteRequest**もう一度です。

IRQL 移行ログには、以上の有効なスタック トレースがあります。 使用してこのログが表示される **! verifier 8**します。 Windows バージョンの Windows 7 より前では、Driver Verifier は管理者特権での IRQL でこれらのスタック トレースの一部を記録しようできます。 そしては大きい IRQL の値が、スタック トレースをキャプチャできませんでした。 Windows 7 では、Driver Verifier は、これらのスタック トレースをキャプチャしようとは

* IRQL を発生させる前に、検証済みのドライバーを呼び出すと[ **KeAcquireSpinLock**](https://msdn.microsoft.com/library/windows/hardware/ff551917)します。
* 呼び出す、IRQL の値を下げた後と確認済みのドライバー [ **KeReleaseSpinLock**](https://msdn.microsoft.com/library/windows/hardware/ff553145)します。

この方法では、Driver Verifier これら IRQL 遷移のスタック トレースのキャプチャできます。

**! 分析**公開されている問題をトリアージできます (Windows 7 での I/O の検証ツールの一部である) が強化された I/O の検証チェックでします。 デバッガーを中断後に、ドライバーの検証ツールによって検出されたドライバーの問題の説明を表示するには、以前の Windows バージョンでは、強化された I/O の検証エラーの報告行いました。 実行している **! 分析**後、このような中断もされません意味のあるトリアージ区切りの多くのため、 **! 分析**に表示されるエラーの説明テキストの情報を使用することはできません、デバッガー。 Windows 7、意味のあるドライバー欠陥については、メモリ内で Driver Verifier で保存されます。 **! 分析**この情報を検索でき、これらの区切りの多くのより意味のある自動トリアージを実行します。

## <a name="driver-verifier-in-windows-vista-updated-february-9-2009"></a>Windows Vista の driver Verifier (*更新します。2009 年 2 月 9 日*)

Windows Vista で追加された新機能については、ホワイト ペーパーを参照してください。 [Windows Vista の Driver Verifier]( https://go.microsoft.com/fwlink/p/?linkid=309794)します。

Windows Vista では、Driver Verifier を新しいテストと機能が拡張されています。

* ドライバーの検証を有効にして、再起動することがなく設定を変更します。
* 強化された低リソース シミュレーション
* 保留中の I/O 要求を強制する
* セキュリティの検査
* 詳細な I/O の検証
* 強化された IRQL 検査
* その他の検査
* ロックされたメモリ ページの追跡
* 追加の自動チェック

## <a name="driver-verifier-in-windows-xp-updated-december-4-2001"></a>Windows XP の driver Verifier (*更新します。2001 年 12 月 4 日*)

Driver Verifier は、Windows カーネル モード ドライバーとグラフィック ドライバーを監視するためのツールです。 Microsoft は、Driver Verifier ドライバーの無効な関数呼び出しを行うまたはシステムの破損の原因がないことを確認するには、そのドライバーをテストするハードウェアの製造元を強くお勧めします。 Driver Verifier は、Microsoft Windows XP の新しいテストと機能が拡張されています。

テストのために、WHQL に送信されるドライバーには、Driver Verifier を渡す必要があります。 Windows XP の Driver Verifier の新機能は次のとおりです。

* ドライバー検証マネージャー、verifier.exe をまったく新しいグラフィカル ユーザー インターフェイス (GUI)
* スタックの切り替えの監視用の新しい自動チェック
* DMA の検証 (HAL の検証とも呼ばれます)、デッドロックの検出、および SCSI 検証用の新しいドライバーの検証オプション
* 「レベル 1」と「レベル 2」のテストを結合する I/O の検証の変更、強化された I/O の省略可能な検証テストします。
* デバッガーの新しい拡張機能[ **! デッドロック**](https://msdn.microsoft.com/library/windows/hardware/ff562326)と[ **! dma**](https://msdn.microsoft.com/library/windows/hardware/ff562369)
* 新しいバグを確認します。0xE6 (ドライバー\_VERIFIER\_DMA\_違反) と 0xF1 (SCSI\_VERIFIER\_検出\_違反)
* 既存のバグの追加のサブ コード 0xC4 および 0xC9 コードを確認します。

ドライバー検証ツールの機能があります。

* **新しい検証機能のコマンド ライン オプション**verifier.exe ユーティリティが新しいパラメーター、 *VolatileDriverList*で使用できる、 **/adddriver**キーワードに追加するドライバーの一覧を指定するには揮発性の設定。 *VolatileDriverList*で使用できる、 **/removedriver**キーワードを削除するドライバーの一覧を指定します。
* **新規! verifier の拡張機能**新規[ **! verifier** ](https://msdn.microsoft.com/library/windows/hardware/ff565591)拡張機能が監視リソース不足または IRQL が発生したときに、追加のログ情報を表示し、スピン ロックします。 オンライン ヘルプも使用できます。
  * *フラグ*0x4 で設定が低リソース シミュレーション中にドライバーの検証ツールによって挿入エラーのログを表示
  * *フラグ*0x8 のセットが検証されているドライバーによって行われた最新の IRQL 変更のログを表示
  * 場合*フラグ*0x4 正確または 0x8 と等しい、数量のパラメーターをレコードまたは表示に含めるには、ログ エントリの数を指定します
  * **でしょうか。** パラメーターは、簡単なヘルプ テキストを示しています。
* **新しい! gdikdx.verifier 拡張機能**

    新しい **! gdikdx.verifier**拡張機能、 **! gdikdx.verifier-s**、グラフィック ドライバーの低リソース シミュレーション中に、GDI のコールバック関数のリストの統計情報が呼び出されます。

* ドライバー検証ツール マネージャーのドライバー検証マネージャー オンライン ヘルプのオンライン ヘルプは、次の方法のいずれかで表示できます。
  * ドライバー検証マネージャー ウィンドウ内の項目を右クリックし **これは何ですか?** ポップアップ メニューから。
  * 疑問符 () をクリックします (**でしょうか。**) ウィンドウの右上隅でドライバー検証マネージャー ウィンドウ内の項目を順にクリックします。
