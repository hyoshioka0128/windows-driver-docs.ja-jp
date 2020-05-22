---
title: カーネル モード ドライバーへのイベント トレーシングの追加
description: カーネル モード ドライバーへのイベント トレーシングの追加
ms.assetid: 74fdb4b2-aad1-4d8a-b146-40a92e1fdbb5
keywords:
- Windows イベントトレーシング WDK、カーネルモード
- ETW WDK、カーネルモード
- カーネルモード ETW WDK ソフトウェアトレース
ms.date: 07/09/2018
ms.localizationpriority: medium
ms.openlocfilehash: b100f9e1be8712a4b9a43cde86cd2721b048ac42
ms.sourcegitcommit: cbcb712a9f1f62c7d67e1b98097a0d8d24bd0c71
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/21/2020
ms.locfileid: "83769506"
---
# <a name="adding-event-tracing-to-kernel-mode-drivers"></a>カーネル モード ドライバーへのイベント トレーシングの追加

このセクションでは、Windows イベントトレーシング (ETW) カーネルモード API を使用して、カーネルモードドライバーにイベントトレースを追加する方法について説明します。 ETW カーネルモード API は Windows Vista で導入されましたが、以前のオペレーティングシステムではサポートされていません。 ドライバーが Windows 2000 以降のトレース機能をサポートする必要がある場合は、 [WPP ソフトウェアトレース](wpp-software-tracing.md)または[WMI イベントトレース](https://docs.microsoft.com/windows-hardware/drivers/kernel/wmi-event-tracing)を使用します。

> [!TIP]
> Windows Driver Kit (WDK) 8.1 および Visual Studio を使用して ETW を実装する方法を示すサンプルコードを表示するには、 [Eventdrv サンプル](https://docs.microsoft.com/samples/microsoft/windows-driver-samples/eventdrv/)を参照してください。

このセクションの内容は次のとおりです。

- [ワークフロー-カーネルモードドライバーへのイベントトレースの追加](#workflow---adding-event-tracing-to-kernel-mode-drivers)

- [1. 発生させるイベントの種類と、イベントを発行する場所を決定します。](#1-decide-the-type-of-events-to-raise-and-where-to-publish-them)

- [2. プロバイダー、イベント、およびチャネルを定義するインストルメンテーションマニフェストを作成する](#2-create-an-instrumentation-manifest-that-defines-the-provider-the-events-and-channels)

- [3. メッセージコンパイラ (Mc) を使用して、インストルメンテーションマニフェストをコンパイルします。](#3-compile-the-instrumentation-manifest-by-using-the-message-compiler-mcexe)

- [4. 生成されたコードを追加して、イベントの発生 (発行) を行います (イベントの登録、登録解除、および書き込み)](#4-add-the-generated-code-to-raise-publish-the-events-register-unregister-and-write-events)

- [5. ドライバーをビルドする](#5-build-the-driver)

- [6. マニフェストをインストールする](#6-install-the-manifest)

- [7. ETW のサポートを確認するためにドライバーをテストする](#7-test-the-driver-to-verify-etw-support)

## <a name="workflow---adding-event-tracing-to-kernel-mode-drivers"></a>ワークフロー-カーネルモードドライバーへのイベントトレースの追加

![カーネルモードドライバーにイベントトレースを追加するプロセスの概要。](images/etw-km-process.png)

## <a name="1-decide-the-type-of-events-to-raise-and-where-to-publish-them"></a>1. 発生させるイベントの種類と、イベントを発行する場所を決定します。

コーディングを開始する前に、ドライバーが Windows イベントトレーシング (ETW) を使用してログに記録するイベントの種類を決定する必要があります。 たとえば、ドライバーの配布後に問題を診断するのに役立つイベントや、ドライバーの開発に役立つイベントをログに記録することができます。 イベントの種類は、チャネルで識別されます。 *チャネル*は、"管理者"、"運用"、"分析"、または "デバッグ" という種類のイベントの名前付きストリームで、テレビチャネルに似ています。 チャネルは、イベントプロバイダーからイベントログとイベントコンシューマーにイベントを配信します。 詳細については、「 [Windows イベントログのリファレンス](https://docs.microsoft.com/windows/win32/wes/windows-event-log-reference)」を参照してください。

開発時には、コードのデバッグに役立つトレースイベントを使用するのが最も一般的です。 この同じチャネルは、ドライバーが展開された後に発生する可能性がある問題のトラブルシューティングを行うために、実稼働コードでも使用できます。 パフォーマンスの測定に使用できるイベントをトレースすることもできます。これらのイベントは、IT プロフェッショナルがサーバーのパフォーマンスを微調整し、ネットワークのボトルネックを特定するのに役立ちます。

## <a name="2-create-an-instrumentation-manifest-that-defines-the-provider-the-events-and-channels"></a>2. プロバイダー、イベント、およびチャネルを定義するインストルメンテーションマニフェストを作成する

インストルメンテーションマニフェストは、プロバイダーが発生させるイベントの正式な説明を提供する XML ファイルです。 インストルメンテーションマニフェストは、イベントプロバイダーを識別し、チャネルまたはチャネル (最大8つ) を指定して、イベントとイベントが使用するテンプレートについて説明します。 さらに、インストルメンテーションマニフェストでは、文字列のローカライズが可能なので、トレースメッセージをローカライズできます。 イベントシステムとイベントコンシューマーは、マニフェストに用意されている構造化 XML データを使用して、クエリと分析を実行できます。

インストルメンテーションマニフェストの詳細については、「[インストルメンテーションマニフェスト (windows) の作成](https://docs.microsoft.com/windows/desktop/WES/writing-an-instrumentation-manifest)」および「 [windows イベントログの使用 (windows)](https://docs.microsoft.com/windows/desktop/WES/using-windows-event-log)」を参照してください。

> [!NOTE]
> インストルメンテーションマニフェストは手動で作成できますが、 \\ \\ \\ \\ \\ WDK と Visual Studio をインストールするときに、% windowssdkdir% Bin x64% windowssdkdir% bin x86 フォルダーに含まれている ECManGen ツールの使用を検討する必要があります。 % WindowsSdkDir% は、このバージョンの WDK がインストールされている Windows kit ディレクトリへのパスを表します。たとえば、C: \\ Program Files (x86) \\ Windows kit \\ 8.1 です。 ECManGen は、XML タグを使用することなく、最初からマニフェストを作成するためのガイドとなるアプリケーションです。 このツールを使用すると、「[インストルメンテーションマニフェスト (windows) の記述](https://docs.microsoft.com/windows/desktop/WES/writing-an-instrumentation-manifest)」セクションおよび「 [eventmanifest スキーマ (windows)](https://docs.microsoft.com/windows/desktop/WES/eventmanifestschema-schema) 」セクションで情報を把握することができます。

次のインストルメンテーションマニフェストは、"Sample Driver" という名前を使用するイベントプロバイダーを示しています。 この名前は、ドライバーのバイナリと同じ名前である必要はありません。 マニフェストでは、プロバイダーの GUID と、メッセージとリソースファイルへのパスも指定します。 メッセージとリソースファイルを使用すると、ETW は、イベントのデコードとレポートに必要なリソースの場所を特定できます。 これらのパスは、ドライバー (.sys) ファイルの場所を指します。 ドライバーは、ターゲットコンピューター上の指定されたディレクトリにインストールされている必要があります。

この例では、名前付きチャネル**システム**を使用します。これは、種類が**Admin**のイベントのチャネルです。このチャネルは、Windows Driver Kit (WDK) の% WindowsSdkDir% include um ディレクトリに用意されている Winmeta .xml ファイルで定義されてい \\ \\ ます。 システム**チャネルは**、システムサービスアカウントで実行されているアプリケーションに対してセキュリティで保護されます。 マニフェストには、イベントが発行されたときに提供されたデータの種類と、その静的コンテンツと動的コンテンツを示すイベントテンプレートが含まれています。 このマニフェスト例 `StartEvent` では、、、およびの3つのイベントを定義し `SampleEventA` `UnloadEvent` ます。

チャネルに加えて、イベントをレベルとキーワードに関連付けることができます。 キーワードおよびレベルを使用すると、イベントを有効にしたり、イベントがパブリッシュされたときにイベントをフィルター処理するためのメカニズムを提供したりできます。 キーワードを使用すると、論理的に関連するイベントをまとめてグループ化できます。 レベルは、イベントの重大度または詳細度 (重大、エラー、警告、情報など) を示すために使用できます。 Winmeta .xml ファイルには、イベント属性の定義済みの値が含まれています。

イベントペイロード (イベントメッセージ、データ) のテンプレートを作成する場合は、入力と出力の種類を指定する必要があります。 サポートされている型については、「 [**InputType 複合型 (Windows)**](https://docs.microsoft.com/windows/desktop/WES/eventmanifestschema-inputtype-complextype)」の「解説」を参照してください。

```XML
<?xml version='1.0' encoding='utf-8' standalone='yes'?>
<instrumentationManifest
    xmlns="http://schemas.microsoft.com/win/2004/08/events"
    xmlns:win="http://manifests.microsoft.com/win/2004/08/windows/events"
    xmlns:xs="http://www.w3.org/2001/XMLSchema"
    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xsi:schemaLocation="http://schemas.microsoft.com/win/2004/08/events eventman.xsd"
    >
  <instrumentation>
    <events>
      <provider
          guid="{b5a0bda9-50fe-4d0e-a83d-bae3f58c94d6}"
          messageFileName="%SystemDrive%\ETWDriverSample\Eventdrv.sys"
          name="Sample Driver"
          resourceFileName="%SystemDrive%\ETWDriverSample\Eventdrv.sys"
          symbol="DriverControlGuid"
          >
        <channels>
          <importChannel
              chid="SYSTEM"
              name="System"
              />
        </channels>
        <templates>
          <template tid="tid_load_template">
            <data
                inType="win:UInt16"
                name="DeviceNameLength"
                outType="xs:unsignedShort"
                />
            <data
                inType="win:UnicodeString"
                name="name"
                outType="xs:string"
                />
            <data
                inType="win:UInt32"
                name="Status"
                outType="xs:unsignedInt"
                />
          </template>
          <template tid="tid_unload_template">
            <data
                inType="win:Pointer"
                name="DeviceObjPtr"
                outType="win:HexInt64"
                />
          </template>
        </templates>
        <events>
          <event
              channel="SYSTEM"
              level="win:Informational"
              message="$(string.StartEvent.EventMessage)"
              opcode="win:Start"
              symbol="StartEvent"
              template="tid_load_template"
              value="1"
              />
          <event
              channel="SYSTEM"
              level="win:Informational"
              message="$(string.SampleEventA.EventMessage)"
              opcode="win:Info"
              symbol="SampleEventA"
              value="2"
              />
          <event
              channel="SYSTEM"
              level="win:Informational"
              message="$(string.UnloadEvent.EventMessage)"
              opcode="win:Stop"
              symbol="UnloadEvent"
              template="tid_unload_template"
              value="3"
              />
        </events>
      </provider>
    </events>
  </instrumentation>
  <localization xmlns="http://schemas.microsoft.com/win/2004/08/events">
    <resources culture="en-US">
      <stringTable>
        <string
            id="StartEvent.EventMessage"
            value="Driver Loaded"
            />
        <string
            id="SampleEventA.EventMessage"
            value="IRP A Occurred"
            />
        <string
            id="UnloadEvent.EventMessage"
            value="Driver Unloaded"
            />
      </stringTable>
    </resources>
  </localization>
</instrumentationManifest>
```

## <a name="3-compile-the-instrumentation-manifest-by-using-the-message-compiler-mcexe"></a>3. メッセージコンパイラ (Mc) を使用して、インストルメンテーションマニフェストをコンパイルします。

ソースコードをコンパイルする前に、[メッセージコンパイラ (Mc)](https://docs.microsoft.com/windows/desktop/WES/message-compiler--mc-exe-)を実行する必要があります。 メッセージコンパイラは、Windows Driver Kit (WDK) に含まれています。 メッセージコンパイラは、イベントプロバイダー、イベント属性、チャネル、およびイベントの定義を含むヘッダーファイルを作成します。 ソース コードには、このヘッダー ファイルをインクルードする必要があります。 また、生成されたリソースコンパイラスクリプト ( \* .rc) と、リソースコンパイラスクリプトに含まれる生成された .bin ファイル (バイナリリソース) も、メッセージコンパイラによって配置されます。

この手順は、いくつかの方法でビルド処理の一部として含めることができます。

- ( [Eventdrv サンプル](https://docs.microsoft.com/samples/microsoft/windows-driver-samples/eventdrv/)に示されているように) メッセージコンパイラタスクをドライバープロジェクトファイルに追加します。

- Visual Studio を使用して、インストルメンテーションマニフェストを追加し、メッセージコンパイラプロパティを構成します。

**メッセージコンパイラタスクをプロジェクトファイルに追加する**ビルドプロセスでメッセージコンパイラを含める方法の例については、 [Eventdrv サンプル](https://docs.microsoft.com/samples/microsoft/windows-driver-samples/eventdrv/)のプロジェクトファイルを参照してください。 Eventdrv .vcxproj ファイルには、メッセージコンパイラを呼び出す** &lt; MessageCompile &gt; **セクションがあります。 メッセージコンパイラは、マニフェストファイル (evntdrv) を入力として使用して、ヘッダーファイル evntdrvEvents を生成します。 また、生成された RC ファイルのパスを指定し、カーネルモードのログ記録マクロを有効にします。 このセクションをコピーし、ドライバープロジェクトファイル (.vcxproj) に追加することができます。

```XML

    <MessageCompile Include="evntdrv.xml">
      <GenerateKernelModeLoggingMacros>true</GenerateKernelModeLoggingMacros>
      <HeaderFilePath>.\$(IntDir)</HeaderFilePath>
      <GeneratedHeaderPath>true</GeneratedHeaderPath>
      <WinmetaPath>"$(SDK_INC_PATH)\winmeta.xml"</WinmetaPath>
      <RCFilePath>.\$(IntDir)</RCFilePath>
      <GeneratedRCAndMessagesPath>true</GeneratedRCAndMessagesPath>
      <GeneratedFilesBaseName>evntdrvEvents</GeneratedFilesBaseName>
      <UseBaseNameOfInput>true</UseBaseNameOfInput>
    </MessageCompile>
```

Eventdrv サンプルをビルドすると、Visual Studio によってイベントトレースに必要なファイルが作成されます。 また、ドライバープロジェクトのリソースファイルの一覧に evntdrv マニフェストを追加します。 マニフェストを右クリックすると、メッセージコンパイラのプロパティページが表示されます。

### <a name="using-visual-studio-to-add-the-instrumentation-manifest"></a>Visual Studio を使用したインストルメンテーションマニフェストの追加

インストルメンテーションマニフェストをドライバープロジェクトに追加し、メッセージコンパイラプロパティを構成して、必要なリソースファイルとヘッダーファイルを作成できます。

### <a name="to-add-the-instrumentation-manifest-to-the-project-using-visual-studio"></a>Visual Studio を使用してインストルメンテーションマニフェストをプロジェクトに追加するには

1. ソリューションエクスプローラーで、マニフェストファイルをドライバープロジェクトに追加します。 [**リソースファイル] [既存の &gt; &gt; 項目の追加**] (たとえば、evntdrv または mydriver. man) を右クリックします。

2. 追加したファイルを右クリックし、[プロパティページ] を使用して項目の種類を**MessageCompile**に変更し、[**適用**] をクリックします。

3. メッセージコンパイラのプロパティが表示されます。 [**全般**設定] で、次のオプションを設定し、[**適用**] をクリックします。

    | 全般                                 | 設定       |
    |-----------------------------------------|---------------|
    | **Generate Kernel Mode Logging Macros (カーネル モード ログ記録マクロを生成する)** | **はい (-km)** |
    | **入力の基本名を使用する**              | **はい (-b)**  |

4. [**ファイルオプション**] で、次のオプションを設定し、[**適用**] をクリックします。

    | ファイル オプション                                    | 設定         |
    |-------------------------------------------------|-----------------|
    | **親カウンターのヘッダーファイルを生成します** | **はい**         |
    | **Header File Path (ヘッダー ファイル パス)**                            | **$(IntDir)**   |
    | **Generated RC and Binary Message Files Path (生成される RC ファイルとバイナリ メッセージ ファイルのパス)**  | **はい**         |
    | **RC File Path (RC ファイル パス)**                                | **$(IntDir)**   |
    | **Generated Files Base Name (生成されるファイルのベース名)**                   | **$ (ファイル名)** |

既定では、メッセージコンパイラは、生成するファイルのベース名として、入力ファイルのベース名を使用します。 ベース名を指定するには、[**生成されたファイルのベース名**(-z)] フィールドを設定します。 Eventdr のサンプルでは、ベース名が*evntdrvEvents*に設定され、evntdrv に含まれるヘッダーファイル evntdrvEvents の名前と一致するようになっています。

> [!NOTE]
> 生成された .rc ファイルを Visual Studio プロジェクトに含めないと、マニフェストファイルのインストール時に見つからないリソースに関するエラーメッセージが表示される場合があります。

## <a name="4-add-the-generated-code-to-raise-publish-the-events-register-unregister-and-write-events"></a>4. 生成されたコードを追加して、イベントの発生 (発行) を行います (イベントの登録、登録解除、および書き込み)

インストルメンテーションマニフェストでは、イベントプロバイダーの名前とイベント記述子を定義しています。 メッセージコンパイラを使用してインストルメンテーションマニフェストをコンパイルすると、メッセージコンパイラによって、リソースを説明するヘッダーファイルが生成され、イベントのマクロも定義されます。 ここで、生成されたコードをドライバーに追加して、これらのイベントを発生させる必要があります。

1. ソースファイルで、メッセージコンパイラ (MC) によって生成されるイベントヘッダーファイルをインクルードします。 たとえば、 [Eventdrv サンプル](https://docs.microsoft.com/samples/microsoft/windows-driver-samples/eventdrv/)では、Evntdrv ソースファイルに、前の手順で生成されたヘッダーファイル (evntdrvEvents) が含まれています。

   ```c++
   #include "evntdrvEvents.h"  
   ```

2. ドライバーをイベントプロバイダーとして登録および登録解除するマクロを追加します。 たとえば、 [Eventdrv サンプル](https://docs.microsoft.com/samples/microsoft/windows-driver-samples/eventdrv/)(evntdrvEvents) のヘッダーファイルでは、メッセージコンパイラはプロバイダーの名前に基づいてマクロを作成します。 マニフェストでは、 [Eventdrv サンプル](https://docs.microsoft.com/samples/microsoft/windows-driver-samples/eventdrv/)では、プロバイダーの名前として "sample Driver" という名前が使用されています。 メッセージコンパイラは、プロバイダーの名前とイベントマクロを組み合わせて、プロバイダー (この場合は**Eventregistersample \_ ドライバー**) を登録します。

   ```ManagedCPlusPlus
   //  This is the generated header file envtdrvEvents.h
   //
   //  ...
   //
   //
   // Register with ETW Vista +
   //
   #ifndef EventRegisterSample_Driver
   #define EventRegisterSample_Driver() McGenEventRegister(&DriverControlGuid, McGenControlCallbackV2, &DriverControlGuid_Context, &Sample_DriverHandle)
   #endif
   ```

   **Eventregister \< *プロバイダー* \> **マクロを[*driverentry*](https://docs.microsoft.com/windows-hardware/drivers/wdf/driverentry-for-kmdf-drivers)関数に追加します。 デバイスオブジェクトを作成および初期化するコードの後に、この関数を追加します。 **Eventregister \< *プロバイダー* \> **関数の呼び出しと**eventregister \< *プロバイダー* \> **の呼び出しを一致させる必要があることに注意してください。 ドライバーの[ </em> *アンロード* * ](<https://msdn.microsoft.com/library/windows/hardware/ff564886>)ルーチンでドライバーの登録を解除できます。

   ```ManagedCPlusPlus
      // DriverEntry function
      // ...


       // Register with ETW
       //
       EventRegisterSample_Driver();
    ```

3. 生成されたコードをドライバーのソースファイルに追加して、マニフェストで指定したイベントを書き込み (発生) します。 マニフェストからコンパイルしたヘッダーファイルには、ドライバー用に生成されたコードが含まれています。 トレースメッセージを ETW に発行するには、ヘッダーファイルで定義されている**eventwrite \< *イベント* \> **関数を使用します。 たとえば、次のコードは、 [Eventdrv サンプル](https://docs.microsoft.com/samples/microsoft/windows-driver-samples/eventdrv/)の evntdrvEvents で定義されているイベントのマクロを示しています。

   これらのイベントを記述するマクロは、、、およびと呼ばれ `EventWriteStartEvent` `EventWriteSampleEventA` `EventWriteUnloadEvent` ます。 これらのマクロの定義でわかるように、マクロ定義には、イベントが有効になっているかどうかを確認する**eventenabled \< *イベント* \> **マクロが自動的に含まれています。 イベントが有効になっていない場合、このチェックによってペイロードを作成する必要がなくなります。

   ```ManagedCPlusPlus

   ///
   // This is the generated header file envtdrvEvents.h
   //
   //  ...
   //
   // Enablement check macro for StartEvent
   //

   #define EventEnabledStartEvent() ((Sample_DriverEnableBits[0] & 0x00000001) != 0)

   //
   // Event Macro for StartEvent
   //
   #define EventWriteStartEvent(Activity, DeviceNameLength, name, Status)\
           EventEnabledStartEvent() ?\
           Template_hzq(Sample_DriverHandle, &StartEvent, Activity, DeviceNameLength, name, Status)\
           : STATUS_SUCCESS\

   //
   // Enablement check macro for SampleEventA
   //

   #define EventEnabledSampleEventA() ((Sample_DriverEnableBits[0] & 0x00000001) != 0)

   //
   // Event Macro for SampleEventA
   //
   #define EventWriteSampleEventA(Activity)\
           EventEnabledSampleEventA() ?\
           TemplateEventDescriptor(Sample_DriverHandle, &SampleEventA, Activity)\
           : STATUS_SUCCESS\

   //
   // Enablement check macro for UnloadEvent
   //

   #define EventEnabledUnloadEvent() ((Sample_DriverEnableBits[0] & 0x00000001) != 0)

   //
   // Event Macro for UnloadEvent
   //
   #define EventWriteUnloadEvent(Activity, DeviceObjPtr)\
           EventEnabledUnloadEvent() ?\
           Template_p(Sample_DriverHandle, &UnloadEvent, Activity, DeviceObjPtr)\
           : STATUS_SUCCESS\
  
    ```

   発生させるイベントのソースコードに**eventwrite \< *イベント* \> **マクロを追加します。 たとえば、次のコードスニペットは、 [Eventdrv サンプル](https://docs.microsoft.com/samples/microsoft/windows-driver-samples/eventdrv/)の[*driverentry*](https://docs.microsoft.com/windows-hardware/drivers/wdf/driverentry-for-kmdf-drivers)ルーチンを示しています。 *Driverentry*には、ドライバーを Etw (*eventregistersample \_ driver*) に登録するマクロと、ドライバーイベントを Etw に書き込むマクロ (*EventWriteStartEvent*) が含まれています。

   ```ManagedCPlusPlus
   NTSTATUS
   DriverEntry(
       IN PDRIVER_OBJECT DriverObject,
       IN PUNICODE_STRING RegistryPath
       )
   /*++

   Routine Description:

       Installable driver initialization entry point.
       This entry point is called directly by the I/O system.

   Arguments:

       DriverObject - pointer to the driver object

       RegistryPath - pointer to a unicode string representing the path
           to driver-specific key in the registry

   Return Value:

      STATUS_SUCCESS if successful
      STATUS_UNSUCCESSFUL  otherwise

   --*/
   {
       NTSTATUS Status = STATUS_SUCCESS;
       UNICODE_STRING DeviceName;
       UNICODE_STRING LinkName;
       PDEVICE_OBJECT EventDrvDeviceObject;
       WCHAR DeviceNameString[128];
       ULONG LengthToCopy = 128 * sizeof(WCHAR);
       UNREFERENCED_PARAMETER (RegistryPath);

       KdPrint(("EventDrv: DriverEntry\n"));

       //
       // Create Dispatch Entry Points.  
       //
       DriverObject->DriverUnload = EventDrvDriverUnload;
       DriverObject->MajorFunction[ IRP_MJ_CREATE ] = EventDrvDispatchOpenClose;
       DriverObject->MajorFunction[ IRP_MJ_CLOSE ] = EventDrvDispatchOpenClose;
       DriverObject->MajorFunction[ IRP_MJ_DEVICE_CONTROL ] = EventDrvDispatchDeviceControl;

       RtlInitUnicodeString( &DeviceName, EventDrv_NT_DEVICE_NAME );

       //
       // Create the Device object
       //
       Status = IoCreateDevice(
                              DriverObject,
                              0,
                              &DeviceName,
                              FILE_DEVICE_UNKNOWN,
                              0,
                              FALSE,
                              &EventDrvDeviceObject);

       if (!NT_SUCCESS(Status)) {
           return Status;
       }

       RtlInitUnicodeString( &LinkName, EventDrv_WIN32_DEVICE_NAME );
       Status = IoCreateSymbolicLink( &LinkName, &DeviceName );

       if ( !NT_SUCCESS( Status )) {
           IoDeleteDevice( EventDrvDeviceObject );
           return Status;
       }

    //
    // Choose a buffering mechanism
    //
    EventDrvDeviceObject->Flags |= DO_BUFFERED_IO;

    //
    // Register with ETW
    //
    EventRegisterSample_Driver();

    //
    // Log an Event with :  DeviceNameLength
    //                      DeviceName
    //                      Status
    //

    // Copy the device name into the WCHAR local buffer in order
    // to place a NULL character at the end, since this field is
    // defined in the manifest as a NULL-terminated string

    if (DeviceName.Length <= 128 * sizeof(WCHAR)) {

        LengthToCopy = DeviceName.Length;

    }

    RtlCopyMemory(DeviceNameString,
                  DeviceName.Buffer,
                  LengthToCopy);

    DeviceNameString[LengthToCopy/sizeof(WCHAR)] = L'\0';

    EventWriteStartEvent(NULL, DeviceName.Length, DeviceNameString, Status);

    return STATUS_SUCCESS;
   }
   ```

発生するイベントのソースコードに、すべての**eventwrite \< *イベント* \> **マクロを追加します。 [Eventdrv サンプル](https://docs.microsoft.com/samples/microsoft/windows-driver-samples/eventdrv/)を調べて、ドライバーのソースコード内のイベントに対して他の2つのマクロがどのように呼び出されるかを確認できます。

4. 生成されたヘッダーファイルから**eventunregister 解除 \< *プロバイダー* \> **マクロを使用して、ドライバーをイベントプロバイダーとして登録解除します。

   この関数呼び出しをドライバーのアンロードルーチンに配置します。 **Eventunregister 解除 \< *プロバイダー* \> **マクロが呼び出された後に、トレース呼び出しを行うことはできません。 プロセスに関連付けられているコールバック関数が無効になったため、プロセスがアンロードされると、イベントプロバイダーの登録を解除できない場合にエラーが発生することがあります。

   ```ManagedCPlusPlus
       // DriverUnload function
       // ...
       //

       //  Unregister the driver as an ETW provider
       //
       EventUnregisterSample_Driver();
   ```

## <a name="5-build-the-driver"></a>5. ドライバーをビルドする

インストルメントマニフェストをプロジェクトに追加し、メッセージコンパイラ (MC) のプロパティを構成した場合は、Visual Studio と MSBuild を使用してドライバープロジェクトまたはソリューションをビルドできます。

1. Visual Studio でドライバーソリューションを開きます。

2. [ビルド] メニューの [**ソリューションのビルド**] をクリックして、サンプルをビルドします。 ソリューションのビルドの詳細については、「[ドライバーのビルド](https://docs.microsoft.com/windows-hardware/drivers/develop/building-a-driver)」を参照してください。

## <a name="6-install-the-manifest"></a>6. マニフェストをインストールする

イベントコンシューマー (イベントログなど) がイベントメタデータを含むバイナリの場所を見つけることができるように、マニフェストをターゲットシステムにインストールする必要があります。 手順 3. でドライバープロジェクトにメッセージコンパイラタスクを追加した場合、インストルメンテーションマニフェストがコンパイルされ、ドライバーをビルドしたときにリソースファイルが生成されています。 Windows イベントのコマンドラインユーティリティ (Wevtutil) を使用して、マニフェストをインストールします。 マニフェストをインストールする構文は次のとおりです。

**wevtutil im** *drivermanifest*

たとえば、Evntdrv サンプルドライバーのマニフェストをインストールするには、昇格された特権 (**管理者として実行**) を使用してコマンドプロンプトウィンドウを開き、Evntdrv ファイルがあるディレクトリに移動して、次のコマンドを入力します。

```c++
Wevtutil.exe im evntdrv.xml
```

トレースセッションが完了したら、次の構文を使用してマニフェストをアンインストールします。

**wevtutil um** *drivermanifest*

たとえば、 [Eventdrv サンプル](https://docs.microsoft.com/samples/microsoft/windows-driver-samples/eventdrv/)のマニフェストをアンインストールするには、次のようにします。

```c++
Wevtutil.exe um evntdrv.xml
```

## <a name="7-test-the-driver-to-verify-etw-support"></a>7. ETW のサポートを確認するためにドライバーをテストする

ドライバーをインストールします。 ドライバーを実行してトレースアクティビティを生成します。 イベントビューアーの結果を表示します。 また、 [Tracelog](tracelog.md)を実行し、イベントトレースログを処理するためのツールである[Tracerpt](https://docs.microsoft.com/windows-server/administration/windows-commands/tracerpt_1)を実行して、イベントトレースログを制御、収集、および表示することもできます。
