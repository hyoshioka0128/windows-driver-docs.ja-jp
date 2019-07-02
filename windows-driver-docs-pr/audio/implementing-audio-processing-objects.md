---
title: オーディオ処理オブジェクトの実装
description: このトピックでは、オーディオ処理オブジェクト (APO) を実装する方法について説明します。 パスワードの詳細については、オーディオ処理オブジェクト アーキテクチャを参照してください。
ms.assetid: 822FAF10-DAB3-48D1-B782-0C80B072D3FB
ms.date: 06/19/2018
ms.localizationpriority: medium
ms.openlocfilehash: a34bf6b46e8420aa95d638c7a374abdf434fa8f1
ms.sourcegitcommit: 2854c02cbe5b2c0010d0c64367cfe8dbd201d3f1
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2019
ms.locfileid: "67499800"
---
# <a name="implementing-audio-processing-objects"></a>オーディオ処理オブジェクトの実装


このトピックでは、オーディオ処理オブジェクト (APO) を実装する方法について説明します。 パスワードの詳細については、次を参照してください。[オーディオ処理オブジェクト アーキテクチャ](audio-processing-object-architecture.md)します。

## <a name="span-idimplementingcustomaposspanspan-idimplementingcustomaposspanspan-idimplementingcustomaposspanimplementing-custom-apos"></a><span id="Implementing_Custom_APOs"></span><span id="implementing_custom_apos"></span><span id="IMPLEMENTING_CUSTOM_APOS"></span>カスタム APOs を実装します。


カスタム APOs は、ユーザー モードで実行して、ダイナミック リンク ライブラリ (DLL) にパッケージ化したため、インプロセス COM オブジェクトとして実装されます。 信号のグラフを処理で挿入する位置に基づく APO の 3 種類があります。

-   Stream の効果 (SFX)
-   モードの効果 (MFX)
-   エンドポイントの効果 (EFX)

各論理デバイスは、各型の 1 つ APO を関連付けることができます。 モードと影響の詳細については、次を参照してください。[オーディオ信号の処理モード](audio-signal-processing-modes.md)します。

