---
title: DMA の検証
description: DMA の検証
ms.assetid: ffcb718a-63f5-49ff-9d36-67b2aa59761f
keywords:
- DMA 検証機能 WDK ドライバー検証ツール
- HAL 検証 WDK ドライバー検証ツール
- 共通バッファー DMA WDK ドライバー検証ツール
- パケット DMA WDK ドライバー検証ツール
- スキャッター-ギャザー DMA WDK ドライバー検証ツール
- システム DMA WDK ドライバー検証ツール
- ダイレクトメモリアクセス WDK ドライバー検証ツール
- DMA エラー WDK ドライバーの検証
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 915f749073f11e6da9b0b8d5f30fb1784765eef7
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72839565"
---
# <a name="dma-verification"></a>DMA の検証


## <span id="ddk_dma_verification_tools"></span><span id="DDK_DMA_VERIFICATION_TOOLS"></span>


DMA 検証では、ダイレクトメモリアクセス (DMA) の使用が監視されます。 Windows の開発に応じて DMA ルーチンが変更されているため、多くのドライバーでは DMA 呼び出しを正しく使用できません。 さらに、一部のドライバーライターは、HAL DMA サブシステムを完全にバイパスしようとします。 これにより、油断のバグがドライバーに導入される可能性があります。

ドライバー検証ツールの DMA 検証オプションで、一般的な DMA エラーをキャッチしようとしています。 **! Dma**カーネルデバッガー拡張機能と共に、ドライバーが dma を適切な方法で使用していることを確認するために使用できます。

この Driver Verifier オプションは、 *HAL の検証*とも呼ばれます。 ドライバーの検証ツールによって生成されるエラーメッセージには、この用語が使用される場合があります。

このドライバーの検証ツールオプションは、Windows XP 以降でのみ使用できます。

### <a name="span-iddifferent_types_of_dmaspanspan-iddifferent_types_of_dmaspandifferent-types-of-dma"></a><span id="different_types_of_dma"></span><span id="DIFFERENT_TYPES_OF_DMA"></span>さまざまな種類の DMA

DMA は、ハードウェアデバイスがプロセッサを使用せずにメモリとの間でデータをやり取りできるようにするメカニズムです。 転送を設定するにはプロセッサが必要です。また、転送が完了すると、デバイスはプロセッサに通知します。 このシステムの利点は、DMA 転送の実行中にプロセッサが他のタスクを実行できることです。

Windows 2000 以降で使用される DMA には、次のような種類があります。

<span id="Common-buffer_DMA"></span><span id="common-buffer_dma"></span><span id="COMMON-BUFFER_DMA"></span>*共通バッファー DMA*  
共通バッファー DMA は、システムがハードウェアとソフトウェアの両方からアクセスできる1つのバッファーを割り当てることができる場合に実行されます。 ドライバーは、バッファーへのアクセスを同期します。 メモリがキャッシュされていないため、ドライバーの同期が容易になります。 共通のバッファーを設定した後、ドライバーとハードウェアの両方で、HAL の介入なしにバッファー内のアドレスに直接書き込むことができます。

<span id="Packet_DMA"></span><span id="packet_dma"></span><span id="PACKET_DMA"></span>*パケット DMA*  
パケット DMA は、ハードウェアで使用するためにマップする必要がある1つの既存のバッファーがある場合に実行されます。 パケット DMA を使用する例として、メモリからディスクへのファイルの転送があります。 このような状況では、ハードウェアがディスクに転送する前にファイルを共通バッファーに転送する必要があるため、このような状況では、共通バッファー DMA を使用することは無駄になります。 代わりに、HAL が調査されます。これにより、ハードウェアがメモリ内の実際のバッファーを検出するために必要な情報がドライバーに与えられます。 この操作は、さまざまなアーキテクチャで動作するルーチンが必要になるため、複雑になります。

