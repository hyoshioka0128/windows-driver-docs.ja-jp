---
title: ライセンス認証コンテキスト
description: ライセンス認証コンテキスト
ms.assetid: 76584379-2AEF-47e0-B14E-C7698903658F
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e971058f70649e42c7ec4cffc01d57416e4005ef
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67373036"
---
# <a name="activation-context"></a>ライセンス認証コンテキスト


TAEF は、テストを実行する必要があります アクティベーション コンテキストを指定するためのメカニズムを提供します。

アクティベーション コンテキストを提供することにより、ユーザーがサイド バイ サイド アセンブリのさまざまなシステム バイナリの特定のバージョンを選択します。 必要な 'アクティベーション コンテキスト' は、マニフェスト ファイルで指定され、'ActivationContext' プロパティを通じて TAEF に渡されることができます。 'ActivationContext' プロパティは、ランタイム パラメーター、またはテスト メタデータとして指定できます。

## <a name="span-idsampleactivationcontextmanifestfilespanspan-idsampleactivationcontextmanifestfilespanspan-idsampleactivationcontextmanifestfilespansample-activation-context-manifest-file"></a><span id="Sample_Activation_Context_manifest_file"></span><span id="sample_activation_context_manifest_file"></span><span id="SAMPLE_ACTIVATION_CONTEXT_MANIFEST_FILE"></span>サンプル アクティベーション コンテキストのマニフェスト ファイル


```cpp
<?xml version="1.0" encoding="UTF-8" standalone="yes"?>
<assembly xmlns="urn:schemas-microsoft-com:asm.v1" manifestVersion="1.0">
  <dependency>
    <dependentAssembly>
      <assemblyIdentity type="win32" name="Microsoft.Windows.Common-Controls" version="6.0.0.0" 
        processorArchitecture="*" publicKeyToken="6595b64144ccf1df"/>
    </dependentAssembly>
  </dependency>
</assembly>
```

マニフェスト ファイルを **'Comctlv6.manifest'** に表示される前のテストの実行時に使用される、comctl32.dll バージョン 6 を指定します。 マニフェスト ファイルの詳細については、次を参照してください[マニフェスト ファイルのリファレンス。](https://docs.microsoft.com/windows/desktop/SbsCs/manifest-files-reference)

## <a name="span-idspecifyingactivationcontextmanifestatthecommandpromptspanspan-idspecifyingactivationcontextmanifestatthecommandpromptspanspan-idspecifyingactivationcontextmanifestatthecommandpromptspanspecifying-activationcontext-manifest-at-the-command-prompt"></a><span id="Specifying_ActivationContext_manifest_at_the_Command_Prompt"></span><span id="specifying_activationcontext_manifest_at_the_command_prompt"></span><span id="SPECIFYING_ACTIVATIONCONTEXT_MANIFEST_AT_THE_COMMAND_PROMPT"></span>コマンド プロンプトで ActivationContext マニフェストを指定します。


``` syntax
te MyUnitTest.dll /ActivationContext:ComctlV6.manifest
```

このコマンドは、ComctlV6.manifest ファイルで指定されているアクティブ化コンテキストを使用して 'MyUnitTest.dll' のすべてのテストを実行します

## <a name="span-idspecifyingactivationcontextmanifestastestmetadataspanspan-idspecifyingactivationcontextmanifestastestmetadataspanspan-idspecifyingactivationcontextmanifestastestmetadataspanspecifying-activationcontext-manifest-as-test-metadata"></a><span id="Specifying_ActivationContext_manifest_as_Test_metadata"></span><span id="specifying_activationcontext_manifest_as_test_metadata"></span><span id="SPECIFYING_ACTIVATIONCONTEXT_MANIFEST_AS_TEST_METADATA"></span>テスト メタデータとして ActivationContext マニフェストを指定します。


特定テスト ケースのみが、指定したアクティブ化のコンテキストで実行する場合は、テスト メソッドで、マニフェスト ファイルに 'ActivationContext' プロパティの値を設定して、実行できます。 たとえば、次のテスト メソッドの宣言はテスト メソッドのみを既定のコンテキストでは、その他のテストの実行中にで指定されたアクティベーション コンテキストの下で ' MyTestMethod' に実行します。

```cpp
        BEGIN_TEST_METHOD(MyTestMethod)
            TEST_METHOD_PROPERTY(L"ActivationContext", L"ComctlV6.manifest")
        END_TEST_METHOD()
```

その他のメタデータ プロパティのようなクラスとアセンブリ レベルで 'ActivationContext' プロパティを設定できることに注意してください。