APO を実装するには、Baseaudioprocessingobject.h ファイルで宣言されている CBaseAudioProcessingObject 基底クラスに基づいてカスタム クラスを作成します。 このアプローチでは、カスタマイズされた APO を作成する CBaseAudioProcessingObject の基本クラスに新しい機能を追加する必要があります。 CBaseAudioProcessingObject 基底クラスは、APO を必要とする機能の多くを実装します。 次の 3 つの必要なインターフェイスのメソッドのほとんどの既定の実装を提供します。 主な例外は、 [ **IAudioProcessingObjectRT::APOProcess** ](https://docs.microsoft.com/windows/desktop/api/audioenginebaseapo/nf-audioenginebaseapo-iaudioprocessingobjectrt-apoprocess)メソッド。

カスタム、APOs を実装するために、次の手順を実行します。

1.  目的のオーディオの処理を提供するカスタム APO com オブジェクトを作成します。
2.  必要に応じてカスタム APOs を構成するためのユーザー インターフェイスを作成します。
3.  インストールし、APOs とカスタム ユーザー インターフェイスを登録する INF ファイルを作成します。

カスタム プロパティ ページの実装の詳細については、次を参照してください。 [APO 効果の構成 UI を実装する](implementing-a-ui-for-configuring-apo-effects.md)します。 以下のスクリーン ショットでは、SwapAPO プロパティを示します。

![スピーカーのプロパティ システムの効果を示すサンプル システムの構成の効果を提供するタブ](images/audio-apo-speaker-properties.png)

## <a name="span-iddesignconsiderationsforcustomapodevelopmentspanspan-iddesignconsiderationsforcustomapodevelopmentspanspan-iddesignconsiderationsforcustomapodevelopmentspandesign-considerations-for-custom-apo-development"></a><span id="Design_Considerations_for_Custom_APO_Development"></span><span id="design_considerations_for_custom_apo_development"></span><span id="DESIGN_CONSIDERATIONS_FOR_CUSTOM_APO_DEVELOPMENT"></span>カスタム APO 開発のための設計に関する考慮事項


すべてのカスタム APOs 次の一般的な特性があります。

-   APO が 1 つの入力を必要し、1 つの出力接続します。 これらの接続は、オーディオのバッファーを複数のチャネルを持つことができます。
-   を通じて渡されるオーディオ データのみを変更、APO その[ **IAudioProcessingObjectRT::APOProcess** ](https://docs.microsoft.com/windows/desktop/api/audioenginebaseapo/nf-audioenginebaseapo-iaudioprocessingobjectrt-apoprocess)ルーチン。 APO、KS トポロジを含む、基になる論理デバイスの設定は変更できません。
-   IUnknown、だけでなく APOs は、次のインターフェイスを公開する必要があります。

    - [IAudioProcessingObject](https://docs.microsoft.com/windows/desktop/api/audioenginebaseapo/nn-audioenginebaseapo-iaudioprocessingobject)します。 初期化とフォーマットのネゴシエーションなどのセットアップ タスクを処理するインターフェイスです。

    - [IAudioProcessingObjectConfiguration](https://docs.microsoft.com/windows/desktop/api/audioenginebaseapo/nn-audioenginebaseapo-iaudioprocessingobjectconfiguration)します。 構成インターフェイスです。

    - [IAudioProcessingObjectRT](https://docs.microsoft.com/windows/desktop/api/audioenginebaseapo/nn-audioenginebaseapo-iaudioprocessingobjectrt)します。 オーディオの処理を行うリアルタイム インターフェイス。 リアルタイム処理のスレッドから呼び出すことができます。

    - [IAudioSystemEffects](https://docs.microsoft.com/windows/desktop/api/audioenginebaseapo/nn-audioenginebaseapo-iaudiosystemeffects)します。 インターフェイスをオーディオ エンジンは、システムの影響 APO として DLL を認識します。

- すべての APOs リアルタイム システムの互換性があります。 これは次のことを意味します。

  - リアルタイムのインターフェイスのメンバーであるすべてのメソッドは、非ブロッキングのメンバーとして実装する必要があります。 する必要がありますいないのブロック、ページのメモリを使用して、または、ブロックしているシステム ルーチンを呼び出します。

  - APO によって処理されるすべてのバッファーは、非ページングである必要があります。 すべてのコードと、プロセス パス内のデータは、非ページングする必要があります。

  - APOs は重要な待機時間をオーディオ処理チェーンに挿入する必要がありますはありません。

- カスタム APOs は IAudioProcessingObjectVBR インターフェイスを公開する必要があります。

**注**  、必要なインターフェイスの詳細については、Windows キットで Audioenginebaseapo.h と Audioenginebaseapo.idl ファイルを参照してください\\&lt;ビルド番号&gt;\\ 。含める\\um フォルダー。

 

## <a name="span-idusingsamplecodetoacceleratethedevelopmentprocessspanspan-idusingsamplecodetoacceleratethedevelopmentprocessspanspan-idusingsamplecodetoacceleratethedevelopmentprocessspanusing-sample-code-to-accelerate-the-development-process"></a><span id="Using_Sample_Code_to_Accelerate_the_Development_Process"></span><span id="using_sample_code_to_accelerate_the_development_process"></span><span id="USING_SAMPLE_CODE_TO_ACCELERATE_THE_DEVELOPMENT_PROCESS"></span>サンプル コードを使用して、開発プロセスを促進するには


コード サンプルをテンプレートとしては、SYSVAD スワップ APO を使用してカスタム APO 開発プロセスを推し進めることができます。 スワップのサンプルでは、オーディオ処理オブジェクトの一部の機能を説明するために開発されたサンプルを示します。 スワップ APO サンプルでは、適切なチャネルを使用した左チャネルを交換し、SFX と MFX の両方の効果を実装します。 有効にし、プロパティ ダイアログ ボックスを使用してチャネル スワップのオーディオ効果を無効にすることができます。

SYSVAD オーディオ サンプルで使用できる、 [Windows ドライバーのサンプル GitHub](https://github.com/Microsoft/Windows-driver-samples)します。

Sysvad オーディオ サンプルは、ここを参照できます。

<https://github.com/Microsoft/Windows-driver-samples/tree/master/audio/sysvad>

**ダウンロードして、GitHub から Sysvad オーディオ サンプルを抽出**

以下の手順をダウンロードして SYSVAD サンプルを開きます。

a. GitHub ツールを使用して、サンプルを使用することができます。 1 つの zip ファイルに汎用ドライバー サンプルをダウンロードすることもできます。

<https://github.com/Microsoft/Windows-driver-samples/archive/master.zip>

b. Master.zip ファイルをローカル ハード ドライブにダウンロードします。

c. 右クリックして*Windows ドライバーのサンプル-master.zip*、選択**すべて展開**します。 新しいフォルダーを指定するか、抽出したファイルを保存する既存のサブスクリプションへの参照します。 たとえば、指定する*c:\\DriverSamples\\* として新しいファイルの抽出先フォルダーです。

d. ファイルが抽出されると、次のサブフォルダーに移動します。

*C:\\DriverSamples\\オーディオ\\Sysvad*

**Visual Studio でのドライバー ソリューションを開く**

Microsoft Visual Studio]、[クリックして**ファイル** &gt; **オープン** &gt; **プロジェクト/ソリューション.** を抽出したファイルを含むフォルダーに移動します (たとえば、 *c:\\DriverSamples\\オーディオ\\Sysvad*)。 ダブルクリックして、 *Sysvad*ソリューション ファイルを開きます。

Visual Studio では、ソリューション エクスプ ローラーを見つけます。 (これがまだ開いていない場合は、選択**ソリューション エクスプ ローラー**から、**ビュー**メニュー)。ソリューション エクスプ ローラーでは、6 つのプロジェクトを含む 1 つのソリューションを確認できます。

**コード SwapAPO 例**

SYSVAD サンプルでは、APO 開発者に特に重要となるはその 1 つには、5 つのプロジェクトがあります。

|                    |                                       |
|--------------------|---------------------------------------|
| **プロジェクト**        | **[説明]**                       |
| SwapAPO            | たとえば APO サンプル コードです。       |

 

Sysvad サンプル内の他のプロジェクトは、次に示します。

|                        |                                            |
|------------------------|--------------------------------------------|
| **プロジェクト**            | **[説明]**                            |
| PhoneAudioSample       | モバイルのオーディオ ドライバーのサンプル コードです。     |
| TabletAudioSample      | 代替オーディオ ドライバーのサンプル コードです。 |
| KeywordDetectorAdapter | キーワード detector のアダプターのサンプル コード |
| EndpointsCommon        | 一般的なエンドポイントのサンプル コードです。          |

 

SwapAPO サンプルについては、プライマリ ヘッダー ファイルは、swapapo.h です。 その他の主要なコード要素を次に示します。

|                      |                                                                   |
|----------------------|-------------------------------------------------------------------|
| **ファイル**             | **[説明]**                                                   |
| Swap.cpp             | スワップ APO の実装が含まれている C++ コードです。        |
| SwapAPOMFX.cpp       | CSwapAPOMFX の実装                                     |
| SwapAPOSFX.cpp       | CSwapAPOSFX の実装                                     |
| SwapAPODll.cpp       | DLL エクスポートの実装です。                                    |
| SwapAPODll.idl       | DLL の COM インターフェイスおよびコクラスの定義。           |
| SwapAPOInterface.idl | スワップ APO 機能のインターフェイスと型定義。    |
| swapapodll.def       | COM は、定義をエクスポートします。                                           |

 

## <a name="span-idimplementingthecomobjectaudioprocessingcodespanspan-idimplementingthecomobjectaudioprocessingcodespanspan-idimplementingthecomobjectaudioprocessingcodespanimplementing-the-com-object-audio-processing-code"></a><span id="Implementing_the_COM_Object_Audio_Processing_Code"></span><span id="implementing_the_com_object_audio_processing_code"></span><span id="IMPLEMENTING_THE_COM_OBJECT_AUDIO_PROCESSING_CODE"></span>COM オブジェクトのオーディオ処理コードを実装します。


システム提供の APO をラップするには、カスタム クラスをに基づいて、 **CBaseAudioProcessingObject**基本クラス、Baseaudioprocessingobject.h ファイルで宣言されています。 このアプローチでは、新しい機能の概要では、 **CBaseAudioProcessingObject**基本クラスをカスタマイズした APO を作成します。 **CBaseAudioProcessingObject**基底クラスは、APO を必要とする機能の多くを実装します。 次の 3 つの必要なインターフェイスのメソッドのほとんどの既定の実装を提供します。 主な例外は、 [ **IAudioProcessingObjectRT::APOProcess** ](https://docs.microsoft.com/windows/desktop/api/audioenginebaseapo/nf-audioenginebaseapo-iaudioprocessingobjectrt-apoprocess)メソッド。

使用して**CBaseAudioProcessingObject**、APO をより簡単に実装することができます。 APO が特殊な形式の要件がない、必要な float32 で動作する場合のフォーマットに含まれているインターフェイス メソッドの既定の実装**CBaseAudioProcessingObject**十分です。 既定の実装を指定するには、3 つだけのメイン メソッドを実装する必要があります。[**IAudioProcessingObject::IsInputFormatSupported**](https://docs.microsoft.com/windows/desktop/api/audioenginebaseapo/nf-audioenginebaseapo-iaudioprocessingobject-isinputformatsupported)、 [ **IAudioProcessingObjectRT::APOProcess**](https://docs.microsoft.com/windows/desktop/api/audioenginebaseapo/nf-audioenginebaseapo-iaudioprocessingobjectrt-apoprocess)、および**ValidateAndCacheConnectionInfo**.

に基づいて、APOs を開発する、 **CBaseAudioProcessingObject**クラスで、次の手順に従います。

1.  継承するクラスを作成**CBaseAudioProcessingObject**します。

    C++ のコード例を次から継承するクラスの作成を示しています。 **CBaseAudioProcessingObject**します。 この概念の実際の実装の手順については、**オーディオ処理オブジェクト ドライバー サンプル**セクション スワップ サンプルに移動しを参照、 *Swapapo.h*ファイル。

    ```cpp
    // Custom APO class - LFX
    Class MyCustomAPOLFX: public CBaseAudioProcessingObject
    {
     public:
    //Code for custom class goes here
    ...
    };
    ```

    **注**   SFX APO によって実行される信号処理が、MFX または、EFX APO によって実行される信号処理と異なるため、ごとに個別のクラスを作成する必要があります。

     

2.  次の 3 つのメソッドを実装します。

    -   [**IAudioProcessingObject::IsInputFormatSupported**](https://docs.microsoft.com/windows/desktop/api/audioenginebaseapo/nf-audioenginebaseapo-iaudioprocessingobject-isinputformatsupported)します。 このメソッドは、オーディオ エンジンと形式のネゴシエーションを処理します。

    -   [**IAudioProcessingObjectRT::APOProcess**](https://docs.microsoft.com/windows/desktop/api/audioenginebaseapo/nf-audioenginebaseapo-iaudioprocessingobjectrt-apoprocess)します。 このメソッドは、信号処理を実行するのに、カスタム アルゴリズムを使用します。

    -   **ValidateAndCacheConnectionInfo**します。 このメソッドは、たとえば、形式の詳細を格納するチャネルの数、サンプリング レート、サンプルの深さ、およびチャネル マスクにメモリを割り当てます。

C++ のコード例を次の実装を示しています、 [ **APOProcess** ](https://docs.microsoft.com/windows/desktop/api/audioenginebaseapo/nf-audioenginebaseapo-iaudioprocessingobjectrt-apoprocess)手順 1. で作成したサンプル クラスのメソッド。 この概念の実際の実装の手順については、**オーディオ処理オブジェクト ドライバー サンプル**セクション スワップ サンプルに移動しを参照、 *Swapapolfx.cpp*ファイル。

```cpp
// Custom implementation of APOProcess method
STDMETHODIMP_ (Void) MyCustomAPOLFX::APOProcess (...)
{
// Code for method goes here. This code is the algorithm that actually
// processes the digital audio signal.
...
}
```

次のコード例の実装を示しています、 **ValidateAndCacheConnectionInfo**メソッド。 このメソッドの実際の実装の手順については、**オーディオ処理オブジェクト ドライバー サンプル**セクション スワップ サンプルに移動しを参照、 *Swapapogfx.cpp*ファイル。

```cpp
// Custom implementation of the ValidateAndCacheConnectionInfo method.
HRESULT CSwapAPOGFX::ValidateAndCacheConnectionInfo( ... )
{
// Code for method goes here.
// The code should validate the input/output format pair.
...
}
```

**注**  残りのインターフェイスとクラスを継承するメソッド**CBaseAudioProcessingObject** Audioenginebaseapo.idl ファイルで詳しく説明します。

 

デスクトップ pc の場合は、カスタム APO に追加した機能を構成するためのユーザー インターフェイスを行うことができます。 詳細については、次を参照してください。 [APOs の構成の UI を実装する](implementing-a-ui-for-configuring-sapos.md)します。

## <a name="span-idreplacingsystem-suppliedaposspanspan-idreplacingsystem-suppliedaposspanspan-idreplacingsystem-suppliedaposspanreplacing-system-supplied-apos"></a><span id="Replacing_System-supplied_APOs"></span><span id="replacing_system-supplied_apos"></span><span id="REPLACING_SYSTEM-SUPPLIED_APOS"></span>システム提供の APOs を置き換える


インターフェイス、APO を実装するときに、2 つの方法があります。 独自の実装を記述するまたは APOs 受信トレイに呼び出すことができます。

この擬似コードでは、システム APO の折り返しを示しています。

```cpp
CMyWrapperAPO::CMyWrapperAPO {
    CoCreateInstance(CLSID_InboxAPO, m_inbox);
}

CMyWrapperAPO::IsInputFormatSupported {
    Return m_inbox->IsInputFormatSupported(…);
}
```

この擬似コードでは、独自のカスタム APO の作成を示しています。

```cpp
CMyFromScratchAPO::IsInputFormatSupported {
    my custom logic
}
```

システムが指定したものを置き換える、APOs を開発する際にインターフェイスやメソッドの次の一覧で、同じ名前を使用する必要があります。 さらにメソッドだけでなく、表示されている必要なメソッドがある一部のインターフェイス。 すべてのメソッドまたは必要なものだけを実装するかどうかを判断するそれらのインターフェイスのリファレンス ページを参照してください。

実装手順の残りの部分では、カスタム APO と同じです。

次のインターフェイスおよび COM コンポーネントのメソッドを実装します。

-   [IAudioProcessingObject](https://docs.microsoft.com/windows/desktop/api/audioenginebaseapo/nn-audioenginebaseapo-iaudioprocessingobject)します。 このインターフェイスに必要なメソッドは次のとおりです。[**初期化**](https://docs.microsoft.com/windows/desktop/api/audioenginebaseapo/nf-audioenginebaseapo-iaudioprocessingobject-initialize)と[ **IsInputFormatSupported します。** ](https://docs.microsoft.com/windows/desktop/api/audioenginebaseapo/nf-audioenginebaseapo-iaudioprocessingobject-isinputformatsupported)
-   [IAudioProcessingObjectConfiguration](https://docs.microsoft.com/windows/desktop/api/audioenginebaseapo/nn-audioenginebaseapo-iaudioprocessingobjectconfiguration)します。 このインターフェイスに必要なメソッドは次のとおりです。[**LockForProcess** ](https://docs.microsoft.com/windows/desktop/api/audioenginebaseapo/nf-audioenginebaseapo-iaudioprocessingobjectconfiguration-lockforprocess)と[ **UnlockForProcess**](https://docs.microsoft.com/windows/desktop/api/audioenginebaseapo/nf-audioenginebaseapo-iaudioprocessingobjectconfiguration-unlockforprocess)
-   [IAudioProcessingObjectRT](https://docs.microsoft.com/windows/desktop/api/audioenginebaseapo/nn-audioenginebaseapo-iaudioprocessingobjectrt)します。 このインターフェイスに必要なメソッドは[ **APOProcess** ](https://docs.microsoft.com/windows/desktop/api/audioenginebaseapo/nf-audioenginebaseapo-iaudioprocessingobjectrt-apoprocess) DSP アルゴリズムを実装するメソッドであるとします。
-   [IAudioSystemEffects](https://docs.microsoft.com/windows/desktop/api/audioenginebaseapo/nn-audioenginebaseapo-iaudiosystemeffects)します。 このインターフェイスを APO として DLL を認識するオーディオ エンジンとなります。

## <a name="span-idworkingwithvisualstudioandaposspanspan-idworkingwithvisualstudioandaposspanspan-idworkingwithvisualstudioandaposspanworking-with-visual-studio-and-apos"></a><span id="Working_with_Visual_Studio_and_APOs"></span><span id="working_with_visual_studio_and_apos"></span><span id="WORKING_WITH_VISUAL_STUDIO_AND_APOS"></span>Visual Studio とパスワードを使用します。


Visual Studio でのパスワードを使用する場合は、APO プロジェクトごとにこれらのタスクを実行します。

**CRT へのリンク**

ドライバーを Windows 10 を対象とは、universal CRT に対して動的にリンクする必要があります。

Windows 8,1 をサポートする必要がある場合は、C/C++、コード生成で、プロジェクトのプロパティを設定して、静的リンクを有効にします。 「ランタイム ライブラリ」に設定 */MT*リリース ビルドまたは */MTd*デバッグ ビルドの場合。 ドライバーは難しい、MSVCRT の再配布するため、この変更が加えられた&lt;n&gt;.dll バイナリ。 ソリューションでは、libcmt.dll を静的にリンクします。 詳細については、次を参照してください。 [/MD、/MT、/LD (ランタイム ライブラリの使用)](https://docs.microsoft.com/cpp/build/reference/md-mt-ld-use-run-time-library)します。

**埋め込みマニフェストの使用を無効にします。**

APO プロジェクトのプロジェクト プロパティを設定して、埋め込まれたマニフェストの使用を無効にします。 選択**マニフェスト ツール**、**入力し、出力**します。 「埋め込みマニフェスト」の既定値から変更*はい*に*いいえ*します。 埋め込みマニフェストを使っている場合、保護された環境内で禁止されている特定の Api を使用するようにトリガーされます。 これは、APO DisableProtectedAudioDG で実行されることを意味 = 1 が WHQL 署名がある場合でも、APO は失敗を読み込むには、このテスト キーが削除されるとします。

## <a name="span-idpackagingyourapowithadriverspanspan-idpackagingyourapowithadriverspanspan-idpackagingyourapowithadriverspanpackaging-your-apo-with-a-driver"></a><span id="Packaging_your_APO_with_a_Driver"></span><span id="packaging_your_apo_with_a_driver"></span><span id="PACKAGING_YOUR_APO_WITH_A_DRIVER"></span>ドライバーを使用して、APO をパッケージ化


ラップし、またはシステム提供の APOs を置換する独自のオーディオ ドライバーの開発するとき、は、ドライバーと APOs にインストールするドライバー パッケージを指定する必要があります。 Windows 10 を参照してください[オーディオのユニバーサル Windows ドライバー](audio-universal-drivers.md)します。 オーディオの関連するドライバー パッケージは、ポリシーと詳細がパッケージ化モデルに従う必要があります。  

カスタム APO は、DLL、および UI が別の UWP またはデスクトップ ブリッジ アプリケーションとしてパッケージ化、構成としてパッケージ化されます。 APO デバイス INF では、関連付けられている INF CopyFile ディレクティブに示されたシステム フォルダーに Dll をコピーします。 APOs を含んでいる DLL は、INF ファイルで、[AddReg] セクションを含めることによって自体を登録する必要があります。

次の段落と INF ファイル フラグメントは、標準の INF ファイルを使用してコピーし、デバイスを登録するために必要な変更を表示します。

Sysvad サンプルに含まれる tabletaudiosample.inf と phoneaudiosample.inf ファイルでは、SwapApo.dll APOs を登録する方法について説明します。

## <a name="span-idregisteringaposforprocessingmodesandeffectsintheinffilespanspan-idregisteringaposforprocessingmodesandeffectsintheinffilespanspan-idregisteringaposforprocessingmodesandeffectsintheinffilespan-registering-apos-for-processing-modes-and-effects-in-the-inf-file"></a><span id="_Registering_APOs_for_Processing_Modes_and_Effects_in_the_INF_File"></span><span id="_registering_apos_for_processing_modes_and_effects_in_the_inf_file"></span><span id="_REGISTERING_APOS_FOR_PROCESSING_MODES_AND_EFFECTS_IN_THE_INF_FILE"></span> 処理モードと INF ファイルで効果の APOs を登録します。


レジストリ キーの特定の利用可能な組み合わせを使用した特定のモードは、APOs を登録できます。 詳細については効果は APOs について使用可能な一般的なは、次を参照してください。[オーディオ処理オブジェクト アーキテクチャ](audio-processing-object-architecture.md)します。

各 APO INF ファイルの設定の情報は次のリファレンス トピックを参照してください。

[鍵\_FX\_StreamEffectClsid](https://docs.microsoft.com/windows-hardware/drivers/audio/pkey-fx-streameffectclsid)

[鍵\_FX\_ModeEffectClsid](https://docs.microsoft.com/windows-hardware/drivers/audio/pkey-fx-modeeffectclsid)

[鍵\_FX\_EndpointEffectClsid](https://docs.microsoft.com/windows-hardware/drivers/audio/pkey-fx-endpointeffectclsid)

[鍵\_SFX\_ProcessingModes\_サポート\_の\_ストリーミング](https://docs.microsoft.com/windows-hardware/drivers/audio/pkey-sfx-processingmodes-supported-for-streaming)

[鍵\_MFX\_ProcessingModes\_サポート\_の\_ストリーミング](https://docs.microsoft.com/windows-hardware/drivers/audio/pkey-mfx-processingmodes-supported-for-streaming)

[鍵\_EFX\_ProcessingModes\_サポート\_の\_ストリーミング](https://docs.microsoft.com/windows-hardware/drivers/audio/pkey-efx-processingmodes-supported-for-streaming)

次のサンプルの INF ファイルでは、オーディオ処理オブジェクト (APOs) の特定のモードを登録する方法を示します。 この一覧から利用可能な組み合わせをについて説明します。

-   鍵\_FX\_鍵で StreamEffectClsid\_SFX\_ProcessingModes\_サポート\_の\_ストリーミング
-   鍵\_FX\_鍵で ModeEffectClsid\_MFX\_ProcessingModes\_ありません\_の\_ストリーミング
-   鍵\_FX\_鍵せず ModeEffectClsid\_MFX\_ProcessingModes\_ありません\_の\_ストリーミング
-   鍵\_FX\_鍵せず EndpointEffectClsid\_EFX\_ProcessingModes\_サポート\_の\_ストリーミング

これらのサンプルに表示されていない 1 つ追加の有効な組み合わせがあります。

-   鍵\_FX\_鍵で EndpointEffectClsid\_EFX\_ProcessingModes\_サポート\_の\_ストリーミング

**SYSVAD タブレット マルチモード ストリーミング効果 APO INF サンプル**

この例では、マルチモード ストリーミング SYSVAD タブレット INF ファイルの AddReg エントリを使用して登録に影響します。

このサンプル コードが SYSVAD オーディオ サンプルは、GitHub で入手できます:<https://github.com/Microsoft/Windows-driver-samples/tree/master/audio/sysvad>します。

このサンプルでは、このシステムの効果の組み合わせを示します。

-   鍵\_FX\_鍵で StreamEffectClsid\_SFX\_ProcessingModes\_サポート\_の\_ストリーミング

-   鍵\_FX\_鍵で ModeEffectClsid\_MFX\_ProcessingModes\_ありません\_の\_ストリーミング

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

サンプルの INF ファイル、EFX\_プロパティをストリーミングする必要はありませんしは、使用されないように、オーディオの処理が、そのレイヤー上のカーネル モードに移行するため、コメント アウト プロパティをストリーミングします。 鍵を指定することが\_FX\_EndpointEffectClsid 検出目的での鍵を指定するとエラーになります\_EFX\_ProcessingModes\_サポートされている\_の\_ストリーミングします。 これは、モードを混在させるため/tee は、APO エンドポイントを挿入することはできません、スタックの下位が発生します。

**コンポーネント化された APO インストール**

Windows 10 では、以降では 1809 をリリース、APO オーディオ エンジンへの登録がコンポーネント化されたオーディオ ドライバー モデルを使用します。 オーディオのコンポーネント化を使用して、スムーズかつ信頼性の高いインストール エクスペリエンスを作成し、コンポーネント サービスを適切にサポートします。 詳細については、次を参照してください。[コンポーネント化されたオーディオ ドライバーのインストールを作成する](https://docs.microsoft.com/windows-hardware/drivers/audio/audio-universal-drivers#creating-a-componentized-audio-driver-installation)します。

次のコード例は、パブリック ComponentizedAudioSampleExtension.inf と ComponentizedApoSample.inf から抽出されます。 ここでは GitHub で入手できる、SYSVAD オーディオ サンプルを参照してください:<https://github.com/Microsoft/Windows-driver-samples/tree/master/audio/sysvad>します。
 
オーディオ エンジン APO の登録が完了 APO の新しく作成されたデバイスを使用します。 新しい APO デバイスの使用をオーディオ エンジンのオーディオ デバイス、オーディオのエンドポイントの兄弟の PNP 子である必要があります。 新しいコンポーネント化された APO 設計では、グローバルに登録する、APO は許可されず、複数のさまざまなドライバーで使用されます。 各ドライバーでは、独自 APO を登録する必要があります。

APO のインストールは、2 つの部分で行われます。 最初に、INF ドライバーの拡張機能は、システムに、APO デバイスを追加します。
 
```inf
[DeviceExtension_Install.Devices]
AddDevice = SwapApo,,Apo_AddDevice
 
[Apo_AddDevice]
HardwareIds = APO\VEN_SMPL&CID_APO
Description = "Audio Proxy APO Sample"
Capabilities = 0x00000008 ; SWDeviceCapabilitiesDriverRequired
```

この APO デバイスは、2 番目の部分では、これを行う ComponentizedApoSample.inf SYSVAD サンプルでは、APO INF のインストールをトリガーします。 この INF ファイルは、APO デバイスを専用です。 AudioProcessingObject としてデバイス クラスを指定し、すべての CLSID の登録と、オーディオ エンジンに登録する APO プロパティを追加します。 
 
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

この INF は、コンポーネント化された APO をインストール、デスクトップ システムで「オーディオ処理オブジェクト」が表示されます Windows デバイス マネージャーでします。 


**Bluetooth のオーディオ サンプル APO INF サンプル**

このサンプルでは、このシステムの効果の組み合わせを示します。

-   鍵\_FX\_鍵で StreamEffectClsid\_SFX\_ProcessingModes\_サポート\_の\_ストリーミング

-   鍵\_FX\_鍵で ModeEffectClsid\_MFX\_ProcessingModes\_ありません\_の\_ストリーミング

このサンプル コードでは、ハンズフリーとステレオの Bluetooth デバイスをサポートします。

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

**APO INF オーディオ サンプル**

このサンプルの INF ファイルは、次のシステムの効果の組み合わせを示しています。

-   鍵\_FX\_鍵で StreamEffectClsid\_SFX\_ProcessingModes\_サポート\_の\_ストリーミング

-   鍵\_FX\_鍵で ModeEffectClsid\_MFX\_ProcessingModes\_ありません\_の\_ストリーミング

-   鍵\_FX\_鍵せず EndpointEffectClsid\_EFX\_ProcessingModes\_サポート\_の\_ストリーミング

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

**CLSID APO INF サンプルとカスタム APO を定義します。**

このサンプルでは、カスタム APO の独自の CLSID を定義する方法を示します。 このサンプルでは、{889C03C8-ABAD-4004-BF0A-BC7BB825E166} MsApoFxProxy CLSID を使用します。 CoCreate ing この GUID は MsApoFxProxy.dll IAudioProcessingObject インターフェイスを実装して、KSPROPSETID によって基になるドライバーのクエリ内のクラスをインスタンス化\_AudioEffectsDiscovery プロパティ セット。

このサンプルの INF ファイルを示しています、 \[BthHfAud\]で、このセクションで、 \[MsApoFxProxy.Registration\] wdmaudio.inf から\[BthHfAud.AnlgACapture.AddReg.Wave\]しこれ鍵を登録します\_FX\_EndpointEffectClsid MsApoFxProxy.dll の CLSID はよく知られているとします。

このサンプルの INF ファイルには、このシステムの効果の組み合わせの使用も示しています。

-   鍵\_FX\_鍵せず EndpointEffectClsid\_EFX\_ProcessingModes\_サポート\_の\_ストリーミング

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

このサンプルの INF ファイルを示しています、 \[MsApoFxProxy.Registration\]と\[MsApoFxProxy.AddReg\]セクション。 これで COM を使用して既知の GUID を登録、 \[MsApoFxProxy.CopyList\]セクション。 このセクションではコピー c: の MsApoFxProxy.dll\\Windows\\system32 します。

```inf
; wdmaudio.inf – this is where WmaLfxGfxDsp.dll is registered
...
;; MsApoFxProxy.Registration section can be called by OEM's to install the discover-effects APO
[MsApoFxProxy.Registration]
AddReg = MsApoFxProxy.AddReg
CopyFiles = MsApoFxProxy.CopyList

[MsApoFxProxy.CopyList]
MsApoFxProxy.dll,,,0x100
...
[MsApoFxProxy.AddReg]
; Discover Effects APO COM registration
HKCR,CLSID\%FX_DISCOVER_EFFECTS_APO_CLSID%,,,%FX_DiscoverEffectsApo_FriendlyName%
HKCR,CLSID\%FX_DISCOVER_EFFECTS_APO_CLSID%\InProcServer32,,,%11%\MsApoFxProxy.dll
HKCR,CLSID\%FX_DISCOVER_EFFECTS_APO_CLSID%\InProcServer32,ThreadingModel,,"Both"

; Discover Effects APO registration
HKCR,AudioEngine\AudioProcessingObjects\%FX_DISCOVER_EFFECTS_APO_CLSID%, "FriendlyName", ,%FX_DiscoverEffectsApo_FriendlyName%
HKCR,AudioEngine\AudioProcessingObjects\%FX_DISCOVER_EFFECTS_APO_CLSID%, "Copyright", ,%MsCopyRight%
HKCR,AudioEngine\AudioProcessingObjects\%FX_DISCOVER_EFFECTS_APO_CLSID%, "MajorVersion", 0x00010001, 1
HKCR,AudioEngine\AudioProcessingObjects\%FX_DISCOVER_EFFECTS_APO_CLSID%, "MinorVersion", 0x00010001, 1
HKCR,AudioEngine\AudioProcessingObjects\%FX_DISCOVER_EFFECTS_APO_CLSID%, "Flags", 0x00010001, 0x0000000d
HKCR,AudioEngine\AudioProcessingObjects\%FX_DISCOVER_EFFECTS_APO_CLSID%, "MinInputConnections", 0x00010001, 1
HKCR,AudioEngine\AudioProcessingObjects\%FX_DISCOVER_EFFECTS_APO_CLSID%, "MaxInputConnections", 0x00010001, 1
HKCR,AudioEngine\AudioProcessingObjects\%FX_DISCOVER_EFFECTS_APO_CLSID%, "MinOutputConnections", 0x00010001, 1
HKCR,AudioEngine\AudioProcessingObjects\%FX_DISCOVER_EFFECTS_APO_CLSID%, "MaxOutputConnections", 0x00010001, 1
HKCR,AudioEngine\AudioProcessingObjects\%FX_DISCOVER_EFFECTS_APO_CLSID%, "MaxInstances", 0x00010001, 0xffffffff
HKCR,AudioEngine\AudioProcessingObjects\%FX_DISCOVER_EFFECTS_APO_CLSID%, "NumAPOInterfaces", 0x00010001, 1
HKCR,AudioEngine\AudioProcessingObjects\%FX_DISCOVER_EFFECTS_APO_CLSID%, "APOInterface0", ,"{FD7F2B29-24D0-4B5C-B177-592C39F9CA10}"
...
```

## <a name="span-idaporegistrationspanspan-idaporegistrationspanspan-idaporegistrationspanapo-registration"></a><span id="APO_Registration"></span><span id="apo_registration"></span><span id="APO_REGISTRATION"></span>APO 登録


APO 登録は、重み付けの計算を使用してエンドポイントへの効果を動的に一致するプロセスをサポートするために使用されます。 重み付けの計算では、次のプロパティ ストアを使用します。 すべてのオーディオ インターフェイスが 0 個以上*エンドポイント プロパティ ストア*と*プロパティ ストアの効果*.inf を使用して、または実行時に登録します。 最も固有のエンドポイント プロパティ ストアと最も固有の効果プロパティ ストアは、重みが最も高い、使用されます。 他のすべてのプロパティ ストアは無視されます。

特異性は、次のように計算されます。

エンドポイント プロパティは、重み付けを格納します。

1. FX 特定 KSNODETYPE を
2. FX KSNODETYPE を\_ANY
3. 特定の KSNODETYPE で MSFX
4. KSNODETYPE で MSFX\_ANY

プロパティ ストアの重み付けの効果します。

1. 特定の KSNODETYPE で EP
2. EP KSNODETYPE で\_ANY
3. 特定の KSNODETYPE で MSEP
4. KSNODETYPE で MSEP\_ANY

番号は 0 から始まるし、連続して増加する必要があります。MSEP\\MSEP 0 の場合、\\1、…、MSEP\\n の場合 (たとえば) EP\\3 がない場合、Windows は EP 探して停止\\n、EP は表示されません\\が存在する場合でも、4

鍵の値\_FX\_(効果プロパティ ストア) の関連付けまたは鍵\_EP\_(エンドポイントのプロパティ ストア) のアソシエーションは、KSPINDESCRIPTOR と比較されます。カーネルのストリーミングで公開されていると、シグナル パスのハードウェアの最後に、暗証番号 (pin) ファクトリのカテゴリの値です。

MSEP と MSFX; のみ Microsoft インボックス クラス ドライバー (これは、サード パーティの開発者によってラップできる) を使用する必要があります。すべてのサード パーティ製ドライバーには、EP と FX を使用する必要があります。

**APO ノード型の互換性**

次のサンプルの INF ファイルは、鍵の設定を示しています。\_FX\_、APO に関連付けられている GUID への関連付けキー。

```inf
;; Property Keys
PKEY_FX_Association = "{D04E05A6-594B-4fb6-A80D-01AF5EED7D1D},0"
"
```

```inf
;; Key value pairs
HKR,"FX\\0",%PKEY_FX_Association%,,%KSNODETYPE_ANY%
```

オーディオのアダプターは複数の入力と出力をサポートできるため、カーネル、カスタム APO と互換性のある (KS) ノードの種類のストリームの種類を明示的に示す必要があります。 %Ksnodetype の KS ノードの種類を関連付けられる前の INF ファイルのフラグメントで、APO が示すように\_任意 % です。 この INF ファイル、KSNODETYPE 後半\_次のように定義されているは。

```inf
[Strings]
;; Define the strings used in MyINF.inf
...
KSNODETYPE_ANY      = "{00000000-0000-0000-0000-000000000000}"
KSNODETYPE_SPEAKER  = "{DFF21CE1-F70F-11D0-B917-00A0C9223196}"
...
```

値**NULL** KSNODETYPE の\_この APO が KS ノード型の任意の型と互換性があるいずれかのことを意味します。 、たとえば、あることを示す、APO のみ KSNODETYPE の KS ノードの種類と互換性のある\_講演者、INF ファイルは、KS ノード型および表示 APO アソシエーション次のようにします。

```inf
;; Key value pairs
...
HKR,"FX\\0",%PKEY_FX_Association%,,%KSNODETYPE_SPEAKER%
...
```

KS の各種ノードの GUID 値の詳細については、Ksmedia.h ヘッダー ファイルを参照してください。

## <a name="span-idtroubleshootingapoloadfailuresspanspan-idtroubleshootingapoloadfailuresspanspan-idtroubleshootingapoloadfailuresspantroubleshooting-apo-load-failures"></a><span id="Troubleshooting_APO_Load_Failures"></span><span id="troubleshooting_apo_load_failures"></span><span id="TROUBLESHOOTING_APO_LOAD_FAILURES"></span>APO 読み込みエラーのトラブルシューティング


以下のエラーを監視する方法を理解するため、次の情報が提供されます。 オーディオのグラフに組み込むの取得に失敗した APOs のトラブルシューティングを行うには、この情報を使用できます。

APO オーディオ システム モニターでは、グラフにパスワードが正常に組み込むかどうかを判断するコードを返します。 指定されたメソッドのいずれかに返される HRESULT 値を追跡することによって、これらのリターン コードを監視します。 SFX、MFX およびグラフに組み込まれている EFX APO ごとに個別の障害カウントの値が維持されます。

オーディオのシステムでは、次の 4 つのメソッドから返された HRESULT 値を監視します。

-   CoCreateInstance

-   IsInputFormatSupported

-   IsOutputFormatSupported

-   LockForProcess

エラー コードをこれらのメソッドのいずれかが戻るたびに、APO 障害カウントの値が増加します。 エラーの数が 0 にリセットされると、APO、オーディオのグラフに組み込むが正常であることを示すコードを返します。 呼び出しは成功、 [ **LockForProcess** ](https://docs.microsoft.com/windows/desktop/api/audioenginebaseapo/nf-audioenginebaseapo-iaudioprocessingobjectconfiguration-lockforprocess)メソッドは、APO が正常に組み込まれていることを示しています。

[ **CoCreateInstance** ](https://docs.microsoft.com/windows/desktop/api/combaseapi/nf-combaseapi-cocreateinstance)具体的には、さまざまな理由から返された HRESULT コードがエラーを示すことが理由があります。 次の 3 つの主な理由は次のとおりです。

-   グラフには、保護されたコンテンツが実行されていると、APO の署名が正しくありません。

-   APO が登録されていません。

-   APO は名前を変更または改ざんされています。

場合は、エラー、SFX の値のカウントが MFX または EFX APO がシステム指定の上限に達すると、SFX、MFX および EFX APOs が鍵を設定して無効になっても、\_エンドポイント\_を無効にする\_SysFx レジストリ キー '1' です。 現在、システム指定の上限は、10 の値です。

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック

[APO 効果を構成するための UI を実装します。](implementing-a-ui-for-configuring-apo-effects.md)  

[Windows オーディオ処理オブジェクト](windows-audio-processing-objects.md)  



