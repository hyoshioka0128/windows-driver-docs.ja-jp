---
title: カーネル モード ドライバーへのイベント トレーシングの追加
description: カーネル モード ドライバーへのイベント トレーシングの追加
ms.assetid: 74fdb4b2-aad1-4d8a-b146-40a92e1fdbb5
keywords:
- Event Tracing for Windows WDK、カーネル モード
- ETW の WDK、カーネル モード
- カーネル モードの ETW WDK ソフトウェア トレース
ms.date: 07/09/2018
ms.localizationpriority: medium
ms.openlocfilehash: d28efb71879df2ae4700e770484753bb15b98bb5
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63332062"
---
# <a name="adding-event-tracing-to-kernel-mode-drivers"></a>カーネル モード ドライバーへのイベント トレーシングの追加

このセクションでは、Event Tracing for Windows (ETW) のカーネル モード API を使用して、イベント トレースのカーネル モード ドライバーを追加する方法について説明します。 ETW カーネル モードの API は、Windows Vista で導入され、は、以前のオペレーティング システムではサポートされていません。 使用[WPP ソフトウェア トレース](wpp-software-tracing.md)または[WMI イベントのトレース](https://msdn.microsoft.com/library/windows/hardware/ff566350)ドライバーが Windows 2000 以降のトレース機能をサポートする必要がある場合。

> [!TIP]
> Windows Driver Kit (WDK) 8.1 と Visual Studio を使用して ETW を実装する方法を示すサンプル コードを表示するのを参照してください。、 [Eventdrv サンプル](https://go.microsoft.com/fwlink/p/?linkid=256109)します。

このセクションの内容

- [ワークフロー - カーネル モード ドライバーへのイベントのトレースの追加](#workflow---adding-event-tracing-to-kernel-mode-drivers)

- [1.発生させるイベントとそれらを公開する場所の種類を決める](#1-decide-the-type-of-events-to-raise-and-where-to-publish-them)

- [2.プロバイダー、イベント、およびチャネルを定義するインストルメンテーション マニフェストを作成します。](#2-create-an-instrumentation-manifest-that-defines-the-provider-the-events-and-channels)

- [3.メッセージ コンパイラ (Mc.exe) を使用して、インストルメンテーション マニフェストをコンパイルします。](#3-compile-the-instrumentation-manifest-by-using-the-message-compiler-mcexe)

- [4.発生させる、生成されたコードを追加 (公開)、イベント (登録、登録を解除、およびイベントの書き込み)](#4-add-the-generated-code-to-raise-publish-the-events-register-unregister-and-write-events)

- [5.ドライバーをビルドします。](#5-build-the-driver)

- [6.マニフェストをインストールします。](#6-install-the-manifest)

- [7.ETW のサポートを確認するドライバーをテストします。](#7-test-the-driver-to-verify-etw-support)

## <a name="workflow---adding-event-tracing-to-kernel-mode-drivers"></a>ワークフロー - カーネル モード ドライバーへのイベントのトレースの追加

![カーネル モード ドライバーにイベントのトレースを追加するプロセスの概要です。](images/etw-km-process.png)

## <a name="1-decide-the-type-of-events-to-raise-and-where-to-publish-them"></a>1.発生させるイベントとそれらを公開する場所の種類を決める

コーディングを開始する前にログを Event Tracing for Windows (ETW) にドライバーをするイベントの種類を決定する必要があります。 たとえばに、ドライバーを配布すると後の問題を診断するのに役立つイベントまたは参考にして、ドライバーを開発中のイベントを記録する可能性があります。 イベントの種類は、チャネルで識別されます。 A*チャネル*が管理者の種類のイベントの名前付きストリーム、運用、分析、またはデバッグのテレビ チャンネルのような特定対象ユーザーにリダイレクトされます。 チャネルは、イベント ログとイベント コンシューマーにイベント プロバイダーからのイベントを配信します。 チャネルとイベントの種類については、次を参照してください。[イベント ログと Windows イベント ログ チャネル](https://go.microsoft.com/fwlink/p/?linkid=62587)します。

開発中は、ほとんどの場合に興味のあるコードをデバッグする際に役立つトレース イベント。 この同じチャネルは、ドライバーを展開した後に表示される問題のトラブルシューティングに役立つ実稼働コードで使用可能性があります。 パフォーマンスを測定するために使用するトレース イベントにすることもこれらのイベントは、IT プロフェッショナルの微調整サーバーのパフォーマンスを向上でき、ネットワークのボトルネックを特定するのに役立ちます。

## <a name="2-create-an-instrumentation-manifest-that-defines-the-provider-the-events-and-channels"></a>2.プロバイダー、イベント、およびチャネルを定義するインストルメンテーション マニフェストを作成します。

インストルメンテーション マニフェストは、プロバイダーが発生するイベントの正式な説明を提供する XML ファイルです。 インストルメンテーション マニフェストは、イベント プロバイダーを識別して、チャネルまたは (最大 8 つ)、チャネルを指定します、イベントについて説明し、イベントのテンプレートを使用しています。 インストルメンテーション マニフェストはさらに、トレース メッセージをローカライズするための文字列のローカライズできます。 システムのイベントとイベント コンシューマー利用できます。 構造化された XML のクエリと分析を実行するマニフェストに指定されたデータ。

インストルメンテーション マニフェストの詳細については、次を参照してください。[インストルメンテーション マニフェスト (Windows) を記述](https://docs.microsoft.com/windows/desktop/WES/writing-an-instrumentation-manifest)と[(Windows) を使用して Windows イベント ログ](https://docs.microsoft.com/windows/desktop/WES/using-windows-event-log)します。

> [!NOTE]
> インストルメンテーション マニフェストを手動で作成することができますが %windowssdkdir に含まれている ECManGen.exe ツールを使用してを考慮する必要があります\\bin\\x64 %windowssdkdir\\bin\\x86\\フォルダー WDK と Visual Studio をインストールするときにします。 % WindowsSdkDir Windows キット ディレクトリに、WDK のこのバージョンがインストールされている例では、c: パスを表す\\Program Files (x86)\\Windows キット\\8.1。 ECManGen.exe は、XML タグを使用することがなく、最初からマニフェストを作成することを案内するアプリケーションです。 情報は、の知識がなくて、[インストルメンテーション マニフェスト (Windows) を記述](https://docs.microsoft.com/windows/desktop/WES/writing-an-instrumentation-manifest)セクションと、 [EventManifest スキーマ (Windows)](https://docs.microsoft.com/windows/desktop/WES/eventmanifestschema-schema)セクションは、このツールを使用する場合に役立ちます。

次のインストルメンテーション マニフェストは、「サンプル ドライバー。」という名前を使用したイベント プロバイダーを示しています。 この名前はバイナリのドライバーの名前と同じであるありませんに注意してください。 マニフェストには、プロバイダーと、メッセージおよびリソース ファイルへのパスの GUID も指定します。 メッセージおよびリソース ファイルでは、ETW をデコードし、イベントを報告するために必要なリソースを検索する場所を知ることができます。 これらのパスは、ドライバー (.sys) ファイルの場所をポイントします。 ターゲット コンピューター上の指定されたディレクトリに、ドライバーをインストールする必要があります。

例では、名前付きのチャネルを使用して**システム**、チャネルの種類のイベントを**管理者**します。このチャネルは %windowssdkdir で Windows Driver Kit (WDK) で提供される Winmeta.xml ファイルで定義\\含める\\um ディレクトリ。 **システム**チャネルがシステムのサービス アカウントで実行されているアプリケーションをセキュリティで保護します。 マニフェストに示されている、静的および動的なコンテンツと共に発行時にイベント データの型を記述するイベント テンプレートが含まれています。 このマニフェストの例には、3 つのイベントが定義されています: `StartEvent`、 `SampleEventA`、および`UnloadEvent`します。

チャネルに加えて、レベルとキーワードでイベントを関連付けることができます。 キーワードおよびレベルは、イベントを有効にして、パブリッシュされるときにイベントをフィルター処理するためのメカニズムを提供する方法を提供します。 キーワードは、論理的に関連するイベントをグループ化できます。 レベルは、または情報または、イベント、たとえば、重要なエラー、警告、詳細度を示すために使用できます。 Winmeta.xml ファイルには、イベント属性の定義済みの値が含まれています。

イベント ペイロード (イベント メッセージ、およびデータ) のテンプレートを作成するときに、入力と出力の種類を指定する必要があります。 サポートされている型の「解説」セクションに記述されます[ **InputType 複合型 (Windows)**](https://docs.microsoft.com/windows/desktop/WES/eventmanifestschema-inputtype-complextype)します。

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

## <a name="3-compile-the-instrumentation-manifest-by-using-the-message-compiler-mcexe"></a>3.メッセージ コンパイラ (Mc.exe) を使用して、インストルメンテーション マニフェストをコンパイルします。

[メッセージ コンパイラ (Mc.exe)](https://docs.microsoft.com/windows/desktop/WES/message-compiler--mc-exe-)ソース コードをコンパイルする前に実行する必要があります。 メッセージ コンパイラは、Windows Driver Kit (WDK) で含まれています。 メッセージ コンパイラは、イベント プロバイダー、イベント属性、チャネル、およびイベントの定義を含むヘッダー ファイルを作成します。 ソース コードには、このヘッダー ファイルをインクルードする必要があります。 メッセージ コンパイラも、生成されたリソース コンパイラのスクリプトを配置 (\*.rc) ファイルとリソース コンパイラのスクリプトが含まれる生成された .bin ファイル (バイナリ リソース)。

この手順は、いくつかの方法でビルド プロセスの一部として含めることができます。

- ドライバーのプロジェクト ファイルへのメッセージ コンパイラ タスクの追加 (ように、 [Eventdrv サンプル](https://go.microsoft.com/fwlink/p/?linkid=256109))。

- インストルメンテーション マニフェストを追加して、メッセージ コンパイラ プロパティを構成するのには、Visual Studio を使用します。

**プロジェクト ファイルへのメッセージ コンパイラ タスクの追加**ビルド プロセスでメッセージ コンパイラを組み込む方法の例は、見て、プロジェクト ファイル、 [Eventdrv サンプル](https://go.microsoft.com/fwlink/p/?linkid=256109)します。 Eventdrv.vcxproj ファイルでは、 **&lt;MessageCompile&gt;** メッセージ コンパイラを呼び出してセクション。 メッセージ コンパイラは、入力として、ヘッダー ファイルの evntdrvEvents.h を生成するのにマニフェスト ファイル (evntdrv.xml) を使用します。 ここでは、生成された RC ファイルのパスを指定し、カーネル モードのログ記録のマクロを有効します。 このセクションをコピーし、ドライバーのプロジェクト ファイル (.vcxproj) に追加できます。

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

Eventdrv.sys サンプルをビルドすると、Visual Studio は、必要なイベントのトレース ファイルを作成します。 また、evntdrv.xml マニフェストをドライバーのプロジェクトのリソース ファイルの一覧に追加します。 右クリックして、メッセージ コンパイラ プロパティ ページを表示するマニフェスト。

### <a name="using-visual-studio-to-add-the-instrumentation-manifest"></a>Visual Studio を使用して、インストルメンテーション マニフェストを追加するには

インストルメンテーション マニフェストをドライバーのプロジェクトに追加でき、必要なリソースとヘッダー ファイルを構築するメッセージ コンパイラ プロパティを構成できます。

### <a name="to-add-the-instrumentation-manifest-to-the-project-using-visual-studio"></a>インストルメンテーション マニフェストを Visual Studio を使用して、プロジェクトに追加するには

1. ソリューション エクスプ ローラーでは、ドライバーのプロジェクトにマニフェスト ファイルを追加します。 右クリックして**リソース ファイル&gt;追加&gt;既存項目の**(evntdrv.xml または mydriver.man など)。

2. 追加したファイルを右クリックし、プロパティ ページを使用して、項目の種類を変更する**MessageCompile**クリック**適用**します。

3. メッセージ コンパイラ プロパティが表示されます。 で、**全般**の設定が、次のオプションを設定し、クリックして**適用**します。

    | 全般                                 | 設定       |
    |-----------------------------------------|---------------|
    | **カーネル モードのログ記録のマクロを生成します。** | **[はい] (-km)** |
    | **入力の基本名を使用して、**              | **[はい] (-b)**  |

4. **ファイル オプション**、次のオプションを設定し、クリックして**適用**します。

    | ファイルのオプション                                    | 設定         |
    |-------------------------------------------------|-----------------|
    | **カウンターを格納するためのヘッダー ファイルを生成します。** | **はい**         |
    | **ヘッダー ファイルのパス**                            | **$ (Intdir)**   |
    | **RC およびバイナリ メッセージの生成されたファイルのパス**  | **はい**         |
    | **RC ファイルのパス**                                | **$ (Intdir)**   |
    | **生成されたファイルのベース名**                   | **$(Filename)** |

既定では、メッセージ コンパイラは生成されるファイルのベース名として、入力ファイルの基本名を使用します。 基本名を指定するには、設定、**ファイルの生成された基本名**(-z) フィールド。 Eventdr.sys サンプルでは、基本名に設定されて*evntdrvEvents* evntdrv.c に含まれているヘッダー ファイル evntdrvEvents.h の名前と一致するようにします。

> [!NOTE]
> Visual Studio プロジェクトで生成される .rc ファイルを含めない場合に関するリソースが見つかりません、マニフェスト ファイルをインストールするときにエラー メッセージが表示することがあります。

## <a name="4-add-the-generated-code-to-raise-publish-the-events-register-unregister-and-write-events"></a>4.発生させる、生成されたコードを追加 (公開)、イベント (登録、登録を解除、およびイベントの書き込み)

インストルメンテーション マニフェストでは、イベント プロバイダーは、イベント記述子の名前を定義します。 メッセージ コンパイラを使用してインストルメンテーション マニフェストをコンパイルするときに、メッセージ コンパイラは、リソースの説明し、も、イベントのマクロが定義されたヘッダー ファイルを生成します。 次に、これらのイベントを発生させるドライバーに生成されたコードを追加する必要があります。

1. ソース ファイルでは、メッセージ コンパイラ (MC.exe) によって生成されるイベントのヘッダー ファイルが含まれます。 たとえば、 [Eventdrv サンプル](https://go.microsoft.com/fwlink/p/?linkid=256109)Evntdrv.c のソース ファイルには、前の手順で生成されたヘッダー ファイル (evntdrvEvents.h) が含まれています。

   ```c++
   #include "evntdrvEvents.h"  
   ```

2. 登録およびイベント プロバイダーとドライバーの登録を解除できるマクロを追加します。 などのヘッダー ファイルで、 [Eventdrv サンプル](https://go.microsoft.com/fwlink/p/?linkid=256109)(evntdrvEvents.h) メッセージ コンパイラは、プロバイダーの名前に基づいたマクロを作成します。 マニフェストで、 [Eventdrv サンプル](https://go.microsoft.com/fwlink/p/?linkid=256109)プロバイダーの名前と名前の「サンプル ドライバー」を使用します。 メッセージ コンパイラは、ここでは、プロバイダーを登録するイベントのマクロとプロバイダーの名前を組み合わせて**EventRegisterSample\_ドライバー**します。

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

   追加、 **EventRegister\<*プロバイダー* \>** マクロを[ *DriverEntry* ](https://docs.microsoft.com/windows-hardware/drivers/wdf/driverentry-for-kmdf-drivers)関数。 作成し、デバイス オブジェクトを初期化するコードの後に、この関数を追加します。 呼び出しと一致する必要があります、 **EventRegister\<*プロバイダー* \>** 関数を呼び出して**EventUnregister\< *プロバイダー*\>** します。 ドライバーのドライバーの登録を解除できます[ </em>*アンロード** ](<https://msdn.microsoft.com/library/windows/hardware/ff564886>)ルーチン。

   ```ManagedCPlusPlus
      // DriverEntry function
      // ...


       // Register with ETW
       //
       EventRegisterSample_Driver();
    ```

3. 生成されたコードを追加 (生成) を記述するドライバーのソース ファイルへのイベントで指定したマニフェスト。 マニフェストからコンパイルされたヘッダー ファイルには、ドライバーに対して生成されたコードが含まれています。 使用して、 **EventWrite\<*イベント*\>**  ETW にトレース メッセージを発行するヘッダー ファイルで定義された関数。 たとえば、次のコードの evntdrvEvents.h で定義されたイベントのマクロを示しています。、 [Eventdrv サンプル](https://go.microsoft.com/fwlink/p/?linkid=256109)します。

   これらのイベントを記述するマクロが呼び出されます。 `EventWriteStartEvent`、 `EventWriteSampleEventA`、および`EventWriteUnloadEvent`します。 マクロ定義が含まれています自動的にこれらのマクロの定義でご覧のとおり、 **EventEnabled\<*イベント*\>** マクロ イベントが有効になっているかどうかをチェックします。 チェックでは、イベントが有効でない場合は、ペイロードを構築する必要があります。

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

   追加、 **EventWrite\<*イベント*\>** マクロを発生させるイベントのソース コードにします。 たとえば、次のコード例では、 [ *DriverEntry* ](https://docs.microsoft.com/windows-hardware/drivers/wdf/driverentry-for-kmdf-drivers)ルーチンから、 [Eventdrv サンプル](https://go.microsoft.com/fwlink/p/?linkid=256109)します。 *DriverEntry*にドライバーを ETW に登録するマクロが含まれます (*EventRegisterSample\_ドライバー*) とドライバーのイベントを ETW に書き込むマクロ (*EventWriteStartEvent*)。

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

追加のすべての**EventWrite\<*イベント*\>** マクロを発生させるイベントのソース コードにします。 調べることができます、 [Eventdrv サンプル](https://go.microsoft.com/fwlink/p/?linkid=256109)にドライバーのソース コードでイベントを他の 2 つのマクロの呼び出し方法を参照してください。

4. 使用するイベント プロバイダーとドライバーの登録を解除、 **EventUnregister\<*プロバイダー* \>** 生成されるヘッダー ファイルからマクロ。

   ドライバー、アンロード ルーチンでは、この関数の呼び出しを配置します。 後のトレースの呼び出しは行われません、 **EventUnregister\<*プロバイダー* \>** マクロが呼び出されます。 プロセスに関連付けられているすべてのコールバック関数が無効になったため、プロセスがアンロードされるとき、イベント プロバイダーを登録解除に失敗したエラーが発生することができます。

   ```ManagedCPlusPlus
       // DriverUnload function
       // ...
       //

       //  Unregister the driver as an ETW provider
       //
       EventUnregisterSample_Driver();
   ```

## <a name="5-build-the-driver"></a>5.ドライバーのビルド

計器マニフェストをプロジェクトに追加し、メッセージ コンパイラ (MC.exe) プロパティを構成する場合は、ドライバーのプロジェクトまたは Visual Studio および MSBuild を使用してソリューションを構築できます。

1. Visual Studio でのドライバー ソリューションを開きます。

2. 選択して、[ビルド] メニューからサンプルをビルド**ソリューションのビルド**します。 ソリューションの構築の詳細については、次を参照してください。[ドライバーをビルド](https://docs.microsoft.com/windows-hardware/drivers/develop/building-a-driver)します。

## <a name="6-install-the-manifest"></a>6.マニフェストをインストールします。

イベント コンシューマー (たとえば、イベント ログ) は、イベントのメタデータを含むバイナリの場所を検索できるように、ターゲット システムに、マニフェストをインストールする必要があります。 手順 3 でドライバーのプロジェクトに、メッセージ コンパイラ タスクを追加した場合は、インストルメンテーション マニフェストがコンパイルされ、リソース ファイルは、ドライバーをビルドしたときに生成されました。 マニフェストをインストールするのに、Windows イベント コマンド ライン ユーティリティ (Wevtutil.exe) を使用します。 マニフェストをインストールするための構文は次のとおりです。

**wevtutil.exe im** *drivermanifest*

たとえば、Evntdrv.sys サンプル ドライバーのマニフェストをインストールするには、管理者特権でコマンド プロンプト ウィンドウを開きます (**管理者として実行**) evntdrv.xml ファイルがあるディレクトリに移動し、入力、次のコマンド:

```c++
Wevtutil.exe im evntdrv.xml
```

トレース セッションが完了したら、次の構文を使用してマニフェストをアンインストールします。

**wevtutil.exe um** *drivermanifest*

たとえばのマニフェストをアンインストールするため、 [Eventdrv サンプル](https://go.microsoft.com/fwlink/p/?linkid=256109):

```c++
Wevtutil.exe um evntdrv.xml
```

## <a name="7-test-the-driver-to-verify-etw-support"></a>7.ETW のサポートを確認するドライバーをテストします。

ドライバーをインストールします。 トレース アクティビティを生成するドライバーを実行します。 イベント ビューアーで結果を表示します。 実行することも[Tracelog](tracelog.md)、し、実行[Tracerpt](https://docs.microsoft.com/windows-server/administration/windows-commands/tracerpt_1)トレースのイベントを処理するためのツールのログ、ログを制御、収集、およびイベント トレースを表示します。
