---
title: DMA の検証
description: DMA の検証
ms.assetid: ffcb718a-63f5-49ff-9d36-67b2aa59761f
keywords:
- DMA の検証機能 WDK Driver Verifier
- HAL 検証 WDK Driver Verifier
- 一般的なバッファー DMA WDK Driver Verifier
- パケット DMA WDK Driver Verifier
- スキャッター/ギャザー DMA WDK Driver Verifier
- システム DMA WDK Driver Verifier
- ダイレクト メモリ アクセス WDK Driver Verifier
- DMA エラー WDK Driver Verifier
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8dc19e70147d3a8ece2a99ea6da041a01185b75c
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56549283"
---
# <a name="dma-verification"></a>DMA の検証


## <span id="ddk_dma_verification_tools"></span><span id="DDK_DMA_VERIFICATION_TOOLS"></span>


DMA の検証は、ダイレクト メモリ アクセス (DMA) の使用を監視します。 DMA ルーチンには Windows の開発が変更されているため多くのドライバーは DMA の呼び出しの不適切な使用を作成します。 さらに、いくつかのドライバー作成者が、HAL DMA サブシステムを完全にバイパスしようとします。 この実習では、ドライバーにバグを発見しにくいを導入できます。

Driver Verifier の DMA の検証オプションは、DMA の一般的なエラーをキャッチしようとします。 と共に、 **! dma**カーネル デバッガー拡張機能ドライバーが適切な方法で DMA を使用していることを確認するために使用できます。

このドライバーの検証オプションともいいます*HAL 検証*です。 ドライバーの検証ツールによって生成された一部のエラー メッセージは、この用語を使用できます。

このドライバーの検証ツールのオプションは、Windows XP で使用できる以降のみです。

### <a name="span-iddifferenttypesofdmaspanspan-iddifferenttypesofdmaspandifferent-types-of-dma"></a><span id="different_types_of_dma"></span><span id="DIFFERENT_TYPES_OF_DMA"></span>DMA のさまざまな種類

DMA は、ハードウェア デバイスは、プロセッサを使用せずにまたはメモリからデータを転送できるメカニズムです。 プロセッサは、転送を設定するために必要なし、転送が完了すると、デバイスで、プロセッサは通知します。 このシステムの利点は、DMA 転送が実行中に、プロセッサに他のタスクを実行できます。

Windows 2000 以降を使用する DMA のいくつかの種類があります。

<span id="Common-buffer_DMA"></span><span id="common-buffer_dma"></span><span id="COMMON-BUFFER_DMA"></span>*一般的なバッファーの DMA*  
一般的なバッファーの DMA では、システムがアクセスできる 1 つのバッファーを割り当てることができる場合、ハードウェアとソフトウェアの両方によって実行されます。 ドライバーは、バッファーへのアクセスを同期します。 メモリがキャッシュ ドライバーのこの同期を簡単に行うされません。 一般的なバッファーを設定した後、ドライバーとハードウェアの両方書き込めるしなくても、バッファー内のアドレスに直接 HAL から。

<span id="Packet_DMA"></span><span id="packet_dma"></span><span id="PACKET_DMA"></span>*DMA パケット*  
使用するため、ハードウェアによってマップされる 1 つの既存バッファーがある場合は、DMA パケットが実行されます。 DMA パケットを使用する例では、メモリからディスクへのファイルの転送です。 このような状況で一般的なバッファー DMA を使用して無駄になります、ため、ファイルが、ハードウェアを使用すると、ディスクに転送できます前に、共通のバッファーに転送する必要があります。 代わりに、HAL に問い合わせます。ハードウェアのメモリ内の実際のバッファーを見つけるために必要な情報、ドライバーを示します。 この操作は、さまざまなアーキテクチャの間で作業に関連するルーチンのですが、複雑になります。

