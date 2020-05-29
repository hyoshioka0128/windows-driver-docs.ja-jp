---
title: ドライバーのセキュリティ チェックリスト
description: この記事では、ドライバー開発者向けのドライバーセキュリティチェックリストについて説明します。
ms.assetid: 25375E02-FCA1-4E94-8D9A-AA396C909278
ms.date: 03/13/2020
ms.localizationpriority: medium
ms.openlocfilehash: f5fb99a4b7c936136b6e7f5776bf3f0b0982be45
ms.sourcegitcommit: 969a98d4866be74e145df617a9f0963053898a0d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/28/2020
ms.locfileid: "84153181"
---
# <a name="driver-security-checklist"></a>ドライバーのセキュリティ チェックリスト

この記事では、ドライバー開発者向けのドライバーセキュリティチェックリストを提供して、ドライバーが侵害されるリスクを軽減します。

## <a name="span-iddriver_security_overviewspanspan-iddriver_security_overviewspanspan-iddriver_security_overviewspandriver-security-overview"></a><span id="Driver_Security_Overview"></span><span id="driver_security_overview"></span><span id="DRIVER_SECURITY_OVERVIEW"></span>ドライバーのセキュリティの概要

セキュリティの欠陥とは、攻撃者がシステムをクラッシュしたり使用できなくなったりするような方法でドライバーが誤動作する原因となる欠陥です。 さらに、ドライバーコードの脆弱性により、攻撃者はカーネルにアクセスして、OS 全体を危険にさらす可能性を高めることができます。 ほとんどの開発者が自分のドライバーを操作しているときは、悪意のある攻撃者がコード内で脆弱性を悪用しようとするかどうかにかかわらず、ドライバーが適切に動作することに重点を置いています。

ただし、ドライバーがリリースされた後、攻撃者は、セキュリティの欠陥を調査して特定することができます。 開発者は、このような脆弱性の可能性を最小限に抑えるために、設計および実装フェーズでこれらの問題を考慮する必要があります。 目標は、ドライバーがリリースされる前に、既知のセキュリティの欠陥をすべて排除することです。

より安全なドライバーを作成するには、システム設計者 (意識的の脅威に対する潜在的な脅威の考え)、コードを実装する開発者、(悪用の原因となる一般的な操作のコーディング)、およびテストチーム (弱点と脆弱性の検出を積極的に試みる) が必要です。 これらのすべてのアクティビティを適切に調整することで、ドライバーのセキュリティが大幅に向上します。

攻撃されるドライバーに関連する問題を回避することに加えて、カーネルメモリをより正確に使用するなど、説明する手順の多くでは、ドライバーの信頼性が向上します。 これにより、サポートコストが削減され、お客様の製品の満足度が向上します。 以下のチェックリストのタスクを完了すると、これらのすべての目標を達成するのに役立ちます。

**セキュリティチェックリスト:** *これらの各トピックで説明されているセキュリティタスクを完了します。*

