---
title: Windows ハードウェア エラー アーキテクチャの定義
description: Windows ハードウェア エラー アーキテクチャの定義
ms.assetid: 4de5ead1-aa17-4c14-9afc-bc0d9689a13e
keywords:
- Windows ハードウェア エラー アーキテクチャ WDK の用語
- WHEA WDK、用語集
- ハードウェア エラー WDK WHEA、用語集
- エラー WDK WHEA、用語集
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 93a9ec87b9597d0461ba3ea687e7c9a2423d24a5
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56537948"
---
# <a name="windows-hardware-error-architecture-definitions"></a>Windows ハードウェア エラー アーキテクチャの定義


次の Windows ハードウェア エラー アーキテクチャ (WHEA) に関連する用語の定義に示します。

<a href="" id="advanced-configuration-and-power-interface--acpi-"></a>Advanced Configuration and Power Interface (ACPI)  
デバイスのオペレーティング システム向けの構成と電源管理のための業界標準インターフェイス。 ACPI の詳細については、、 [ACPI 仕様](https://go.microsoft.com/fwlink/p/?linkid=69483)を参照してください。

<a href="" id="baseboard-management-controller--bmc-"></a>ベースボード管理コント ローラー (BMC)  
監視と、特定の環境のエラー条件の処理など、プラットフォーム固有の機能を管理するマザーボード上のハードウェア コンポーネントのセット。

<a href="" id="corrected-machine-check--cmc-"></a>マシン チェック (CMC) を修正しました  
ハードウェアまたはファームウェアによって修正されたプロセッサで検出されたエラー条件。 CMC を割り込みシグナル通知するか、オペレーティング システムによって定期的にポーリング エラー レジスタにビットを設定して、通常、オペレーティング システムに報告されます。 これは、致命的でないエラー状態です。

<a href="" id="corrected-platform-error--cpe-"></a>修正されたプラットフォーム エラー (CPE)  
プラットフォーム ハードウェアが修正されましたが、ハードウェアまたはファームウェアによって検出されたエラー条件。 CPE を割り込みシグナル通知するか、オペレーティング システムによって定期的にポーリング エラー レジスタにビットを設定して、通常、オペレーティング システムに報告されます。 これは、致命的でないエラー状態です。

<a href="" id="event-log--el-"></a>イベント ログ (EL)  
システム コンポーネントで発生するイベントを追跡する Windows オペレーティング システムのコンポーネント。 WHEA では、システム イベント ログを使用して、ハードウェア エラーのイベントを記録します。

<a href="" id="event-tracing-for-windows--etw-"></a>Event Tracing for Windows (ETW)  
ETW は、ソフトウェア開発者を起動し、イベント トレース セッションを停止するには、トレースのイベントを提供およびトレース イベントを使用するアプリケーションをインストルメント化する機能を提供します。 WHEA では、ハードウェアのエラー イベントのサブスクライバーに通知して、システム イベント ログでハードウェア エラー イベントを記録する、ETW が使用されます。

<a href="" id="extensible-firmware-interface--efi-"></a>拡張ファームウェア インターフェイス (EFI)  
オペレーティング システムとプラットフォーム ハードウェア間のインターフェイスの次世代のモデル。 インターフェイスは、プラットフォームに関連する情報、およびブートおよびランタイム サービスの呼び出しを含む、オペレーティング システムとそのローダーを使用できるデータ テーブルで構成されます。 同時に、これらのオペレーティング システムを起動し、ブート前のアプリケーションを実行する標準的な環境を提供します。 EFI の詳細については、、 [Unified Extensible Firmware Interface (UEFI) 仕様](https://go.microsoft.com/fwlink/p/?linkid=69484)を参照してください。

<a href="" id="intelligent-platform-management-interface--ipmi-"></a>Intelligent Platform Management Interface (IPMI)  
監視し、管理機能に使用されるハードウェア プラットフォームに組み込まれているインターフェイス。 IPMI は主に、システム ハードウェアの正常性を監視し、環境のエラー状況を処理に使用します。 IPMI の詳細については、、 [IPMI 仕様](https://go.microsoft.com/fwlink/p/?linkid=69485)を参照してください。

<a href="" id="low-level-hardware-error-handler--llheh-"></a>低レベルのハードウェア エラー ハンドラー (LLHEH)  
ハードウェアのエラー条件に応答して実行される最初のオペレーティング システム コード。 LLHEH、割り込みハンドラー、例外ハンドラー、ポーリングのルーチンまたはシステム ファームウェアによって呼び出されるコールバック ルーチンを使用できます。 すべての LLHEHs は、一般的なハードウェア エラー レポート関数を介してオペレーティング システムにハードウェア エラーを報告します。

<a href="" id="machine-check-abort--mca-"></a>マシン チェック中止 (MCA)  
Itanium プロセッサがハードウェア エラーが発生したことを示す、オペレーティング システムに報告する例外。

<a href="" id="machine-check-architecture--mca-"></a>マシン チェック アーキテクチャ (MCA)  
オペレーティング システムにハードウェア エラーを報告するために使用、ハードウェアとソフトウェア アーキテクチャです。

<a href="" id="machine-check-exception--mce-"></a>マシン チェック例外 (MCE)  
X86 または x64 プロセッサがハードウェア エラーが発生したことを示す、オペレーティング システムに報告する例外。

<a href="" id="machine-specific-register--msr-"></a>コンピューターの特定の登録 (MSR)  
システム ソフトウェアで特定の機能を実装するために使用される特定のプロセッサを登録します。 各 MSR の操作は、各プロセッサまたはプロセッサ ファミリに固有です。

<a href="" id="nonmaskable-interrupt--nmi-"></a>マスク不可能割り込み (NMI)  
プロセッサの現在の割り込みの優先度レベルに関係なく、オペレーティング システム、プロセッサを報告する割り込みです。 NMI は通常、プラットフォームのハードウェアの致命的なエラー状態を検出したときに通知されます。

<a href="" id="pci-express-advanced-error-reporting--pcie-aer-"></a>PCI Express Advanced エラー報告 (PCIe AER)  
堅牢なエラーが報告、標準的な PCI Express エラー レポート機構を提供する PCI Express の省略可能な拡張機能。 PCIe AER の詳細については、、 [PCI Express 仕様](https://go.microsoft.com/fwlink/p/?linkid=69486)を参照してください。

<a href="" id="platform-specific-hardware-error-driver--pshed-"></a>プラットフォーム固有のハードウェア エラー ドライバー (PSHED)  
ハードウェア エラー報告の基盤となるプラットフォームの機能の抽象化を提供する WHEA コンポーネント。 Microsoft では、各プロセッサ アーキテクチャを PSHEDs を提供します。 プラットフォーム ベンダーは、プラットフォーム固有の機能を活用するよう PSHED にプラグインを実装することによって、PSHED 機能を補うことができます。

<a href="" id="service-control-interrupt--sci-"></a>サービス コントロール (SCI) を中断します。  
ACPI ドライバーによって処理される割り込みです。 ACPI ドライバーは、SCI の受領デバイス、割り込みシグナル状態になるし、デバイスをそれに応じて応答を決定します。

<a href="" id="service-processor--sp-"></a>サービスのプロセッサ (SP)  
マイクロ コント ローラー、環境状態の監視と、特定のエラー条件の処理などのプラットフォームに固有の機能を管理するメインのプロセッサとは異なります。 サービスのプロセッサは、通常は、ベースボード管理コント ローラーのハードウェアのコンポーネントです。

 

 




