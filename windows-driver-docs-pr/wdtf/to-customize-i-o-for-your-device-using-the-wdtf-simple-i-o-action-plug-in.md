---
title: プラグインを WDTF 単純な I/O 操作を使用してデバイスの I/O をカスタマイズします。
description: デバイスの基本的なテストとテストを記述した場合、Visual Studio テスト テンプレートを使用してから最大のメリットを取得するには、プラグインの単純な I/O でデバイスをサポートする必要があります。
ms.assetid: 96BC880B-79DC-4CB1-BD79-87B0A4717634
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 284247bde18720594753b2cd323aa25818fd6832
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63367450"
---
# <a name="how-to-customize-io-for-your-device-using-the-wdtf-simple-io-action-plug-in"></a>WDTF シンプル I/O アクション プラグインを使ってデバイスの I/O をカスタマイズする方法


デバイスの基本的なテストとテストを記述した場合、Visual Studio テスト テンプレートを使用してから最大のメリットを取得するには、プラグインの単純な I/O でデバイスをサポートする必要があります。 デバイスの種類がサポートされているかどうかと、テストに固有の要件があるかどうかを確認するには、「[提供されている WDTF シンプル I/O プラグイン](provided-wdtf-simpleio-plug-ins.md)」をご覧ください。デバイスがサポートされていない場合プラグインを作成する、Microsoft Visual studio を使用して、 **WDTF 単純な I/O 操作プラグイン**テンプレート。

### <a name="prerequisites"></a>前提条件

