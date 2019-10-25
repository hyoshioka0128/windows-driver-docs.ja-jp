---
title: WDTF simple i/o action プラグインを使用してデバイス i/o をカスタマイズする
description: Visual Studio テストテンプレートを使用して作成したデバイスの基本的なテストとテストを最大限に活用するには、単純な i/o プラグインによってデバイスがサポートされている必要があります。
ms.assetid: 96BC880B-79DC-4CB1-BD79-87B0A4717634
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: cdeb8b063816163eceb4194ff0a19d967ec3c8d8
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844386"
---
# <a name="how-to-customize-io-for-your-device-using-the-wdtf-simple-io-action-plug-in"></a>WDTF シンプル I/O アクション プラグインを使ってデバイスの I/O をカスタマイズする方法


Visual Studio テストテンプレートを使用して作成したデバイスの基本的なテストとテストを最大限に活用するには、単純な i/o プラグインによってデバイスがサポートされている必要があります。 デバイスの種類がサポートされているかどうかを確認し、テストに関する特定の要件があるかどうかを確認するには、「 [WDTF Simple i/o プラグインの提供](provided-wdtf-simpleio-plug-ins.md)」を参照してください。デバイスがサポートされていない場合は、 **Wdtf Simple I/o Action プラグイン**テンプレートを使用して Microsoft Visual Studio にプラグインを作成できます。

### <a name="prerequisites"></a>前提条件

