---
title: APO 効果を構成するための UI の実装
description: このトピックでは、ユーザーが、効果を構成できるユーザー インターフェイス (UI) を実装する方法について説明します。
ms.assetid: C8D1CB20-2E77-430A-9933-4BDFFB997158
ms.date: 11/08/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1f5e67efffcf1228841b3bb454571d33c85d2c04
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67359931"
---
# <a name="implementing-a-ui-for-configuring-apo-effects"></a>APO 効果を構成するための UI の実装


このトピックでは、ユーザーが、効果を構成できるユーザー インターフェイス (UI) を実装する方法について説明します。 パスワードの詳細については、次を参照してください。[オーディオ処理オブジェクト アーキテクチャ](audio-processing-object-architecture.md)します。

## <a name="span-idoverviewspanspan-idoverviewspanspan-idoverviewspanoverview"></a><span id="Overview"></span><span id="overview"></span><span id="OVERVIEW"></span>概要


よく、APO は、ユーザーが、効果を構成できる UI を提供します。 この UI はたとえば、いくつかの異なるシグナル処理アルゴリズムから選択するユーザーを許可します。 Microsoft では、標準の Windows デバイスの構成 UI を提供します。 カスタム APO にユーザーがアクセスできる設定がある場合、開発者は、適切な構成 UI を提供する必要があります。 構成 UI はしたデバイス ドライバがインストールされているし、登録プロセスで、APO に関連付けられています。

**注**  製造元は、その APOs をサポートするように設計されたカスタム プロパティ ページでこのプロパティ ページを置き換えることができます。 そのカスタム APO にユーザーがアクセスできる設定がない場合は、製造元を持たない任意の UI をまったくこともできます。

 

標準の拡張設定 タブは、以下に示します。

![低音ブーストなどの機能強化を示すスピーカーのプロパティがそのプランの 4 つの効果をタブします。](images/audio-apo-enhancements-properties.png)

UI の機能強化の構成に使用できる 3 つのオプションは。

1. 鍵を指定しない\_SYSFX\_UiClsid – すべての拡張設定 タブは表示されません。
2. 指定の鍵\_SYSFX\_UiClsid の標準的な組み込みの拡張機能プロパティ ページの UI の CLSID はよく知られていると等しく、組み込みの機能拡張 タブが表示されます。
3. 独自のカスタムの CLSID を持つ独自のプロパティ ページを作成し、鍵を設定\_SYSFX\_UiClsid にカスタムの CLSID - と等しく、カスタム タブが表示されます。
このスクリーン ショットでは、SYSVAD スワップ APO サンプルのカスタム プロパティ ページを示します。

![スピーカーのプロパティ システムの効果を示すサンプル システムの構成の効果を提供するタブ](images/audio-apo-speaker-properties.png)

このスクリーン ショットでは、コントロール パネルの サウンド アプレットを示します。

![ヘッドホン仮想オーディオ デバイスを示すサウンドのプロパティ](images/audio-apo-sound-properties.png)

に、コントロール パネルのサウンド アプレットを新しいプロパティ ページを追加するには、システム提供のサウンド アプレットを新しいタブを追加する必要があります。 つまりカスタム APOs は登録されているし、初期化、それぞれのプロパティ ページは利用できること、システム提供の拡張機能ページと。 2 つの異なる画像のプロパティ ページにまたがって通信を実装する複雑な困難になります。 新しいプロパティ ページの機能設定をいくつかの機能強化のページで既定の設定が競合することになります。

したがって最も実用的なアプローチは、ここでは、システムが指定したパスワードを交換するために開発するカスタム APOs を構成するための個別の UI を実装します。

## <a name="span-idhowtoimplementauiforconfiguringtheeffectsspanspan-idhowtoimplementauiforconfiguringtheeffectsspanspan-idhowtoimplementauiforconfiguringtheeffectsspanhow-to-implement-a-ui-for-configuring-the-effects"></a><span id="How_to_Implement_a_UI_for_Configuring_the_Effects"></span><span id="how_to_implement_a_ui_for_configuring_the_effects"></span><span id="HOW_TO_IMPLEMENT_A_UI_FOR_CONFIGURING_THE_EFFECTS"></span>影響を構成するための UI を実装する方法