<span id="Scatter_gather_DMA"></span><span id="scatter_gather_dma"></span><span id="SCATTER_GATHER_DMA"></span>*DMA のスキャッター/ギャザー*  
スキャッター/ギャザー DMA は、一度にいくつかの DMA パケット転送を設定するショートカット メソッドです。 ネットワーク経由でパケットを転送する場合など、ネットワーク スタックの各部分は独自のヘッダー (TCP、IP、イーサネット、およびなど) を追加します。 これらのヘッダーは、すべてメモリ内の異なる場所から割り当てられます。 この場合は、スキャッター/ギャザー DMA では、ハードウェアによって各 header、およびアクセスするための data セグメントにマップする HAL にバッチ要求を発行して時間を保存します。 パケットの各部分のパケット DMA ルーチンを呼び出すのではなくは、このメソッドは、各ルーチンを 1 回呼び出すし、HAL のそれぞれを個別にマッピングを担当することができます。

**注**  *スキャッター/ギャザー機能*デバイスがスキャッター/ギャザー ルーチンを使用できることはありません。 スキャッター/ギャザー機能は、デバイスの説明、デバイスが特定の範囲だけではなく、メモリ内の任意の領域から読み取り/書き込みできることを示すフラグを参照します。

 

<span id="System_DMA"></span><span id="system_dma"></span><span id="SYSTEM_DMA"></span>*DMA システム*  
システム DMA は、転送を直接実行するマザーボード上のシステム DMA コント ローラーをプログラミングによって実行されます。 ISA カードのみでは、システム DMA を使用できます。

### <a name="span-ideffectsofdmaverificationspanspan-ideffectsofdmaverificationspaneffects-of-dma-verification"></a><span id="effects_of_dma_verification"></span><span id="EFFECTS_OF_DMA_VERIFICATION"></span>DMA の検証の効果

DMA の検証がアクティブで、Driver Verifier は DMA ルーチンを含むコーポレーションを検出します。

-   オーバーランまたは underrunning DMA メモリ バッファー (これらのエラーは、ハードウェアまたはドライバーによって行うことできます)。

-   二重解放共通バッファー、アダプタのチャネル、マップの登録、または一覧のスキャッター/ギャザーします。

-   共通のバッファー、アダプタのチャネル、マップのレジスタ、スキャッター/ギャザー リスト、またはアダプターを解放していないによってメモリをリークが発生します。

-   1 つ以上のアダプター チャネル アダプターの存在を一度に 1 つがあります。

-   既に解放されてし、存在しないアダプターを使用しようとしています。

-   アダプターがバッファーをフラッシュしません。

-   アダプターの未解決の参照カウントが多すぎることです。

-   (すべてのバッファーには DMA の転送の開始前にロックする必要があります) ページング バッファーでは、DMA を実行します。

-   完全修飾フラグを使用する MDL で DMA を実行します。

-   無効なシステム アドレス、最初の MDL 前に、または後の最初の MDL 最後を参照しているまたは MDL バッファーよりも長いし、MDL 内のページ境界を越える転送の長さを使用します。

-   同時に、多くのマップのレジスタの割り当てまたは割り当てが許可されている最大数よりも多くのマップ レジスタ。

-   マップの double 型のマッピングを登録します。

-   いくつかまだマップされているときに、マップのレジスタを解放しようとしています。

-   マップされていない map レジスタをフラッシュしようとしています。

-   マップの登録ファイルの末尾が多すぎるのバイトをフラッシュしようとしています。

-   不適切な IRQL で DMA ルーチンを呼び出しています。

-   Null 値 DMA を渡す\_HAL のルーチンへのアダプター。

-   MDL でアドレスが含まれていない場合、アドレスと、MDL を HAL ルーチンに渡します。

-   既にマップされて、アドレス範囲をマップしようとしています。

-   マップされていないバッファーをフラッシュしようとしています。

-   転送するため、長さ 0 のバッファーをマップしようとしています。

