---
title: オーディオ処理オブジェクトの実装
description: このトピックでは、オーディオ処理オブジェクト (APO) を実装する方法について説明します。 APOs に関する一般的な情報については、「オーディオ処理オブジェクトのアーキテクチャ」を参照してください。
ms.assetid: 822FAF10-DAB3-48D1-B782-0C80B072D3FB
ms.date: 03/26/2020
ms.localizationpriority: medium
ms.openlocfilehash: c153272cefea02a61ed411feb3e70c6a44b794c7
ms.sourcegitcommit: c81abcddfd3e819ee105db5adc7937dda96b7fb4
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/27/2020
ms.locfileid: "80359897"
---
# <a name="implementing-audio-processing-objects"></a>オーディオ処理オブジェクトの実装

このトピックでは、オーディオ処理オブジェクト (APO) を実装する方法について説明します。 APOs に関する一般的な情報については、「[オーディオ処理オブジェクトのアーキテクチャ](audio-processing-object-architecture.md)」を参照してください。

## <a name="span-idimplementing_custom_aposspanspan-idimplementing_custom_aposspanspan-idimplementing_custom_aposspanimplementing-custom-apos"></a><span id="Implementing_Custom_APOs"></span><span id="implementing_custom_apos"></span><span id="IMPLEMENTING_CUSTOM_APOS"></span>カスタム APOs を実装する

カスタム APOs はインプロセス COM オブジェクトとして実装されているため、ユーザーモードで実行し、ダイナミックリンクライブラリ (DLL) にパッケージ化します。 "APO" は、信号処理グラフに挿入される場所に基づいて3種類あります。

- ストリーム効果 (SFX)
- モードの効果 (MFX)
- エンドポイント効果 (EFX)

各論理デバイスは、種類ごとに1つの APO に関連付けることができます。 モードと効果の詳細については、「[オーディオ信号処理モード](audio-signal-processing-modes.md)」を参照してください。

