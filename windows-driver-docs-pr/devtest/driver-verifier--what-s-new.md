---
title: ドライバーの検証ツールの新機能
description: ドライバーの検証ツールは、Windows 2000 以降のすべてのバージョンの Windows で使用できます。 各バージョンには、Windows ドライバーのバグを検出するための新機能とチェックが導入されています。 このセクションでは、変更の概要と関連ドキュメントへのリンクを示します。
ms.assetid: EAC30108-F8A2-4914-9218-2E0672982B7E
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5d7caa464c9032c594587ce77ba1b2f1aef5437f
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72839563"
---
# <a name="driver-verifier-whats-new"></a>ドライバーの検証ツール: 新機能

[ドライバーの検証ツール](driver-verifier.md)は、windows 2000 以降のすべてのバージョンの windows で使用できます。 各バージョンには、Windows ドライバーのバグを検出するための新機能とチェックが導入されています。 このセクションでは、変更の概要と関連ドキュメントへのリンクを示します。

* [Windows 10 のドライバーの検証ツール](#driver-verifier-in-windows10-updated-may-8-2018)
* [Windows 8.1 のドライバーの検証機能](#driver-verifier-in-windows-8-1-updated-june-17-2013)
* [Windows 8 のドライバーの検証ツール](#driver-verifier-in-windows-8-updated-october-20-2012)
* [Windows 7 のドライバーの検証ツール](#driver-verifier-in-windows-7-updated-october-22-2012)
* [Windows Vista のドライバーの検証ツール](#driver-verifier-in-windows-vista-updated-february-9-2009)
* [Windows XP のドライバーの検証ツール](#driver-verifier-in-windows-xp-updated-december-4-2001)

## <a name="driver-verifier-in-windows10-updated-may-8-2018"></a>Windows 10 のドライバーの検証ツール (*更新日: 2018 年5月8日*)

> [!IMPORTANT]
> Windows 10 1803 以降のバージョンでは、ドライバーの検証ツールを実行すると、Windows Driver Framework (WDF) の検証が自動的に有効になりなくなりました。 以下の点に注意してください。

* WDF の検証は、ドライバー検証ツールの `/standard` フラグの一部として有効にすることもできます。 詳細については、「 [Driver Verifier コマンド構文](https://docs.microsoft.com/windows-hardware/drivers/devtest/verifier-command-line)」を参照してください。
* WDF の検証は自動的に有効にならないため、この変更は、構文 `/flags 0x209BB` で DV を有効にする場合に影響を与えます。

Windows 10 以降、driver verifier には、次のテクノロジの新しいドライバー検証規則が含まれています。

* [オーディオドライバーの新しい規則](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)
* [AVStream ドライバーの新しい規則](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)
* [KMDF ドライバーに関する](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)4 つの新しい規則
* [NDIS ドライバーに関する](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)3 つの新しい規則

## <a name="driver-verifier-in-windows-8-1-updated-june-17-2013"></a>Windows 8-1 のドライバーの検証 (*更新日: 6 月 2013 17 日*)

Windows 8.1 以降、ドライバーの検証ツールでは、エラーを検出するための4つの新しいオプションが導入されています。

* [Ndis/WIFI 検証](ndis-wifi-verification.md)オプションは、ndis ミニポートドライバーとオペレーティングシステムカーネルの間の適切な相互作用を確認する一連の ndis およびワイヤレス LAN ルールを適用します。

* [体系的な低リソースシミュレーション](systematic-low-resource-simulation.md)オプションは、カーネルモードドライバーにリソースエラーを挿入します。

* [カーネル同期遅延ファジー](kernel-synchronization-delay-fuzzing.md)化オプションでは、ドライバーの同時実行のバグを検出するために、スレッドのスケジュールをランダム化します。

* [VM スイッチ検証](vm-switch-verification.md)オプションは、 [Hyper-v 拡張可能スイッチ](https://docs.microsoft.com/windows-hardware/drivers/network/hyper-v-extensible-switch)内で実行されるフィルタードライバー (拡張可能なスイッチ拡張機能) を監視します。
* 新しいデバッガー拡張機能: [ **! ruleinfo**](https://docs.microsoft.com/windows-hardware/drivers/debugger/-ruleinfo)

## <a name="driver-verifier-in-windows-8-updated-october-20-2012"></a>Windows 8 のドライバーの検証ツール (*更新日: 2012 年10月20日*)

Windows 8 以降では、ドライバーの検証ツールで、エラーを検出するための5つの新しいオプションが導入されています。

* [ [Power Framework 遅延ファジー](concurrency-stress-test.md) ] オプションを選択すると、ランダムな実行遅延が挿入され、電源管理フレームワーク (pofx) を使用するドライバーの同時実行のバグを検出できます。 実行の遅延には、上限があります。 このオプションは、電源管理フレームワーク (PoFx) を直接利用しないドライバーには推奨されません。
* [ [Ddi 準拠の確認](ddi-compliance-checking.md)] オプションでは、[静的ドライバーの検証ツール](static-driver-verifier.md)が使用するのと同じデバイスドライバーインターフェイス (DDI) の使用規則を適用して、ドライバーが関数に対して必要な IRQL で関数呼び出しを行うかどうかを確認します。 DDI 準拠の確認は、標準ドライバーの検証ツールのオプションの一部として実行されます。
* [インバリアントな Mdl チェックスタック](invariant-mdl-checking-for-stack.md)オプションは、ドライバーがドライバースタック全体で不変の mdl バッファーを処理する方法を監視します。
* [インバリアントな Mdl チェックドライバー](invariant-mdl-checking-for-driver.md)オプションは、ドライバーがドライバー単位で不変の mdl バッファーを処理する方法を監視します。
* [スタックベースのエラー挿入](stack-based-failure-injection.md)オプションにより、カーネルモードドライバーにリソース割り当てエラーが挿入されます。

Visual Studio 2012 および WDK for Windows 8 を使用してドライバーをビルド、配置、およびテストする場合、テスト用にドライバーを展開するときに、ドライバーの検証ツールをテストコンピューターで実行するように構成することもできます。

## <a name="driver-verifier-in-windows-7-updated-october-22-2012"></a>Windows 7 のドライバーの検証ツール (*更新日: 2012 年10月22日*)

Windows 7 で追加された新機能の詳細については、「Windows 7 のホワイトペーパー[ドライバーの検証ツール]( https://go.microsoft.com/fwlink/p/?linkid=309793)」を参照してください。

Windows 7 では、ドライバーの検証ツールが、一般的なドライバーのバグの多くのクラスを公開できるようにする新しいテストと機能によって、ドライバーの検証機能が強化されています。

* カーネルドライバーからのユーザーハンドルへの不適切な参照
* I/o 検証の機能強化
* 特別なプール、プールの追跡、リソース不足のシミュレーションの機能強化
* 同期メカニズムの不適切な使用方法
* オブジェクト参照が正しくありません
* DPC ルーチンからのプールクォータの課金
* システムシャットダウンのブロックまたは遅延
* 強制的に保留中の i/o 要求が改善されました

Windows 7 では、ドライバーの検証ツールによって、キューに置かれたスピンロックがチェックされます これらのチェックには次のものが含まれます。

* 割り込み要求レベル (IRQL) の値を生成する必要がある操作 ( [**KeAcquireInStackQueuedSpinLock**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff551899(v=vs.85))など) が、実際には irql の値を小さくしていないことを確認しています。

* IRQL 値を下げる必要がある操作 ( [**KeReleaseInStackQueuedSpinLock**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kereleaseinstackqueuedspinlock)など) が実際には irql 値を生成していないことを確認しています。

* [FORCE Irql チェック](force-irql-checking.md)オプションが有効になっている場合に、システムプロセスのワーキングセットをトリミングします。\_レベル以上のディスパッチに irql が発生している場合は、ドライバーが昇格された状態で実行されている間に、ページング可能なメモリへの参照を公開しようとします。IRQL.

* デッドロック検出オプションが有効になっている場合にデッドロックが発生する可能性を予測する。

* 同じ KSPIN\_使用しようとすると、デッドロック検出オプションが有効になっているときに、スピンロックとして、およびスタックキューに格納されたスピンロックとしてデータ構造をロックします。

* スピンロックアドレスとして使用されるユーザーモード仮想アドレスなど、明らかに間違ったポインター値を確認しています。

* Driver Verifier IRQL ログの IRQL 遷移をログに記録します。 この情報は、Windows デバッガーの **! verifier 8**拡張機能を使用するときに表示されます。 「 [ **! Verifier**](https://docs.microsoft.com/windows-hardware/drivers/debugger/-verifier)」を参照してください。

## <a name="additional-debugging-information"></a>追加のデバッグ情報

Windows 7 では、ドライバーの検証ツールは、デバッグに役立つ次の追加情報を提供します。

スタックトレースを含むログは、 [**KeEnterCriticalRegion**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-keentercriticalregion)に対する最近の呼び出しと、検証されたドライバーから[**KeLeaveCriticalRegion**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-keleavecriticalregion)が呼び出されたときに発生します。 ログの内容は、Windows デバッガーの **! verifier 0x200**デバッガー拡張機能を使用して表示されます。 この情報は、スレッドが予期せずクリティカルなリージョンで実行されている場合や、既に残されている重要なリージョンを離れることがあるシナリオを理解するのに役立ちます。

**! Verifier 0x40**デバッガー拡張機能を使用して、 [Force Pending i/o Requests](force-pending-i-o-requests.md)ログの追加情報を表示できます。 以前のバージョンの Windows では、ログには、ドライバー検証ツールが強制的に保留される各 IRP のスタックトレースが1つだけ含まれていました。 これは、強制保留中の IRP に対して初めて[**IoCompleteRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocompleterequest)が呼び出された時点からのスタックトレースでした。 Windows 7 では、強制された保留中の IRP ごとに少なくとも2つのログエントリがあります。

* ドライバーの検証ツールが IRP を強制的に保留にした時点のスタックトレース。 ドライバーの検証ツールは、検証済みのドライバーのいずれかが[**IoCallDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocalldriver)を呼び出したときに強制的に保留される irp の一部を選択します。
* 完了前に、強制保留中の IRP に対する各[**IoCompleteRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocompleterequest)呼び出しのスタックトレースが検証されたドライバーに到達します。 同じ IRP に対して複数の**IoCompleteRequest**呼び出しが存在する可能性があります。これは、いずれかのドライバーが完了ルーチンから完了を一時的に停止してから、もう一度**IoCompleteRequest**を呼び出して再開できるためです。

IRQL 遷移ログに有効なスタックトレースがあります。 このログは、 **! verifier 8**を使用して表示されます。 Windows 7 より前のバージョンの Windows では、ドライバーの検証ツールは、昇格された IRQL でこれらのスタックトレースの一部をログに記録しようとし、高い IRQL 値が原因でスタックトレースをキャプチャできませんでした。 Windows 7 では、ドライバーの検証ツールは、次のスタックトレースをキャプチャしようとします。

* たとえば、検証されたドライバーが[**KeAcquireSpinLock**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-keacquirespinlock)を呼び出す場合など、IRQL を上げる前。
* 検証されたドライバーが[**KeReleaseSpinLock**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kereleasespinlock)を呼び出すと、IRQL が低下します。

これにより、ドライバーの検証ツールは、これらの IRQL 遷移スタックトレースの多くをキャプチャできます。

**! analyze**では、強化された I/o 検証ツールのチェック (Windows 7 の i/o 検証機能の一部) によって公開されている問題をトリアージできます。 以前のバージョンの Windows では、強化された i/o 検証ツールのエラー報告により、ドライバーの検証ツールによって検出されたドライバーの欠陥の説明と、デバッガーの中断が示されていました。 ! **Analyze**はデバッガーに表示されるエラーの説明テキストからの情報を使用できないため、このような中断の後に **! analyze**を実行すると、これらの中断の多くに対して意味のあるトリアージになりません。 Windows 7 では、これらのドライバーの欠陥に関する意味のある情報が、ドライバーの検証ツールによってメモリに保存されます。 **! analyze**は、この情報を見つけて、これらの中断の多くに対して、より意味のある自動トリアージを実行できます。

## <a name="driver-verifier-in-windows-vista-updated-february-9-2009"></a>Windows Vista のドライバーの検証ツール (*更新日: 2009 年2月9日*)

Windows Vista で追加された新機能の詳細については、「Windows Vista のホワイトペーパー[ドライバーの検証ツール]( https://go.microsoft.com/fwlink/p/?linkid=309794)」を参照してください。

Windows Vista では、新しいテストと機能によってドライバーの検証機能が強化されています。

* ドライバーの検証を有効にし、再起動せずに設定を変更する
* 強化された低リソースシミュレーション
* 保留中の i/o 要求を強制する
* セキュリティチェック
* より詳細な i/o 検証
* 拡張 IRQL チェック
* その他のチェック
* ロックされたメモリページの追跡
* その他の自動チェック

## <a name="driver-verifier-in-windows-xp-updated-december-4-2001"></a>Windows XP のドライバーの検証ツール (*更新日: 2001 年12月4日*)

Driver Verifier は、Windows カーネルモードドライバーとグラフィックスドライバーを監視するためのツールです。 ドライバーが正しくない関数呼び出しを行ったりシステムが破損したりしないように、ドライバーの検証ツールを使用してドライバーをテストするハードウェアの製造元を強くお勧めします。 Driver Verifier は、Microsoft Windows XP の新しいテストと機能によって強化されています。

テストのために WHQL に送信されたドライバーは、ドライバーの検証ツールに合格する必要があります。 Windows XP の新しいドライバーの検証機能は次のとおりです。

* Driver Verifier Manager: verifier 用のすべての新しいグラフィカルユーザーインターフェイス (GUI)
* スタック切り替えの監視の新しい自動チェック
* DMA 検証 (HAL 検証とも呼ばれます)、デッドロック検出、SCSI 検証用の新しいドライバー検証ツールオプション
* "レベル 1" と "レベル 2" のテストを組み合わせた i/o 検証の変更、オプションの拡張 i/o 検証テスト
* 新しいデバッガー拡張機能[ **! デッドロック**](https://docs.microsoft.com/windows-hardware/drivers/debugger/-deadlock)と[ **! dma**](https://docs.microsoft.com/windows-hardware/drivers/debugger/-dma)
* 新しいバグチェック: 0xE6 (ドライバー\_VERIFIER\_DMA\_違反) と 0xF1 (SCSI\_検証ツール\_検出された\_違反)
* 既存のバグチェックコードの追加サブコード0xC4 および0Xc4

ドライバーの検証機能には次のものも含まれます。

* **新しい検証ツールのコマンドラインオプション**Ngen.exe ユーティリティには、新しいパラメーター *VolatileDriverList*があります。このパラメーターは、 **/adddriver**キーワードと共に使用して、揮発性設定に追加するドライバーの一覧を指定できます。 *VolatileDriverList*を **/removedriver**キーワードと共に使用して、削除するドライバーの一覧を指定できます。
* **新しい! verifier 拡張機能**新しい[ **! 検証ツール**](https://docs.microsoft.com/windows-hardware/drivers/debugger/-verifier)の拡張機能では、リソースの不足または IRQL の監視時に、追加のログ情報が表示されます。 オンラインヘルプも利用できます。
  * 0x4 で設定された*フラグ*により、リソース不足のシミュレーション中にドライバーの検証ツールによって挿入されたエラーのログが表示されます
  * 0x8 で設定された*フラグ*を使用すると、検証するドライバーによって行われた最新の IRQL の変更のログが表示されます。
  * *フラグ*が0x4 または0x8 と等しい場合、Quantity パラメーターは、表示に含めるレコードまたはログエントリの数を指定します。
  * **?** パラメーターを使用して簡単なヘルプテキストを表示する
* **New! gdikdx 拡張機能**

    新しい **! gdikdx**拡張機能である **! gdikdx**は、グラフィックスドライバーの低リソースシミュレーション中に呼び出される GDI コールバック関数に関する統計を一覧表示します。

* Driver verifier manager のオンラインヘルプドライバー検証マネージャーのオンラインヘルプは、次のいずれかの方法で表示できます。
  * [Driver Verifier マネージャー] ウィンドウで項目を右クリックし、ポップアップメニューから [何を選択します**か?** ] を選択します。
  * ウィンドウの右上隅にある疑問符 ( **?** ) をクリックし、[Driver Verifier マネージャー] ウィンドウで項目をクリックします。