<span id="Scatter_gather_DMA"></span><span id="scatter_gather_dma"></span><span id="SCATTER_GATHER_DMA"></span>*スキャッター/ギャザー DMA*  
スキャッター/ギャザー DMA は、一度に複数のパケット DMA 転送を設定するショートカットメソッドです。 たとえば、ネットワーク上でパケットを転送する場合、ネットワークスタックの各部分には、独自のヘッダー (TCP、IP、イーサネットなど) が追加されます。 これらのヘッダーは、メモリ内のさまざまな場所から割り当てられます。 この場合、スキャッター/ギャザー DMA は、ハードウェアによるアクセスのために各ヘッダーとデータセグメントをマップするために、HAL にバッチ要求を発行することによって時間を節約します。 パケットの各部分に対してパケット DMA ルーチンを呼び出す必要がなく、このメソッドは各ルーチンを1回呼び出します。これにより、HAL は各ルーチンを個別にマップすることができます。

**注**  *スキャッター/ギャザー機能*は、デバイスがスキャッター/ギャザールーチンを使用できることを意味するものではありません。 スキャッター/ギャザー機能は、デバイスの説明の中で、デバイスが特定の範囲だけではなく、メモリ内の任意の領域から読み書きできることを示すフラグを指します。

 

<span id="System_DMA"></span><span id="system_dma"></span><span id="SYSTEM_DMA"></span>*システム DMA*  
システム DMA は、直接転送を行うために、マザーボード上のシステム DMA コントローラーをプログラミングすることによって実行されます。 システム DMA を使用できるのは ISA カードだけです。

### <a name="span-ideffects_of_dma_verificationspanspan-ideffects_of_dma_verificationspaneffects-of-dma-verification"></a><span id="effects_of_dma_verification"></span><span id="EFFECTS_OF_DMA_VERIFICATION"></span>DMA 検証の影響

DMA 検証がアクティブになっている場合、ドライバー検証ツールは次のような DMA ルーチンの不適切な使用を検出します。

-   Underrunning または DMA メモリバッファーをオーバーランします (これらのエラーは、ハードウェアまたはドライバーによって行うことができます)。

-   共通のバッファー、アダプターチャネル、マップレジスタ、またはスキャッター/ギャザーリストをダブル解放します。

-   一般的なバッファー、アダプターチャネル、マップレジスタ、スキャッター/ギャザーリスト、またはアダプターを解放せずにメモリをリークする。

-   アダプターに対して一度に複数のアダプターチャネルが存在する。

-   既に解放され、存在しないアダプターを使用しようとしています。

-   アダプターバッファーをフラッシュしていません。

-   アダプターの未解決の参照カウントが多すぎます。

-   ページング可能なバッファーで DMA を実行する (DMA 転送を開始する前にすべてのバッファーをロックする必要があります)。

-   破損したフラグを使用して、MDL で DMA を実行します。

-   最初の MDL の前、または最初の MDL の終了後、または mdl バッファーより長く、mdl 内のページ境界を越える転送長を使用して、無効なシステムアドレスを参照しています。

-   一度に割り当てられたマップレジスタが多すぎるか、許可されている最大数より多くのマップレジスタが割り当てられています。

-   マップレジスタのダブルマッピング。

-   マップレジスタの一部がまだマップされている間、マップレジスタを解放しようとしています。

-   マップされていないマップレジスタをフラッシュしようとしています。

-   マップレジスタファイルの末尾にあるバイトをフラッシュしようとしています。

-   不適切な IRQL で DMA ルーチンを呼び出しています。

-   Null 値 DMA\_アダプターを HAL ルーチンに渡します。

-   アドレスが MDL に含まれていない場合に、アドレスと MDL を HAL ルーチンに渡す。

-   既にマップされているアドレス範囲をマップしようとしています。

-   マップされていないバッファーをフラッシュしようとしています。

-   転送用に長さ0のバッファーをマップしようとしています。

-   廃止された関数[**HalGetAdapter**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff546644(v=vs.85))を呼び出しています (すべてのドライバーは[**IoGetDmaAdapter**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iogetdmaadapter)を使用する必要があります)。

