---
title: APO 効果を構成するための UI の実装
description: このトピックでは、ユーザーが効果を構成できるようにするユーザーインターフェイス (UI) を実装する方法について説明します。
ms.assetid: C8D1CB20-2E77-430A-9933-4BDFFB997158
ms.date: 10/07/2019
ms.localizationpriority: medium
ms.openlocfilehash: d5fef103f27a884bb808e99878e8a511b3b17617
ms.sourcegitcommit: bff7fdcac628f8b62bd9df2658ca56301d1f8b07
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/08/2019
ms.locfileid: "72030805"
---
# <a name="implementing-a-ui-for-configuring-apo-effects"></a>APO 効果を構成するための UI の実装

このトピックでは、ユーザーが効果を構成できるようにするユーザーインターフェイス (UI) を実装する方法について説明します。 APOs に関する一般的な情報については、「[オーディオ処理オブジェクトのアーキテクチャ](audio-processing-object-architecture.md)」を参照してください。

## <a name="span-idoverviewspanspan-idoverviewspanspan-idoverviewspanoverview"></a><span id="Overview"></span><span id="overview"></span><span id="OVERVIEW"></span>概要

> [!NOTE]
> このカスタマイズは、Windows 10 バージョン1809以降ではサポートされなくなりました。また、PropPageExtensions プロジェクトが Sysvad サンプルに存在しなくなりました。 Windows の新しいバージョンでは、ハードウェアサポートアプリを作成することをお勧めします。 詳しくは、「[ハードウェア サポート アプリ (HSA):Steps for Driver Developers (ハードウェア サポート アプリ (HSA): ドライバー開発者向け手順)](https://docs.microsoft.com/windows-hardware/drivers/devapps/hardware-support-app--hsa--steps-for-driver-developers)」をご覧ください。
>

APO は一般に、ユーザーが効果を構成するための UI を提供します。 たとえば、この UI では、さまざまなシグナル処理アルゴリズムからユーザーが選択できるようにすることができます。 Microsoft では、標準の Windows APOs 用の構成 UI を提供しています。 カスタム APO にユーザーがアクセスできる設定がある場合、開発者は適切な構成 UI を提供する必要があります。 構成 UI はデバイスドライバーと共にインストールされ、登録プロセスによって APO に関連付けられます。

**注**   の製造元は、このプロパティページを APOs をサポートするように設計されたカスタムプロパティページに置き換えることができます。 カスタム APO にユーザーがアクセスできる設定がない場合、製造元は UI をまったく使用しないことも選択できます。

[標準の拡張] タブを次に示します。

![低音ブーストなど4つの効果を提供する [拡張] タブを表示するスピーカーのプロパティ](images/audio-apo-enhancements-properties.png)

[拡張機能の構成] UI では、次の3つのオプションを使用できます。

1. No PKEY @ no__t-0SYSFX @ no__t-1UiClsid all – [拡張なし] タブが表示されます。
2. PKEY @ no__t-0SYSFX @ no__t を指定します。標準の組み込み機能拡張プロパティページの UI の既知の CLSID と同じです。組み込みの [拡張機能] タブが表示されます。
3. 独自のカスタム CLSID を使用して独自のプロパティページを作成し、PKEY @ no__t-0SYSFX @ no__t をカスタム CLSID に設定します。カスタムタブが表示されます。
このスクリーンショットは、SYSVAD Swap APO サンプルのカスタムプロパティページを示しています。

![システム効果の構成を提供するシステム効果のサンプルタブを表示するスピーカーのプロパティ](images/audio-apo-speaker-properties.png)

このスクリーンショットは、コントロールパネルの [サウンド] アプレットを示しています。

![ヘッドホン仮想オーディオデバイスを示すサウンドプロパティ](images/audio-apo-sound-properties.png)

コントロールパネルの [サウンド] アプレットに新しいプロパティページを追加するには、システムによって提供されるサウンドアプレットに新しいタブを追加する必要があります。 つまり、カスタム APOs が登録され初期化されると、そのプロパティページがシステムによって提供される拡張機能ページと共に使用できるようになります。 2つの異なる APOs のプロパティページ間で通信を実装することは困難で複雑です。 [拡張] ページの一部の既定の設定が、[新しいプロパティ] ページの機能設定と競合する可能性があります。

そのため、ここで最も実用的な方法は、システムで指定された APOs を置き換えるために開発したカスタム APOs を構成するための個別の UI を実装することです。

## <a name="span-idhow_to_implement_a_ui_for_configuring_the_effectsspanspan-idhow_to_implement_a_ui_for_configuring_the_effectsspanspan-idhow_to_implement_a_ui_for_configuring_the_effectsspanhow-to-implement-a-ui-for-configuring-the-effects"></a><span id="How_to_Implement_a_UI_for_Configuring_the_Effects"></span><span id="how_to_implement_a_ui_for_configuring_the_effects"></span><span id="HOW_TO_IMPLEMENT_A_UI_FOR_CONFIGURING_THE_EFFECTS"></span>効果を構成するための UI を実装する方法


システム効果の UI APO の CLSID は、オーディオエンドポイントのプロパティストアから取得できます。 [オーディオコントロールパネル] 項目は、現在コンテキスト内にあるオーディオエンドポイントからこの CLSID を取得します。 [オーディオコントロールパネル] 項目が、適切なカスタムシステム効果 UI を起動すると、それにオーディオエンドポイントが渡されます。 その後、UI はエンドポイントプロパティストアにアクセスして、プロパティ設定の読み取りと調整を行うことができます。 他のプログラムが設定を変更した場合に備えて、UI はプロパティストアの通知にも登録する必要があります。

**Cbaseaudioprocessingobject**基本クラスを使用してカスタム APO を設計し、システムによって提供される APOs をラップする場合は、既定のプロパティページを置き換えることができます。

Microsoft では、コントロールパネルの [サウンド] アプレットの拡張機能プロパティページを提供しています。 これは、システムによって提供されるシステム効果 APO に関連付けられている既定のプロパティページです。 ベンダーは、カスタムプロパティページプロバイダーを実装して登録することで、この既定のプロパティページをカスタムページに置き換えることができます。

拡張機能プロパティページを置き換える方法については、「[プロパティシートについ](https://go.microsoft.com/fwlink/p/?linkid=106006)て」を参照してください。

カスタムプロパティページプロバイダーを設計および実装するには、次の手順を実行します。

1. カスタムプロパティページを作成します。 詳細については、「[プロパティシートの作成](https://go.microsoft.com/fwlink/p/?linkid=106006)」を参照してください。

2. プロパティページを DLL としてパッケージ化します。 カスタムページを DLL としてパッケージ化する方法の詳細については、「 [dll の作成と使用](https://go.microsoft.com/fwlink/p/?linkid=106014)」を参照してください。

3. [INF ファイル](https://docs.microsoft.com/windows-hardware/drivers/install/overview-of-inf-files)を変更して、プロパティページの DLL をインストールして登録します。

    次の INF ファイルフラグメントは、カスタムプロパティページを登録するように INF ファイルを変更する方法を示しています。

    ```inf
    [SysFx.AddReg]
    ...
    HKR,"FX\\0",%PKEY_SYSFX_UiClsid%,,%SYSFX_UI_CLSID%
    ...
    [Strings]
    PKEY_SYSFX_UiClsid = "{D04E05A6-594B-4FB6-A80D-01AF5EED7D1D},3"
    SYSFX_UI_CLSID     = "{YOUR GUID GOES HERE}"
    ```

    また、上記の INF ファイルの指示に従って、インストールプロセスによって適切なレジストリキーが次のように変更されます。

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

    既定のプロパティページの CLSID は、カスタムプロパティページの CLSID に置き換えられます。

4. INF ファイルの global AddReg セクションで、CLSID を COM に登録します。

    SYSVAD tabletaudiosample ファイルから抜粋したサンプルの INF ファイルセクションでは、その方法を示しています。 @No__t-0SWAPAPO @ no__t セクションは、グローバル AddReg セクションにあります。 @No__t-0SWAPAPO. AddReg @ no__t-1 は、特定の KSCATEGORY @ no__t-2AUDIO インターフェイスの AddReg セクションの一部です。

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

**使用またはラップ (windows の効果を)**

Windows によって提供される効果を直接使用する場合、またはラップする場合は、次の手順を実行します。

1. 上記の手順3に従って、効果プロパティストアに CLSID を登録します。

2. 上記の手順4に従って、CLSID を COM に登録します。 さらに、次に示すように、インクルードおよび*必要*なステートメントを使用して、指定された wdmaudio を*インクルード*し、inf ファイルで呼び出す必要があります。

    ```cpp
    [YourGlobalSection]
    Include=wdmaudio.inf
    Needs=mssysfx.CopyFilesAndRegister
    ```

## <a name="span-idsysvad_swapapo_ui_sample_codespanspan-idsysvad_swapapo_ui_sample_codespanspan-idsysvad_swapapo_ui_sample_codespansysvad-swapapo-ui-sample-code"></a><span id="SYSVAD_SwapAPO_UI_Sample_Code"></span><span id="sysvad_swapapo_ui_sample_code"></span><span id="SYSVAD_SWAPAPO_UI_SAMPLE_CODE"></span>SYSVAD SwapAPO UI サンプルコード


SYVAD Swap APO コードサンプルをテンプレートとして使用すると、カスタムの APO 開発プロセスを高速化できます。 スワップ APO サンプルに関する一般的な情報については、「[オーディオ処理オブジェクトの実装](implementing-audio-processing-objects.md)」を参照してください。

## <a name="span-idrelated_topicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック
[オーディオ処理オブジェクトのアーキテクチャ](audio-processing-object-architecture.md)  
[Windows オーディオ処理オブジェクト](windows-audio-processing-objects.md)  
[オーディオ処理オブジェクトの実装](implementing-audio-processing-objects.md)  
