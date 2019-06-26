---
title: WDTF シナリオの作成
description: WDTF シナリオでは、WDTF フレームワークを使用してカスタマイズして自動テストのデバイスに重点を置いたシナリオを構築します。
ms.assetid: f9e3de20-28be-40c6-802c-f4637b3f6c20
keywords:
- Windows デバイスのテスト フレームワーク WDK、スクリプト
- WDTF WDK、スクリプト
- WDK WDTF スクリプト
- テスト スクリプト WDK WDTF
- ファントム デバイス WDK WDTF
- 削除済みデバイス WDK WDTF
- ホット スワップ デバイス WDK WDTF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1b1dc0dc8a9659b9678b94e5a1c364217d9710bb
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67386251"
---
# <a name="creating-wdtf-scenarios"></a>WDTF シナリオの作成


インスタンスを作成して、WDTF ベースのシナリオを開始することができます、 [ **IWDTF2** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)を含む集計インターフェイス[ **DeviceDepot** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdtf/nf-wdtf-iwdtf2-get_devicedepot)と[ **SystemDepot** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdtf/nf-wdtf-iwdtf2-get_systemdepot)プロパティ。

1 つまたは複数のターゲット オブジェクトを収集するには、使用、 [ **IWDTFDeviceDepot2** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdtf/nn-wdtf-iwdtfdevicedepot2)インターフェイス、および使用して、**クエリ**メソッドを[単純なデータ評価言語](simple-data-evaluation-language-overview.md) (SDEL)。

スクリプトを使用して特定のターゲットを調べることがありますも、 [ **IWDTFTarget2::Eval** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdtf/nf-wdtf-iwdtftarget2-eval)メソッド。 ターゲットを選択した後はそれらを使用して制御[1 つまたは複数のアクション インターフェイス](controlling-targets.md)します。

WDTF シナリオの開発を開始する前に、WDTF をインストールする必要があります。 参照してください[WDTF クイック スタート](wdtf-quick-start-.md)詳細についてはします。

このトピックでは、次のセクションでは、WDTF の基本的なシナリオを作成する方法について説明します。

### <a name="simple-wdtf-scenario"></a>単純な WDTF シナリオ

次の VBScript コード サンプル (WDTF\_Sample1.vbs) WDTF を使用して有効にして、ファントム以外のすべてのデバイスを無効にする簡単なシナリオを示しています。 A*ファントム以外のデバイス*は任意のデバイスを物理的に存在します。 完全なサンプルは、次を参照してください。[サンプル WDTF シナリオ](sample-wdtf-scenarios.md)します。

```cpp
Set WDTF = WScript.CreateObject("WDTF.WDTF")
For Each Device In WDTF.DeviceDepot.Query("IsPhantom=false AND IsDisableable")
    On Error Resume Next
    Set DevMan = Device.GetInterface("DeviceManagement")
    If err <> 0 Then
 DevMan.Disable()
 DevMan.Enable()
    End If
Next
```

このシナリオを実行するにを実行して**CScript.exe WDTF\_Sample1.vbs**します。

### <a name="storing-target-information-by-using-context"></a>コンテキストを使用してターゲットの情報を格納します。

VBScript などの一部のプログラミング言語のオブジェクト参照を簡単に管理しません。 WDTF でこの管理を簡素化する各ターゲットを提供します、 [**コンテキスト**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdtf/nf-wdtf-iwdtftarget2-put_context)など、任意のキー/値ペアを格納するのに使用できるプロパティは、アクティブなオブジェクトを参照します。 このプロパティは、後で使用できるように、アクションのインターフェイスを格納するために特に便利です。 次の VBScript コードの例のストア、 [ **IWDTFSimpleIOStressAction2** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdtfinterfaces/nn-wdtfinterfaces-iwdtfsimpleiostressaction2)アクション内で名前付き**コンテキスト**項目。

```cpp
deviceObj.Context("IWDTFSimpleIOStressAction2") = SimpleIOObj
```

後で、シナリオ、停止、一時停止、または再開できます、 [ **IWDTFSimpleIOStressAction2** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdtfinterfaces/nn-wdtfinterfaces-iwdtfsimpleiostressaction2)インターフェイスを介してアクセスして[**コンテキスト**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdtf/nf-wdtf-iwdtftarget2-put_context)次のコード例は、もう一度として。

```cpp
Device.Context("IWDTFSimpleIOStressAction2").Stop
```

### <a name="detecting-phantom-devices"></a>ファントムのデバイスを検出します。

ファントムのデバイスでは、過去のコンピューターに物理的にインストールされたデバイスしますが、現在存在ではありません。 たとえば、ファントムのデバイスでは、USB マウスを接続されていない可能性があります。 高速化をオンになってまたはデバイスを削除するコンピューターに接続されているデバイスの再インストールを簡略化は、Windows オペレーティング システムはインストールされているデバイス ドライバーを保持が、ファントムとしてマークします。

デバイスの種類のターゲットには、 **IsPhantom**属性 (と**IsAttached**属性に相当は**IsPhantom**= false)、ハードウェアの物理的なを指定します。存在します。 次の VBScript コード例は、コンピューターに物理的に存在するすべてのデバイスのコレクションを一覧表示します。

```cpp
Set NonPhantomDevices = WDTF.DeviceDepot.Query ("IsAttached")
```

複数の属性のキーワードを参照してください。 [SDEL トークン](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)します。

 

 