-   テスト対象のデバイスがテストコンピューターにインストールされています。
-   テストに署名され、テストコンピューターにインストールされているドライバーパッケージ。 ドライバーが正しくインストールされていることを確認するには、「[ドライバーパッケージのテスト方法](https://docs.microsoft.com/windows-hardware/drivers)」を参照してください。
-   展開用に構成され、プロビジョニングされたテスト コンピューター。 「 [Visual Studio を使用した実行時のドライバーのテスト](https://docs.microsoft.com/windows-hardware/drivers)」を参照してください。

<a name="instructions"></a>手順
------------

### <a href="" id="create-a-project-for-a-wdtf-simple-i-o-action-plug-in-"></a>手順 1: WDTF Simple i/o Action プラグイン用のプロジェクトを作成する

1. **[ファイル]** メニューの **[新規作成] &gt; [プロジェクト]** をクリックします。
2. **[新しいプロジェクト]** ダイアログボックスのインストールされているテンプレートの一覧から、[ **Visual C++&gt;Windows Driver&gt;テスト]&gt;Wdtf Simple i/o Action プラグイン**を選択します。
3. 単純な i/o プロジェクトと場所の名前を指定します (または既定値を使用します)。
4. プロジェクトテンプレートによって、Visual Studio ソリューションが生成されます。 このソリューションには、デバイスの単純な i/o プラグインを作成するために必要なすべてのファイルが含まれています。 ファイルの名前は、WDTF<em>&lt;project&gt;</em>SimpleIoAction\*の形式になります。 単純な i/o プロジェクトの既定の名前は (Devicetype です。
5. このテンプレートは、プロジェクトの WDTF Simple i/o Action インターフェイスを作成します。 インターフェイスは、IWDTFTarget2 インターフェイスのインスタンスに対して動作します。
6. WDTF Simple i/o プラグインソリューションをビルドして、すべての必要なファイルが存在することを確認します。
7. 実装ファイルにコードを追加することにより、ターゲットを設定し、単純な i/o アクション (Open、Close、および RunIO) を実装するメソッドを実装します。 ファイルの名前は、CWDTF*project*SimpleIoActionImpl ファイルの形式になります。

### <a href="" id="implement-the-settarget-method-for-your-device"></a>手順 2: デバイスの SetTarget 使用方法を実装する

- プロジェクトの実装ファイル (たとえば、CWDTFmyDeviceTypeSimpleIoActionImpl) を開き、 [**Iaction:: settarget**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdtf/nf-wdtf-iaction-settarget) settarget メソッドのインスタンスを探します。 このメソッドには、コメントでマークされたセクションがあります。 TODO: これは、デバイスとの互換性をチェックするコードを実装する必要がある場所を示します。

  **Settarget**メソッドは、各インスタンスに対して wdtf によって1回呼び出されます。 主な目的は2つあります。

  - そのため、WDTF では、オブジェクトがデバイスターゲットをサポートしているかどうかを判断できます。 pMainTarget
  - CWDTF<em>&lt;プロジェクト&gt;</em>SimpleIoActionImpl インスタンスは、後で Open ()、Close ()、runio () の各メソッド呼び出しを実行するために、ターゲットから必要な情報を取得できます。

  このメソッドの実装では、ターゲットがサポートされていないことを示すために、E\_NOINTERFACE を返す必要があります。 ターゲットがサポートされている場合、メソッドは、S\_OK を返す必要があります。 他のエラーが発生した場合、メソッドはエラーを示す HRESULT を返す必要があります。

  ```ManagedCPlusPlus
       
      ////
      // TODO: 1)  Perform your checks to see if your implementation is compatible with the target.
      //       Use the ITarget::GetValue() & ITarget::Eval() method to get the necessary data , info 
      //       to determine that. 
      //       2)  Also get the necessary info and save it in a member variable 
      //       to accomplish the later Open() method call.
  ```

### <a href="" id="implement-simpleioaction-to-open-the-interface"></a>手順 3: SimpleIoAction を実装してインターフェイスを開く

次に、指定された Open () メソッドを実装して、テスト用に ITarget を開く必要があります。

この[**open**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdtfinterfaces/nf-wdtfinterfaces-iwdtfsimpleioex2-open)メソッドは、ターゲットデバイスを開こうとします。 メソッドがこれを実行できない場合、メソッドはエラーを示す HRESULT を返す必要があります。 SimpleIO インターフェイスが既に開いている (初期化されている) 場合、このメソッドは失敗します。 この方法の実装方法は、ITarget の型と、状況に最も適したものによって異なります。 これは、CreateFile () を使用してハンドルを開く必要があることを意味します。 これは、進行中のテストケースを追跡できるように、コンテキスト構造を初期化することを意味します。 エラーが発生した場合は、メソッドで COMReportError () を使用することをお勧めします。これにより、エラーの説明と、今後の発生を防ぐのに役立つ情報や手順が提供されます。

ISimpleIO\_アクションが既に開かれている場合  このメソッドは失敗する**ことに注意**してください。

 

-   プロジェクトの実装ファイル (たとえば、CWDTFmyDeviceTypeSimpleIoActionImpl) を開き、 [**open**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdtfinterfaces/nf-wdtfinterfaces-iwdtfsimpleioex2-open)メソッドのインスタンスを探します。 このメソッドには、コメントと TODO でマークされたセクションがあります。

    ```cpp
    //
       //   TODO: Add code for your implementation of Open() here.
       //
       //
       //  To return failure use COMReportError(,,,).  For example the following 
       //  will return E_FAIL as the error code and "My Device error String"  as
       //  the error string.
       //
       //  COMReportError(WDTF, E_FAIL, "My Device error String");
       //
    ```

### <a href="" id="implement-the-simpleioaction-method-to--close-the-interface"></a>手順 4: インターフェイスを閉じるための SimpleIoAction メソッドの実装

このメソッドは、以前に開いたテストコンテキストを閉じる必要があります。 失敗した HRESULT を報告する必要がある場合でも、コンテキストをクリアする必要があります。 を閉じるときに発生するエラーが発生するケースはごくわずかです。 この方法では、Open () で実行したすべての操作を元に戻す必要があります。 これは、既に開かれているハンドルを CloseHandle () で閉じる必要があることを意味します。 エラーが発生した場合は、対応可能な説明を入力してください。

ISimpleIO\_アクションが既に閉じられているか、一度も開かれていない**場合  この**メソッドは失敗します。

 

-   プロジェクトの実装ファイル (たとえば、CWDTFmyDeviceTypeSimpleIoActionImpl) を開き、 [**Close**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdtfinterfaces/nf-wdtfinterfaces-iwdtfsimpleioex2-close)メソッドのインスタンスを探します。 このメソッドには、コメントと TODO でマークされたセクションがあります。

    ```cpp
    //
       //  //
       //   TODO: Add code for your implementation of Close() here.
       //
       // 
       //
       //  To return failure use COMReportError(,,,).  For example the following 
       //  will return E_FAIL as the error code and "My Device error String"  as
       //  the error string.
       //
       //  COMReportError(WDTF, E_FAIL, "My Device error String");
       //
     
       //
    ```

### <a href="" id="implement-the-simpleioaction-method-to-perform-simple-i-o-operations-"></a>手順 5: 単純な i/o 操作を実行するための SimpleIoAction メソッドを実装する

このメソッドは、ターゲットに対して少数の入出力操作を実行する必要があります。 その後、メソッドは i/o 操作が正しく完了したことを確認する必要があります。 次に、各テストで、デバイスに対して i/o を実行する時間を制御できます。 RunIo () メソッドを呼び出すたびに、少量の i/o だけが実行されます。 WDTF は、ループ内で RunIo () を繰り返し呼び出して、より多くの i/o を実行します。 一般に、1つの RunIo () メソッド呼び出しを数秒で保持します。

ISimpleIO\_アクションが現在閉じている場合  このメソッドは失敗する**ことに注意**してください。

 

-   プロジェクトの実装ファイル (たとえば、CWDTFmyDeviceTypeSimpleIoActionImpl) を開き、RunIO メソッドのインスタンスを探します。 このメソッドには、コメントと TODO でマークされたセクションがあります。

    ```cpp
    //
       //  //
       //   TODO: Add code for your implmentaiton of RunIO() here.
       //
       // 
       //
       //  To return failure use COMReportError(,,,).  For example the following 
       //  will return E_FAIL as the error code and "My Device error String"  as
       //  the error string.
       //
       //  COMReportError(WDTF, E_FAIL, "My Device error String");
       //
     
       //
    ```

### <a href="" id="build-and-install-the-simple-i-o-action-plugin-"></a>手順 6: 単純な i/o アクションプラグインをビルドしてインストールする

まだ行っていない場合は、テスト用にコンピューターを構成する必要があります。 詳細については、「[ドライバーの展開およびテスト用にコンピューターをプロビジョニングする (wdk 8.1)](https://docs.microsoft.com/windows-hardware/drivers/gettingstarted/provision-a-target-computer-wdk-8-1) 」または「[ドライバーの展開およびテスト用にコンピューターをプロビジョニングする (wdk 8)](https://docs.microsoft.com/windows-hardware/drivers/gettingstarted/provision-a-target-computer-wdk-8-1)」を参照してください。

1. ソリューションをビルドします。

   単純な i/o アクションプラグインをビルドすると、2つのテストが作成されます。 これらのテストでは、テストコンピューターにプラグインをインストールしてアンインストールします。 既定では、単純な i/o アクションプラグインファイルはテスト**グループエクスプローラー**のテストカテゴリ **[My test] カテゴリ**に表示されます。

2. 単純な i/o アクションプラグインをインストールするには、テストコンピューターで " **Register WDTF** <em>&lt;Project&gt;</em> **SimpleIOAction** " という名前のテストを実行します。 テストの選択と実行の詳細については、「 [Visual Studio を使用して実行時にドライバーをテストする方法](https://docs.microsoft.com/windows-hardware/drivers)」を参照してください。
3. 単純な i/o アクションプラグインがインストールされていることを確認するには、テストコンピューターで**WDTF Simple I/o プラグインが**テストされているディスプレイデバイスを実行します。 プラグインとデバイスが結果に表示されます。 詳細については、「[カスタム WDTF Simple I/o Action プラグインがデバイスに必要かどうかを判断](test-your-device-to-see-if-you-need-to-customize-the-wdtf-simple-i-o-action-plug-in.md)する方法」を参照してください。
4. 単純な i/o アクションプラグインをアンインストールするには、テストコンピューターで SimpleIOAction **WDTF** <em>&lt;Project&gt;</em>という名前のテストを実行します。 **WDTF Simple i/o プラグインテストが**実行されているディスプレイデバイスを実行することで、プラグインがアンインストールされたことを確認できます。

## <a name="related-topics"></a>関連トピック
[Test Authoring and Execution Framework (TAEF)](https://docs.microsoft.com/windows-hardware/drivers/taef/index)  
[デバイスにカスタム WDTF Simple i/o Action プラグインが必要かどうかを判断する方法](test-your-device-to-see-if-you-need-to-customize-the-wdtf-simple-i-o-action-plug-in.md)  
[Visual Studio を使って実行時にドライバーをテストする方法](https://docs.microsoft.com/windows-hardware/drivers)  