ドライバーの検証ツールは、ドライバーの動作を監視し、これらの違反が発生した場合にバグチェックの0xE6 を発行します。 バグチェックパラメーターの一覧については、「 [**Bug Check 0xE6**](https://docs.microsoft.com/windows-hardware/drivers/debugger/bug-check-0xe6--driver-verifier-dma-violation) (DRIVER\_VERIFIER\_DMA\_違反)」を参照してください。

### <a name="span-idwhen_is_dma_verification_useful_spanspan-idwhen_is_dma_verification_useful_spanwhen-is-dma-verification-useful"></a><span id="when_is_dma_verification_useful_"></span><span id="WHEN_IS_DMA_VERIFICATION_USEFUL_"></span>DMA の検証が役に立つのはどのような場合ですか?

(HAL DMA ルーチンを呼び出すことによって) DMA を直接使用するすべてのドライバーは、DMA 検証を使用してテストする必要があります。

また、ミニポートドライバーもテストする必要があります。これは、多くの場合、dma を使用するポートドライバーを呼び出すことによって DMA を間接的に使用するためです。

DMA 検証は、ドライバーまたはハードウェアデバイスが DMA バッファーをオーバーランするときに、メモリの破損を検出するための効果的な方法でもあります。

### <a name="span-idmonitoring_dma_verificationspanspan-idmonitoring_dma_verificationspanmonitoring-dma-verification"></a><span id="monitoring_dma_verification"></span><span id="MONITORING_DMA_VERIFICATION"></span>DMA 検証の監視

カーネルデバッガー拡張機能の**dma**は、大量の dma 情報を表示するために使用できます。 各 DMA アダプターの動作に関するさまざまな詳細情報を表示できます。 Windows 用デバッグツールのパッケージに関するドキュメントに、 **! dma**拡張機能の詳細な例と、デバッガー拡張機能に関する一般的な情報が記載されています。 詳細については、「 [Windows デバッグ](https://docs.microsoft.com/windows-hardware/drivers/debugger/index)」を参照してください。

### <a name="span-idactivating_this_optionspanspan-idactivating_this_optionspanactivating-this-option"></a><span id="activating_this_option"></span><span id="ACTIVATING_THIS_OPTION"></span>このオプションをアクティブにする

ドライバー検証ツールマネージャーまたは Verifier コマンドラインを使用して、1つまたは複数のドライバーの DMA 検証機能をアクティブ化できます。 詳細については、「[ドライバーの検証オプションの選択](selecting-driver-verifier-options.md)」を参照してください。

-   **コマンドラインで**

    コマンドラインでは、DMA 検証オプションは**ビット 7 (0x80)** で表されます。 DMA の検証をアクティブにするには、フラグ値0x80 を使用するか、または0x80 をフラグ値に追加します。 次に、例を示します。

    ```
    verifier /flags 0x80 /driver MyDriver.sys
    ```

    この機能は、次回の起動時にアクティブになります。

    Windows Vista 以降のバージョンの Windows では、 **/volatile**パラメーターをコマンドに追加することで、コンピューターを再起動せずに、DMA の検証をアクティブ化および非アクティブ化することもできます。 次に、例を示します。

    ```
    verifier /volatile /flags 0x80 /adddriver MyDriver.sys
    ```

    この設定は直ちに有効になりますが、コンピューターをシャットダウンまたは再起動すると失われます。 詳細については、「 [Volatile 設定の使用](using-volatile-settings.md)」を参照してください。

    DMA 検証機能は、標準設定にも含まれています。 次に、例を示します。

    ```
    verifier /standard /driver MyDriver.sys
    ```

-   **ドライバー検証マネージャーの使用**

    1.  ドライバー検証マネージャーを起動します。 コマンドプロンプトウィンドウで「 **Verifier** 」と入力します。
    2.  [**カスタム設定の作成] (コード開発者向け)** を選択し、 **[次へ]** をクリックします。
    3.  [**完全な一覧から個々の設定を選択]** を選択します。
    4.  **[DMA の確認]** を選択します。

    DMA 検証機能は、標準設定にも含まれています。 この機能を使用するには、ドライバー検証マネージャーで **[標準設定の作成]** をクリックします。

 

 





