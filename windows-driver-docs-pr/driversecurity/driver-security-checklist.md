---
title: ドライバーのセキュリティ チェックリスト
description: この記事では、ドライバー開発者向けのドライバーのセキュリティのチェックリストを提供します。
ms.assetid: 25375E02-FCA1-4E94-8D9A-AA396C909278
ms.date: 04/02/2019
ms.localizationpriority: medium
ms.openlocfilehash: 18c3e78adf67644de5cdfd8c434cf36d4ba78739
ms.sourcegitcommit: 5402ab8a5ecc5e1933d4191174a09f96c000deb0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/04/2019
ms.locfileid: "59003639"
---
# <a name="driver-security-checklist"></a>ドライバーのセキュリティ チェックリスト

この記事では、ドライバーが侵害されるリスクを減らすためにドライバー開発者向けのドライバーのセキュリティ チェックリストを提供します。

## <a name="span-iddriversecurityoverviewspanspan-iddriversecurityoverviewspanspan-iddriversecurityoverviewspandriver-security-overview"></a><span id="Driver_Security_Overview"></span><span id="driver_security_overview"></span><span id="DRIVER_SECURITY_OVERVIEW"></span>ドライバーのセキュリティの概要

セキュリティ上の欠陥では、攻撃者に方法は、システムがクラッシュすることで、ドライバーが誤動作が発生するか、使用できなくなることができる任意の欠陥です。 さらに、ドライバーのコードの脆弱性は、OS 全体を危険にさらす可能性を作成する、カーネルにアクセスする攻撃者を許可できます。 ほとんどの開発者は、そのドライバーで作業しているで正常に動作するドライバーを入手して、コード内の脆弱性を悪用する悪意のある攻撃者を試むかどうかではなく、フォーカスは。

ドライバーがリリースされると、ただし、攻撃者がプローブし、セキュリティ上の欠陥を試行できます。 開発者は、このような脆弱性の可能性を最小限に抑えるために、設計と実装フェーズ中にこれらの問題を検討する必要があります。 目標は、ドライバーがリリースされる前に、すべての既知のセキュリティの欠陥を除去することです。

コード (防御的なコーディングの脆弱性のソースは、一般的な操作)、およびテストを実装する開発者 (意識的考え方ドライバーに潜在的な脅威の)、システム設計者の協力が必要より安全なドライバーを作成します。チーム (脆弱性および脆弱性を見つけるに事前にしようとしています)。 によってこれらのアクティビティのすべてを適切に調整、ドライバーのセキュリティを大幅に向上します。

攻撃を受けるドライバーに関連する問題を回避するだけでなく、ドライバーの信頼性が向上カーネル メモリがより正確な使用など、説明する手順の多くは。 サポート コストが削減され、製品に対する顧客満足度が向上されます。 以下のチェックリストのタスクを完了すると、これらすべての目標を達成するのに役立ちます。

**セキュリティ チェックリスト:***次の各トピックで説明されているセキュリティ タスクを完了します。*