システムの効果の UI APO の CLSID は、オーディオ、エンドポイントのプロパティ ストアから使用できます。 オーディオのコントロール パネルの項目は、現在のコンテキスト内にあるオーディオ エンドポイントからこの CLSID を取得します。 オーディオ コントロール パネル項目には、適切なカスタム システム エフェクト UI が起動したら、渡します、オーディオのエンドポイント。 UI を読み取ってプロパティの設定を調整するエンドポイントのプロパティ ストアにアクセスできます。 他のプログラム設定を変更する場合に、UI のプロパティ ストアの通知を登録する必要がありますも。

使用してカスタム APO を設計する場合は、 **CBaseAudioProcessingObject**基底クラスとシステム提供の APOs をラップする、既定のプロパティ ページを置き換えることができます。

Microsoft では、コントロール パネルのサウンド アプレットの拡張機能プロパティ ページを提供します。 これは、システムのシステム提供の効果 APO に関連付けられている既定のプロパティ ページです。 ベンダーは、実装およびカスタム プロパティ ページのプロバイダーの登録をカスタムのページでこの既定のプロパティ ページを置換できます。

参照してください[プロパティ シートについて](https://go.microsoft.com/fwlink/p/?linkid=106006)拡張機能のプロパティ ページを交換する方法についてはします。

を設計およびカスタム プロパティ ページのプロバイダーを実装するには、次の手順を実行します。

1.  カスタム プロパティ ページを作成します。 参照してください[プロパティ シートを作成する](https://go.microsoft.com/fwlink/p/?linkid=106006)詳細についてはします。

2.  プロパティ ページを DLL としてパッケージ化します。 参照してください[の作成と DLL を使用する](https://go.microsoft.com/fwlink/p/?linkid=106014)カスタム ページの DLL としてパッケージ化の詳細についてはトピック。

3.  変更、 [INF ファイル](https://docs.microsoft.com/windows-hardware/drivers/install/overview-of-inf-files)をインストールし、プロパティ ページの DLL を登録します。

    次の INF ファイル フラグメントは、カスタム プロパティ ページを登録する INF ファイルを変更する方法を示します。

    ```inf
    [SysFx.AddReg]
    ...
    HKR,"FX\\0",%PKEY_SYSFX_UiClsid%,,%SYSFX_UI_CLSID%
    ...
    [Strings]
    PKEY_SYSFX_UiClsid = "{D04E05A6-594B-4FB6-A80D-01AF5EED7D1D},3"
    SYSFX_UI_CLSID     = "{YOUR GUID GOES HERE}"
    ```

    上記の INF ファイルの手順の結果として、インストール プロセス、適切なレジストリ キーを変更次のようにします。

    ```text
    HKLM
     SOFTWARE
      Microsoft
      Windows
       CurrentVersion
      MMDevices
      Audio
       Render
      Endpoint
      FXProperties
       ...
      "{D04E05A6-594B-4FB6-A80D-01Af5EED7D1D},3"=
                         "{YOUR CLSID GOES HERE}"
    ```

    既定のプロパティ ページの CLSID は、カスタム プロパティ ページの CLSID に置き換えられます。

4.  INF ファイルでグローバル AddReg セクションで、com、CLSID を登録します

    SYSVAD tabletaudiosample.inf ファイルから取得した、サンプル INF ファイルのセクションでは、これを行う方法を示します。 \[SWAPAPO します。AddReg\]セクションは、グローバル AddReg セクションでは。 \[SWAPAPO します。I.Association0.AddReg\] AddReg セクションの一部が、特定の KSCATEGORY\_オーディオ インターフェイス。

    ```inf
    [SWAPAPO.AddReg]
    …

    ; Effects UI page COM registration
    HKCR,CLSID\%FX_UI_CLSID%,,,"CplPage Class"
    HKCR,CLSID\%FX_UI_CLSID%\InProcServer32,,,%11%\PropPageExt.dll
    HKCR,CLSID\%FX_UI_CLSID%\InProcServer32,ThreadingModel,,"Apartment"
    …

    [SWAPAPO.I.Association0.AddReg]
    …

    HKR,FX\0,%PKEY_FX_UserInterfaceClsid%,,%FX_UI_CLSID%

    …
    [Strings]
    FX_UI_CLSID     = "{YOUR GUID GOES HERE}"
     
    ```

**使用して、または windows 効果の折り返し**

Windows で提供される効果を直接使用または、それらをラップする場合は、次の手順を完了します。

1.  効果のプロパティ ストアに、CLSID を登録する、上の 3 つの手順に従います。

2.  手順 4 の上、CLSID を COM に登録するには 使用して指定された wdmaudio.inf を呼び出す必要がありますがさらに、 *Include*と*必要がある*INF でステートメントが次に示すようにファイルします。

    ```cpp
    [YourGlobalSection]
    Include=wdmaudio.inf
    Needs=mssysfx.CopyFilesAndRegister
    ```

## <a name="span-idsysvadswapapouisamplecodespanspan-idsysvadswapapouisamplecodespanspan-idsysvadswapapouisamplecodespansysvad-swapapo-ui-sample-code"></a><span id="SYSVAD_SwapAPO_UI_Sample_Code"></span><span id="sysvad_swapapo_ui_sample_code"></span><span id="SYSVAD_SWAPAPO_UI_SAMPLE_CODE"></span>SYSVAD SwapAPO UI のサンプル コード


コード サンプルをテンプレートとしては、SYVAD スワップ APO を使用してカスタム APO 開発プロセスを推し進めることができます。 スワップ APO サンプルについては、次を参照してください。[オーディオ処理オブジェクトを実装する](implementing-audio-processing-objects.md)します。

**コード例**

ある SYSVAD サンプル、PropPageExtensions プロジェクトに 6 つのプロジェクトにはプロパティ ページの例 APO のサンプル コードが含まれています。

|                    |                                                            |
|--------------------|------------------------------------------------------------|
| **プロジェクト**        | **説明**                                            |
| PropPageExtensions | サンプル コードなどのカスタム プロパティ ページの UI 拡張機能 |

 

次のコード サンプルでは、カスタム UI の開発に取り組む確認に役立ちます。

|                         |                                                                                                      |
|-------------------------|------------------------------------------------------------------------------------------------------|
| **名前**                | **説明**                                                                                      |
| SwapPropPage.cpp        | CSwapPropPage クラスの実装                                                            |
| CplExt.cpp              | コントロール パネルの拡張機能の DLL のエクスポートの実装                                       |
| UIWidgets.cpp           | CUIWidget と派生クラスの実装                                                      |
| AdvEndpointPropPage.cpp | CAdvEndpointPropPage の実装                                                               |
| Parts.cpp               | CPart と派生クラスの実装です。                                                         |
| TopologyExaminers.cpp   | コネクタとエンドポイントなど、オーディオのトポロジを調べることをサポートするメソッドの実装です。 |

 

次のヘッダー ファイルは、プロパティ ページの拡張機能サンプルで使用されます。

|                       |
|-----------------------|
| **名前**              |
| swapproppage.h        |
| uiwidgets.h           |
| advendpointproppage.h |
| parts.h               |
| topologyexaminers.h   |

 

PropPageExtensions サンプルを理解して、ヘッダーを確認し、[プロパティ] ページのテキストの定義に関連するソース コードを確認することがあります。 お客様の要件が、サンプル コードの説明のような場合は、作成し、カスタム UI ページを更新するコードの大部分を再利用することができます。

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック
[オーディオ処理オブジェクト アーキテクチャ](audio-processing-object-architecture.md)  
[Windows オーディオ処理オブジェクト](windows-audio-processing-objects.md)  
[オーディオ処理オブジェクトの実装](implementing-audio-processing-objects.md)  



