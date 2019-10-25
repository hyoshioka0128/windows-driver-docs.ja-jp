---
title: WDTF シナリオの作成
description: WDTF のシナリオでは、WDTF framework を使用して、デバイスに焦点を合わせた自動テストおよびカスタマイズされたテストシナリオを構築します。
ms.assetid: f9e3de20-28be-40c6-802c-f4637b3f6c20
keywords:
- Windows デバイステストフレームワーク WDK、スクリプト
- WDTF WDK、スクリプト
- スクリプト WDK WDTF
- テストスクリプト WDK WDTF
- ファントムデバイス WDK WDTF
- 削除されたデバイスの WDK WDTF
- ホットスワップデバイス WDK WDTF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: fa5a3f2573acb3d0b5983ad6940f6cea3f0cb531
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841666"
---
# <a name="creating-wdtf-scenarios"></a>WDTF シナリオの作成


WDTF ベースのシナリオを開始するには、 [**devicedepot**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdtf/nf-wdtf-iwdtf2-get_devicedepot)と[**systemdepot**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdtf/nf-wdtf-iwdtf2-get_systemdepot)のプロパティを含む[**IWDTF2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/index) aggregation インターフェイスのインスタンスを作成します。

1つ以上の対象オブジェクトを収集するには、 [**IWDTFDeviceDepot2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdtf/nn-wdtf-iwdtfdevicedepot2)インターフェイスを使用し、[単純なデータ評価言語](simple-data-evaluation-language-overview.md)(Sdel) で**クエリ**メソッドを使用します。

スクリプトでは、 [**IWDTFTarget2:: Eval**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdtf/nf-wdtf-iwdtftarget2-eval)メソッドを使用して特定のターゲットを調べることもできます。 ターゲットを選択した後、 [1 つまたは複数のアクションインターフェイス](controlling-targets.md)を使用してコントロールを制御します。

WDTF シナリオの開発を開始する前に、WDTF をインストールする必要があります。 詳細については、「 [Wdtf クイックスタート](wdtf-quick-start-.md)」を参照してください。

このトピックの次のセクションでは、基本的な WDTF シナリオを作成する方法について説明します。

### <a name="simple-wdtf-scenario"></a>単純な WDTF シナリオ

次の VBScript コードサンプル (WDTF\_サンプル 1) は、WDTF を使用してすべての非ファントムデバイスを有効または無効にする簡略化されたシナリオを示しています。 *ファントム以外のデバイス*は、物理的に存在するデバイスです。 完全なサンプルについては、「 [WDTF のサンプルシナリオ](sample-wdtf-scenarios.md)」を参照してください。

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

このシナリオを実行するには、 **cscript.exe WDTF\_サンプル 1**を実行します。

### <a name="storing-target-information-by-using-context"></a>コンテキストを使用したターゲット情報の格納

VBScript などの一部のプログラミング言語では、オブジェクト参照を簡単に管理できません。 WDTF でのこの管理を簡略化するために、各ターゲットには、アクティブなオブジェクトへの参照を含む任意のキー/値のペアを格納するために使用できる[**コンテキスト**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdtf/nf-wdtf-iwdtftarget2-put_context)プロパティが用意されています。 このプロパティは、後で使用できるようにアクションインターフェイスを格納する場合に特に便利です。 次の VBScript コード例では、名前付き**コンテキスト**項目内に[**IWDTFSimpleIOStressAction2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdtfinterfaces/nn-wdtfinterfaces-iwdtfsimpleiostressaction2)アクションを格納します。

```cpp
deviceObj.Context("IWDTFSimpleIOStressAction2") = SimpleIOObj
```

後で、次のコード例に示すように、[**コンテキスト**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdtf/nf-wdtf-iwdtftarget2-put_context)を使用して再度アクセスすることで、 [**IWDTFSimpleIOStressAction2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdtfinterfaces/nn-wdtfinterfaces-iwdtfsimpleiostressaction2)インターフェイスを停止、一時停止、または再起動することができます。

```cpp
Device.Context("IWDTFSimpleIOStressAction2").Stop
```

### <a name="detecting-phantom-devices"></a>ファントムデバイスの検出

ファントムデバイスとは、以前にコンピューターに物理的にインストールされていたが、現在は存在していないデバイスのことです。 たとえば、ファントムデバイスは、プラグを抜いた USB マウスである場合があります。 オンまたはオフになっているコンピューターに接続されているデバイスの再インストールを高速化し、簡素化するために、Windows オペレーティングシステムではデバイスドライバーがインストールされたままになりますが、デバイスはファントムとしてマークされます。

デバイスの種類のターゲットには、ハードウェアの物理的な存在を指定する**IsPhantom**属性 (および**IsPhantom**= False に相当する**isattached**属性) が含まれます。 次の VBScript コード例では、コンピューターに物理的に存在するすべてのデバイスのコレクションを一覧表示します。

```cpp
Set NonPhantomDevices = WDTF.DeviceDepot.Query ("IsAttached")
```

属性キーワードの詳細については、「 [Sdel トークン](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)」を参照してください。

 

 