![空のチェック ボックス](images/checkbox.png)[カーネル ドライバーが必要であることを確認します。](#confirmkernel)

![空のチェック ボックス](images/checkbox.png)[ドライバー フレームワークを使用](#confirmkernel)

![空のチェック ボックス](images/checkbox.png)[のみのソフトウェア ドライバーへのアクセス制御](#controlsoftwareonly)

![空のチェック ボックス](images/checkbox.png)[ドライバーのコードをテストする実稼働署名されて操作を行います](#donotproductionsign) 

![空のチェック ボックス](images/checkbox.png)[脅威分析を実行します。](#threatanalysis)

![空のチェック ボックス](images/checkbox.png)[安全なコーディングのガイドラインに従ってドライバー](#driversecuritycodepractices)

![空のチェック ボックス](images/checkbox.png)[Device Guard の検証の互換性](#dgc)

![空のチェック ボックス](images/checkbox.png)[テクノロジ固有のコードのベスト プラクティスに従う](#technologyspecificcodepractices)

![空のチェック ボックス](images/checkbox.png)[ピア コード レビューの実行](#peercodereview)

![空のチェック ボックス](images/checkbox.png)[ドライバーへのアクセス制御の管理](#managingdriveraccesscontrol)

![空のチェック ボックス](images/checkbox.png)[デバイス インストールのセキュリティを強化](#enhancedeviceinstallationsecurity)

![空のチェック ボックス](images/checkbox.png)[リリースの適切なドライバーの署名の実行](#releasedriversigning)

![空のチェック ボックス](images/checkbox.png)[Visual Studio でコード分析を使用して、ドライバーのセキュリティを調査するには](#use-code-analysis)

![空のチェック ボックスをオン](images/checkbox.png)[の脆弱性を確認する Static Driver Verifier を使用](#sdv)

![空のチェック ボックス](images/checkbox.png)[Binscope Binary Analyzer を使用したコードを確認してください。](#binscope)

![空のチェック ボックス](images/checkbox.png)[コード検証ツールを使用](#codevalidationtools)

![空のチェック ボックス](images/checkbox.png)[デバッガー手法と拡張機能を確認してください](#debugger)

![空のチェック ボックス](images/checkbox.png)[レビューのセキュリティ保護されたリソースのコーディング](#securecodingresources)

[重要な習得事項の概要](#keytakeaways)

## <a name="span-idconfirmkernelspanconfirm-that-a-kernel-driver-is-required"></a><span id="confirmkernel"></span>カーネル ドライバーが必要であることを確認します。

**セキュリティ チェックリスト項目\#1。***カーネル ドライバーが必要であると、Windows サービスやアプリなどの低リスクのアプローチがより適切なオプションではないことを確認します。*

ドライバーは、Windows カーネルで live し、オペレーティング システム全体を公開するカーネルを実行中に問題が発生します。 他のオプションを使用できる場合可能性がありますするコストを削減し、新しいカーネル ドライバーを作成するよりも少ない関連するリスクがあります。
Windows ドライバーで、組み込みの使用に関する詳細については、次を参照してください。[ドライバーを作成する必要がありますか?](https://docs.microsoft.com/windows-hardware/drivers/gettingstarted/do-you-need-to-write-a-driver-)します。

バック グラウンド タスクを使用する方法の詳細については、次を参照してください。[バック グラウンド タスクを使用してアプリをサポートして](https://docs.microsoft.com/windows/uwp/launch-resume/support-your-app-with-background-tasks)します。

Windows サービスを使用する方法の詳細については、次を参照してください。[サービス](https://msdn.microsoft.com/library/windows/desktop/ms685141.aspx)します。

## <a name="span-idconfirmkernelspanuse-the-driver-frameworks"></a><span id="confirmkernel"></span>ドライバーのフレームワークを使用します。 

**セキュリティ チェックリスト項目\#2。***コードのサイズを縮小しの信頼性とセキュリティを向上させるには、ドライバー フレームワークを使用します。*

使用して、 [Windows Driver Frameworks](https://docs.microsoft.com/windows-hardware/drivers/wdf/)コードのサイズを縮小し、it の信頼性とセキュリティを向上します。  最初に、確認[ドライバーの開発を使用して WDF](https://docs.microsoft.com/windows-hardware/drivers/wdf/using-the-framework-to-develop-a-driver)します。 ドライバーを使用して、低いリスク ユーザー モード フレームワーク (UMDF) については、次を参照してください。[ドライバー モデルを選択する](https://docs.microsoft.com/windows-hardware/drivers/gettingstarted/choosing-a-driver-model)します。

以前の形式を記述[Windows Driver Model (WDM)](https://docs.microsoft.com/windows-hardware/drivers/kernel/windows-driver-model)ドライバーは時間がかかり、コストがかかり、ほぼ常に ドライバー フレームワークで使用できるコードを再作成する必要があります。

Windows Driver Framework のソース コードはオープン ソースとは、GitHub で入手できます。 これは、Windows 10 に付属している、WDF ランタイム ライブラリの作成元となるソース コードです。 ドライバーと WDF のやりとりを追跡できるとき、ドライバーをさらに効果的にデバッグできます。 ダウンロード[ https://github.com/Microsoft/Windows-Driver-Frameworks](https://github.com/Microsoft/Windows-Driver-Frameworks)します。


## <a name="span-idcontrolsoftwareonlyspancontrol-access-to-software-only-drivers"></a><span id="controlsoftwareonly"></span>のみのソフトウェア ドライバーへのアクセス制御

**セキュリティ チェックリスト項目\#3。***ソフトウェア専用のドライバーを作成する場合は、追加のアクセス制御を実装する必要があります。*

ソフトウェアのみのカーネル ドライバーが特定のハードウェア Id に関連付けられますにプラグ アンド プレイ (PnP) を使用しないと、任意の PC で実行できます。 1 つ、本来、攻撃ベクトルを作成する以外の目的でこのようなドライバーを使用できます。 

ソフトウェアのみのカーネル ドライバーには、追加のリスクが含まれている、ために必要があります (たとえば、PnP ドライバーの作成を有効にする一意の PnP ID を使用してまたは SMBIOS の表に、特定のハードウェアの有無をチェックして) 特定のハードウェア上で実行に制限されています。

たとえば、OEM である Fabrikam が、システムのオーバーク ロックのユーティリティを使用するドライバーを配布したいとします。  このソフトウェア専用のドライバー別の OEM からのシステム上で実行する場合は、システムが不安定になるか、破損可能性があります。  Fabrikam のシステムでは、Windows Update を通じて更新可能になっている PnP ドライバーの作成を有効にする一意の PnP ID を含める必要があります。  これが可能であればではなく、Fabrikam レガシ ドライバーを作成する場合は、そのドライバーはことに (たとえば、すべての機能を有効にする前の表に、SMBIOS の調査) を Fabrikam のシステムで実行されてを確認するもう 1 つのメソッドを検索する必要があります。 


## <a name="span-iddonotproductionsignspan-do-not-production-sign-test-code"></a><span id="donotproductionsign"></span> 実稼働署名しないコードをテストします。

**セキュリティ チェックリスト項目\#4。***いない実稼働コード記号開発、テスト、製造カーネル ドライバーのコードを実行します。*

カーネル ドライバーの開発に使用されるコード、テスト、または製造するとセキュリティが侵害される危険な機能がなどがあります。  この危険なコードは、Windows によって信頼されている証明書で署名することはありません必要があります。  危険なドライバーのコードを実行するための適切なメカニズムは、UEFI セキュア ブートを無効にする、BCD"TESTSIGNING"を有効にして、開発、テスト、および、(たとえば、1 つ makecert.exe によって生成された) 信頼されていない証明書を使用して製造コードの署名には。

信頼できるソフトウェア発行元証明書 (SPC) または Windows Hardware Quality Labs (WHQL) の署名によって署名されたコードでは、Windows コードの整合性とセキュリティ テクノロジのバイパスを容易にする必要がありますされません。  コードは、信頼された SPC または WHQL 署名によって署名されて、前にからのガイダンスに従うことを確認最初[信頼性の高いカーネル モード ドライバーの作成](https://docs.microsoft.com/windows-hardware/drivers/kernel/creating-reliable-kernel-mode-drivers)です。 さらに、コードは、任意の危険な動作、以下で説明を含めることはできません。  ドライバーの署名の詳細については、次を参照してください。[リリース ドライバーの署名](#releasedriversigning)この記事で後述します。

危険な動作の例については、次のとおりです。

- ユーザー モードに任意のカーネル、物理的、またはデバイスのメモリをマップする機能を提供します。
- ポート入力/出力 (I/O) を含め、任意のカーネルや物理デバイス メモリを読み書きする機能を提供します。
- Windows アクセス制御をバイパスする記憶域へのアクセスを提供します。 
- 管理するためのハードウェアまたはドライバーがファームウェアを変更する機能を提供します。  


## <a name="span-idthreatanalysisspanspan-idthreatanalysisspanspan-idthreatanalysisspanperform-threat-analysis"></a><span id="ThreatAnalysis"></span><span id="threatanalysis"></span><span id="THREATANALYSIS"></span>脅威の分析を実行します。


**セキュリティ チェックリスト項目\#5。***既存のドライバーの脅威モデルを変更するか、ドライバーのカスタムの脅威モデルを作成します。*

セキュリティを検討する際に、一般的な方法論は、可能な攻撃の種類を記述しようとする特定の脅威モデルを作成します。 この手法は、開発者は、ドライバーに対して潜在的な攻撃ベクトルを事前に検討を強制するためにドライバーを設計するときに便利です。 潜在的な脅威を特定したこと、ドライバー開発者を検討ドライバー コンポーネントの全体的なセキュリティを強化するためにこれらの脅威に対する防御のことを意味します。

この記事では、軽量の脅威モデルを作成するためのドライバー固有のガイダンスを提供します。[脅威のドライバーをモデル化](threat-modeling-for-drivers.md)します。 この記事では、脅威モデル ダイアグラムには、ドライバーの開始点として使用できるドライバーの例を提供します。

![仮定のカーネル モード ドライバー用のサンプル データ フロー ダイアグラム](images/sampledataflowdiagramkernelmodedriver.gif)

独自の製品のセキュリティを向上させるために、Ihv と Oem によってセキュリティ開発ライフ サイクル (SDL) のベスト プラクティスと関連付けられているツールを使用できます。 詳細については、次を参照してください。 [oem 向けの推奨事項を SDL](https://docs.microsoft.com/en-us/windows-hardware/drivers/bringup/security-overview#sdl-recommendations-for-oems)します。


## <a name="span-iddriversecuritycodepracticesspanspan-iddriversecuritycodepracticesspanspan-iddriversecuritycodepracticesspanfollow-driver-secure-coding-guidelines"></a><span id="DriverSecurityCodePractices"></span><span id="driversecuritycodepractices"></span><span id="DRIVERSECURITYCODEPRACTICES"></span>ドライバーのセキュリティ保護されたコーディングのガイドラインに従ってください。

**セキュリティ チェックリスト項目\#6。***コードをレビューし、既知のコードの脆弱性を削除します。*

セキュリティで保護されたドライバーの作成のコア アクティビティが既知のソフトウェアの脆弱性を回避するために変更する必要があるコードの領域を特定します。 これらの既知のソフトウェアの脆弱性の多くを上書きするか、それ以外の場合、ドライバーを使用するメモリの場所を構成する他の問題を回避するためにメモリの使用の継続的に厳密な管理を処理します。

[コード検証ツール](#codevalidationtools)この記事のセクションには、既知のソフトウェアの脆弱性を見つけやすいように使用できるソフトウェア ツールがについて説明します。


**メモリ バッファー**

- 常に、バッファーが要求されたすべてのデータを保持できることを確認する入力と出力バッファーのサイズを確認します。 詳細については、次を参照してください。[バッファーのサイズを確認するエラー](https://msdn.microsoft.com/library/windows/hardware/ff545679)します。

- 呼び出し元に返す前に 0 で、すべての出力バッファーを適切に初期化します。 詳細については、次を参照してください。[出力バッファーの初期化に失敗した](https://msdn.microsoft.com/library/windows/hardware/ff545693)します。

- 可変長バッファーを検証します。 詳細については、次を参照してください。[可変長バッファーの検証に失敗した](https://msdn.microsoft.com/library/windows/hardware/ff545709)します。 バッファー操作および使用の詳細については[ **ProbeForRead** ](https://msdn.microsoft.com/library/windows/hardware/ff559876)と[ **ProbeForWrite** ](https://msdn.microsoft.com/library/windows/hardware/ff559879)のアドレスを検証する、バッファーは、「[バッファー処理](https://msdn.microsoft.com/library/windows/hardware/ff539004)します。


**Ioctl でのデータ バッファーにアクセスするため、適切なメソッドを使用します。**

ユーザー モード アプリケーションとシステムのデバイス間でデータを転送する Windows ドライバーの主な責務のいずれかです。 データ バッファーにアクセスするための 3 つのメソッドは、次の表に表示されます。 

|IOCTL バッファーの種類 | まとめ                                    | 詳細情報 |  
|------------------|--------------------------------------------|-------------------------------------------------------------------------|
| METHOD_BUFFERED  |ほとんど入らないをお勧めします。            | [バッファー付き I/O の使用](https://docs.microsoft.com/windows-hardware/drivers/kernel/using-buffered-i-o)
| METHOD_IN_DIRECT または METHOD_OUT_DIRECT |いくつかの高速ハードウェア I/O の使用    |[ダイレクト I/O の使用](https://docs.microsoft.com/windows-hardware/drivers/kernel/using-direct-i-o) |
| METHOD_NEITHER |できる限り避ける |[バッファー付き I/O とダイレクト I/O のどちらも使用しない](https://docs.microsoft.com/windows-hardware/drivers/kernel/using-neither-buffered-nor-direct-i-o)|

一般にバッファー I/O は推奨最も安全なバッファリング メソッドを提供します。 使用する場合としても、軽減する必要がある埋め込みポインターなどのリスクがある I/O をバッファーします。

Ioctl でバッファーを操作の詳細については、次を参照してください。[メソッドにアクセスするデータ バッファーの](https://docs.microsoft.com/windows-hardware/drivers/kernel/methods-for-accessing-data-buffers)します。

**バッファリングされた I/O の IOCTL の使用中のエラー**

- 関連するバッファーの IOCTL のサイズを確認します。 詳細については、次を参照してください。[バッファーのサイズを確認するエラー](https://msdn.microsoft.com/library/windows/hardware/ff545679)します。
 
- 出力バッファーを適切に初期化します。 詳細については、次を参照してください。[出力バッファーの初期化に失敗した](https://msdn.microsoft.com/library/windows/hardware/ff545693)します。

- 可変長バッファーを正しく検証します。 詳細については、次を参照してください。[可変長バッファーの検証に失敗した](https://msdn.microsoft.com/library/windows/hardware/ff545709)します。

- バッファー内の I/O を使用する場合は、必ずし、で OutputBuffer の適切な長さを返す、 [IO_STATUS_BLOCK](https://msdn.microsoft.com/library/windows/hardware/ff550671.aspx)情報フィールドの構造体。  読み取り要求から直接長さを返すだけに直接はありません。  たとえば、ユーザー空間から返されたデータが 4 K のバッファーがあることを示すような状況を検討してください。  ドライバーは、実際には 200 (バイト単位) を返す必要がありますのみが、代わりに、[情報] フィールドに 4 K を返すだけの場合は、情報漏えいの脆弱性が発生しました。 以前のバージョンの Windows では、バッファーの I/O の I/O マネージャーを使用してバッファーが消去されないために、この問題が発生します。  そのため、ユーザーのアプリ取得元の 200 バイトのデータと、バッファー (非ページ プールの内容) に任意の 4 K-200 バイトがあった。 バッファーの I/O のすべての使用と Ioctl だけでなく、この状況が発生することができます。

**IOCTL ダイレクト i/o エラー**

長さ 0 のバッファーを正しく処理します。 詳細については、次を参照してください。[ダイレクト I/O エラー](https://msdn.microsoft.com/library/windows/hardware/ff544300)します。

**ユーザー領域のアドレスを参照するエラー**
- バッファー内の I/O 要求に埋め込まれているポインターを検証します。 詳細については、次を参照してください。[ユーザー スペースのアドレスを参照するエラー](https://msdn.microsoft.com/library/windows/hardware/ff544308)します。

- などの Api を使用して、使用する前に、ユーザー空間で任意のアドレスを検証[ **ProbeForRead** ](https://msdn.microsoft.com/library/windows/hardware/ff559876)と[ **ProbeForWrite** ](https://msdn.microsoft.com/library/windows/hardware/ff559879)とき適切です。 

**TOCTOU 脆弱性**

[潜在的な使用の時間を確認時](https://en.wikipedia.org/wiki/Time_of_check_to_time_of_use)(TOCTOU) の脆弱性 (Ioctl 用または読み取り/書き込み) は、ダイレクト I/O を使用する場合。  ドライバーは、ユーザーのデータ バッファーへのアクセス、ユーザーは同時にアクセスしていることに注意します。 

このリスクを管理するユーザー データのバッファーからメモリのみを検証する必要があるすべてのパラメーターをコピーします (スタックやプール) などのカーネル モードからアクセスできます。 します。  後で、データにアクセスできません、ユーザー アプリケーションを検証、渡されたデータを操作します。

**ドライバーのコードは、メモリの正しい使用を行う必要があります。**

- すべてのドライバー プールの割り当ては、非実行可能ファイル (NX) のプールでなければなりません。 NX メモリ プールの使用は本質的に実行可能ファイル (np 受信) のプールを非ページ、使用するよりもセキュリティが強化されオーバーフロー攻撃に対する保護を強化します。 

- デバイス ドライバーは、さまざまなのユーザー モードとカーネルをカーネルの I/O、要求を正しく処理する必要があります。 

HVCI 仮想化をサポートするドライバーを許可するには、追加のメモリ要件があります。 詳細については、次を参照してください。[デバイス ガード互換性](#dgc)この記事で後述します。

**ハンドル数**

- ユーザー モードとカーネル モードのメモリの間で渡されたハンドルを検証します。 詳細については、次を参照してください。[処理管理](https://msdn.microsoft.com/library/windows/hardware/ff547382)と[オブジェクトの処理の検証に失敗した](https://msdn.microsoft.com/library/windows/hardware/ff545703)します。

**デバイス オブジェクト**

- デバイス オブジェクトをセキュリティで保護します。 詳細については、次を参照してください。[デバイス オブジェクトのセキュリティで保護する](https://msdn.microsoft.com/library/windows/hardware/ff563688)します。

- デバイス オブジェクトを検証します。 詳細については、次を参照してください。[デバイス オブジェクトの検証に失敗した](https://msdn.microsoft.com/library/windows/hardware/ff545700)します。

**Irp**

**WDF と Irp** 

WDF を使用する利点の 1 つは、ドライバーを WDF 通常は直接アクセスしていないこと Irp です。 たとえば、フレームワークには、KMDF/UMDF を I/O キューで受信するフレームワーク要求オブジェクトを読み取り、書き込み、およびデバイスの I/O 制御操作を表す WDM Irp に変換します。 

WDM ドライバーを作成する場合は、次のガイダンスを確認します。

**IRP I/O バッファーを適切に管理します。**

次の記事では、IRP の入力値の検証に関する情報を提供します。

[バッファー付き I/O を使用した DispatchReadWrite](https://msdn.microsoft.com/library/windows/hardware/ff543388)

[バッファー付き I/O のエラー](https://msdn.microsoft.com/library/windows/hardware/ff544293)

[ダイレクト I/O を使用した DispatchReadWrite](https://msdn.microsoft.com/library/windows/hardware/ff543393)

[ダイレクト I/O のエラー](https://msdn.microsoft.com/library/windows/hardware/ff544300)

[I/O 制御コードに関するセキュリティの問題](https://msdn.microsoft.com/library/windows/hardware/ff563700)

バッファーのアドレスと長さなどの IRP に関連付けられている値の検証を検討してください。 

どちらの I/O を使用する場合は、する読み取りと書き込みとは異なり、バッファー I/O およびダイレクト I/O とは異なりが I/O マネージャーによってを検証 I/O IOCTL のどちらを使用する場合、バッファー ポインターと長さがないことに注意してください。  


**IRP の完了操作を適切に処理します。**

ドライバーは IRP の状態のステータス値を持つ決して完了する必要があります\_成功しない限り、実際にサポートし、IRP を処理します。 IRP の完了操作を処理する正しい方法については、次を参照してください。 [Irp の完了](https://msdn.microsoft.com/library/windows/hardware/ff542018)します。

**保留中の状態のドライバー IRP を管理します。**

IRP を保存し、両方の呼び出しを含むを検討する必要があります前に、ドライバーは IRP の保留をマークする必要があります[ **IoMarkIrpPending** ](https://msdn.microsoft.com/library/windows/hardware/ff549422)と、インタロックされたシーケンスの割り当て。 詳細については、次を参照してください。[ドライバーの状態を確認するエラー](https://msdn.microsoft.com/library/windows/hardware/ff545672)と[を保持している受信 Irp ときに、デバイスが一時停止](https://docs.microsoft.com/windows-hardware/drivers/kernel/holding-incoming-irps-when-a-device-is-paused)します。

**IRP の取り消し操作を適切に処理します。**

操作のキャンセルは難しいコードに正しくため、通常は非同期的に実行します。 ハンドルが操作をキャンセルするコードの問題はことができますので、このコードは、通常では実行されません頻繁に実行中のシステムに、時間が長く気付かない移動します。 すべての提供情報を理解し、必ず[Irp のキャンセル](https://msdn.microsoft.com/library/windows/hardware/ff540748)します。 特に注意[同期 IRP のキャンセル](https://msdn.microsoft.com/library/windows/hardware/ff564531)と[Irp の検討時にキャンセルを指す](https://msdn.microsoft.com/library/windows/hardware/ff559700)します。

推奨される操作のキャンセルに関連付けられている同期の問題を最小限に抑える方法の 1 つを実装するためには、[キャンセル セーフ IRP キュー](https://msdn.microsoft.com/library/windows/hardware/ff540755)します。

**IRP のクリーンアップを処理し、適切に操作を終了**

間の違いを理解しているかどうかを必ず[ **IRP\_MJ\_クリーンアップ**](https://msdn.microsoft.com/library/windows/hardware/ff550718)と[ **IRP\_MJ\_閉じる** ](https://msdn.microsoft.com/library/windows/hardware/ff550720)要求。 アプリケーションは、ファイル オブジェクトのすべてのハンドルを閉じますが、すべての I/O の前にも要求が完了した後、クリーンアップ要求が到着します。 閉じる要求は、ファイル オブジェクトのすべての I/O 要求が完了またはキャンセルされた後に到着します。 詳しくは、次の記事をご覧ください。

[DispatchCreate、DispatchClose、DispatchCreateClose ルーチン](https://msdn.microsoft.com/library/windows/hardware/ff543279)

[DispatchCleanup ルーチン](https://msdn.microsoft.com/library/windows/hardware/ff543242)

[クリーンアップ操作と閉じる操作の処理エラー](https://msdn.microsoft.com/library/windows/hardware/ff544304)

Irp を正しく処理の詳細については、次を参照してください。 [Irp の処理で関連するエラー](https://msdn.microsoft.com/library/windows/hardware/ff540543)します。

**その他のセキュリティの問題**

- ロックまたはインタロックされたシーケンスを使用すると、競合状態を回避できます。 詳細については、次を参照してください。[マルチプロセッサ環境でエラー](https://msdn.microsoft.com/library/windows/hardware/ff544288)します。

- 各種のユーザー モードとカーネルをカーネルの I/O 要求に、デバイス ドライバーを正しく処理されることを確認します。

- TDI フィルターや Lsp がインストールされていないこと、ドライバー、または関連付けられているソフトウェア パッケージのインストールまたは使用状況の中に確認してください。 

**安全な関数を使用して、**

- 安全な文字列関数を使用します。 詳細については、次を参照してください。[安全な文字列関数を使用して](https://msdn.microsoft.com/library/windows/hardware/ff565508)します。

- 安全な算術関数を使用します。 詳細については、次を参照してください[算術関数](https://msdn.microsoft.com/library/windows/hardware/hh406348)で[安全な整数ライブラリ ルーチン。](https://msdn.microsoft.com/library/windows/hardware/hh406570)

- 安全な変換関数を使用します。 詳細については、次を参照してください[変換関数](https://msdn.microsoft.com/library/windows/hardware/hh450942)で[安全な整数ライブラリ ルーチン。](https://msdn.microsoft.com/library/windows/hardware/hh406570)

**追加のコードの脆弱性**

考えられる脆弱性がここで示しているだけでなくは、この記事では、カーネル モード ドライバーのコードのセキュリティ強化の詳細についてをは。[信頼性の高いカーネル モード ドライバーを作成する](https://msdn.microsoft.com/library/windows/hardware/ff542904)します。

C および C++ のセキュリティで保護されたコーディングについての詳細については、次を参照してください。[セキュリティ保護されたリソースをコーディング](#securecodingresources)この記事の最後にします。



## <a name="span-idmanagingdriveraccesscontrolspanspan-idmanagingdriveraccesscontrolspanspan-idmanagingdriveraccesscontrolspanmanage-driver-access-control"></a><span id="ManagingDriverAccessControl"></span><span id="managingdriveraccesscontrol"></span><span id="MANAGINGDRIVERACCESSCONTROL"></span>ドライバーのアクセス制御を管理します。

**セキュリティ チェックリスト項目\#7。***アクセスを制御する正しくことを確認するには、ドライバーを確認します。*

**ドライバーのアクセス制御の WDF の管理**

ユーザーがコンピューターのデバイスやファイルを不適切にアクセスできないようにするドライバーが動作する必要があります。 デバイスとファイルを不正アクセスを防ぐため、次の操作をする必要があります。

-   必要な場合にのみ、デバイス オブジェクトの名前を付けます。 名前付きのデバイス オブジェクトは、一般にのみ例については、旧システムのために必要な特定の名前を使用してデバイスを開くことが必要とするアプリケーションがある場合、または非 PNP デバイス/制御デバイスを使用している場合。  WDF のドライバーがデバイスに名前、PnP FDO を使用して、シンボリック リンクを作成するために必要がないことに注意してください[WdfDeviceCreateSymbolicLink](https://msdn.microsoft.com/library/windows/hardware/ff545939.aspx)します。

-   デバイス オブジェクトとインターフェイスへのアクセスをセキュリティで保護します。 

アプリケーションまたはその他の WDF ドライバー、PnP デバイス PDO へのアクセスを許可する、するためには、デバイスのインターフェイスを使用する必要があります。 詳細については、次を参照してください。[を使用してデバイスのインターフェイス](https://docs.microsoft.com/windows-hardware/drivers/wdf/using-device-interfaces)します。 デバイスのインターフェイスは、デバイス スタックの PDO へのシンボリック リンクとして機能します。 

PDO へのアクセスを制御するだ方法の 1 つは、INF の SDDL 文字列を指定することです。 INF ファイルの SDDL 文字列でない場合、Windows は既定のセキュリティ記述子を適用します。 詳細については、次を参照してください。[デバイス オブジェクトのセキュリティで保護する](https://docs.microsoft.com/windows-hardware/drivers/kernel/securing-device-objects)と[デバイス オブジェクトの SDDL](https://docs.microsoft.com/windows-hardware/drivers/kernel/sddl-for-device-objects)します。 

アクセスの制御に関する詳細については、次の記事を参照してください。

[KMDF ドライバーでのデバイス アクセスの制御](https://msdn.microsoft.com/windows/hardware/drivers/wdf/controlling-device-access-in-kmdf-drivers)

[名、セキュリティ記述子、およびデバイス クラスのデバイス オブジェクトにアクセスできるようにしています.安全な](https://www.osr.com/nt-insider/2017-issue1/making-device-objects-accessible-safe)から、 *February 2017 年 1 月、NT Insider ニュースレター*によって発行された[OSR](https://www.osr.com)します。


**ドライバーへのアクセスの制御 - WDM を管理します。**

WDM ドライバーを使用して、名前付きのデバイス オブジェクトを使用した場合は使用できます[IoCreateDeviceSecure](https://msdn.microsoft.com/library/windows/hardware/ff548407.aspx)しセキュリティを確保する SDDL を指定します。 実装に[IoCreateDeviceSecure](https://msdn.microsoft.com/library/windows/hardware/ff548407.aspx) DeviceClassGuid を常にカスタム クラス GUID を指定します。 既存のクラス GUID は、ここを指定する必要があります。 そうと、セキュリティの設定またはそのクラスに属している他のデバイスの互換性を中断する可能性があります。 詳細については、次を参照してください。 [WdmlibIoCreateDeviceSecure](https://msdn.microsoft.com/library/windows/hardware/mt800803.aspx)します。
   
詳しくは、次の記事をご覧ください。

[デバイス アクセスの制御](https://msdn.microsoft.com/library/windows/hardware/ff542063)

[デバイスの名前空間アクセスの制御](https://msdn.microsoft.com/library/windows/hardware/ff542068)

[ドライバー開発者向けの Windows セキュリティ モデル](windows-security-model.md)


**セキュリティ識別子 (Sid) のリスクの階層** 

次のセクションでは、ドライバーのコードで使用される一般的な Sid のリスクの階層について説明します。 SDDL の詳細については、次を参照してください。[デバイス オブジェクトの SDDL](https://msdn.microsoft.com/library/windows/hardware/ff563667)、 [SID 文字列](https://msdn.microsoft.com/library/windows/desktop/aa379602.aspx)、および[SDDL 文字列の構文](https://msdn.microsoft.com/library/cc230374.aspx)します。 

場合は、カーネルにアクセスするには、低い特権の呼び出し元ができる、コードのリスクが増加したことを理解しておく必要があります。 この概要の図では、ドライバーの機能を低い特権の Sid のアクセスを許可するようにリスクが高まります。

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

次の一般的な最小特権のセキュリティの原則、最小のレベルの関数は、ドライバーに必要なアクセスだけを構成します。

**WDM 細かい IOCTL セキュリティ コントロール**

Ioctl が呼び出し元のユーザー モードで送信されるときにセキュリティをさらに管理するドライバーのコードを含めることができます、 [IoValidateDeviceIoControlAccess](https://msdn.microsoft.com/library/windows/hardware/ff550418.aspx)関数。 この関数は、アクセス権を確認するためのドライバーをできます。 IOCTL を受信すると、ドライバーを呼び出すことができます[IoValidateDeviceIoControlAccess](https://msdn.microsoft.com/library/windows/hardware/ff550418.aspx)FILE_READ_ACCESS、FILE_WRITE_ACCESS、またはその両方を指定します。 

詳細な IOCTL セキュリティ制御を実装する前に説明した手法を使用してドライバーへのアクセスを管理する必要は置き換えられません。

詳しくは、次の記事をご覧ください。

[I/O 制御コードの定義](https://docs.microsoft.com/windows-hardware/drivers/kernel/defining-i-o-control-codes)


## <a name="span-iddgcspanspan-iddgcspanvalidate-device-guard-compatibility"></a><span id="DGC"></span><span id="dgc"></span>Device Guard の互換性を検証します。

**セキュリティ チェックリスト項目\#8。***互換性のある Device Guard をあるように、ドライバーがメモリを使用することを検証します。*

**メモリ使用量と Device Guard の互換性**

Device Guard では、ハードウェア テクノロジと仮想化を使用して、オペレーティング システムの残りの部分からコードの整合性 (CI) の意思決定関数を分離します。 仮想化ベースのセキュリティを使用して、CI を分離する、カーネル メモリは、実行可能になることができますのみの方法は、CI の認証です。 そのため、カーネル メモリのページは決して書き込み可能または実行可能 (W+X) にならず、実行可能コードを直接変更することはできません。 

Device Guard の互換性のあるコードを実装するには、次のドライバー コードになっていることを確認します。

- 既定では、NX にオプトインします。
- NX Api/フラグを使用して、メモリの割り当て (NonPagedPoolNx)
- 書き込み可能な実行可能ファイルのセクションでは使用しません
- 実行可能なシステム メモリを直接変更しようとはしません
- カーネルの動的なコードを使用しません
- 実行可能ファイルとしてデータ ファイルを読み込みません
- セクションの配置は 0x1000 の倍数 (ページ\_サイズ)。 例: ドライバー\_配置 0x1000 を =

詳細については、ツールと互換性のないメモリ呼び出しの一覧を使用して、次を参照してください。 [HVCI ドライバーの互換性を評価するデバイス ガード準備ツールを使用して](use-device-guard-readiness-tool.md)します。

Device Guard の詳細については、次を参照してください。 [Windows 10 Device Guard とドライバーの互換性](https://blogs.msdn.microsoft.com/windows_hardware_certification/2015/05/22/driver-compatibility-with-device-guard-in-windows-10/)します。

関連するシステムの基礎のセキュリティ テストの詳細については、次を参照してください。 [Device Guard のコンプライアンス対応がテスト](https://docs.microsoft.com/en-us/windows-hardware/test/hlk/testref/10c242b6-49f6-491d-876c-c39b22b36abc)と[Device Guard とドライバーの互換性](https://docs.microsoft.com/en-us/windows-hardware/test/hlk/testref/driver-compatibility-with-device-guard)します。



## <a name="span-idtechnologyspecificcodepracticesspanfollow-technology-specific-code-best-practices"></a><span id="technologyspecificcodepractices"></span>テクノロジ固有のコードのベスト プラクティスに従う


**セキュリティ チェックリスト項目\#9。***ドライバーの次のテクノロジに固有のガイダンスを確認します。*

*ファイル システム*

詳細については、ファイル システム ドライバーのセキュリティについて、次の記事を参照してください。

[ファイル システムのセキュリティに関する考慮事項](https://msdn.microsoft.com/windows/hardware/drivers/ifs/security-considerations-for-file-systems)

[ファイル システムのセキュリティに関する問題](https://msdn.microsoft.com/windows/hardware/drivers/ifs/file-system-security-issues)

[ファイル システム向けのセキュリティ機能](https://msdn.microsoft.com/windows/hardware/drivers/ifs/security-features-for-file-systems)

[ファイル システム フィルター ドライバーのセキュリティに関する考慮事項](https://msdn.microsoft.com/windows/hardware/drivers/ifs/security-considerations-for-file-system-filter-drivers)

*NDIS - ネットワーク*

NDIS ドライバーのセキュリティについては、次を参照してください。[ネットワーク ドライバーのセキュリティ問題](https://msdn.microsoft.com/windows/hardware/drivers/network/security-issues-for-network-drivers)します。

*ディスプレイ*

ディスプレイ ドライバーのセキュリティについては、次を参照してください。&lt;コンテンツ保留中&gt;します。


*プリンター*

プリンター ドライバーのセキュリティに関連する情報は、次を参照してください。 [V4 プリンター ドライバーのセキュリティに関する考慮事項](https://msdn.microsoft.com/library/windows/hardware/jj863679)します。

*Windows Image Acquisition (WIA) ドライバーのセキュリティの問題*

WIA セキュリティについては、次を参照してください。[セキュリティの問題を Windows Image Acquisition (WIA) ドライバー](https://msdn.microsoft.com/windows/hardware/drivers/image/security-issues-for-wia-drivers)します。



## <a name="span-idenhancedeviceinstallationsecurityspanenhance-device-installation-security"></a><span id="enhancedeviceinstallationsecurity"></span>デバイス インストールのセキュリティを強化します。

**セキュリティ チェックリスト項目\#10。***ベスト プラクティスをフォローしているかどうかを確認するドライバーの inf の作成とインストールのガイダンスを確認します。*

ドライバーをインストールするコードを作成するときに、デバイスのインストールが常に安全な方法で実行することを確認しておく必要があります。 セキュリティで保護されたデバイスのインストールは、1 つには、次は。
 
- デバイスとそのデバイスのインターフェイス クラスへのアクセス制限
- デバイスの作成されたドライバー サービスへのアクセスを制限
- ドライバー ファイルを変更または削除から保護します。
- デバイスのレジストリ エントリへのアクセス制限
- デバイスの WMI クラスへのアクセス制限
- 正しく SetupAPI 関数を使用します。

詳しくは、次の記事をご覧ください。

[セキュリティで保護されたデバイスのインストールの作成](https://msdn.microsoft.com/windows/hardware/drivers/install/creating-secure-device-installations)

[SetupAPI の使用に関するガイドライン](https://msdn.microsoft.com/windows/hardware/drivers/install/guidelines-for-using-setupapi)

[デバイス インストール関数の使用](https://msdn.microsoft.com/windows/hardware/drivers/install/using-device-installation-functions)

[デバイスとドライバーのインストールに関する高度なトピック](https://msdn.microsoft.com/windows/hardware/drivers/install/device-and-driver-installation-advanced-topics)



## <a name="span-idpeercodereviewspanperform-peer-code-review"></a><span id="peercodereview"></span>ピア コード レビューを実行します。

**セキュリティ チェックリスト項目\#11。***他のツールとプロセスには表示されません問題を見つけるために、ピア コード レビューを実行します。*

不足している問題を見つけるために、知識の豊富なコードのレビュー担当者をシークします。 目の 2 番目のセットには、多くの場合したが見過ごしている可能性のある問題が表示されます。

内部的にコードを確認する適切なスタッフを持っていない場合は、この目的の社外のヘルプを魅力的な検討してください。



## <a name="span-idreleasedriversigningspanspan-idreleasedriversigningspanspan-idreleasedriversigningspanexecute-proper-release-driver-signing"></a><span id="ReleaseDriverSigning"></span><span id="releasedriversigning"></span><span id="RELEASEDRIVERSIGNING"></span>リリースの適切なドライバーの署名を実行します。


**セキュリティ チェックリスト項目\#12。***Windows のパートナー ポータルを使用して、配布用にドライバーを適切に署名します。*

ドライバー パッケージを一般にリリースする前に、パッケージの認定依頼を提出することをお勧めします。 詳細については、次を参照してください[パフォーマンス、互換性をテスト](https://msdn.microsoft.com/windows/hardware/commercialize/test/index)、[ハードウェア プログラムの概要](https://msdn.microsoft.com/windows/hardware/drivers/dashboard/get-started-with-the-hardware-dashboard)、[ハードウェア ダッシュ ボード サービス](https://msdn.microsoft.com/windows/hardware/drivers/dashboard/dashboard-services)、および[。構成証明の公開リリースのカーネル ドライバーの署名](https://msdn.microsoft.com/windows/hardware/drivers/dashboard/attestation-signing-a-kernel-driver-for-public-release)します。



## <a name="span-iduse-code-analysisspanuse-code-analysis-in-visual-studio-to-investigate-driver-security"></a><span id="use-code-analysis"></span>Visual Studio でコード分析を使用して、ドライバーのセキュリティを調査するには

**セキュリティ チェックリスト項目\#13。***Visual Studio でコード分析の機能を使用して、ドライバー コードの脆弱性を確認する次の手順に従います。*

Visual Studio でコード分析の機能を使用して、コードでセキュリティの脆弱性を確認します。 Windows Driver Kit (WDK) では、ネイティブ ドライバー コードの問題を確認するように設計された規則セットをインストールします。

詳細については、次を参照してください。[ドライバーのコード分析を実行する方法](https://msdn.microsoft.com/windows/hardware/drivers/devtest/how-to-run-code-analysis-for-drivers)します。

詳細については、次を参照してください。 [Code Analysis for drivers の概要](https://msdn.microsoft.com/library/windows/hardware/hh698231.aspx)します。 コード分析の詳細については、次を参照してください。 [Visual Studio 2013 での静的コード分析の深さ](https://blogs.msdn.microsoft.com/hkamel/2013/10/24/visual-studio-2013-static-code-analysis-in-depth-what-when-and-how/)します。

コード分析について理解しておくことが使用するサンプル ドライバーのいずれかの例では、おすすめのトースター サンプルでは、<https://github.com/Microsoft/Windows-driver-samples/tree/master/general/toaster/toastDrv/kmdf/func/featured>または ELAM 早期起動マルウェア対策サンプル<https://github.com/Microsoft/Windows-driver-samples/tree/master/security/elam>します。

1. Visual Studio でのドライバー ソリューションを開きます。

2. Visual Studio で、ソリューション内の各プロジェクトの目的の規則セットを使用するプロジェクトのプロパティを変更します。 以下に例を示します。プロジェクト&gt;&gt;プロパティ&gt;&gt;コード分析&gt;&gt;全般]、[選択*推奨ドライバー規則*します。 Recommenced ドライバー規則だけでなく、使用、*推奨ネイティブ規則*ルール セット。

3. ビルドを選択します。 &gt; &gt;ソリューションでコード分析を実行します。

4. 警告を表示、**エラー一覧**ビルドのタブが Visual Studio のウィンドウを出力します。

コードで問題のある領域を表示するには、各警告の説明をクリックします。

追加情報を表示するリンクされた警告コードをクリックします。

コードが、変更する必要があるかどうか、または注釈を許可、コードの意図を適切にコード分析エンジンに追加する必要があるかどうかを決定します。 コードの注釈の詳細については、次を参照してください。 [C と C++ コードの欠陥を削減する SAL 注釈を使って](https://msdn.microsoft.com/library/ms182032.aspx)と[Windows ドライバーの SAL 2.0 注釈](https://msdn.microsoft.com/windows/hardware/drivers/devtest/sal-2-annotations-for-windows-drivers)します。

SAL の概要については、OSR から使用可能な次の記事を参照してください。
https://www.osr.com/blog/2015/02/23/sal-annotations-dont-hate-im-beautiful/

## <a name="span-idsdvspanspan-idsdvspanuse-static-driver-verifier-to-check-for-vulnerabilities"></a><span id="SDV"></span><span id="sdv"></span>Static Driver Verifier を使用して、脆弱性を確認するには

**セキュリティ チェックリスト項目\#14。***Visual Studio で Static Driver Verifier (SDV) を使用して、ドライバーのコードの脆弱性を確認する次の手順に従います。*

Static Driver Verifier (SDV) では、一連のインターフェイスのルールと、オペレーティング システムのモデルを使用して、ドライバーが Windows オペレーティング システムに適切かどうかを判断します。 SDV は、ドライバーでの潜在的なバグを指すドライバー コードの欠陥を検出します。

詳細については、次を参照してください。 [Static Driver Verifier の導入](https://msdn.microsoft.com/windows/hardware/drivers/devtest/introducing-static-driver-verifier)と[Static Driver Verifier](https://msdn.microsoft.com/windows/hardware/drivers/devtest/static-driver-verifier)します。 SDV で、特定の種類のドライバーのみがサポートされていることに注意してください。 SDV を検証するドライバーの詳細については、次を参照してください。[ドライバーのサポートされている](https://msdn.microsoft.com/windows/hardware/drivers/devtest/supported-drivers)します。

SDV に理解して、サンプル ドライバーのいずれかを使用できます (おすすめトースター サンプルなど: <https://github.com/Microsoft/Windows-driver-samples/tree/master/general/toaster/toastDrv/kmdf/func/featured>)。

1. Visual Studio では、対象となるドライバー ソリューションを開きます。

2. Visual Studio で、変更、ビルドの種類を*リリース*します。 Static Driver Verifier は、ビルドの種類がリリースでは、デバッグないである必要があります。

3. Visual Studio でビルドを選択します。 &gt; &gt;ソリューションのビルド。

4. Visual Studio で、ドライバーを選択します。 &gt; &gt; Static Driver Verifier を起動します。

5. SDV での*ルール* タブで *既定**規則セット*。

既定の規則は、多くの一般的な問題を検索より広範なを実行していることを検討してください*ドライバーのすべてのルール*ルール セットもします。

6. *Main*  タブの SDV は、次のようにクリックします。*開始*します。

7. SDV が完了すると、出力で警告を確認します。 *Main*  タブで見つかった欠陥の合計数が表示されます。

8. SDV のレポート ページを読み込み、可能なコードの脆弱性に関連する情報を検証するには、各警告をクリックします。 検証結果を調査して、SDV の確認に失敗した、ドライバーのパスを識別するためには、レポートを使用します。 詳細については、次を参照してください。[静的ドライバー検証ツールのレポート](https://msdn.microsoft.com/library/windows/hardware/ff552834)します。




## <a name="span-idbinscopespanspan-idbinscopespanspan-idbinscopespancheck-code-with-binscope-binary-analyzer"></a><span id="BinScope"></span><span id="binscope"></span><span id="BINSCOPE"></span>BinScope Binary Analyzer を使用したコードを確認してください。

**セキュリティ チェックリスト項目\#15。***BinScope を使用して、既知のセキュリティの問題を最小限に抑えるコンパイルとビルド オプションが構成されている二重にチェックするこれらの手順に従います。*

BinScope を使用して、コーディングと可能性のあるレンダリングできるアプリケーションまたは攻撃ベクトルとして使用される攻撃に対して脆弱プラクティスの構築を識別するためにアプリケーションのバイナリ ファイルを調べます。

詳細については、次を参照してください。[新しいバージョンの BinScope Binary Analyzer](https://cloudblogs.microsoft.com/microsoftsecure/2014/11/20/new-binscope-released/) 、ユーザーと入門ガイドは、ツールのダウンロードに含まれているとします。


発送するコードで、セキュリティのコンパイル オプションが正しく構成されているかを検証する次の手順に従います。

1. BinScope アナライザーおよび関連ドキュメントはこちらからダウンロード:<https://www.microsoft.com/download/details.aspx?id=44995>します。

2. レビュー、 *BinScope ファースト ステップ ガイド*ダウンロードしました。

3. ターゲット コンピューターのテストを検証するコンパイル済みコードを含む BinScope をインストールするのに MSI ファイルを使用します。

4. コマンド プロンプト ウィンドウを開き、バイナリのコンパイル済みのドライバーを確認するには、次のコマンドを実行します。 コンパイル済みのドライバーの .sys ファイルによって をポイントするパスを更新します。

```cpp
C:\Program Files\Microsoft BinScope 2014>binscope "C:\Samples\KMDF_Echo_Driver\echo.sys" /verbose /html /logfile c:\mylog.htm 
```

5. ブラウザーを使用して、すべてのチェックに (PASS) はマークされていることを確認する BinScope レポートを確認します。

既定では、HTML レポートが書き込まれます\\ユーザー\\&lt;username&gt;\\BinScope\\

ログ ファイルに出力があります。 次の 3 つのカテゴリがあります。

-   失敗したチェック\[失敗\]
-   完了していないことを確認します\[エラー\]
-   チェックに合格\[を渡す\]

合格したチェックは既定では、ログに書き込まれませんしを使用して有効にする必要がありますに注意してください、/verbose スイッチします。

```cpp
Results for Microsoft BinScope 2014 run on MyPC at 2017-01-28T00:18:48.3828242Z

Failed Checks
No failed checks. 
Passed Checks

• C:\Samples\KMDF_Echo_Driver\echo.sys - ATLVersionCheck (PASS)
• C:\Samples\KMDF_Echo_Driver\echo.sys - ATLVulnCheck (PASS)
• C:\Samples\KMDF_Echo_Driver\echo.sys - CompilerVersionCheck (PASS)
• C:\Samples\KMDF_Echo_Driver\echo.sys - DBCheck (PASS)
• C:\Samples\KMDF_Echo_Driver\echo.sys - DefaultGSCookieCheck (PASS)
• C:\Samples\KMDF_Echo_Driver\echo.sys - ExecutableImportsCheck (PASS)
• C:\Samples\KMDF_Echo_Driver\echo.sys - GSCheck (PASS)
• C:\Samples\KMDF_Echo_Driver\echo.sys - GSFriendlyInitCheck (PASS)
• C:\Samples\KMDF_Echo_Driver\echo.sys - GSFunctionSafeBuffersCheck (PASS)
• C:\Samples\KMDF_Echo_Driver\echo.sys - HighEntropyVACheck (PASS)
• C:\Samples\KMDF_Echo_Driver\echo.sys - NXCheck (PASS)
• C:\Samples\KMDF_Echo_Driver\echo.sys - RSA32Check (PASS)
• C:\Samples\KMDF_Echo_Driver\echo.sys - SafeSEHCheck (PASS)
• C:\Samples\KMDF_Echo_Driver\echo.sys - SharedSectionCheck (PASS)
• C:\Samples\KMDF_Echo_Driver\echo.sys - VB6Check (PASS)
• C:\Samples\KMDF_Echo_Driver\echo.sys - WXCheck (PASS)

Checks Executed:
• ATLVersionCheck
• ATLVulnCheck
• CompilerVersionCheck
• DBCheck
• DefaultGSCookieCheck
• ExecutableImportsCheck
• GSCheck
• GSFriendlyInitCheck
• GSFunctionSafeBuffersCheck
• HighEntropyVACheck
• NXCheck
• RSA32Check
• SafeSEHCheck
• SharedSectionCheck
• VB6Check
• WXCheck

All Scanned Items

• C:\Samples\KMDF_Echo_Driver\echo.sys
```

## <a name="span-idcodevalidationtoolsspanspan-idcodevalidationtoolsspanspan-idcodevalidationtoolsspanuse-additional-code-validation-tools"></a><span id="CodeValidationTools"></span><span id="codevalidationtools"></span><span id="CODEVALIDATIONTOOLS"></span>追加のコード検証ツールを使用します。

**セキュリティ チェックリスト項目\#16。***コード セキュリティに関する推奨事項に従うことを検証して、開発プロセスで欠落されたギャップを探すには、これらの追加ツールを使用します。*

ほかに[Visual Studio Code 分析](#use-code-analysis)、 [Static Driver Verifier](#sdv)、および[Binscope](#binscope)で欠落されたギャップを探すために、次のツールを使用して前述のとおり、開発プロセス。

**ドライバーの検証ツール**

Driver Verifier は、ドライバーのテストをライブにできます。 Driver Verifier は、Windows カーネル モード ドライバーと無効な関数呼び出しまたはシステムが破損する可能性がありますアクションを検出するグラフィック ドライバーを監視します。 Driver Verifier は、負荷と不適切な動作を検索するテストのさまざまな Windows ドライバーをサブジェクトことができます。 詳細については、次を参照してください。 [Driver Verifier](https://msdn.microsoft.com/windows/hardware/drivers/devtest/driver-verifier)します。

**ハードウェアの互換性プログラムのテスト**

ハードウェアの互換性プログラムには、セキュリティが含まれています。 関連するコードの脆弱性を確認するテストを使用できます。 Windows ハードウェア互換性プログラムは、Windows ハードウェア ラボ キット (HLK) でテストを活用します。 HLK デバイス基礎テストは、ドライバーのコードと脆弱性のプローブを実行するためのコマンドラインで使用できます。 デバイスの基本テストとハードウェアの互換性プログラムの一般情報は、次を参照してください。 [Windows ハードウェア ラボ キット](https://docs.microsoft.com/en-us/windows-hardware/test/hlk/windows-hardware-lab-kit)します。

次のテストでは、コードの脆弱性に関連するいくつかの動作のドライバー コードの確認に役立つ可能性があるテストの例を示します。

 [DF - ファジー ランダム IOCTL テスト (信頼性)](https://docs.microsoft.com/windows-hardware/test/hlk/testref/236b8ad5-0ba1-4075-80a6-ae9dafb71c94)

 [DF - ファジーはサブ テスト (信頼性) 開きます](https://docs.microsoft.com/windows-hardware/test/hlk/testref/92bf534e-aa48-4aeb-b3cd-e46fb7cc7d80)

 [DF - ファジー 0 長バッファー FSCTL テスト (信頼性)](https://docs.microsoft.com/windows-hardware/test/hlk/testref/5f5f6c7e-d5db-4ff1-8cee-da47203ab070)

 [DF - ファジー ランダム FSCTL テスト (信頼性)](https://docs.microsoft.com/windows-hardware/test/hlk/testref/e529e34e-076a-4978-926f-7eca333e8f4d)

 [DF - その他の API をファジー テスト (信頼性)](https://docs.microsoft.com/windows-hardware/test/hlk/testref/fb305d04-6e8c-4dfc-9984-9692df82fbd8)

 使用することも、[カーネル同期遅延ファジー テスト](https://docs.microsoft.com/windows-hardware/drivers/devtest/kernel-synchronization-delay-fuzzing)Driver Verifier に含まれます。

(同時実行ハードウェアおよびオペレーティング システム) の混乱のテストがテスト PnP ドライバーさまざまなデバイス ドライバーのファジー テストを実行し、システムの電源が同時にテストします。 詳細については、次を参照してください。 [CHAOS テスト (デバイスの基本)](https://docs.microsoft.com/en-us/windows-hardware/drivers/devtest/chaos-tests--device-fundamentals-)します。

デバイスの基礎の侵入テストは、セキュリティのテストの重要なコンポーネントである入力による攻撃のさまざまなフォームを実行します。 攻撃および侵入テストは、ソフトウェア インターフェイスでの脆弱性を識別に役立つことができます。 詳細については、次を参照してください。[侵入テスト (デバイスの基本)](https://docs.microsoft.com/en-us/windows-hardware/drivers/devtest/penetration-tests--device-fundamentals-)します。

使用して、 [Device Guard のコンプライアンス テスト](https://docs.microsoft.com/en-us/windows-hardware/test/hlk/testref/10c242b6-49f6-491d-876c-c39b22b36abc)、と共に、ドライバーが Device Guard の互換性のあることを確認する、この記事で説明されているその他のツール。


**カスタム プロパティとドメイン固有のテスト ツール**

カスタム ドメイン固有のセキュリティのテストの開発を検討してください。 追加のテストを開発するには、ソフトウェアとドライバーの開発中の特定の種類で使い慣れた関連のない開発リソースの元の設計者と 1 つまたは複数のセキュリティ侵入の分析に詳しい人から入力を収集し、防止します。



## <a name="span-iddebuggerspanspan-iddebuggerspanspan-iddebuggerspanreview-debugger-techniques-and-extensions"></a><span id="Debugger"></span><span id="debugger"></span><span id="DEBUGGER"></span>レビューのデバッガー方法と拡張機能


**セキュリティ チェックリスト項目\#17。***これらのデバッガー ツールを確認し、開発ワークフローのデバッグでの使用を検討してください。*

**! 悪用 Crash Analyzer**

! 悪用 Crash Analyzer は、解析がクラッシュの固有の問題を探してログで、Windows デバッガー拡張機能。 クラッシュの種類を調べても、エラーが、悪意のあるハッカーに悪用されることであるかどうかを確認しようとしています。

Microsoft Security Engineering Center (MSEC)、作成、。 Crash Analyzer を悪用します。 ダウンロードすることができます、codeplex から:<https://msecdbg.codeplex.com/>します。

詳細については、次を参照してください[!。クラッシュが悪用可能なアナライザー バージョン 1.6](https://blogs.microsoft.com/microsoftsecure/2013/06/13/exploitable-crash-analyzer-version-1-6/)および Channel 9 ビデオ[! 悪用 Crash Analyzer](https://channel9.msdn.com/blogs/pdcnews/bang-exploitable-security-analyzer)します。

**セキュリティ関連のデバッガー コマンド**

! Acl の拡張機能は、書式設定し、アクセス制御リスト (ACL) の内容を表示します。 詳細については、次を参照してください。[オブジェクトの ACL の決定](https://msdn.microsoft.com/library/windows/hardware/ff541868)と[ **! acl**](https://msdn.microsoft.com/library/windows/hardware/ff561510)します。

します。 トークンの拡張機能には、セキュリティ トークンのオブジェクトの書式設定されたビューが表示されます。 詳細については、次を参照してください。 [ **! トークン**](https://msdn.microsoft.com/library/windows/hardware/ff565477)します。

! Tokenfields 拡張機能は、名前とアクセス トークンのオブジェクト (トークンの構造) 内のフィールドのオフセットが表示されます。 詳細については、次を参照してください。 [ **! tokenfields**](https://msdn.microsoft.com/library/windows/hardware/ff565478)します。

! Sid の拡張機能では、指定したアドレスにセキュリティ識別子 (SID) が表示されます。 詳細については、次を参照してください。 [ **! sid**](https://msdn.microsoft.com/library/windows/hardware/ff565344)します。

! Sd の拡張機能は、指定したアドレスにセキュリティ記述子を表示します。 詳細については、次を参照してください。 [ **! sd**](https://msdn.microsoft.com/library/windows/hardware/ff564930)します。


## <a name="span-idsecurecodingresourcesspanspan-idsecurecodingresourcesspanspan-idsecurecodingresourcesspanreview-secure-coding-resources"></a><span id="SecureCodingResources"></span><span id="securecodingresources"></span><span id="SECURECODINGRESOURCES"></span>セキュリティ保護されたリソースをコード レビュー


**セキュリティ チェックリスト項目\#18。***展開ドライバー開発者向けに適用されるセキュリティで保護されたコーディング ベスト プラクティスについての理解にこれらのリソースを確認します。*

*詳細については、ドライバーのセキュリティはこれらのリソースを確認してください。*

**セキュリティで保護されたカーネル モード ドライバーのコーディングのガイドライン**

[信頼性の高いカーネルモード ドライバーの作成](https://msdn.microsoft.com/library/windows/hardware/ff542904.aspx)

**セキュリティで保護されたコーディング組織**

[Carnegie Mellon University SEI CERT](https://www.cert.org/)

カーネギー メロン大学 SEI CERT[コーディング標準 C:安全性と信頼性が高く、セキュリティで保護されたシステムを開発するためのルール](https://www.securecoding.cert.org/confluence/display/c/SEI+CERT+C+Coding+Standard)(2016年のエディション)。

証明書の[セキュリティを構築](https://www.us-cert.gov/bsi)

MITRE - [CERT C でアドレス指定の弱点は、コーディング標準をセキュリティで保護](https://cwe.mitre.org/data/definitions/734.html)

成熟度モデル (BSIMM) - セキュリティの構築 [https://www.bsimm.com/](https://www.bsimm.com/)

SAFECode- [https://www.safecode.org/](https://www.safecode.org/)


**OSR**

[OSR](https://www.osr.com)ドライバーの開発のトレーニングおよびコンサルティング サービスを提供します。 OSR ニュースレターからこれらの記事では、ドライバーのセキュリティの問題が強調表示します。

[名、セキュリティ記述子、およびデバイス クラスのデバイス オブジェクトにアクセスできるようにしています. 安全な](https://www.osr.com/nt-insider/2017-issue1/making-device-objects-accessible-safe)

[すると Protection--内でドライバーとデバイスのセキュリティを使用して、ことごとく](https://www.osronline.com/article.cfm?article=100)

[ドライバーの手法のアンケートのロックダウン](https://www.osronline.com/article.cfm?article=357) 

[Meltdown と Spectre:ドライバーのでしょうか。](https://www.osr.com/blog/2018/01/23/meltdown-spectre-drivers/) 

**ケース スタディ**

[ドライバーの脆弱性にアラート: からMicrosoft Defender ATP 調査 unearths 特権エスカレーション欠陥](https://www.microsoft.com/security/blog/2019/03/25/from-alert-to-driver-vulnerability-microsoft-defender-atp-investigation-unearths-privilege-escalation-flaw/)


**書籍**

*ソフトウェアのセキュリティの 24 の deadly sins: プログラミングの欠陥とその解決方法*Michael Howard、David LeBlanc、John Viega して

*ソフトウェアのセキュリティ評価のアート: 識別して、ソフトウェアの脆弱性の防止*、Mark Dowd、John マクドナルドおよび Justin Schuh

*セキュリティで保護されたソフトウェアの第 2 版の書き込み*、Michael Howard と David leblanc 共著

*ソフトウェアのセキュリティ評価のアート:識別して、ソフトウェアの脆弱性の防止*、Mark Dowd と John マクドナルド

*Secure Coding in C および C++ (ソフトウェア エンジニア リング SEI シリーズ) 2 nd Edition*、Robert C. Seacord

*Microsoft Windows ドライバーのプログラミング モデルの (2 nd Edition)*、Walter Oney

*Windows Driver Foundation (開発者向けリファレンス) でドライバーの開発*、小額 Orwick と Guy Smith 


**トレーニング**

Windows ドライバーのクラスルーム トレーニング、次などのベンダーから提供されています。

- [OSR](https://www.osr.com) 
- [Winsider](https://www.windows-internals.com/)
- [Azius](https://www.azius.com)

セキュリティ保護されたコーディング オンライン トレーニングは、使用可能なさまざまなソースから。 たとえば、このコースは coursera などから入手できます。

[https://www.coursera.org/learn/software-security](https://www.coursera.org/learn/software-security).

SAFECode では、無料トレーニングにも用意されています。

[SAFECode.org/training](https://safecode.org/training/)

**プロフェッショナルな認定資格**

 証明書の提供、[コーディング Professional 証明書のセキュリティで保護された](https://www.cert.org/go/secure-coding/)します。


## <a name="span-idkeytakeawaysspansummary-of-key-takeaways"></a><span id="keytakeaways"></span>重要な習得事項の概要

ドライバーのセキュリティは、多くの要素を含む複雑な作業ですが、考慮すべきいくつかの要点を次に示します。

-   ドライバーは、windows カーネルで live し、オペレーティング システム全体を公開するカーネルを実行中に問題が発生します。 このため、セキュリティを考慮してドライバーのセキュリティ機能と設計に細心の注意してください。

-   最小特権の原則が適用されます。

    a.   厳密な SDDL 文字列を使用して、ドライバーへのアクセス制限

    b.   個々 の IOCTL をさらに制限します。 

-   さらに攻撃ベクトルを特定できるかどうか何か制限を考慮する脅威モデルを作成します。
-   ユーザー モードから渡された埋め込みポインターに関して注意します。 アクセスを除く、try 内、広範囲に必要なバッファーの値でキャプチャと比較してない場合は (ToCToU) を使用して問題の時間のチェックの時刻に発生しやすい.
-   不明な場合は、メソッドのバッファリング IOCTL として METHOD_BUFFERED を使用します。
-   ユーティリティのスキャン コードを使用して、既知のコードの脆弱性を検索し、問題を修復します。
-   不足している問題を見つけるために、知識の豊富なコードのレビュー担当者をシークします。
-   ドライバーの検証方法を使用し、コーナー ケースを含む、複数の入力が、ドライバーをテストします。

 

[この記事に関するコメントをマイクロソフトに送信](mailto:wsddocfb@microsoft.com?subject=Documentation%20feedback%20[hw_design/hw_design]:%20Driver%20security%20checklist%20%20RELEASE:%20%286/16/2017%29&body=%0A%0APRIVACY%20STATEMENT%0A%0AWe%20use%20your%20feedback%20to%20improve%20the%20documentation.%20We%20don't%20use%20your%20email%20address%20for%20any%20other%20purpose,%20and%20we'll%20remove%20your%20email%20address%20from%20our%20system%20after%20the%20issue%20that%20you're%20reporting%20is%20fixed.%20While%20we're%20working%20to%20fix%20this%20issue,%20we%20might%20send%20you%20an%20email%20message%20to%20ask%20for%20more%20info.%20Later,%20we%20might%20also%20send%20you%20an%20email%20message%20to%20let%20you%20know%20that%20we've%20addressed%20your%20feedback.%0A%0AFor%20more%20info%20about%20Microsoft's%20privacy%20policy,%20see%20 https://privacy.microsoft.com/default.aspx. "このトピックに関するコメントをマイクロソフトに送信します。")