![空のチェックボックス](images/checkbox.png)[カーネルドライバーが必要であることを確認します](#confirmkernel)

![空のチェックボックス](images/checkbox.png)[ドライバーフレームワークを使用する](#confirmkernel)

![空のチェックボックス](images/checkbox.png)[ソフトウェアのみのドライバーへのアクセスを制御する](#controlsoftwareonly)

![空のチェックボックス](images/checkbox.png)[は、テストドライバーコードをテストしません](#donotproductionsign)。

![空のチェックボックス](images/checkbox.png)[脅威分析の実行](#threatanalysis)

![空のチェックボックス](images/checkbox.png)[ドライバーの安全なコーディングのガイドラインに従う](#driversecuritycodepractices)

![空のチェックボックス](images/checkbox.png)[HVCI 互換性の検証](#dgc)

![空のチェックボックス](images/checkbox.png)[テクノロジ固有のコードのベストプラクティスに従う](#technologyspecificcodepractices)

![空のチェックボックス](images/checkbox.png)[ピアコードレビューを実行](#peercodereview)する

![空のチェックボックス](images/checkbox.png)[ドライバーアクセス制御の管理](#managingdriveraccesscontrol)

![空のチェックボックス](images/checkbox.png)[デバイスのインストールのセキュリティを強化](#enhancedeviceinstallationsecurity)する

![空のチェックボックス](images/checkbox.png)[適切なリリースドライバーの署名を実行](#releasedriversigning)する

![空のチェックボックス](images/checkbox.png)[Visual Studio でコード分析を使用してドライバーのセキュリティを調査する](#use-code-analysis)

![空のチェックボックス](images/checkbox.png)[静的ドライバーの検証ツールを使用して脆弱性を確認する](#sdv)

![空](images/checkbox.png)[の Checkbox チェックコードと BinSkim Binary Analyzer](#binskim)

![空のチェックボックス](images/checkbox.png)[コード検証ツールを使用する](#codevalidationtools)

![空のチェックボックス](images/checkbox.png)[デバッガーの手法と拡張機能の確認](#debugger)

![空のチェックボックス](images/checkbox.png)[セキュリティで保護されたコーディングリソースの確認](#securecodingresources)

[重要な情報の概要](#keytakeaways)

## <a name="span-idconfirmkernelspanconfirm-that-a-kernel-driver-is-required"></a><span id="confirmkernel"></span>カーネルドライバーが必要であることを確認する

**セキュリティチェックリスト項目 \# 1:** *カーネルドライバーが必要であること、および Windows サービスやアプリなどの低いリスクアプローチが適していないことを確認します。*

ドライバーは Windows カーネル内に存在し、カーネルで実行するときに問題が発生すると、オペレーティングシステム全体が公開されます。 他のオプションが使用可能な場合、新しいカーネルドライバーを作成するよりもコストが低くなり、関連するリスクが少なくなる可能性があります。
組み込みの Windows ドライバーの使用方法の詳細については、「[ドライバーを作成する必要がありますか?](https://docs.microsoft.com/windows-hardware/drivers/gettingstarted/do-you-need-to-write-a-driver-)」を参照してください。

バックグラウンドタスクの使用方法の詳細については、「バックグラウンドタスクを使用し[たアプリのサポート](https://docs.microsoft.com/windows/uwp/launch-resume/support-your-app-with-background-tasks)」を参照してください。

Windows サービスの使用方法については、「[サービス](https://docs.microsoft.com/windows/desktop/Services/services)」を参照してください。

## <a name="span-idconfirmkernelspanuse-the-driver-frameworks"></a><span id="confirmkernel"></span>ドライバーフレームワークを使用する

**セキュリティチェックリスト項目 \# 2:** *ドライバーフレームワークを使用して、コードのサイズを縮小し、信頼性とセキュリティを向上させます。*

[Windows ドライバーフレームワーク](https://docs.microsoft.com/windows-hardware/drivers/wdf/)を使用して、コードのサイズを縮小し、信頼性とセキュリティを向上させます。  使用を開始するには、「 [WDF を使用してドライバーを開発する](https://docs.microsoft.com/windows-hardware/drivers/wdf/using-the-framework-to-develop-a-driver)」を参照してください。 低リスクのユーザーモードフレームワークドライバー (UMDF) の使用方法については、「[ドライバーモデルの選択](https://docs.microsoft.com/windows-hardware/drivers/gettingstarted/choosing-a-driver-model)」を参照してください。

古い形式の[Windows Driver Model (WDM)](https://docs.microsoft.com/windows-hardware/drivers/kernel/windows-driver-model)ドライバーを記述する方が時間がかかり、コストがかかり、ほとんどの場合、ドライバーフレームワークで使用可能なコードを再作成する必要があります。

Windows Driver Framework のソースコードはオープンソースであり、GitHub で入手できます。 これは、Windows 10 に付属する WDF ランタイム ライブラリのソース コードと同じです。 ドライバーと WDF のやりとりを追跡できるとき、ドライバーをさらに効果的にデバッグできます。 からダウンロード [https://github.com/Microsoft/Windows-Driver-Frameworks](https://github.com/Microsoft/Windows-Driver-Frameworks) します。

## <a name="span-idcontrolsoftwareonlyspancontrol-access-to-software-only-drivers"></a><span id="controlsoftwareonly"></span>ソフトウェアのみのドライバーへのアクセスを制御する

**セキュリティチェックリスト項目 \# 3:** *ソフトウェア専用ドライバーを作成する場合は、追加のアクセス制御を実装する必要があります。*

ソフトウェアのみのカーネルドライバーは、プラグアンドプレイ (PnP) を使用して特定のハードウェア Id に関連付けられることはなく、任意の PC で実行できます。 このようなドライバーは、最初に意図したもの以外の目的で使用できます。攻撃ベクトルを作成します。

ソフトウェアのみのカーネルドライバーは追加のリスクを含んでいるため、特定のハードウェア上で実行するように制限する必要があります (たとえば、一意の PnP ID を使用して PnP ドライバーの作成を有効にするか、特定のハードウェアがあるかどうかを SMBIOS テーブルでチェックします)。

たとえば、OEM Fabrikam が、システムのオーバークロックユーティリティを有効にするドライバーを配布するとします。  このソフトウェアのみのドライバーを別の OEM のシステムで実行する場合は、システムの不安定性または破損が発生する可能性があります。  Fabrikam のシステムには、Windows Update でも更新可能な PnP ドライバーの作成を有効にするための一意の PnP ID を含める必要があります。  これが不可能で、Fabrikam の作成者が従来のドライバーを使用している場合は、そのドライバーが Fabrikam システムで実行されていることを確認する別の方法を見つける必要があります (たとえば、すべての機能を有効にする前に SMBIOS テーブルを調べるなど)。

## <a name="span-iddonotproductionsignspan-do-not-production-sign-test-code"></a><span id="donotproductionsign"></span>テストコードを運用環境に署名しない

**セキュリティチェックリスト項目 \# 4:** *実稼働コード署名の開発、テスト、およびカーネルドライバーコードの製造を行いません。*

開発、テスト、または製造に使用されるカーネルドライバーのコードには、セキュリティ上のリスクをもたらす危険な機能が含まれている可能性があります。  この危険なコードは、Windows によって信頼されている証明書で署名されることはありません。  危険なドライバーコードを実行するための正しいメカニズムは、UEFI セキュアブートを無効にし、BCD "TESTSIGNING" を有効にし、信頼されていない証明書 (たとえば、makecert によって生成されたもの) を使用して開発、テスト、および製造コードに署名することです。

信頼できるソフトウェア発行元証明書 (SPC) または Windows Hardware Quality Labs (WHQL) の署名によって署名されたコードは、Windows コードの整合性とセキュリティテクノロジをバイパスできないようにする必要があります。  信頼された SPC または WHQL 署名によってコードが署名される前に、まず、[信頼性の高いカーネルモードドライバーの作成](https://docs.microsoft.com/windows-hardware/drivers/kernel/creating-reliable-kernel-mode-drivers)に関するガイダンスに準拠していることを確認します。 また、コードには、次に示す危険な動作を含めることはできません。  ドライバーの署名の詳細については、この記事で後述する「[リリースドライバーの署名](#releasedriversigning)」を参照してください。

危険な動作の例を次に示します。

- 任意のカーネル、物理、またはデバイスのメモリをユーザーモードにマップする機能を提供します。
- 任意のカーネル、物理またはデバイスのメモリ (ポートの入出力 (i/o) を含む) を読み書きする機能を提供します。
- Windows アクセス制御をバイパスするストレージへのアクセスを提供します。
- ドライバーが管理するように設計されていないハードウェアまたはファームウェアを変更する機能を提供します。  

## <a name="span-idthreatanalysisspanspan-idthreatanalysisspanspan-idthreatanalysisspanperform-threat-analysis"></a><span id="ThreatAnalysis"></span><span id="threatanalysis"></span><span id="THREATANALYSIS"></span>脅威分析を実行する

**セキュリティチェックリスト項目 \# 5:** *既存のドライバー脅威モデルを変更するか、ドライバーのカスタム脅威モデルを作成します。*

セキュリティを考慮して、一般的な方法としては、可能な攻撃の種類を記述する特定の脅威モデルを作成する方法があります。 この手法は、開発者がドライバーに対する潜在的な攻撃ベクトルを事前に考慮することを強制するため、ドライバーを設計するときに役立ちます。 潜在的な脅威を特定した後、ドライバーの開発者は、ドライバーコンポーネントの全体的なセキュリティを強化ために、これらの脅威に対する防御手段を検討できます。

この記事では、簡易脅威モデルを作成するためのドライバー固有のガイダンスとして、[ドライバーの脅威の](threat-modeling-for-drivers.md)モデル化について説明します。 この記事では、ドライバーの開始点として使用できるドライバー脅威モデル図の例を示します。

![架空のカーネルモードドライバーのサンプルデータフロー図](images/sampledataflowdiagramkernelmodedriver.gif)

セキュリティ開発ライフサイクル (SDL) のベストプラクティスと関連付けられているツールを、Ihv および Oem が製品のセキュリティを向上させるために使用できます。 詳細については、「 [oem 向けの SDL の推奨事項](https://docs.microsoft.com/windows-hardware/drivers/bringup/security-overview#sdl-recommendations-for-oems)」を参照してください。

## <a name="span-iddriversecuritycodepracticesspanspan-iddriversecuritycodepracticesspanspan-iddriversecuritycodepracticesspanfollow-driver-secure-coding-guidelines"></a><span id="DriverSecurityCodePractices"></span><span id="driversecuritycodepractices"></span><span id="DRIVERSECURITYCODEPRACTICES"></span>ドライバーの安全なコーディングのガイドラインに従う

**セキュリティチェックリスト項目 \# 6:** *コードを確認し、既知のコードの脆弱性を削除します。*

セキュリティで保護されたドライバーを作成するための主要なアクティビティは、既知のソフトウェアの脆弱性を回避するために変更する必要があるコード内の領域を識別することです。 これらの既知のソフトウェアの脆弱性の多くは、メモリの使用を厳密に追跡して、他のユーザーの問題を回避したり、ドライバーが使用するメモリの場所を上書きしたりしないようにします。

この記事の「[コード検証ツール](#codevalidationtools)」セクションでは、既知のソフトウェアの脆弱性を見つけるために使用できるソフトウェアツールについて説明します。

**メモリバッファー**

- バッファーが要求されたすべてのデータを保持できることを確認するために、入力バッファーと出力バッファーのサイズを常に確認してください。 詳細については、「[バッファーのサイズを確認できませんでした](https://docs.microsoft.com/windows-hardware/drivers/kernel/failure-to-check-the-size-of-buffers)。」を参照してください。

- すべての出力バッファーをゼロで初期化してから、呼び出し元に返すようにします。 詳細については、「[出力バッファーを初期化できませ](https://docs.microsoft.com/windows-hardware/drivers/kernel/failure-to-initialize-output-buffers)ん」を参照してください。

- 可変長バッファーを検証します。 詳細については、「[可変長バッファーの検証の失敗](https://docs.microsoft.com/windows-hardware/drivers/kernel/failure-to-validate-variable-length-buffers)」を参照してください。 バッファーの操作と[**ProbeForRead**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-probeforread)と[**ProbeForWrite**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-probeforwrite)を使用したバッファーのアドレスの検証の詳細については、「[バッファー処理](https://docs.microsoft.com/windows-hardware/drivers/ifs/buffer-handling)」を参照してください。

**Ioctl を使用してデータバッファーにアクセスするための適切なメソッドを使用する**

Windows ドライバーの主な役割の1つは、ユーザーモードアプリケーションとシステムデバイス間でデータを転送することです。 次の表に、データバッファーにアクセスするための3つの方法を示します。

|IOCTL バッファーの種類 | まとめ                                    | 詳細情報 |  
|------------------|--------------------------------------------|-------------------------------------------------------------------------|
| METHOD_BUFFERED  |ほとんどの situtations に推奨            | [バッファー付き I/O の使用](https://docs.microsoft.com/windows-hardware/drivers/kernel/using-buffered-i-o)
| METHOD_IN_DIRECT または METHOD_OUT_DIRECT |一部の高速ハードウェア i/o で使用されます。    |[ダイレクト I/O の使用](https://docs.microsoft.com/windows-hardware/drivers/kernel/using-direct-i-o) |
| METHOD_NEITHER |可能な限り回避する |[バッファー付き I/O とダイレクト I/O のどちらも使用しない](https://docs.microsoft.com/windows-hardware/drivers/kernel/using-neither-buffered-nor-direct-i-o)|

一般に、バッファー内の i/o は、最も安全なバッファリング方法を提供するため、お勧めします。 ただし、バッファリングされた i/o を使用する場合でも、軽減する必要がある埋め込みポインターなどのリスクがあります。

Ioctl でのバッファーの使用の詳細については、「[データバッファーにアクセスするためのメソッド](https://docs.microsoft.com/windows-hardware/drivers/kernel/methods-for-accessing-data-buffers)」を参照してください。

**IOCTL でバッファリングされる i/o の使用エラー**

- IOCTL 関連のバッファーのサイズを確認します。 詳細については、「[バッファーのサイズを確認できませんでした](https://docs.microsoft.com/windows-hardware/drivers/kernel/failure-to-check-the-size-of-buffers)。」を参照してください。

- 出力バッファーを適切に初期化します。 詳細については、「[出力バッファーを初期化できませ](https://docs.microsoft.com/windows-hardware/drivers/kernel/failure-to-initialize-output-buffers)ん」を参照してください。

- 可変長バッファーを適切に検証します。 詳細については、「[可変長バッファーの検証の失敗](https://docs.microsoft.com/windows-hardware/drivers/kernel/failure-to-validate-variable-length-buffers)」を参照してください。

- バッファーされた i/o を使用する場合は、[ [IO_STATUS_BLOCK](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_io_status_block)構造情報] フィールドに出力バッファーの適切な長さを指定してください。  読み取り要求から直接長さを直接返すだけではありません。  たとえば、ユーザー空間から返されたデータが4K バッファーがあることを示しているとします。  ドライバーが実際には200バイトのみを返す必要があるが、代わりに情報フィールドで4K が返されるだけの場合は、情報漏えいの脆弱性が発生しています。 この問題は、以前のバージョンの Windows では、i/o マネージャーがバッファー i/o に使用するバッファーがゼロになっていないために発生します。  このため、ユーザーアプリは、元の200バイトのデータと、バッファー (非ページプールのコンテンツ) にあるものをすべて 4K ~ 200 バイトに戻します。 このシナリオは、Ioctl だけでなく、バッファリングされた i/o を使用する場合にも発生する可能性があります。

**IOCTL direct i/o のエラー**

長さ0のバッファーを正しく処理します。 詳細については、「 [Direct i/o のエラー](https://docs.microsoft.com/windows-hardware/drivers/kernel/errors-in-direct-i-o)」を参照してください。

**ユーザー領域のアドレスを参照中のエラー**

- バッファーされた i/o 要求に埋め込まれたポインターを検証します。 詳細については、「[ユーザー領域の参照」の「エラー](https://docs.microsoft.com/windows-hardware/drivers/kernel/errors-in-referencing-user-space-addresses)」を参照してください。

- 必要に応じて、 [**ProbeForRead**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-probeforread)や[**ProbeForWrite**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-probeforwrite)などの api を使用して、使用する前に、ユーザー空間内の任意のアドレスを検証します。

**TOCTOU の脆弱性**

直接 i/o (Ioctl または読み取り/書き込み用) を使用しているときに、TOCTOU ( [time to use) の](https://en.wikipedia.org/wiki/Time_of_check_to_time_of_use)脆弱性が発生する可能性があります。  ドライバーはユーザーデータバッファーにアクセスしているため、ユーザーが同時にアクセスできることに注意してください。

このリスクを管理するには、ユーザーデータバッファーから検証する必要のあるすべてのパラメーターを、カーネルモード (スタック、プールなど) からのみ accessibly されるメモリにコピーします。  ユーザーアプリケーションがデータにアクセスできない場合は、渡されたデータを検証して、操作します。

**ドライバーコードでメモリの正しい使用を行う必要がある**

- すべてのドライバープールの割り当ては、実行可能でない (NX) プールにある必要があります。 NX メモリプールを使用することは、本質的に、実行可能な非ページ (NP) プールを使用するよりも安全性が高く、オーバーフロー攻撃に対する保護が強化されています。

- デバイスドライバーは、カーネル i/o の要求に加えて、さまざまなユーザーモードを正しく処理する必要があります。

ドライバーが HVCI 仮想化をサポートできるようにするには、追加のメモリ要件があります。 詳細については、この記事で後述する「 [Hvci の互換性](#dgc)」を参照してください。

**Handles**

- ユーザーモードとカーネルモードのメモリの間で渡されるハンドルを検証します。 詳細については、「[ハンドル管理](https://docs.microsoft.com/windows-hardware/drivers/ifs/handle-management)と[エラーによるオブジェクトハンドルの検証」を](https://docs.microsoft.com/windows-hardware/drivers/kernel/failure-to-validate-object-handles)参照してください。

**デバイスオブジェクト**

- デバイスオブジェクトをセキュリティで保護します。 詳細については、「[デバイスオブジェクトのセキュリティ保護](https://docs.microsoft.com/windows-hardware/drivers/kernel/securing-device-objects)」を参照してください。

- デバイスオブジェクトを検証します。 詳細については、「[デバイスオブジェクトの検証エラー](https://docs.microsoft.com/windows-hardware/drivers/kernel/failure-to-validate-device-objects)」を参照してください。

**Irp**

**WDF と Irp**

WDF を使用する利点の1つは、WDF ドライバーは通常、Irp に直接アクセスしないことです。 たとえば、フレームワークは、読み取り、書き込み、およびデバイス i/o 制御操作を表す WDM Irp を、KMDF/UMDF が i/o キューで受信するフレームワーク要求オブジェクトに変換します。

WDM ドライバーを作成する場合は、次のガイダンスを確認してください。

**IRP i/o バッファーを適切に管理する**

次の記事では、IRP 入力値の検証に関する情報を提供します。

[バッファー付き I/O を使用した DispatchReadWrite](https://docs.microsoft.com/windows-hardware/drivers/kernel/dispatchreadwrite-using-buffered-i-o)

[バッファー付き I/O のエラー](https://docs.microsoft.com/windows-hardware/drivers/kernel/errors-in-buffered-i-o)

[ダイレクト I/O を使用した DispatchReadWrite](https://docs.microsoft.com/windows-hardware/drivers/kernel/dispatchreadwrite-using-direct-i-o)

[ダイレクト I/O のエラー](https://docs.microsoft.com/windows-hardware/drivers/kernel/errors-in-direct-i-o)

[I/O 制御コードに関するセキュリティの問題](https://docs.microsoft.com/windows-hardware/drivers/kernel/security-issues-for-i-o-control-codes)

バッファーのアドレスや長さなど、IRP に関連付けられている値を検証することを検討してください。

どちらの i/o も使用しないことを選択した場合は、読み取りと書き込みのほか、バッファーに格納されている i/o やダイレクト i/o とは異なり、i/o IOCTL を使用していない場合、バッファーポインターと長さは i/o マネージャーによって検証されないことに注意してください。  

**IRP 完了操作を正しく処理する**

Irp を \_ 実際にサポートして処理しない限り、状態値が SUCCESS の irp は、ドライバーで完了することはできません。 IRP の完了操作を処理する正しい方法については、「 [irp の完了](https://docs.microsoft.com/windows-hardware/drivers/kernel/completing-irps)」を参照してください。

**ドライバーの IRP 保留状態の管理**

ドライバーは、irp を保存する前に保留中の IRP をマークする必要があります。また、 [**Iomarkirppending**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iomarkirppending)の呼び出しと、インタロックされたシーケンス内の割り当ての両方を含めることを検討する必要があります。 詳細については、「[ドライバーの状態を確認できませ](https://docs.microsoft.com/windows-hardware/drivers/kernel/failure-to-check-a-driver-s-state)ん」および「[デバイスが一時停止したときに受信 irp を保持](https://docs.microsoft.com/windows-hardware/drivers/kernel/holding-incoming-irps-when-a-device-is-paused)する」を参照してください。

**IRP のキャンセル操作を適切に処理する**

通常、キャンセル操作は非同期的に実行されるため、適切にコーディングするのが困難な場合があります。 通常、このコードは実行中のシステムで頻繁に実行されないため、キャンセル操作を処理するコードの問題は、長時間気付かないことがあります。 「 [Irp の取り消し](https://docs.microsoft.com/windows-hardware/drivers/kernel/canceling-irps)」で提供されているすべての情報を読んで理解してください。 Irp を[キャンセルするときに考慮する必要が](https://docs.microsoft.com/windows-hardware/drivers/kernel/points-to-consider-when-canceling-irps)ある[irp のキャンセル](https://docs.microsoft.com/windows-hardware/drivers/kernel/synchronizing-irp-cancellation)とポイントの同期に特に注意してください。

キャンセル操作に関連する同期の問題を最小限に抑える方法として、[キャンセルセーフの IRP キュー](https://docs.microsoft.com/windows-hardware/drivers/kernel/cancel-safe-irp-queues)を実装することをお勧めします。

**IRP のクリーンアップと終了操作を正しく処理する**

[**Irp \_ MJ \_ CLEANUP**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-cleanup)要求と[**irp \_ MJ \_ CLOSE**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-close)要求の違いを理解していることを確認してください。 クリーンアップ要求は、アプリケーションがファイルオブジェクトのすべてのハンドルを閉じた後に到着しますが、すべての i/o 要求が完了する前に発生することもあります。 Close 要求は、ファイルオブジェクトのすべての i/o 要求が完了または取り消された後に到着します。 詳細については、以下の記事を参照してください。

[DispatchCreate、DispatchClose、DispatchCreateClose ルーチン](https://docs.microsoft.com/windows-hardware/drivers/kernel/dispatchcreate--dispatchclose--and-dispatchcreateclose-routines)

[DispatchCleanup ルーチン](https://docs.microsoft.com/windows-hardware/drivers/kernel/dispatchcleanup-routines)

[クリーンアップ操作と閉じる操作の処理エラー](https://docs.microsoft.com/windows-hardware/drivers/kernel/errors-in-handling-cleanup-and-close-operations)

Irp を正しく処理する方法の詳細については、「 [irp の処理に関するその他のエラー](https://docs.microsoft.com/windows-hardware/drivers/kernel/additional-errors-in-handling-irps)」を参照してください。

**その他のセキュリティの問題**

- 競合状態を回避するには、ロックまたはインタロックされたシーケンスを使用します。 詳細については、「[マルチプロセッサ環境でのエラー](https://docs.microsoft.com/windows-hardware/drivers/kernel/errors-in-a-multiprocessor-environment)」を参照してください。

- デバイスドライバーがさまざまなユーザーモードおよびカーネルのカーネル i/o 要求を適切に処理していることを確認します。

- インストール時または使用時に、ドライバーまたは関連付けられているソフトウェアパッケージによって、TDI フィルターまたは Lsp がインストールされていないことを確認します。

**セーフ関数の使用**

- 安全な文字列関数を使用します。 詳細については、「[安全な文字列関数の使用](https://docs.microsoft.com/windows-hardware/drivers/kernel/using-safe-string-functions)」を参照してください。

- 安全な算術関数を使用します。 詳細については、「[安全な整数ライブラリルーチン](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)の[算術関数](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)」を参照してください。

- 安全な変換関数を使用します。 詳細については、「[安全な整数ライブラリルーチン](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)の[変換関数](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)」を参照してください。

**その他のコードの脆弱性**

この記事では、ここで説明する脆弱性に加えて、カーネルモードドライバーコードのセキュリティ強化に関する追加情報を提供します。[信頼できるカーネルモードドライバーの作成](https://docs.microsoft.com/windows-hardware/drivers/kernel/creating-reliable-kernel-mode-drivers)。

C および C++ のセキュリティで保護されたコーディングの詳細については、この記事の最後にある「[安全なコーディングリソース](#securecodingresources)」を参照してください。

## <a name="span-idmanagingdriveraccesscontrolspanspan-idmanagingdriveraccesscontrolspanspan-idmanagingdriveraccesscontrolspanmanage-driver-access-control"></a><span id="ManagingDriverAccessControl"></span><span id="managingdriveraccesscontrol"></span><span id="MANAGINGDRIVERACCESSCONTROL"></span>ドライバーアクセス制御の管理

**セキュリティチェックリスト項目 \# 7:** *アクセスを適切に制御していることを確認するために、ドライバーを確認*します。

**ドライバーアクセス制御の管理-WDF**

ユーザーがコンピューターのデバイスとファイルに不適切にアクセスできないようにするには、ドライバーが機能している必要があります。 デバイスとファイルへの不正アクセスを防ぐには、次のことを行う必要があります。

- 必要な場合にのみ、デバイスオブジェクトに名前を指定します。 名前付きデバイスオブジェクトは、一般に、特定の名前を使用してデバイスを開くことが想定されているアプリケーションや、PNP 以外のデバイス/コントロールデバイスを使用している場合など、従来の理由でのみ必要になります。  [WdfDeviceCreateSymbolicLink](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdevicecreatesymboliclink)を使用してシンボリックリンクを作成するには、WDF ドライバーが PNP デバイス FDO に名前を付ける必要はないことに注意してください。

- デバイスオブジェクトとインターフェイスへのアクセスをセキュリティで保護します。

アプリケーションまたはその他の WDF ドライバーが PnP デバイス PDO にアクセスできるようにするには、デバイスインターフェイスを使用する必要があります。 詳細については、「[デバイスインターフェイスの使用](https://docs.microsoft.com/windows-hardware/drivers/wdf/using-device-interfaces)」を参照してください。 デバイスインターフェイスは、デバイススタックの PDO へのシンボリックリンクとして機能します。

PDO へのアクセスを制御する betters 方法の1つは、INF で SDDL 文字列を指定することです。 SDDL 文字列が INF ファイルにない場合は、Windows によって既定のセキュリティ記述子が適用されます。 詳細については、「デバイスオブジェクトの[セキュリティ保護](https://docs.microsoft.com/windows-hardware/drivers/kernel/securing-device-objects)」と「[デバイスオブジェクトの SDDL](https://docs.microsoft.com/windows-hardware/drivers/kernel/sddl-for-device-objects)」を参照してください。

アクセス制御の詳細については、次の記事を参照してください。

[KMDF ドライバーでのデバイス アクセスの制御](https://docs.microsoft.com/windows-hardware/drivers/wdf/controlling-device-access-in-kmdf-drivers)

[名前、セキュリティ記述子、デバイスクラス-デバイスオブジェクトにアクセスできるようにしています...](https://www.osr.com/nt-insider/2017-issue1/making-device-objects-accessible-safe/)2017 年1月から安全に、 [OSR](https://www.osr.com)で公開され*た NT Insider ニュースレター*です。

**ドライバーアクセス制御の管理-WDM**

WDM ドライバーを使用していて、名前付きデバイスオブジェクトを使用している場合は、 [Iocreateデバイス](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdmsec/nf-wdmsec-wdmlibiocreatedevicesecure)を使用し、SDDL を指定してセキュリティ保護することができます。 [IocreateDeviceClassGuid](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdmsec/nf-wdmsec-wdmlibiocreatedevicesecure)を実装するときは、常にカスタムクラス GUID を指定します。 ここでは、既存のクラス GUID を指定しないでください。 これにより、そのクラスに属する他のデバイスのセキュリティ設定または互換性が損なわれる可能性があります。 詳細については、「 [WdmlibIoCreateDeviceSecure](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdmsec/nf-wdmsec-wdmlibiocreatedevicesecure)」を参照してください。

詳細については、以下の記事を参照してください。

[デバイス アクセスの制御](https://docs.microsoft.com/windows-hardware/drivers/kernel/controlling-device-access)

[デバイスの名前空間アクセスの制御](https://docs.microsoft.com/windows-hardware/drivers/kernel/controlling-device-namespace-access)

[ドライバー開発者向けの Windows セキュリティ モデル](windows-security-model.md)

**セキュリティ識別子 (Sid) のリスク階層**

次のセクションでは、ドライバーコードで使用される共通 Sid のリスク階層について説明します。 SDDL に関する一般的な情報については、「デバイスオブジェクト、 [SID 文字列](https://docs.microsoft.com/windows/desktop/SecAuthZ/sid-strings)、 [sddl 文字列構文](https://docs.microsoft.com/openspecs/windows_protocols/ms-dtyp/f4296d69-1c0f-491f-9587-a960b292d070)[の sddl](https://docs.microsoft.com/windows-hardware/drivers/kernel/sddl-for-device-objects)」を参照してください。

低い特権の呼び出し元がカーネルへのアクセスを許可されている場合、コードのリスクが増加することを理解しておくことが重要です。 この概要図では、より低い特権の Sid がドライバーの機能にアクセスできるようになると、リスクが増加します。

```cpp
SY (System)
\/
BA (Built-in Administrators)
\/
LS (Local Service)
\/
BU (Built-in User)
\/
AC (Application Container)
```

一般的な最小特権のセキュリティ原則に従って、ドライバーが機能するために必要な最小限のアクセスレベルのみを構成します。

**WDM の詳細な IOCTL セキュリティ制御**

ユーザーモードの呼び出し元によって Ioctl が送信されるときにセキュリティをさらに管理するために、ドライバーコードには[IoValidateDeviceIoControlAccess](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iovalidatedeviceiocontrolaccess)関数を含めることができます。 この関数を使用すると、ドライバーはアクセス権を確認できます。 IOCTL を受け取ると、ドライバーは、FILE_READ_ACCESS、FILE_WRITE_ACCESS、またはその両方を指定して[IoValidateDeviceIoControlAccess](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iovalidatedeviceiocontrolaccess)を呼び出すことができます。

詳細な IOCTL セキュリティ制御を実装しても、上記の手法を使用したドライバーアクセスの管理は不要になります。

詳細については、以下の記事を参照してください。

[I/O 制御コードの定義](https://docs.microsoft.com/windows-hardware/drivers/kernel/defining-i-o-control-codes)

## <a name="span-iddgcspanspan-iddgcspanvalidate-hvci-compatibility"></a><span id="DGC"></span><span id="dgc"></span>HVCI 互換性の検証

**セキュリティチェックリスト項目 \# 8:** *hvci と互換性があるように、ドライバーがメモリを使用していることを確認*します。

**メモリ使用量と HVCI の互換性**

HVCI は、ハードウェアテクノロジと仮想化を使用して、コード整合性 (CI) の意思決定機能をオペレーティングシステムの他の部分から分離します。 仮想化ベースのセキュリティを使用して CI を分離する場合、カーネルメモリを実行可能ファイルにする唯一の方法は、CI の検証を使用することです。 そのため、カーネル メモリのページは決して書き込み可能または実行可能 (W+X) にならず、実行可能コードを直接変更することはできません。

HVCI 互換コードを実装するには、ドライバーコードが次のことを実行するようにします。

- 既定で NX に設定する
- メモリ割り当てに NX Api/フラグを使用します (NonPagedPoolNx)
- 書き込み可能および実行可能ファイルの両方のセクションを使用しない
- 実行可能なシステムメモリを直接変更しません。
- カーネルで動的コードを使用しない
- 実行可能ファイルとしてデータファイルを読み込みません
- セクションの配置は、0x1000 (ページサイズ) の倍数です \_ 。 例: ドライバーの \_ アラインメント = 0x1000

ツールの使用および互換性のないメモリ呼び出しの一覧については、「 [HVCI ドライバーの互換性を評価](use-device-guard-readiness-tool.md)する」を参照してください。

関連するシステムの基礎セキュリティテストの詳細については、「 [Device guard](https://docs.microsoft.com/windows-hardware/test/hlk/testref/10c242b6-49f6-491d-876c-c39b22b36abc)と[Device Guard の互換性](https://docs.microsoft.com/windows-hardware/test/hlk/testref/driver-compatibility-with-device-guard)テストおよびドライバーの互換性」を参照してください。

## <a name="span-idtechnologyspecificcodepracticesspanfollow-technology-specific-code-best-practices"></a><span id="technologyspecificcodepractices"></span>テクノロジ固有のコードのベストプラクティスに従う

**セキュリティチェックリスト項目 \# 9:** *次のテクノロジ固有のドライバーに関するガイダンスを確認します。*

*ファイルシステム*

ファイルシステムドライバーのセキュリティの詳細については、次の記事を参照してください。

[ファイル システムのセキュリティに関する考慮事項](https://docs.microsoft.com/windows-hardware/drivers/ifs/security-considerations-for-file-systems)

[ファイル システムのセキュリティに関する問題](https://docs.microsoft.com/windows-hardware/drivers/ifs/file-system-security-issues)

[ファイル システム向けのセキュリティ機能](https://docs.microsoft.com/windows-hardware/drivers/ifs/security-features-for-file-systems)

[ファイル システム フィルター ドライバーのセキュリティに関する考慮事項](https://docs.microsoft.com/windows-hardware/drivers/ifs/security-considerations-for-file-system-filter-drivers)

*NDIS-ネットワーク*

NDIS ドライバーのセキュリティについては、「[ネットワークドライバーのセキュリティの問題](https://docs.microsoft.com/windows-hardware/drivers/network/security-issues-for-network-drivers)」を参照してください。

*ディスプレイ*

ディスプレイドライバーのセキュリティについては、「保留中のコンテンツ」を参照してください &lt; &gt; 。

*プリンター*

プリンタードライバーのセキュリティに関する詳細については、「 [V4 プリンタードライバーのセキュリティに関する考慮事項](https://docs.microsoft.com/windows-hardware/drivers/print/v4-printer-driver-security-considerations)」を参照してください。

*Windows イメージ取得 (WIA) ドライバーに関するセキュリティの問題*

WIA のセキュリティについては、「 [Windows イメージ取得 (wia) ドライバーのセキュリティの問題](https://docs.microsoft.com/windows-hardware/drivers/image/security-issues-for-wia-drivers)」を参照してください。

## <a name="span-idenhancedeviceinstallationsecurityspanenhance-device-installation-security"></a><span id="enhancedeviceinstallationsecurity"></span>デバイスのインストールセキュリティを強化する

**セキュリティチェックリスト項目 \# 10:** *ドライバー inf の作成とインストールのガイダンスを確認し、ベストプラクティスに従っていることを確認します。*

ドライバーをインストールするコードを作成する場合は、デバイスのインストールが常に安全な方法で実行されるようにする必要があります。 セキュリティで保護されたデバイスのインストールとは、次のようなものです。

- デバイスとそのデバイスインターフェイスクラスへのアクセスを制限します。
- デバイス用に作成されたドライバーサービスへのアクセスを制限します。
- ドライバーファイルの変更または削除を防止します。
- デバイスのレジストリエントリへのアクセスを制限します。
- デバイスの WMI クラスへのアクセスを制限します。
- Setupapi.log 関数を正しく使用します

詳細については、以下の記事を参照してください。

[セキュリティで保護されたデバイスのインストールの作成](https://docs.microsoft.com/windows-hardware/drivers/install/creating-secure-device-installations)

[SetupAPI の使用に関するガイドライン](https://docs.microsoft.com/windows-hardware/drivers/install/guidelines-for-using-setupapi)

[デバイス インストール関数の使用](https://docs.microsoft.com/windows-hardware/drivers/install/using-device-installation-functions)

[デバイスとドライバーのインストールに関する高度なトピック](https://docs.microsoft.com/windows-hardware/drivers/install/device-and-driver-installation-advanced-topics)

## <a name="span-idpeercodereviewspanperform-peer-code-review"></a><span id="peercodereview"></span>ピアコードレビューの実行

**セキュリティチェックリスト項目 \# 11:** *ピアコードレビューを実行し、他のツールやプロセスによって表示されない問題を探し*ます。

知識のあるコードレビュー担当者に相談して、問題が発生した可能性のある問題を探します。 2番目の目のセットには、見落とされがちな問題が表示されることがよくあります。

コードを内部的にレビューするのに適したスタッフがいない場合は、この目的に対して外部のヘルプを使用することを検討してください。

## <a name="span-idreleasedriversigningspanspan-idreleasedriversigningspanspan-idreleasedriversigningspanexecute-proper-release-driver-signing"></a><span id="ReleaseDriverSigning"></span><span id="releasedriversigning"></span><span id="RELEASEDRIVERSIGNING"></span>適切なリリースドライバーの署名を実行する

**セキュリティチェックリスト項目 \# 12:** *Windows パートナーポータルを使用して、配布するドライバーに適切に署名します。*

ドライバー パッケージを一般にリリースする前に、パッケージの認定依頼を提出することをお勧めします。 詳細については、「[パフォーマンスと互換性のテスト](https://docs.microsoft.com/windows-hardware/test/index)」、「[ハードウェアプログラムの概要](https://docs.microsoft.com/windows-hardware/drivers/dashboard/get-started-with-the-hardware-dashboard)」、「[ハードウェアダッシュボードサービス](https://docs.microsoft.com/windows-hardware/drivers/dashboard/dashboard-services)」、および「[構成証明](https://docs.microsoft.com/windows-hardware/drivers/dashboard/attestation-signing-a-kernel-driver-for-public-release)」を参照してください。

## <a name="span-iduse-code-analysisspanuse-code-analysis-in-visual-studio-to-investigate-driver-security"></a><span id="use-code-analysis"></span>Visual Studio でコード分析を使用してドライバーのセキュリティを調査する

**セキュリティチェックリスト項目 \# 13:** *Visual Studio のコード分析機能を使用して、ドライバーコードの脆弱性を確認するには、次の手順に従います。*

Visual Studio のコード分析機能を使用して、コード内のセキュリティの脆弱性を確認します。 Windows Driver Kit (WDK) は、ネイティブドライバーコードの問題をチェックするように設計された規則セットをインストールします。

詳細については、「[ドライバーのコード分析を実行する方法](https://docs.microsoft.com/windows-hardware/drivers/devtest/how-to-run-code-analysis-for-drivers)」を参照してください。

詳細については、「[ドライバーのコード分析の概要](https://docs.microsoft.com/windows-hardware/drivers/devtest/code-analysis-for-drivers-overview)」を参照してください。 コード分析の背景の詳細については、「 [Visual Studio 2013 の静的コード分析の詳細](https://blogs.msdn.microsoft.com/hkamel/2013/10/24/visual-studio-2013-static-code-analysis-in-depth-what-when-and-how/)」を参照してください。

コード分析に慣れるには、サンプルドライバー (おすすめのトースターサンプル、 <https://github.com/Microsoft/Windows-driver-samples/tree/master/general/toaster/toastDrv/kmdf/func/featured> ELAM 起動時マルウェア対策サンプルなど) のいずれかを使用でき <https://github.com/Microsoft/Windows-driver-samples/tree/master/security/elam> ます。

1. Visual Studio でドライバーソリューションを開きます。

2. Visual Studio で、ソリューション内の各プロジェクトについて、目的の規則セットを使用するようにプロジェクトのプロパティを変更します。 例: プロジェクト &gt; &gt; プロパティ &gt; &gt; コード分析 &gt; &gt; 全般、推奨さ*れるドライバー規則*を選択します。 Recommenced ドライバーの規則を使用するだけでなく、"*推奨されるネイティブ規則*" 規則セットを使用します。

3. &gt; &gt; ソリューションでビルド実行コード分析を選択します。

4. Visual Studio の [ビルド出力] ウィンドウの [**エラー一覧**] タブで警告を表示します。

各警告の説明をクリックして、コード内の問題のある領域を確認します。

リンク先の警告コードをクリックすると、追加情報が表示されます。

コードを変更する必要があるかどうか、またはコード分析エンジンがコードの意図に適切に従うために注釈を追加する必要があるかどうかを判断します。 コード注釈の詳細については、「SAL 注釈を使用して、Windows ドライバーの[C/c + + のコード障害](https://docs.microsoft.com/visualstudio/code-quality/using-sal-annotations-to-reduce-c-cpp-code-defects?view=vs-2015)と[Sal 2.0 の注釈](https://docs.microsoft.com/windows-hardware/drivers/devtest/sal-2-annotations-for-windows-drivers)を減らす」を参照してください。

SAL に関する一般的な情報については、OSR から入手できるこの記事を参照してください。
[https://www.osr.com/blog/2015/02/23/sal-annotations-dont-hate-im-beautiful/](https://www.osr.com/blog/2015/02/23/sal-annotations-dont-hate-im-beautiful/)

## <a name="span-idsdvspanspan-idsdvspanuse-static-driver-verifier-to-check-for-vulnerabilities"></a><span id="SDV"></span><span id="sdv"></span>静的ドライバー検証ツールを使用して脆弱性を確認する

**セキュリティチェックリスト項目 \# 14:** *Visual Studio で静的ドライバー検証ツール (sdv) を使用して、ドライバーコードの脆弱性を確認するに*は、次の手順に従います。

静的ドライバー検証ツール (SDV) は、一連のインターフェイス規則とオペレーティングシステムのモデルを使用して、ドライバーが Windows オペレーティングシステムと正しく通信するかどうかを判断します。 SDV は、ドライバーの潜在的なバグを指している可能性のあるドライバーコードの欠陥を検出します。

詳細については、「[静的ドライバー検証](https://docs.microsoft.com/windows-hardware/drivers/devtest/introducing-static-driver-verifier)機能と[静的ドライバー検証](https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier)機能の概要」を参照してください。 SDV では、特定の種類のドライバーのみがサポートされていることに注意してください。 SDV で検証できるドライバーの詳細については、「[サポートされ](https://docs.microsoft.com/windows-hardware/drivers/devtest/supported-drivers)ているドライバー」を参照してください。

SDV に慣れるには、サンプルドライバー (たとえば、おすすめのトースターサンプル) のいずれかを使用し <https://github.com/Microsoft/Windows-driver-samples/tree/master/general/toaster/toastDrv/kmdf/func/featured> ます。

1. Visual Studio で対象のドライバーソリューションを開きます。

2. Visual Studio で、ビルドの種類を [*リリース*] に変更します。 静的ドライバーの検証ツールでは、ビルドの種類がデバッグではなくリリースであることが必要です。

3. Visual Studio で、[ビルド] [ソリューションのビルド] を選択し &gt; &gt; ます。

4. Visual Studio で、[ドライバー] [起動] [静的ドライバーの検証] を選択し &gt; &gt; ます。

5. SDV の [*規則*] タブで、[*規則セット*] の下の [*既定*] を選択します。

既定のルールでは多くの一般的な問題が検出されますが、さらに広範な*ドライバールール*のルールセットを実行することを検討してください。

6. SDV の*メイン*タブで、[*開始*] をクリックします。

7. SDV が完了したら、出力の警告を確認します。 [*メイン*] タブには、見つかった欠陥の合計数が表示されます。

8. 各警告をクリックして SDV レポートページを読み込み、コードの脆弱性に関連する情報を確認します。 レポートを使用して、検証結果を調査し、SDV 検証に失敗したドライバーのパスを特定します。 詳細については、「 [Static Driver Verifier Report](https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier-report)」を参照してください。

## <a name="span-idbinskimspanspan-idbinskimspanspan-idbinskimspancheck-code-with-the-binskim-binary-analyzer"></a><span id="BinSkim"></span><span id="binskim"></span><span id="BINSKIM"></span>BinSkim Binary Analyzer を使用してコードを確認する

**セキュリティチェックリスト項目 \# 15:** *binskim を使用して、コンパイルおよびビルドオプションが既知のセキュリティ問題を最小限に抑えるように構成されていることを確認するには、次の手順に従います。*

BinSkim を使用してバイナリファイルを調査し、バイナリを脆弱にする可能性があるコーディングと作成の手法を特定します。

ビンの詳細チェック:

- 古いコンパイラツールセットの使用-バイナリは、最新のコンパイラツールセットに対してコンパイルし、現在のコンパイラレベルと OS によって提供されるセキュリティの軽減策を最大限に活用できるようにする必要があります。
- 安全でないコンパイル設定-バイナリは、OS によって提供されるセキュリティの緩和策を有効にし、コンパイラエラーや実行可能な警告の報告を最大化するために、最も安全な設定を使用してコンパイルする必要があります。
- 署名に関する問題-署名付きバイナリは、暗号強度の高いアルゴリズムで署名する必要があります。

BinSkim はオープンソースツールであり、静的な分析結果交換形式 ([SARIF](https://github.com/oasis-tcs/sarif-spec)) 形式を使用する出力ファイルを生成します。 ビンの説明は、前の[Binskim](https://www.microsoft.com/security/blog/2014/11/20/new-binscope-released/)ツールに代わるものです。

ビンの詳細については、「 [Binskim ユーザーガイド](https://github.com/microsoft/binskim/blob/master/docs/UserGuide.md)」を参照してください。

次の手順に従って、配布するコードでセキュリティコンパイルオプションが適切に構成されていることを確認します。

1. クロスプラットフォーム[.NET Core SDK](https://dotnet.microsoft.com/download)をダウンロードしてインストールします。

2. ビンの表示をダウンロードするには、NuGet パッケージなど、いくつかのオプションがあります。 この例では、次の BinSkim を含む zip ファイルをダウンロード <https://github.com/microsoft/binskim> して、64ビットの WINDOWS PC にインストールします。

3. [**複製またはダウンロード**] ボタンをクリックし、[download Zip] \ (Zip の <https://github.com/microsoft/binskim> **ダウンロード**\) を選択します。

4. ダウンロードした zip ファイルをクリックして解凍します (たとえば、) `C:\binskim-master` 。

5. Visual Studio がインストールされていることを確認します。 Visual Studio のダウンロードとインストールの詳細については、「 [Visual studio のインストール](https://docs.microsoft.com/visualstudio/install/install-visual-studio?view=vs-2019)」を参照してください。

6. Visual Studio の開発者コマンドプロンプトウィンドウを開き、ファイルを解凍したディレクトリに移動します。  

```console
C:\> Cd \binskim-master
```

7. 参加リストのルートで**Buildandtest. cmd**を実行して、リリースビルドが成功し、すべてのテストが成功することを確認します。

```console
C:\binskim-master> BuildAndTest.cmd

Welcome to .NET Core 3.1!
---------------------
SDK Version: 3.1.101

...

C:\binskim-master\bld\bin\AnyCPU_Release\Publish\netcoreapp2.0\win-x64\BinSkim.Sdk.dll
1 File(s) copied
C:\binskim-master\bld\bin\AnyCPU_Release\Publish\netcoreapp2.0\linux-x64\BinSkim.Sdk.dll
1 File(s) copied

...

```

8. ビルドプロセスでは、BinSkim 実行可能ファイルを含む一連のディレクトリが作成されます。 Win-x64 ビットのビルド出力ディレクトリに移動します。  

```console
C:\binskim-master> Cd \binskim-master\bld\bin\AnyCPU_Release\Publish\netcoreapp2.0\win-x64>
```

9. [分析] オプションのヘルプを表示します。

```console
C:\binskim-master\bld\bin\AnyCPU_Release\Publish\netcoreapp2.0\win-x64> BinSkim help analyze

BinSkim PE/MSIL Analysis Driver 1.6.0.0

  --sympath                      Symbols path value, e.g., SRV*http://msdl.microsoft.com/download/symbols or Cache*d:\symbols;Srv*http://symweb. See
                                 https://docs.microsoft.com/en-us/windows-hardware/drivers/debugger/advanced-symsrv-use for syntax information. Note that BinSkim will clear the
                                 _NT_SYMBOL_PATH environment variable at runtime. Use this argument for symbol information instead.

  --local-symbol-directories     A set of semicolon-delimited local directory paths that will be examined when attempting to locate PDBs.

  -o, --output                   File path to which analysis output will be written.

  --verbose                      Emit verbose output. The resulting comprehensive report is designed to provide appropriate evidence for compliance scenarios.

...
  
```

**シンボルパスの設定**

BinSkim on を実行しているコンピューターで分析しているすべてのコードをビルドする場合は、通常、シンボルパスを設定する必要はありません。 これは、コンパイルしたローカルボックスでシンボルファイルを使用できるためです。 より複雑なビルドシステムを使用している場合や、シンボルを (コンパイルされたバイナリではなく) 別の場所にリダイレクトしている場合は、を使用して、 `--local-symbol-directories` シンボルファイルの検索にこれらの場所を追加します。
コードがコードに含まれていないコンパイル済みバイナリを参照している場合は、これらのコード依存関係のセキュリティを確認するために、ウィンドウデバッガー sympath を使用してシンボルを取得できます。 これらの依存関係で問題が見つかった場合は、修正できない可能性があります。 ただし、これらの依存関係を使用して、受け入れている可能性のあるセキュリティリスクを認識しておくと役立つ場合があります。

> [!TIP]
>ネットワークシンボルサーバーを参照するシンボルパスを追加する場合は、ローカルキャッシュの場所を追加して、シンボルをキャッシュするローカルパスを指定します。 この操作を行わないと、ビンのざっとのパフォーマンスが著しく低下する可能性があります。 次の例では、d:\symbols. でローカルキャッシュを指定します。
`--sympath Cache*d:\symbols;Srv*http://symweb`
Sympath の詳細については、「 [Windows デバッガーのシンボルパス](https://docs.microsoft.com/windows-hardware/drivers/debugger/symbol-path)」を参照してください。

10. 次のコマンドを実行して、コンパイル済みのドライバーバイナリを分析します。 コンパイルされた driver .sys ファイルを指すようにターゲットパスを更新します。

```console
C:\binskim-master\bld\bin\AnyCPU_Release\Publish\netcoreapp2.0\win-x64> BinSkim analyze "C:\Samples\KMDF_Echo_Driver\echo.sys"
```

11. 詳細については、次のような verbose オプションを追加してください。

```console
C:\binskim-master\bld\bin\AnyCPU_Release\Publish\netcoreapp2.0\win-x64> BinSkim analyze "C:\Samples\KMDF_Echo_Driver\osrusbfx2.sys" --verbose
```
> [!NOTE]
>--Verbose オプションを指定すると、すべてのチェックに対して明示的な合格/不合格の結果が生成されます。 詳細を指定しない場合は、ビンの表示で検出された不具合のみが表示されます。 ログファイルのサイズが大きくなるため、--verbose オプションは通常、実際のオートメーションシステムには推奨されません。これは、多くの "成功" の結果の途中で埋め込まれるため、個々のエラーが発生したときに個別のエラーを取得するのが困難になるためです。

12. コマンドの出力を確認して、考えられる問題を探します。 この例の出力は、成功した3つのテストを示しています。 BA2002 など、ルールに関する追加情報については、 [Binskim ユーザーガイド](https://github.com/microsoft/binskim/blob/master/docs/UserGuide.md)を参照してください。

```console
Analyzing...
Analyzing 'osrusbfx2.sys'...
...

C:\Samples\KMDF_Echo_Driver\osrusbfx2.sys\Debug\osrusbfx2.sys: pass BA2002: 'osrusbfx2.sys' does not incorporate any known vulnerable dependencies, as configured by current policy.
C:\Samples\KMDF_Echo_Driver\Debug\osrusbfx2.sys: pass BA2005: 'osrusbfx2.sys' is not known to be an obsolete binary that is vulnerable to one or more security problems.
C:\Samples\KMDF_Echo_Driver\osrusbfx2.sys: pass BA2006: All linked modules of 'osrusbfx2.sys' generated by the Microsoft front-end satisfy configured policy (compiler minimum version 17.0.65501.17013).
```

13. この出力は、ドライバーが ELF バイナリではないことを示すためにテスト BA3001 が実行されないことを示しています。

```console
...
C:\Samples\KMDF_Echo_Driver\Debug\osrusbfx2.sys: notapplicable BA3001: 'osrusbfx2.sys' was not evaluated for check 'EnablePositionIndependentExecutable' as the analysis is not relevant based on observed metadata: image is not an ELF binary.
```

14. この出力は、テスト BA2007 のエラーを示しています。

```console
...

C:\Samples\KMDF_Echo_Driver\Debug\osrusbfx2.sys: error BA2007: 'osrusbfx2.sys' disables compiler warning(s) which are required by policy.
A compiler warning is typically required if it has a high likelihood of flagging memory corruption, information disclosure, or double-free vulnerabilities.
To resolve this issue, enable the indicated warning(s) by removing /Wxxxx switches (where xxxx is a warning id indicated here) from your command line, and resolve any warnings subsequently raised during compilation.
```

Visual Studio でこれらの警告を有効にするには、プロジェクトの [プロパティページ] の [C/c + +] で、[**特定の警告を無効**にする] で除外しない値を削除します。

![Visual Studio 2019 で特定の警告を無効にするためのダイアログボックス](images/disable-specific-warnings-dialog.png)

ドライバープロジェクト用の Visual Studio の既定のコンパイルオプションでは、次のような警告を無効にすることができます。 これらの警告は、BinSkim によって報告されます。

[C4603-' name ': マクロが定義されていないか、プリコンパイル済みヘッダーの使用後に定義が異なります](https://docs.microsoft.com/cpp/error-messages/compiler-warnings/compiler-warning-level-1-c4603)

[C4627-' description ': プリコンパイル済みヘッダーの使用を検索しているときにスキップされました](https://docs.microsoft.com/cpp/error-messages/compiler-warnings/compiler-warning-level-1-c4627)

[C4986-' 宣言 ': 例外指定が前の宣言と一致しません](https://docs.microsoft.com/cpp/error-messages/compiler-warnings/compiler-warning-c4986)

コンパイラの警告の詳細については、「コンパイラの[バージョン別のコンパイラ警告](https://docs.microsoft.com/cpp/error-messages/compiler-warnings/compiler-warnings-by-compiler-version?view=vs-2019)」を参照してください。

## <a name="span-idcodevalidationtoolsspanspan-idcodevalidationtoolsspanspan-idcodevalidationtoolsspanuse-additional-code-validation-tools"></a><span id="CodeValidationTools"></span><span id="codevalidationtools"></span><span id="CODEVALIDATIONTOOLS"></span>追加のコード検証ツールを使用する

**セキュリティチェックリスト項目 \# 16:** *これらの追加のツールを使用して、コードがセキュリティに関する推奨事項に準拠しているかどうかを検証し、開発プロセスで欠落しているギャップを調べることができます。*

前に説明した[Visual Studio Code 分析](#use-code-analysis)、[静的ドライバー検証](#sdv)ツール、 [binskim](#binskim)に加えて、次のツールを使用して、開発プロセスで欠落したギャップを調査します。

**ドライバーの検証ツール**

ドライバーの検証ツールを使用すると、ドライバーをライブテストできます。 ドライバーの検証ツールは、Windows カーネルモード ドライバーとグラフィックス ドライバーを監視して、無効な関数呼び出しやシステムを破損する可能性があるアクションを検出します。 ドライバーの検証ツールでは、Windows ドライバーがさまざまなストレスとテストを受けて、不適切な動作を見つけることができます。 詳細については、「 [Driver Verifier](https://docs.microsoft.com/windows-hardware/drivers/devtest/driver-verifier)」を参照してください。

**ハードウェア互換性プログラムテスト**

ハードウェア互換性プログラムには、コードの脆弱性を探すために使用できる、セキュリティ関連のテストが含まれています。 Windows ハードウェア互換性プログラムは、Windows Hardware Lab Kit (HLK) のテストを活用します。 HLK デバイスの基本テストをコマンドラインで使用して、ドライバーコードを実行し、脆弱性をプローブすることができます。 デバイスの基本テストおよびハードウェアの互換性プログラムに関する一般的な情報については、「 [Windows ハードウェアラボキット](https://docs.microsoft.com/windows-hardware/test/hlk/)」を参照してください。

次のテストは、コードの脆弱性に関連するいくつかの動作のドライバーコードを確認するのに役立つ可能性があるテストの例です。

 [DF - ランダム IOCTL のファジー テスト (信頼性)](https://docs.microsoft.com/windows-hardware/test/hlk/testref/236b8ad5-0ba1-4075-80a6-ae9dafb71c94)

 [DF - サブオープンのファジー テスト (信頼性)](https://docs.microsoft.com/windows-hardware/test/hlk/testref/92bf534e-aa48-4aeb-b3cd-e46fb7cc7d80)

 [DF - 0 長バッファー FSCTL のファジー テスト (信頼性)](https://docs.microsoft.com/windows-hardware/test/hlk/testref/5f5f6c7e-d5db-4ff1-8cee-da47203ab070)

 [DF - ランダム FSCTL のファジー テスト (信頼性)](https://docs.microsoft.com/windows-hardware/test/hlk/testref/e529e34e-076a-4978-926f-7eca333e8f4d)

 [DF - Misc API のファジー テスト (信頼性)](https://docs.microsoft.com/windows-hardware/test/hlk/testref/fb305d04-6e8c-4dfc-9984-9692df82fbd8)

 また、ドライバー検証ツールに含まれている[カーネル同期遅延ファジー化](https://docs.microsoft.com/windows-hardware/drivers/devtest/kernel-synchronization-delay-fuzzing)を使用することもできます。

混乱 (ハードウェアとオペレーティングシステムの同時実行) テストでは、さまざまな PnP ドライバーテスト、デバイスドライバーのファジーテスト、および電源システムテストが同時に実行されます。 詳細については、「[混乱テスト (デバイスの基礎)](https://docs.microsoft.com/windows-hardware/drivers/devtest/chaos-tests--device-fundamentals-)」を参照してください。

デバイスの基本侵入テストは、セキュリティテストの重要なコンポーネントであるさまざまな形式の入力攻撃を実行します。 攻撃および侵入テストは、ソフトウェアインターフェイスの脆弱性を特定するのに役立ちます。 詳細については、「[侵入テスト (デバイスの基礎)](https://docs.microsoft.com/windows-hardware/drivers/devtest/penetration-tests--device-fundamentals-)」を参照してください。

この記事で説明されている他のツールと共に[Device Guard コンプライアンステスト](https://docs.microsoft.com/windows-hardware/test/hlk/testref/10c242b6-49f6-491d-876c-c39b22b36abc)を使用して、ドライバーが hvci と互換性があることを確認します。

**カスタムおよびドメイン固有のテストツール**

ドメイン固有のカスタムセキュリティテストの開発を検討します。 追加のテストを開発するには、ソフトウェアの元の設計者からの入力と、開発中の特定の種類のドライバーによく使用されている関連のない開発リソース、およびセキュリティの侵入の分析と防止についてよく知られている1人以上の開発リソースを収集します。

## <a name="span-iddebuggerspanspan-iddebuggerspanspan-iddebuggerspanreview-debugger-techniques-and-extensions"></a><span id="Debugger"></span><span id="debugger"></span><span id="DEBUGGER"></span>デバッガーの手法と拡張機能の確認

**セキュリティチェックリスト項目 \# 17:** *これらのデバッガーツールを確認し、開発デバッグワークフローでの使用を検討します。*

**! 利用可能クラッシュアナライザー**

! の悪用可能なクラッシュアナライザーは、クラッシュログを解析して一意の問題を探す Windows デバッガー拡張機能です。 また、クラッシュの種類を調べ、エラーが悪意のあるハッカーによって悪用される可能性のあるものかどうかを判断しようとします。

Microsoft Security Engineering Center (ミリ秒) は、! の悪用可能クラッシュアナライザーを作成しました。 Codeplex からをダウンロードできます <https://msecdbg.codeplex.com/> 。

詳細については、「」を参照してください[。悪用可能な crash analyzer バージョン 1.6](https://www.microsoft.com/security/blog/2013/06/13/exploitable-crash-analyzer-version-1-6/)と Channel 9 video [! クラッシュアナライザー](https://channel9.msdn.com/blogs/pdcnews/bang-exploitable-security-analyzer)。

**セキュリティ関連のデバッガーコマンド**

! Acl 拡張機能では、アクセス制御リスト (ACL) の内容を書式設定して表示します。 詳細については、「オブジェクトと acl[の acl の決定](https://docs.microsoft.com/windows-hardware/drivers/debugger/determining-the-acl-of-an-object)」を[**参照して**](https://docs.microsoft.com/windows-hardware/drivers/debugger/-acl)ください。

! Token extension は、セキュリティトークンオブジェクトの書式付きビューを表示します。 詳細については、「 [**! token**](https://docs.microsoft.com/windows-hardware/drivers/debugger/-token)」を参照してください。

! Tokenfields 拡張機能には、アクセストークンオブジェクト (トークン構造) 内のフィールドの名前とオフセットが表示されます。 詳細については、「」[**を参照してください。**](https://docs.microsoft.com/windows-hardware/drivers/debugger/-tokenfields)

! Sid 拡張子は、指定されたアドレスにあるセキュリティ識別子 (SID) を表示します。 詳細については、「 [**! sid**](https://docs.microsoft.com/windows-hardware/drivers/debugger/-sid)」を参照してください。

! Sd 拡張機能は、指定されたアドレスにあるセキュリティ記述子を表示します。 詳細については、「 [**! sd**](https://docs.microsoft.com/windows-hardware/drivers/debugger/-sd)」を参照してください。

## <a name="span-idsecurecodingresourcesspanspan-idsecurecodingresourcesspanspan-idsecurecodingresourcesspanreview-secure-coding-resources"></a><span id="SecureCodingResources"></span><span id="securecodingresources"></span><span id="SECURECODINGRESOURCES"></span>安全なコーディングリソースの確認

**セキュリティチェックリスト項目 \# 18:** *これらのリソースを確認して、ドライバー開発者に適用されるセキュリティで保護されたコーディングのベストプラクティスについて理解を深めます。*

*ドライバーのセキュリティの詳細については、次のリソースを参照してください。*

**セキュリティで保護されたカーネルモードドライバーのコーディングガイドライン**

[信頼性の高いカーネルモード ドライバーの作成](https://docs.microsoft.com/windows-hardware/drivers/kernel/creating-reliable-kernel-mode-drivers)

**安全なコーディング組織**

[カーネギーメロン大学 SEI CERT](https://www.sei.cmu.edu/about/divisions/cert/index.cfm)

カーネギーメロン大学 SEI CERT [C コーディング標準: 安全で信頼性が高く、セキュリティで保護されたシステム (2016 Edition) を開発するための規則](https://www.securecoding.cert.org/confluence/display/c/SEI+CERT+C+Coding+Standard)。

CERT-[でのセキュリティの構築](https://www.us-cert.gov/bsi)

MITRE- [CERT C Secure コーディング Standard によってアドレス指定される脆弱性](https://cwe.mitre.org/data/definitions/734.html)

成熟度モデル (BSIMM) でセキュリティを構築する[https://www.bsimm.com/](https://www.bsimm.com/)

Saf Ecode-[https://safecode.org/](https://safecode.org/)

**OSR**

[OSR](https://www.osr.com)は、ドライバー開発トレーニングとコンサルティングサービスを提供します。 OSR ニュースレターの次の記事では、ドライバーのセキュリティに関する問題を取り上げています。

[名前、セキュリティ記述子、デバイスクラス-デバイスオブジェクトにアクセスできるようにしています...安全](https://www.osr.com/nt-insider/2017-issue1/making-device-objects-accessible-safe/)

[ことごとくで保護を使用しています。 & デバイスのセキュリティ](https://www.osronline.com/article.cfm^article=100.htm)

[ドライバーのロックダウン-手法の調査](https://www.osronline.com/article.cfm^article=357.htm)

[Meltdown と Spectre: ドライバーについて](https://www.osr.com/blog/2018/01/23/meltdown-spectre-drivers/)

**ケーススタディ**

[アラートからドライバーへの脆弱性: Microsoft Defender ATP 調査の特権エスカレーションの欠陥](https://www.microsoft.com/security/blog/2019/03/25/from-alert-to-driver-vulnerability-microsoft-defender-atp-investigation-unearths-privilege-escalation-flaw/)

**書籍**

*ソフトウェアセキュリティの24個の危険な点: プログラミングの欠陥と*、Michael Howard、David Leblanc 著、John 閲覧 ga での修正方法

*ソフトウェアのセキュリティ評価の最先端: ソフトウェアの脆弱性の特定と防止*、Mark Dowd、John のマクドナルドと Justin

*セキュアソフトウェア Second Edition*、Michael Howard、David Leblanc 著の作成

*ソフトウェアのセキュリティ評価の最先端: ソフトウェアの脆弱性の特定と防止*、Mark Dowd と John のマクドナルド

*C および C++ での安全なコーディング (ソフトウェアエンジニアリングの SEI シリーズ) 第2版*、Robert c. Seacord

*Microsoft Windows Driver Model (第2版)*、Walter Oney プログラミングする

*Windows Driver Foundation (開発者向けリファレンス)*、少額 Orwick、Guy Smith を使用したドライバーの開発

**トレーニング**

Windows ドライバーのクラスルームトレーニングは、次のようなベンダーから入手できます。

- [OSR](https://www.osr.com)
- [Winsider](https://www.windows-internals.com/)
- [Azius](https://azius.com/)

セキュリティで保護されたコーディングオンライントレーニングは、さまざまなソースから入手できます。 たとえば、このコースは coursera から入手できます。

[https://www.coursera.org/learn/software-security](https://www.coursera.org/learn/software-security).

また、フリートレーニングも用意されています。

[SAFECode.org/training](https://safecode.org/training/)

**Professional 認定**

 CERT は、[セキュリティで保護されたコーディングプロフェッショナル認定](https://www.sei.cmu.edu/education-outreach/credentials/index.cfm)を提供します。

## <a name="span-idkeytakeawaysspansummary-of-key-takeaways"></a><span id="keytakeaways"></span>重要な情報の概要

ドライバーのセキュリティは、多くの要素を含む複雑な作業ですが、次の点を考慮する必要があります。

- ドライバーは windows カーネル内に存在し、カーネルで実行するときに問題が発生すると、オペレーティングシステム全体が公開されます。 このため、セキュリティを考慮して、ドライバーのセキュリティと設計に注意を払ってください。

- 最小限の特権の原則を適用します。

    a. 厳格な SDDL 文字列を使用して、ドライバーへのアクセスを制限する

    b. 個々の IOCTL をさらに制限する

- 攻撃ベクトルを識別するための脅威モデルを作成し、さらに何かを制限できるかどうかを検討します。
- モードでは、埋め込みポインターが使用されていることに注意してください。 このような場合は、プローブして、try の内部でアクセスする必要があります。また、バッファーの値がキャプチャされ、比較される場合を除き、使用時間 (ToCToU) の問題を確認することができます。
- わからない場合は、METHOD_BUFFERED を IOCTL バッファリング方法として使用します。
- コードスキャンユーティリティを使用して既知のコードの脆弱性を検索し、特定された問題を修復します。
- 知識のあるコードレビュー担当者に相談して、問題が発生した可能性のある問題を探します。
- ドライバー検証を使用し、コーナーケースを含む複数の入力でドライバーをテストします。