-   古い形式の関数を呼び出す[ **HalGetAdapter** ](https://msdn.microsoft.com/library/windows/hardware/ff546596) (すべてのドライバーを使用する必要があります[ **IoGetDmaAdapter** ](https://msdn.microsoft.com/library/windows/hardware/ff549220)代わりに)。

Driver Verifier は、ドライバーの動作を監視し、これらの違反が発生した場合、バグ チェック 0xE6 を発行します。 参照してください[**バグ チェック 0xE6** ](https://msdn.microsoft.com/library/windows/hardware/ff560341) (ドライバー\_VERIFIER\_DMA\_違反)、バグの一覧については、パラメーターを確認します。

### <a name="span-idwhenisdmaverificationusefulspanspan-idwhenisdmaverificationusefulspanwhen-is-dma-verification-useful"></a><span id="when_is_dma_verification_useful_"></span><span id="WHEN_IS_DMA_VERIFICATION_USEFUL_"></span>DMA の検証の便利なはいつか

DMA の検証では、直接 (を呼び出して、HAL DMA ルーチン) DMA を使用するすべてのドライバーをテストする必要があります。

さらに、ミニポート ドライバーもテストしてください、DMA を直接 (を呼び出して DMA を使用するポート ドライバー) 多くの場合、使用するため。

DMA の検証には、効果的な方法が見つけると、いずれかのドライバー、またはハードウェア デバイス DMA バッファー オーバーランのメモリの破損を検出することもできます。

### <a name="span-idmonitoringdmaverificationspanspan-idmonitoringdmaverificationspanmonitoring-dma-verification"></a><span id="monitoring_dma_verification"></span><span id="MONITORING_DMA_VERIFICATION"></span>DMA の検証の監視

カーネル デバッガー拡張機能 **! dma**豊富な DMA の情報を表示するために使用できます。 各 DMA アダプターの動作に関するさまざまな詳細を表示できます。 詳細な例は、 **! dma**拡張機能とツールを Windows のデバッグ パッケージ内のドキュメントで、デバッガーの拡張機能に関する一般的な情報。 参照してください[Windows デバッグ](https://msdn.microsoft.com/library/windows/hardware/ff551063)詳細についてはします。

### <a name="span-idactivatingthisoptionspanspan-idactivatingthisoptionspanactivating-this-option"></a><span id="activating_this_option"></span><span id="ACTIVATING_THIS_OPTION"></span>このオプションをアクティブ化します。

ドライバー検証マネージャーまたは Verifier.exe コマンドラインを使用して、1 つまたは複数のドライバーの DMA の検証機能をアクティブにできます。 詳細については、次を参照してください。[ドライバー検証ツールのオプションの選択](selecting-driver-verifier-options.md)します。

-   **コマンドラインで**

    、コマンドラインでは、DMA の検証オプションで表される**ビット 7 (0x80)** します。 DMA の検証を有効にするには、0x80 のフラグの値を使用して、または 0x80 をフラグ値に追加します。 次に、例を示します。

    ```
    verifier /flags 0x80 /driver MyDriver.sys
    ```

    この機能は、[次へ] の起動後にアクティブになります。

    Windows Vista と Windows の以降のバージョンでもアクティブ化し、DMA の検証を追加することで、コンピューターを再起動しなくても非アクティブ化することができます、 **/volatile**パラメーターをコマンド。 次に、例を示します。

    ```
    verifier /volatile /flags 0x80 /adddriver MyDriver.sys
    ```

    この設定は、すぐに有効は、シャット ダウンするか、コンピューターを再起動すると失われます。 詳細については、次を参照してください。[揮発性の設定を使用する](using-volatile-settings.md)します。

    DMA の検証機能は、標準の設定にも含まれます。 次に、例を示します。

    ```
    verifier /standard /driver MyDriver.sys
    ```

-   **ドライバー検証マネージャーを使用します。**

    1.  ドライバー検証マネージャーを起動します。 型**Verifier**コマンド プロンプト ウィンドウでします。
    2.  選択 **(コード開発者) 用のカスタム設定を作成する**順にクリックします**次**します。
    3.  選択**完全な一覧から個々 の設定を選択します。** します。
    4.  選択 (チェック) **DMA の検証**です。

    DMA の検証機能は、標準の設定にも含まれます。 この機能では、ドライバー検証マネージャーでを使用する をクリックして**標準設定の作成**です。

 

 