APO を実装するには、カスタムクラスの基本クラスを使用します。これは、Baseaudioprocessingobject .h ファイルで宣言されています。 この方法では、CBaseAudioProcessingObject 基本クラスに新しい機能を追加して、カスタマイズされた APO を作成します。 CBaseAudioProcessingObject 基底クラスは、APO が必要とする機能の多くを実装します。 これは、3つの必須インターフェイスのほとんどのメソッドに既定の実装を提供します。 主な例外は、 [**Iaudioprocessingの Trt:: アポストロフィ process**](https://docs.microsoft.com/windows/desktop/api/audioenginebaseapo/nf-audioenginebaseapo-iaudioprocessingobjectrt-apoprocess)メソッドです。

カスタム APOs を実装するには、次の手順を実行します。

1. 必要なオーディオ処理を提供するカスタムの APO com オブジェクトを作成します。
2. 必要に応じて、を使用してカスタム APOs を構成するためのユーザーインターフェイスを作成します。
3. APOs およびカスタムユーザーインターフェイスをインストールして登録するための INF ファイルを作成します。

## <a name="span-iddesign_considerations_for_custom_apo_developmentspanspan-iddesign_considerations_for_custom_apo_developmentspanspan-iddesign_considerations_for_custom_apo_developmentspandesign-considerations-for-custom-apo-development"></a><span id="Design_Considerations_for_Custom_APO_Development"></span><span id="design_considerations_for_custom_apo_development"></span><span id="DESIGN_CONSIDERATIONS_FOR_CUSTOM_APO_DEVELOPMENT"></span>カスタム APO 開発の設計に関する考慮事項

すべてのカスタム APOs には、次の一般的な特性が必要です。

- APO には、1つの入力と1つの出力接続が必要です。 これらの接続はオーディオバッファーであり、複数のチャネルを持つことができます。
- APO は、 [**Iaudioprocessingの Trt:: アポストロフィプロセス**](https://docs.microsoft.com/windows/desktop/api/audioenginebaseapo/nf-audioenginebaseapo-iaudioprocessingobjectrt-apoprocess)ルーチンを通じて渡されるオーディオデータのみを変更できます。 APO は、基になる論理デバイス (KS トポロジを含む) の設定を変更できません。
- IUnknown に加えて、APOs は次のインターフェイスを公開する必要があります。

    - [Iaudioprocessingobject](https://docs.microsoft.com/windows/desktop/api/audioenginebaseapo/nn-audioenginebaseapo-iaudioprocessingobject)。 初期化や形式ネゴシエーションなどのセットアップタスクを処理するインターフェイス。

    - [Iaudioprocessingobjectconfiguration](https://docs.microsoft.com/windows/desktop/api/audioenginebaseapo/nn-audioenginebaseapo-iaudioprocessingobjectconfiguration)。 構成インターフェイス。

    - [Iaudioprocessingの Trt](https://docs.microsoft.com/windows/desktop/api/audioenginebaseapo/nn-audioenginebaseapo-iaudioprocessingobjectrt)。 オーディオ処理を処理するリアルタイムインターフェイス。 これは、リアルタイム処理スレッドから呼び出すことができます。

    - [Iaudiosystemeffects](https://docs.microsoft.com/windows/desktop/api/audioenginebaseapo/nn-audioenginebaseapo-iaudiosystemeffects)。 オーディオエンジンが DLL をシステムとして認識するインターフェイスは、"APO" になります。

- すべての APOs には、リアルタイムのシステム互換性が必要です。 これは次のことを意味します。

  - リアルタイムインターフェイスのメンバーであるすべてのメソッドは、非ブロッキングメンバーとして実装する必要があります。 ブロックしたり、ページングされたメモリを使用したり、ブロックしているシステムルーチンを呼び出したりすることはできません。

  - APO によって処理されるすべてのバッファーは、非ページングである必要があります。 プロセスパス内のすべてのコードとデータは、非ページングである必要があります。

  - APOs は、オーディオ処理チェーンに大きな待機時間を導入しないでください。

- カスタム APOs は IAudioProcessingObjectVBR インターフェイスを公開できません。

**注**  必要なインターフェイスの詳細については、Windows キット\\&lt;ビルド番号&gt;\\um フォルダーを含める」を参照してください。\\

## <a name="span-idusing_sample_code_to_accelerate_the_development_processspanspan-idusing_sample_code_to_accelerate_the_development_processspanspan-idusing_sample_code_to_accelerate_the_development_processspanusing-sample-code-to-accelerate-the-development-process"></a><span id="Using_Sample_Code_to_Accelerate_the_Development_Process"></span><span id="using_sample_code_to_accelerate_the_development_process"></span><span id="USING_SAMPLE_CODE_TO_ACCELERATE_THE_DEVELOPMENT_PROCESS"></span>サンプルコードを使用して開発プロセスを高速化する

SYSVAD Swap APO コードサンプルをテンプレートとして使用すると、カスタムの APO 開発プロセスを高速化できます。 Swap サンプルは、オーディオ処理オブジェクトの一部の機能を示すために開発されたサンプルです。 Swap APO サンプルでは、左チャネルと右チャネルを交換し、SFX 効果と MFX 効果の両方を実装します。 チャネルスワップのオーディオ効果を有効または無効にするには、[プロパティ] ダイアログを使用します。

SYSVAD audio サンプルは、 [Windows Driver Samples GitHub](https://github.com/Microsoft/Windows-driver-samples)で入手できます。

Sysvad audio サンプルは次の場所で参照できます。

<https://github.com/Microsoft/Windows-driver-samples/tree/master/audio/sysvad>

**GitHub から Sysvad audio サンプルをダウンロードして抽出する**

SYSVAD サンプルをダウンロードして開くには、次の手順に従います。

a. GitHub ツールを使用して、サンプルを操作できます。 また、ユニバーサルドライバーのサンプルを1つの zip ファイルにダウンロードすることもできます。

<https://github.com/Microsoft/Windows-driver-samples/archive/master.zip>

b. マスター .zip ファイルをローカルハードドライブにダウンロードします。

c. *Windows-driver-samples-master*を右クリックし、 **[すべて展開]** を選択します。 新しいフォルダーを指定するか、抽出されたファイルを格納する既存のフォルダーを参照します。 たとえば、 *C:\\DriverSamples\\* を、ファイルを抽出する新しいフォルダーとして指定できます。

d. ファイルが抽出されたら、次のサブフォルダーに移動します。

*C:\\DriverSamples\\Audio\\Sysvad*

**Visual Studio でドライバーソリューションを開く**

Microsoft Visual Studio で、[&gt;**ファイル**] をクリックして &gt;**プロジェクト/ソリューション...** を**開き**、抽出したファイルが格納されているフォルダー (たとえば、 *C:\\driversamples\\Audio\\Sysvad*) に移動します。 *Sysvad*ソリューションファイルをダブルクリックして開きます。

Visual Studio で、ソリューションエクスプローラーを見つけます。 (まだ開いていない場合は、 **[表示]** メニューの **[ソリューションエクスプローラー]** をクリックします)。ソリューションエクスプローラーには、6つのプロジェクトを持つソリューションが1つ表示されます。

**SwapAPO のコード例**

SYSVAD サンプルには5つのプロジェクトがあります。そのうちの1つは、APO 開発者にとって最も重要なものです。

|                    |                                       |
|--------------------|---------------------------------------|
| **作品**        | **説明**                       |
| SwapAPO            | APO の例のサンプルコードです。       |

Sysvad サンプル内の他のプロジェクトは、以下にまとめられています。

|                        |                                            |
|------------------------|--------------------------------------------|
| **作品**            | **説明**                            |
| 電話のオーディオサンプル       | モバイルオーディオドライバーのサンプルコードです。     |
| TabletAudioSample      | 代替オーディオドライバーのサンプルコードです。 |
| KeywordDetectorAdapter | キーワード検出アダプターのサンプルコード |
| EndpointsCommon        | 一般的なエンドポイントのサンプルコードです。          |

SwapAPO サンプルのプライマリヘッダーファイルは、swapapo. h です。 その他の主要なコード要素を以下にまとめます。

|                      |                                                                   |
|----------------------|-------------------------------------------------------------------|
| **ファイル**             | **説明**                                                   |
| .Cpp の入れ替え             | C++スワップ APO の実装を含むコード。        |
| SwapAPOMFX .cpp       | CSwapAPOMFX の実装                                     |
| SwapAPOSFX .cpp       | CSwapAPOSFX の実装                                     |
| Swapアポストロフィ       | DLL のエクスポートの実装。                                    |
| Swapアポストロフィ       | DLL の COM インターフェイスおよびコクラスの定義。           |
| Swapアポストロフィ | スワップ APO 機能のインターフェイスと型の定義。    |
| swapアポストロフィ (def)       | COM エクスポートの定義                                           |

## <a name="span-idimplementing_the_com_object_audio_processing_codespanspan-idimplementing_the_com_object_audio_processing_codespanspan-idimplementing_the_com_object_audio_processing_codespanimplementing-the-com-object-audio-processing-code"></a><span id="Implementing_the_COM_Object_Audio_Processing_Code"></span><span id="implementing_the_com_object_audio_processing_code"></span><span id="IMPLEMENTING_THE_COM_OBJECT_AUDIO_PROCESSING_CODE"></span>COM オブジェクトのオーディオ処理コードの実装

システムによって提供される APO をラップするには、カスタムクラスを**cbaseaudioprocessingobject**基本クラスに基づいて指定します。これは、baseaudioprocessingobject .h ファイルで宣言されています。 この方法では、 **Cbaseaudioprocessingobject**基底クラスに新しい機能を導入し、カスタマイズされた APO を作成します。 **Cbaseaudioprocessingobject**基底クラスは、APO が必要とする機能の多くを実装します。 これは、3つの必須インターフェイスのほとんどのメソッドに既定の実装を提供します。 主な例外は、 [**Iaudioprocessingの Trt:: アポストロフィ process**](https://docs.microsoft.com/windows/desktop/api/audioenginebaseapo/nf-audioenginebaseapo-iaudioprocessingobjectrt-apoprocess)メソッドです。

**Cbaseaudioprocessingobject**を使用すると、APO をより簡単に実装できます。 APO に特別な形式の要件がなく、必要な float32 形式で動作する場合、 **Cbaseaudioprocessingobject**に含まれるインターフェイスメソッドの既定の実装で十分である必要があります。 既定の実装では、 [**Iaudioprocessingobject:: IsInputFormatSupported**](https://docs.microsoft.com/windows/desktop/api/audioenginebaseapo/nf-audioenginebaseapo-iaudioprocessingobject-isinputformatsupported)、 [**iaudioprocessingobject Trt:: アポストロフィ Process**](https://docs.microsoft.com/windows/desktop/api/audioenginebaseapo/nf-audioenginebaseapo-iaudioprocessingobjectrt-apoprocess)、および**validateandcacheconnectioninfo**という3つの主要なメソッドのみを実装する必要があります。

**Cbaseaudioprocessingobject**クラスに基づいて APOs を開発するには、次の手順を実行します。

1. **Cbaseaudioprocessingobject**から継承するクラスを作成します。

    次C++のコード例は、 **Cbaseaudioprocessingobject**から継承するクラスを作成する方法を示しています。 この概念の実際の実装については、「**オーディオ処理オブジェクトドライバーのサンプル**」の手順に従ってスワップのサンプルにアクセスし、次に*swapapo .h*ファイルを参照してください。

    ```cpp
    // Custom APO class - LFX
    Class MyCustomAPOLFX: public CBaseAudioProcessingObject
    {
     public:
    //Code for custom class goes here
    ...
    };
    ```

    **注**   SFX APO によって実行されるシグナル処理は、mfx または EFX APO によって実行される信号処理とは異なるため、それぞれに個別のクラスを作成する必要があります。

2. 次の3つのメソッドを実装します。

    - [**Iaudioprocessingobject:: IsInputFormatSupported**](https://docs.microsoft.com/windows/desktop/api/audioenginebaseapo/nf-audioenginebaseapo-iaudioprocessingobject-isinputformatsupported)。 このメソッドは、オーディオエンジンを使用した形式ネゴシエーションを処理します。

    - [**Iaudioprocessingの Trt:: アポストロフィプロセス**](https://docs.microsoft.com/windows/desktop/api/audioenginebaseapo/nf-audioenginebaseapo-iaudioprocessingobjectrt-apoprocess)。 このメソッドは、カスタムアルゴリズムを使用してシグナル処理を実行します。

    - **Validateandcacheconnectioninfo**。 このメソッドは、チャネル数、サンプリングレート、サンプルの深さ、チャネルマスクなどの形式の詳細を格納するためにメモリを割り当てます。

次C++のコード例は、手順 1. で作成したサンプルクラスの[**アポストロフィ process**](https://docs.microsoft.com/windows/desktop/api/audioenginebaseapo/nf-audioenginebaseapo-iaudioprocessingobjectrt-apoprocess)メソッドの実装を示しています。 この概念の実際の実装については、「 **Audio Processing Objects Driver sample** 」セクションの手順に従ってスワップサンプルにアクセスし、 *Swapapolfx*ファイルを参照してください。

```cpp
// Custom implementation of APOProcess method
STDMETHODIMP_ (Void) MyCustomAPOLFX::APOProcess (...)
{
// Code for method goes here. This code is the algorithm that actually
// processes the digital audio signal.
...
}
```

次のコード例は、 **Validateandcacheconnectioninfo**メソッドの実装を示しています。 このメソッドの実際の実装については、「**オーディオ処理オブジェクトドライバーのサンプル**」の手順に従ってスワップのサンプルにアクセスし、次に*swapアポストロフィ*ファイルを参照してください。

```cpp
// Custom implementation of the ValidateAndCacheConnectionInfo method.
HRESULT CSwapAPOGFX::ValidateAndCacheConnectionInfo( ... )
{
// Code for method goes here.
// The code should validate the input/output format pair.
...
}
```

クラスが**Cbaseaudioprocessingobject**から継承する残りのインターフェイスとメソッドについては、Audioenginebaseapo ファイルで詳しく説明されています **。  **

デスクトップ Pc の場合は、カスタム APO に追加した機能を構成するためのユーザーインターフェイスを提供できます。 詳細については、「 [APOs を構成するための UI の実装](implementing-a-ui-for-configuring-sapos.md)」を参照してください。

## <a name="span-idreplacing_system-supplied_aposspanspan-idreplacing_system-supplied_aposspanspan-idreplacing_system-supplied_aposspanreplacing-system-supplied-apos"></a><span id="Replacing_System-supplied_APOs"></span><span id="replacing_system-supplied_apos"></span><span id="REPLACING_SYSTEM-SUPPLIED_APOS"></span>システム指定の APOs を置き換える

APO インターフェイスを実装する場合、2つの方法があります。独自の実装を記述することも、受信トレイ APOs を呼び出すこともできます。

この擬似コードは、システム APO をラップする方法を示しています。

```cpp
CMyWrapperAPO::CMyWrapperAPO {
    CoCreateInstance(CLSID_InboxAPO, m_inbox);
}

CMyWrapperAPO::IsInputFormatSupported {
    Return m_inbox->IsInputFormatSupported(…);
}
```

この擬似コードは、独自のカスタム APO を作成する方法を示しています。

```cpp
CMyFromScratchAPO::IsInputFormatSupported {
    my custom logic
}
```

システムによって提供されるものを置き換えるために APOs を開発する場合は、インターフェイスとメソッドについて、次の一覧の同じ名前を使用する必要があります。 いくつかのインターフェイスには、必要なメソッドに加えて、さらに多くのメソッドがあります。 これらのインターフェイスの参照ページを参照して、すべてのメソッドを実装するか、必要なメソッドのみを実装するかを決定します。

実装手順の残りの部分は、カスタム APO と同じです。

COM コンポーネントに対して、次のインターフェイスとメソッドを実装します。

- [Iaudioprocessingobject](https://docs.microsoft.com/windows/desktop/api/audioenginebaseapo/nn-audioenginebaseapo-iaudioprocessingobject)。 このインターフェイスに必要なメソッドは、 [**Initialize**](https://docs.microsoft.com/windows/desktop/api/audioenginebaseapo/nf-audioenginebaseapo-iaudioprocessingobject-initialize)と[**IsInputFormatSupported です。** ](https://docs.microsoft.com/windows/desktop/api/audioenginebaseapo/nf-audioenginebaseapo-iaudioprocessingobject-isinputformatsupported)
- [Iaudioprocessingobjectconfiguration](https://docs.microsoft.com/windows/desktop/api/audioenginebaseapo/nn-audioenginebaseapo-iaudioprocessingobjectconfiguration)。 このインターフェイスに必要なメソッドは、 [**Lockforprocess**](https://docs.microsoft.com/windows/desktop/api/audioenginebaseapo/nf-audioenginebaseapo-iaudioprocessingobjectconfiguration-lockforprocess)と[**UnlockForProcess**](https://docs.microsoft.com/windows/desktop/api/audioenginebaseapo/nf-audioenginebaseapo-iaudioprocessingobjectconfiguration-unlockforprocess)です。
- [Iaudioprocessingの Trt](https://docs.microsoft.com/windows/desktop/api/audioenginebaseapo/nn-audioenginebaseapo-iaudioprocessingobjectrt)。 このインターフェイスに必要なメソッドは、"[**アポストロフィ**](https://docs.microsoft.com/windows/desktop/api/audioenginebaseapo/nf-audioenginebaseapo-iaudioprocessingobjectrt-apoprocess)" であり、DSP アルゴリズムを実装するメソッドです。
- [Iaudiosystemeffects](https://docs.microsoft.com/windows/desktop/api/audioenginebaseapo/nn-audioenginebaseapo-iaudiosystemeffects)。 このインターフェイスにより、オーディオエンジンは DLL を APO と認識します。

## <a name="span-idworking_with_visual_studio_and_aposspanspan-idworking_with_visual_studio_and_aposspanspan-idworking_with_visual_studio_and_aposspanworking-with-visual-studio-and-apos"></a><span id="Working_with_Visual_Studio_and_APOs"></span><span id="working_with_visual_studio_and_apos"></span><span id="WORKING_WITH_VISUAL_STUDIO_AND_APOS"></span>Visual Studio と APOs の使用

Visual Studio で APOs を使用する場合は、各 APO プロジェクトに対してこれらのタスクを実行します。

### <a name="link-to-the-crt"></a>CRT へのリンク

Windows 10 を対象とするドライバーは、ユニバーサル CRT に動的にリンクする必要があります。

Windows 8、1をサポートする必要がある場合は、プロジェクトのプロパティを C/C++、コード生成で設定して、静的リンクを有効にします。 リリースビルドの場合は "Runtime Library" を */mt*に、デバッグビルドの場合は */MTd*に設定します。 この変更が加えられました。ドライバーの場合、MSVCRT.DLL&lt;n&gt;バイナリに再配布するのは困難です。 この解決策は、libcmt.lib を静的にリンクすることです。 詳細については[、「/md、/mt、/ld (ランタイムライブラリの使用)](https://docs.microsoft.com/cpp/build/reference/md-mt-ld-use-run-time-library) 」を参照してください。

### <a name="disable-use-of-an-embedded-manifest"></a>埋め込みマニフェストの使用を無効にする

APO プロジェクトのプロジェクトプロパティを設定して、埋め込みマニフェストの使用を無効にします。 **[マニフェストツール]** 、 **[入力および出力]** を選択します。 次に、[埋め込みマニフェスト] を既定の *[はい]* から [*いいえ*] に変更します。 埋め込みマニフェストがある場合は、保護された環境内で禁止されている特定の Api の使用がトリガーされます。 つまり、APO は DisableProtectedAudioDG = 1 で実行されますが、このテストキーが削除されると、WHQL に署名されている場合でも、APO の読み込みに失敗します。

## <a name="span-idpackaging_your_apo_with_a_driverspanspan-idpackaging_your_apo_with_a_driverspanspan-idpackaging_your_apo_with_a_driverspanpackaging-your-apo-with-a-driver"></a><span id="Packaging_your_APO_with_a_Driver"></span><span id="packaging_your_apo_with_a_driver"></span><span id="PACKAGING_YOUR_APO_WITH_A_DRIVER"></span>ドライバーを使用して APO をパッケージ化する

独自のオーディオドライバーを開発し、システムによって提供される APOs をラップまたは交換するときは、ドライバーと APOs をインストールするためのドライバーパッケージを用意する必要があります。 Windows 10 については、「[オーディオ用ユニバーサル Windows ドライバー](audio-universal-drivers.md)」を参照してください。 オーディオ関連のドライバーパッケージは、そこで詳細に説明されているポリシーとパッケージングモデルに従う必要があります。  

カスタム APO は DLL としてパッケージ化され、すべての構成 UI は個別の UWP またはデスクトップブリッジアプリとしてパッケージ化されます。 APO デバイス INF は、関連付けられている INF CopyFile ディレクティブに示されているシステムフォルダーに Dll をコピーします。 APOs を含む DLL は、AddReg セクションを INF ファイルに含めることによって、それ自体を登録する必要があります。

次の段落および INF ファイルフラグメントは、標準の INF ファイルを使用して APOs をコピーおよび登録するために必要な変更を示しています。

Sysvad サンプルに含まれている inf ファイルは、SwapApo .dll APOs の登録方法を示しています。

## <a name="span-id_registering_apos_for_processing_modes_and_effects_in_the_inf_filespanspan-id_registering_apos_for_processing_modes_and_effects_in_the_inf_filespanspan-id_registering_apos_for_processing_modes_and_effects_in_the_inf_filespan-registering-apos-for-processing-modes-and-effects-in-the-inf-file"></a><span id="_Registering_APOs_for_Processing_Modes_and_Effects_in_the_INF_File"></span><span id="_registering_apos_for_processing_modes_and_effects_in_the_inf_file"></span><span id="_REGISTERING_APOS_FOR_PROCESSING_MODES_AND_EFFECTS_IN_THE_INF_FILE"></span>ファイルの処理モードと効果を INF ファイルに登録しています

レジストリキーの許可されている組み合わせを使用して、特定のモードの APOs を登録できます。 使用できる効果と APOs に関する一般的な情報の詳細については、「[オーディオ処理オブジェクトのアーキテクチャ](audio-processing-object-architecture.md)」を参照してください。

各 APO INF ファイル設定の詳細については、次のリファレンストピックを参照してください。

[PKEY\_FX\_StreamEffectClsid](https://docs.microsoft.com/windows-hardware/drivers/audio/pkey-fx-streameffectclsid)

[PKEY\_FX\_ModeEffectClsid](https://docs.microsoft.com/windows-hardware/drivers/audio/pkey-fx-modeeffectclsid)

[PKEY\_FX\_EndpointEffectClsid](https://docs.microsoft.com/windows-hardware/drivers/audio/pkey-fx-endpointeffectclsid)

[PKEY\_SFX\_ProcessingModes\_\_Streaming でサポートされている\_](https://docs.microsoft.com/windows-hardware/drivers/audio/pkey-sfx-processingmodes-supported-for-streaming)

[PKEY\_MFX\_ProcessingModes\_\_Streaming でサポートされている\_](https://docs.microsoft.com/windows-hardware/drivers/audio/pkey-mfx-processingmodes-supported-for-streaming)

[PKEY\_EFX\_ProcessingModes\_\_Streaming でサポートされている\_](https://docs.microsoft.com/windows-hardware/drivers/audio/pkey-efx-processingmodes-supported-for-streaming)

次の INF ファイルのサンプルは、特定のモードのオーディオ処理オブジェクト (APOs) を登録する方法を示しています。 これらの例では、この一覧から使用可能な組み合わせを示します。

- PKEY\_FX\_StreamEffectClsid と PKEY\_SFX\_ProcessingModes\_\_Streaming でサポートされて\_
- PKEY\_FX\_ModeEffectClsid と PKEY\_MFX\_ProcessingModes\_\_Streaming の\_
- PKEY\_FX\_PKEY\_MFX\_ProcessingModes\_\_Streaming の\_
- PKEY\_FX\_EndpointEffectClsid を使用しない PKEY\_EFX\_ProcessingModes\_\_Streaming でサポートされている\_

これらのサンプルでは、有効な組み合わせが1つ追加されています。

- PKEY\_FX\_EndpointEffectClsid と PKEY\_EFX\_ProcessingModes\_\_Streaming でサポートされて\_

### <a name="sysvad-tablet-multi-mode-streaming-effect-apo-inf-sample"></a>SYSVAD タブレットマルチモードストリーミング効果 APO INF サンプル

このサンプルでは、SYSVAD タブレット INF ファイルの AddReg エントリを使用して登録されているマルチモードのストリーミング効果を示します。

このサンプルコードは、SYSVAD audio サンプルから入手でき、GitHub: <https://github.com/Microsoft/Windows-driver-samples/tree/master/audio/sysvad>にあります。

このサンプルでは、次のシステム効果の組み合わせを示します。

- PKEY\_FX\_StreamEffectClsid と PKEY\_SFX\_ProcessingModes\_\_Streaming でサポートされて\_
- PKEY\_FX\_ModeEffectClsid と PKEY\_MFX\_ProcessingModes\_\_Streaming の\_

```inf
[SWAPAPO.I.Association0.AddReg]
; Instruct audio endpoint builder to set CLSID for property page provider into the
; endpoint property store
HKR,EP\0,%PKEY_AudioEndpoint_ControlPanelPageProvider%,,%AUDIOENDPOINT_EXT_UI_CLSID%

; Instruct audio endpoint builder to set the CLSIDs for stream, mode, and endpoint APOs
; into the effects property store
HKR,FX\0,%PKEY_FX_StreamEffectClsid%,,%FX_STREAM_CLSID%
HKR,FX\0,%PKEY_FX_ModeEffectClsid%,,%FX_MODE_CLSID%
HKR,FX\0,%PKEY_FX_UserInterfaceClsid%,,%FX_UI_CLSID%

; Driver developer would replace the list of supported processing modes here
; Concatenate GUIDs for DEFAULT, MEDIA, MOVIE
HKR,FX\0,%PKEY_SFX_ProcessingModes_Supported_For_Streaming%,%REG_MULTI_SZ%,%AUDIO_SIGNALPROCESSINGMODE_DEFAULT%,%AUDIO_SIGNALPROCESSINGMODE_MEDIA%,%AUDIO_SIGNALPROCESSINGMODE_MOVIE%

; Concatenate GUIDs for DEFAULT, MEDIA, MOVIE
HKR,FX\0,%PKEY_MFX_ProcessingModes_Supported_For_Streaming%,%REG_MULTI_SZ%,%AUDIO_SIGNALPROCESSINGMODE_DEFAULT%,%AUDIO_SIGNALPROCESSINGMODE_MEDIA%,%AUDIO_SIGNALPROCESSINGMODE_MOVIE%

;HKR,FX\0,%PKEY_EFX_ProcessingModes_Supported_For_Streaming%,0x00010000,%AUDIO_SIGNALPROCESSINGMODE_DEFAULT%
```

サンプルの INF ファイルでは、"EFX\_Streaming" プロパティがコメントアウトされています。これは、オーディオ処理がそのレイヤー上のカーネルモードに遷移したためです。ストリーミングプロパティは必要なく、使用されません。 検出を目的として PKEY\_FX\_EndpointEffectClsid を指定することは有効ですが、\_ストリーミングでサポートされている\_\_PKEY\_EFX\_ProcessingModes を指定するとエラーになります。 これは、モードミックス/t がスタックの下位に発生し、エンドポイント APO を挿入できないためです。

### <a name="componentized-apo-installation"></a>コンポーネント APO のインストール

Windows 10 以降のリリース1809では、オーディオエンジンによる APO 登録で、コンポーネント化されたオーディオドライバーモデルが使用されています。 Audio コンポーネント化を使用すると、より滑らかで信頼性の高いインストールエクスペリエンスが実現し、コンポーネントサービスのサポートが強化されます。 詳細については、「[コンポーネント化オーディオドライバーのインストールの作成](https://docs.microsoft.com/windows-hardware/drivers/audio/audio-universal-drivers#creating-a-componentized-audio-driver-installation)」を参照してください。

次のコード例は、パブリック ComponentizedAudioSampleExtension と ComponentizedApoSample から抽出されます。 <https://github.com/Microsoft/Windows-driver-samples/tree/master/audio/sysvad>については、GitHub で入手できる SYSVAD audio サンプルを参照してください。
 
オーディオエンジンへの APO の登録は、新しく作成された APO デバイスを使用して行われます。 オーディオエンジンで新しい APO デバイスを使用するには、オーディオデバイスの PNP 子 (オーディオエンドポイントの兄弟) である必要があります。 新しいコンポーネントの APO 設計では、APO がグローバルに登録され、複数の異なるドライバーによって使用されることは許可されていません。 各ドライバーは独自の APO のを登録する必要があります。

APO のインストールは、2つの部分で行われます。 まず、ドライバー拡張機能の INF は、次のように、システムに APO デバイスを追加します。
 
```inf
[DeviceExtension_Install.Devices]
AddDevice = SwapApo,,Apo_AddDevice
 
[Apo_AddDevice]
HardwareIds = APO\VEN_SMPL&CID_APO
Description = "Audio Proxy APO Sample"
Capabilities = 0x00000008 ; SWDeviceCapabilitiesDriverRequired
```

この APO デバイスは、SYSVAD サンプルの2番目の部分である APO INF をトリガーします。これは ComponentizedApoSample で行われます。 この INF ファイルは、APO デバイス専用です。 これは、デバイスクラスを AudioProcessingObject として指定し、CLSID 登録のすべての APO プロパティを追加し、オーディオエンジンに登録します。

>[!NOTE]
> INF ファイルのサンプルでは、ほとんどの場合、HKR レジストリキーを使用して、状態の分離をサポートしています。 前のサンプルでは、HKCR を使用して永続的な値を格納していました。 例外は、コンポーネントオブジェクトモデル (COM) オブジェクトの登録です。キーは HKCR の下に記述できます。
詳細については、「[ユニバーサル INF ファイルの使用](https://docs.microsoft.com/windows-hardware/drivers/install/using-a-universal-inf-file)」を参照してください。
 
```inf
[Version]
Signature   = "$WINDOWS NT$"
Class       = AudioProcessingObject
ClassGuid   = {5989fce8-9cd0-467d-8a6a-5419e31529d4}
 
[ApoComponents.NT$ARCH$]
%Apo.ComponentDesc% = ApoComponent_Install,APO\VEN_SMPL&CID_APO
 
[Apo_AddReg]
; CLSID registration
HKCR,CLSID\%SWAP_FX_STREAM_CLSID%,,,%SFX_FriendlyName%
HKCR,CLSID\%SWAP_FX_STREAM_CLSID%\InProcServer32,,0x00020000,%%SystemRoot%%\System32\swapapo.dll
HKCR,CLSID\%SWAP_FX_STREAM_CLSID%\InProcServer32,ThreadingModel,,"Both"
…
;Audio engine registration
HKR,AudioEngine\AudioProcessingObjects\%SWAP_FX_STREAM_CLSID%,"FriendlyName",,%SFX_FriendlyName%
...
```

この INF によってコンポーネント APO がインストールされると、デスクトップシステムの "オーディオ処理オブジェクト" が Windows デバイスマネージャーに表示されます。

### <a name="bluetooth-audio-sample-apo-inf-sample"></a>Bluetooth オーディオサンプル APO INF サンプル

このサンプルでは、次のシステム効果の組み合わせを示します。

- PKEY\_FX\_StreamEffectClsid と PKEY\_SFX\_ProcessingModes\_\_Streaming でサポートされて\_

- PKEY\_FX\_ModeEffectClsid と PKEY\_MFX\_ProcessingModes\_\_Streaming の\_

このサンプルコードでは、Bluetooth ハンズフリーおよびステレオデバイスがサポートされています。

```inf
; wdma_bt.inf – example usage
...
[BthA2DP]
Include=ks.inf, wdmaudio.inf, BtaMpm.inf
Needs=KS.Registration,WDMAUDIO.Registration,BtaMPM.CopyFilesOnly,mssysfx.CopyFilesAndRegister
...
[BTAudio.SysFx.Render]
HKR,"FX\\0",%PKEY_ItemNameDisplay%,,%FX_FriendlyName%
HKR,"FX\\0",%PKEY_FX_StreamEffectClsid%,,%FX_STREAM_CLSID%
HKR,"FX\\0",%PKEY_FX_ModeEffectClsid%,,%FX_MODE_CLSID%
HKR,"FX\\0",%PKEY_FX_UiClsid%,,%FX_UI_CLSID%
HKR,"FX\\0",%PKEY_FX_Association%,,%KSNODETYPE_ANY%
HKR,"FX\\0",%PKEY_SFX_ProcessingModes_Supported_For_Streaming%,0x00010000,%AUDIO_SIGNALPROCESSINGMODE_DEFAULT%
HKR,"FX\\0",%PKEY_MFX_ProcessingModes_Supported_For_Streaming%,0x00010000,%AUDIO_SIGNALPROCESSINGMODE_DEFAULT%
...
[Strings]
FX_UI_CLSID      = "{5860E1C5-F95C-4a7a-8EC8-8AEF24F379A1}"
FX_STREAM_CLSID  = "{62dc1a93-ae24-464c-a43e-452f824c4250}"
PKEY_FX_StreamEffectClsid   = "{D04E05A6-594B-4fb6-A80D-01AF5EED7D1D},5"
PKEY_FX_ModeEffectClsid     = "{D04E05A6-594B-4fb6-A80D-01AF5EED7D1D},6"
PKEY_SFX_ProcessingModes_Supported_For_Streaming = "{D3993A3F-99C2-4402-B5EC-A92A0367664B},5"
PKEY_MFX_ProcessingModes_Supported_For_Streaming = "{D3993A3F-99C2-4402-B5EC-A92A0367664B},6"
AUDIO_SIGNALPROCESSINGMODE_DEFAULT = "{C18E2F7E-933D-4965-B7D1-1EEF228D2AF3}"
```

### <a name="apo-inf-audio-sample"></a>APO INF オーディオサンプル

このサンプル INF ファイルは、次のシステム効果の組み合わせを示しています。

- PKEY\_FX\_StreamEffectClsid と PKEY\_SFX\_ProcessingModes\_\_Streaming でサポートされて\_

- PKEY\_FX\_ModeEffectClsid と PKEY\_MFX\_ProcessingModes\_\_Streaming の\_

- PKEY\_FX\_EndpointEffectClsid を使用しない PKEY\_EFX\_ProcessingModes\_\_Streaming でサポートされている\_

```inf
[MyDevice.Interfaces]
AddInterface=%KSCATEGORY_AUDIO%,%MyFilterName%,MyAudioInterface
 
[MyAudioInterface]
AddReg=MyAudioInterface.AddReg
 
[MyAudioInterface.AddReg]
;To register an APO for discovery, use the following property keys in the .inf (or at runtime when registering the KSCATEGORY_AUDIO device interface):
HKR,"FX\\0",%PKEY_FX_StreamEffectClsid%,,%FX_STREAM_CLSID%
HKR,"FX\\0",%PKEY_FX_ModeEffectClsid%,,%FX_MODE_CLSID%
HKR,"FX\\0",%PKEY_FX_EndpointEffectClsid%,,%FX_MODE_CLSID%
 
;To register an APO for streaming and discovery, add the following property keys as well (to the same section):
HKR,"FX\\0",%PKEY_SFX_ProcessingModes_For_Streaming%,%REG_MULTI_SZ%,%AUDIO_SIGNALPROCESSINGMODE_DEFAULT%,%AUDIO_SIGNALPROCESSINGMODE_MOVIE%,%AUDIO_SIGNALPROCESSINGMODE_COMMUNICATIONS%
 
;To register an APO for streaming in multiple modes, use a REG_MULTI_SZ property and include all the modes:
HKR,"FX\\0",%PKEY_MFX_ProcessingModes_For_Streaming%,%REG_MULTI_SZ%,%AUDIO_SIGNALPROCESSINGMODE_DEFAULT%,%AUDIO_SIGNALPROCESSINGMODE_MOVIE%,%AUDIO_SIGNALPROCESSINGMODE_COMMUNICATIONS%
```

### <a name="define-a-custom-apo-and-clsid-apo-inf-sample"></a>カスタム APO および CLSID APO INF サンプルを定義する

このサンプルでは、カスタム APO 用に独自の CLSID を定義する方法を示します。 このサンプルでは、MsApoFxProxy CLSID {ABAD-4004-BF0A-BC7BB825E166} を使用します。 この GUID を CoCreate すると、MsApoFxProxy 内のクラスがインスタンス化されます。このクラスは IAudioProcessingObject インターフェイスを実装し、基になるドライバーに対して KSK PROPSETID\_Audio Discovery プロパティセットを使用してクエリを行います。

この INF ファイルのサンプルでは、\[BthHfAud\] セクションを示します。このセクションでは \[MsApoFxProxy\] を wdmaudio. BthHfAud \[から取得します。これにより、AddReg\]FX\_PKEY が EndpointEffectClsid の既知の CLSID として登録されます。\_

この INF ファイルのサンプルでは、このシステム効果の組み合わせの使用方法も示しています。

- PKEY\_FX\_EndpointEffectClsid を使用しない PKEY\_EFX\_ProcessingModes\_\_Streaming でサポートされている\_

```inf
;wdma_bt.inf
[BthHfAud]
Include=ks.inf, wdmaudio.inf, BtaMpm.inf
Needs=KS.Registration, WDMAUDIO.Registration, BtaMPM.CopyFilesOnly, MsApoFxProxy.Registration
CopyFiles=BthHfAud.CopyList
AddReg=BthHfAud.AddReg

; Called by needs entry in oem inf 
[BthHfAudOEM.CopyFiles]
CopyFiles=BthHfAud.CopyList

[BthHfAud.AnlgACapture.AddReg.Wave]
HKR,,CLSID,,%KSProxy.CLSID%
HKR,"FX\\0",%PKEY_FX_Association%,,%KSNODETYPE_ANY%
HKR,"FX\\0",%PKEY_FX_EndpointEffectClsid%,,%FX_DISCOVER_EFFECTS_APO_CLSID%
#endif
```

### <a name="sample-apo-effect-registration"></a>APO エフェクト登録のサンプル

このサンプルでは、Sysvad ComponentizedApoSample inx の\] Apo_AddReg \[を示します。 このセクションでは、スワップストリーム GUID を COM に登録し、スワップストリームの APO 効果を登録します。 \[Apo_CopyFiles\] セクションでは、swapapo .dll を C:\\Windows\\system32 にコピーします。

```inf
; ComponentizedApoSample.inx

...

[ApoComponent_Install]
CopyFiles = Apo_CopyFiles
AddReg    = Apo_AddReg

[Apo_CopyFiles]
swapapo.dll

...

[Apo_AddReg]
; Swap Stream effect APO COM registration
HKCR,CLSID\%SWAP_FX_STREAM_CLSID%,,,%SFX_FriendlyName%
HKCR,CLSID\%SWAP_FX_STREAM_CLSID%\InProcServer32,,0x00020000,%13%\swapapo.dll
HKCR,CLSID\%SWAP_FX_STREAM_CLSID%\InProcServer32,ThreadingModel,,"Both"

'''
; Swap Stream effect APO registration
HKR,AudioEngine\AudioProcessingObjects\%SWAP_FX_STREAM_CLSID%,"FriendlyName",,%SFX_FriendlyName%
HKR,AudioEngine\AudioProcessingObjects\%SWAP_FX_STREAM_CLSID%,"Copyright",,%Copyright%
HKR,AudioEngine\AudioProcessingObjects\%SWAP_FX_STREAM_CLSID%,"MajorVersion",0x00010001,1
HKR,AudioEngine\AudioProcessingObjects\%SWAP_FX_STREAM_CLSID%,"MinorVersion",0x00010001,1
HKR,AudioEngine\AudioProcessingObjects\%SWAP_FX_STREAM_CLSID%,"Flags",0x00010001,%APO_FLAG_DEFAULT%
HKR,AudioEngine\AudioProcessingObjects\%SWAP_FX_STREAM_CLSID%,"MinInputConnections",0x00010001,1
HKR,AudioEngine\AudioProcessingObjects\%SWAP_FX_STREAM_CLSID%,"MaxInputConnections",0x00010001,1
HKR,AudioEngine\AudioProcessingObjects\%SWAP_FX_STREAM_CLSID%,"MinOutputConnections",0x00010001,1
HKR,AudioEngine\AudioProcessingObjects\%SWAP_FX_STREAM_CLSID%,"MaxOutputConnections",0x00010001,1
HKR,AudioEngine\AudioProcessingObjects\%SWAP_FX_STREAM_CLSID%,"MaxInstances",0x00010001,0xffffffff
HKR,AudioEngine\AudioProcessingObjects\%SWAP_FX_STREAM_CLSID%,"NumAPOInterfaces",0x00010001,1
HKR,AudioEngine\AudioProcessingObjects\%SWAP_FX_STREAM_CLSID%,"APOInterface0",,"{FD7F2B29-24D0-4B5C-B177-592C39F9CA10}"
...

[Strings]
; Driver developers would replace these CLSIDs with those of their own APOs
SWAP_FX_STREAM_CLSID   = "{B48DEA3F-D962-425a-8D9A-9A5BB37A9904}"

...
```

## <a name="span-idapo_registrationspanspan-idapo_registrationspanspan-idapo_registrationspanapo-registration"></a><span id="APO_Registration"></span><span id="apo_registration"></span><span id="APO_REGISTRATION"></span>APO 登録

APO 登録は、重み付け計算を使用してエンドポイントへの効果を動的に照合するプロセスをサポートするために使用されます。 重み付け計算では、次のプロパティストアを使用します。 各オーディオインターフェイスには、0個以上の*エンドポイントプロパティストア*と、.inf または実行時に登録された*プロパティストア*があります。 最も限定的なエンドポイントプロパティストアと最も限定的な効果プロパティストアは、重みが最も高く、使用されます。 その他のすべてのプロパティストアは無視されます。

特異性は次のように計算されます。

エンドポイントプロパティに重み付けを格納する

1. 特定の KSNODETYPE を持つ FX
2. KSNODETYPE を使用した FX\_任意
3. 特定の KSNODETYPE を持つ MSFX
4. KSNODETYPE を使用した MSFX\_任意

Effects プロパティストアの重み付け

1. 特定の KSNODETYPE を使用した EP
2. KSNODETYPE を使用した EP\_任意
3. 特定の KSNODETYPE を持つ MSEP
4. MSEP と KSNODETYPE\_任意

数値は0から順番に増加する必要があります: MSEP\\0、MSEP\\1、...、MSEP\\n (たとえば) EP\\3 がない場合、Windows は EP\\n の検索を停止し、EP\\4 (存在する場合でも) は表示されません。

PKEY\_FX\_Association (効果プロパティストアの場合) または PKEY\_EP\_アソシエーション (エンドポイントプロパティストアの場合) の値が KSPINDESCRIPTOR と比較されます。カーネルストリーミングによって公開されるシグナルパスのハードウェア終端のピンファクトリのカテゴリ値。

Microsoft 受信トレイクラスドライバー (サードパーティの開発者がラップできるドライバー) のみ、MSEP と MSFX を使用する必要があります。すべてのサードパーティのドライバーは、EP と FX を使用する必要があります。

### <a name="apo-node-type-compatibility"></a>APO ノード型の互換性

次の INF ファイルのサンプルでは、PKEY\_FX\_Association キーを、APO に関連付けられている GUID に設定しています。

```inf
;; Property Keys
PKEY_FX_Association = "{D04E05A6-594B-4fb6-A80D-01AF5EED7D1D},0"
"
```

```inf
;; Key value pairs
HKR,"FX\\0",%PKEY_FX_Association%,,%KSNODETYPE_ANY%
```

オーディオアダプターは複数の入力と出力をサポートすることができるため、カスタム APO に互換性がある種類のカーネルストリーミング (KS) ノードタイプを明示的に指定する必要があります。 前の INF ファイルフラグメントでは、APO は% KSNODETYPE\_の KS ノードタイプに関連付けられています。 この INF ファイルでは、KSNODETYPE\_ANY は次のように定義されています。

```inf
[Strings]
;; Define the strings used in MyINF.inf
...
KSNODETYPE_ANY      = "{00000000-0000-0000-0000-000000000000}"
KSNODETYPE_SPEAKER  = "{DFF21CE1-F70F-11D0-B917-00A0C9223196}"
...
```

KSNODETYPE の値が**NULL**の場合\_any は、この APO が任意の型の KS ノード型と互換性があることを意味します。 たとえば、APO が KSNODETYPE\_スピーカーの KS ノードタイプとのみ互換性があることを示すために、INF ファイルでは次のように KS ノードの種類と APO の関連付けが表示されます。

```inf
;; Key value pairs
...
HKR,"FX\\0",%PKEY_FX_Association%,,%KSNODETYPE_SPEAKER%
...
```

さまざまな KS ノード型の GUID 値の詳細については、「Ksmedia .h ヘッダーファイル」を参照してください。

## <a name="span-idtroubleshooting_apo_load_failuresspanspan-idtroubleshooting_apo_load_failuresspanspan-idtroubleshooting_apo_load_failuresspantroubleshooting-apo-load-failures"></a><span id="Troubleshooting_APO_Load_Failures"></span><span id="troubleshooting_apo_load_failures"></span><span id="TROUBLESHOOTING_APO_LOAD_FAILURES"></span>APO 読み込みエラーのトラブルシューティング

次の情報は、APOs の障害がどのように監視されるかを理解するのに役立ちます。 この情報を使用すると、オーディオグラフへの組み込みに失敗した問題のトラブルシューティングを行うことができます。

オーディオシステムは、APO リターンコードを監視して、APOs がグラフに正常に組み込まれているかどうかを判断します。 指定されたメソッドのいずれかによって返される HRESULT 値を追跡することで、リターンコードを監視します。 システムは、グラフに組み込まれている SFX、MFX、および EFX APO ごとに個別のエラー数の値を保持します。

オーディオシステムは、次の4つのメソッドから返された HRESULT 値を監視します。

- CoCreateInstance

- IsInputFormatSupported

- サポートされている isoutputformat

- LockForProcess

これらのメソッドの1つがエラーコードを返すたびに、APO に対してエラー数の値が増加します。 APO がオーディオグラフに正常に組み込まれたことを示すコードを返した場合、エラー数は0にリセットされます。 [**Lockforprocess**](https://docs.microsoft.com/windows/desktop/api/audioenginebaseapo/nf-audioenginebaseapo-iaudioprocessingobjectconfiguration-lockforprocess)メソッドを正常に呼び出すことは、APO が正常に組み込まれたことを示しています。

特に、 [**CoCreateInstance**](https://docs.microsoft.com/windows/desktop/api/combaseapi/nf-combaseapi-cocreateinstance)では、返される HRESULT コードがエラーを示す可能性があります。 主な理由は次の3つです。

- グラフで保護されたコンテンツが実行されていますが、APO に正しく署名されていません。

- APO が登録されていません。

- APO の名前が変更されたか、改ざんされています。

また、SFX、MFX、または EFX APO の失敗数の値がシステムによって指定された制限に達した場合、SFX、MFX、および EFX APOs は、PKEY\_エンド\_ポイントを設定することによって無効にし、SysFx レジストリキー\_を ' 1 ' に設定することによって無効にします。 システム指定の制限は、現在、10の値です。

## <a name="span-idrelated_topicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック

[Windows オーディオ処理オブジェクト](windows-audio-processing-objects.md)

[ユニバーサル INF ファイルの使用](https://docs.microsoft.com/windows-hardware/drivers/install/using-a-universal-inf-file)

[コンポーネント化オーディオドライバーのインストールの作成](https://docs.microsoft.com/windows-hardware/drivers/audio/audio-universal-drivers#creating-a-componentized-audio-driver-installation)