-   テスト対象のデバイスは、テスト コンピューターにインストールされます。
-   テストは、ドライバー パッケージは署名され、テスト コンピューターにインストールされています。 ドライバーが正しくインストールされていることを確認するを参照してください。[ドライバー パッケージをテストする方法](https://msdn.microsoft.com/windows-drivers/develop/test_a_driver_package)します。
-   展開用に構成され、プロビジョニングされたテスト コンピューター。 参照してください[Visual Studio を使用して実行時のドライバーをテストします。](https://msdn.microsoft.com/windows-drivers/develop/testing_a_driver_at_runtime)

<a name="instructions"></a>手順
------------

### <a href="" id="create-a-project-for-a-wdtf-simple-i-o-action-plug-in-"></a>手順 1:プラグイン WDTF 単純な I/O 操作のプロジェクトを作成します。

1. **[ファイル]** メニューの **[新規作成] &gt; [プロジェクト]** をクリックします。
2. インストール済みテンプレートの一覧から、**新しいプロジェクト**ダイアログ ボックスで、 **Visual C &gt; Windows ドライバー&gt;テスト&gt;WDTF 単純な I/O 操作プラグイン**します。
3. 単純な I/O プロジェクトと場所の名前を指定します (または、既定値を使用します。)
4. プロジェクト テンプレートは、Visual Studio ソリューションを生成します。 ソリューションには、単純な I/O デバイスのプラグインを作成する必要があるすべてのファイルが含まれています。 ファイルの名前として具現 WDTF<em>&lt;プロジェクト&gt;</em>SimpleIoAction\*します。 単純な I/O プロジェクトの既定の名前は、DeviceType です。
5. テンプレートは、プロジェクトの WDTF 単純な I/O 操作のインターフェイスを作成します。 インターフェイスは、IWDTFTarget2 インターフェイスのインスタンスに機能します。
6. 必要なすべてのファイルが存在することを確認する WDTF 単純な I/O プラグイン ソリューションをビルドします。
7. ターゲットを設定し、実装ファイル内のコードを追加して単純な I/O 操作 (Open、Close、および RunIO) を実装するメソッドを実装します。 ファイルの名前には、フォーム CWDTF*プロジェクト*SimpleIoActionImpl.cpp ファイル。

### <a href="" id="implement-the-settarget-method-for-your-device"></a>手順 2:デバイスの SetTarget メソッドを実装します。

- たとえば、CWDTFmyDeviceTypeSimpleIoActionImpl.cpp、プロジェクトの実装ファイルを開きのインスタンスを検索[ **IAction::SetTarget** ](https://msdn.microsoft.com/library/windows/hardware/ff538790) SetTarget メソッド。 このメソッドは、コメントと TODO でマークされたセクション: デバイスとの互換性をチェックするコードを実装することを示します。

  **SetTarget**メソッドを呼び出して 1 回 WDTF インスタンスごとにします。 2 つの主な目的があります。

  - WDTF は、オブジェクトがデバイスのターゲット pMainTarget をサポートしているかを確認できるように
  - ように、CWDTF<em>&lt;プロジェクト&gt;</em>SimpleIoActionImpl インスタンスは、後で Open()、Close()、RunIO() メソッドの呼び出しを実行するターゲットから必要な情報を取得できます。

  このメソッドの実装を返す必要があります E\_NOINTERFACE をターゲットがサポートされていないことを示します。 メソッドが返す必要があります S\_了解のターゲットがサポートされている場合。 その他のエラーが発生した場合、メソッドは、エラーを示す HRESULT を返す必要があります。

  ```ManagedCPlusPlus
       
      ////
      // TODO: 1)  Perform your checks to see if your implementation is compatible with the target.
      //       Use the ITarget::GetValue() & ITarget::Eval() method to get the necessary data , info 
      //       to determine that. 
      //       2)  Also get the necessary info and save it in a member variable 
      //       to accomplish the later Open() method call.
  ```

### <a href="" id="implement-simpleioaction-to-open-the-interface"></a>手順 3:インターフェイスを開く SimpleIoAction を実装します。

次に、指定された、Open() メソッドを実装することによってテスト用 ITarget を開く必要があります。

これは、 [**開く**](https://msdn.microsoft.com/library/windows/hardware/hh451153)メソッドは、ターゲット デバイスを開こうとする必要があります。 メソッドでこれを行うことがない場合、メソッドは、エラーを示す HRESULT を返す必要があります。 SimpleIO インターフェイスは既に開かれている (初期化されている) 場合、このメソッドが失敗する必要があります。 このメソッドを実装する方法は、ITarget 型と自分の状況に最も適したは、何かによって異なります。 これはおそらく CreateFile() でそれを識別するハンドルを開く必要があることを意味します。 おそらく context 構造は、継続的なテスト_ケースの追跡を維持できるように初期化することを意味します。 エラーが発生した場合は、このメソッドは、理想的 COMReportError () を使用する必要があり、エラーと情報または今後の発生を防ぐために手順の説明を入力する必要があります。

**注**  場合、このメソッドが失敗する必要があります ISimpleIO\_アクションは既に開かれています。

 

-   たとえば、CWDTFmyDeviceTypeSimpleIoActionImpl.cpp、プロジェクトの実装ファイルを開きのインスタンスを検索[**オープン**](https://msdn.microsoft.com/library/windows/hardware/hh451153)メソッド。 このメソッドでは、コメントと TODO でマークされたセクションがあります。

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

### <a href="" id="implement-the-simpleioaction-method-to--close-the-interface"></a>手順 4:インターフェイスを閉じる SimpleIoAction メソッドを実装します。

このメソッドは、既に開かれているテスト コンテキストを閉じる必要があります。 失敗を報告する必要があるあって、コンテキストをクリアする必要があります HRESULT。 閉じるときに発生するエラー センスがにより、実際には、いくつかのケースのみがあります。 このメソッドでは、Open() で実行したすべての操作を元に戻す必要があります。 おそらくしたがって CloseHandle() で以前に開かれたハンドルを閉じる必要があります。 エラーが発生した場合に、そのアクションにつながる説明を入力してください。

**注**  場合、このメソッドが失敗する必要があります、ISimpleIO\_アクションが既に閉じられているまたは開かれたことはありません。

 

-   たとえば、CWDTFmyDeviceTypeSimpleIoActionImpl.cpp、プロジェクトの実装ファイルを開きのインスタンスを検索、 [**閉じる**](https://msdn.microsoft.com/library/windows/hardware/hh451151)メソッド。 このメソッドでは、コメントと TODO でマークされたセクションがあります。

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

### <a href="" id="implement-the-simpleioaction-method-to-perform-simple-i-o-operations-"></a>手順 5:単純な I/O 操作を実行する SimpleIoAction メソッドを実装します。

このメソッドは、少数のターゲットの入力と出力の操作を実行する必要があります。 メソッドは、I/O 操作が正常に完了したことを確認する必要があります。 次に、各テストでは、デバイスに I/O を実行する期間を制御できます。 RunIo() メソッドを呼び出すたびには、I/O 量が少ないのみを実行する必要があります。 WDTF は、I/O を実行するループ内で RunIo() を繰り返し呼び出すされます。 一般に、いくつかの秒に 1 つ RunIo() メソッドの呼び出しを保持するお試しください。

**注**  場合、このメソッドが失敗する必要があります ISimpleIO\_アクションは現在閉じられています。

 

-   CWDTFmyDeviceTypeSimpleIoActionImpl.cpp など、プロジェクトの実装ファイルを開き、RunIO メソッドのインスタンスを検索します。 このメソッドでは、コメントと TODO でマークされたセクションがあります。

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

### <a href="" id="build-and-install-the-simple-i-o-action-plugin-"></a>手順 6:ビルドし、単純な I/O 操作プラグインのインストール

されていない場合は、テスト用コンピューターを構成する必要があります。 詳細については、次を参照してください。[ドライバーの展開のためにコンピューターをプロビジョニングし、テスト (WDK 8.1)](https://msdn.microsoft.com/library/windows/hardware/dn745909)または[ドライバーの展開のためにコンピューターをプロビジョニングし、テスト (WDK 8)](https://msdn.microsoft.com/library/windows/hardware/dn745909)します。

1. ソリューションをビルドします。

   プラグインの単純な I/O 操作をビルドすると、2 つのテストが作成されます。 これらのテストでは、インストールし、テスト コンピューターでプラグインをアンインストールします。 既定では、単純な I/O 操作のプラグイン ファイルの表示で**テスト グループ エクスプ ローラー**、テスト カテゴリ**マイ テスト カテゴリ**。

2. 単純な I/O 操作のプラグインをインストールするには、という名前のテストを実行**登録 WDTF**<em>&lt;プロジェクト&gt;</em>**SimpleIOAction.DLL**テスト コンピューター. 選択し、実行に関する情報のテストは、「の[Visual Studio を使用して実行時にドライバーをテストする方法](https://msdn.microsoft.com/windows-drivers/develop/testing_a_driver_at_runtime)します。
3. 単純な I/O 操作のプラグインがインストールされていることを確認するには、実行、 **WDTF 単純な I/O プラグインのデバイスを表示**テスト コンピューターでテストします。 プラグインし、デバイスは、結果に表示する必要があります。 詳細については、次を参照してください。[カスタム WDTF 単純な I/O 操作プラグインをが、デバイスに必要な場合を判断する方法を](test-your-device-to-see-if-you-need-to-customize-the-wdtf-simple-i-o-action-plug-in.md)します。
4. 単純な I/O 操作のプラグインをアンインストールするには、という名前のテストを実行**の登録を解除 WDTF**<em>&lt;プロジェクト&gt;</em>**SimpleIOAction.DLL**のテストコンピューター。 実行して、プラグインをアンインストールすることを確認することができます、 **WDTF 単純な I/O プラグインのデバイスを表示**をテストします。

## <a name="related-topics"></a>関連トピック
[Test Authoring and Execution Framework (TAEF)](https://msdn.microsoft.com/library/windows/hardware/hh439725)  
[カスタム WDTF 単純な I/O 操作プラグインが、デバイスに必要なかどうかを判断する方法](test-your-device-to-see-if-you-need-to-customize-the-wdtf-simple-i-o-action-plug-in.md)  
[Visual Studio を使って実行時にドライバーをテストする方法](https://msdn.microsoft.com/windows-drivers/develop/testing_a_driver_at_runtime)  



