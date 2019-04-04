---
title: AVStream、ミニドライバーの初期化
description: AVStream、ミニドライバーの初期化
ms.assetid: 666d6efb-93ec-43f3-87c5-ea1a3983bfd0
keywords:
- AVStream WDK、ミニドライバーの初期化
- ミニドライバー WDK AVStream、初期化しています
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 55f37482cee0942ee987d3972076aa0cc3435a39
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56553786"
---
# <a name="initializing-an-avstream-minidriver"></a>AVStream、ミニドライバーの初期化





独自の呼び出しでデバイスの初期化を処理しない AVStream ミニドライバー [ **KsInitializeDriver** ](https://msdn.microsoft.com/library/windows/hardware/ff562683)ミニドライバーから[ **DriverEntry**](https://msdn.microsoft.com/library/windows/hardware/ff554081)ルーチン。 **KsInitializeDriver** AVStream ドライバーのドライバー オブジェクトを初期化します、ディスパッチ、PnP IRP だけでなく、デバイスのメッセージを追加およびアンロードします。

呼び出し元に**KsInitializeDriver**、ミニドライバーがレジストリのパスへのポインターを初期化するためにドライバー オブジェクトと、必要に応じて、デバイス記述子オブジェクトへのポインターを渡します。 渡すことに注意してください、 [ **KSDEVICE\_記述子**](https://msdn.microsoft.com/library/windows/hardware/ff561691)オブジェクトは必要ありません。 ミニドライバーがデバイス記述子を渡すと場合、AVStream は AddDevice 時に指定された特性を持つデバイスを作成します。

デバイス記述子オブジェクトにはへのポインターが含まれています、 [ **KSDEVICE\_ディスパッチ**](https://msdn.microsoft.com/library/windows/hardware/ff561693)構造だけでなく、配列のフィルター記述子。 提供、 [ **KSFILTER\_記述子**](https://msdn.microsoft.com/library/windows/hardware/ff562553)の各フィルターの種類、ミニドライバーをサポートします。 ミニドライバーを呼び出すと[ **KsInitializeDriver**](https://msdn.microsoft.com/library/windows/hardware/ff562683)AVStream、ミニドライバーによって公開されているフィルターの種類ごとにフィルター ファクトリ オブジェクトを作成します。 個別のフィルターは、関連付けを作成する項目の作成 IRP の受信時にフィルター ファクトリによってインスタンス化されます。 各フィルター記述子の配列へのポインターを格納する[ **KSPIN\_記述子\_EX** ](https://msdn.microsoft.com/library/windows/hardware/ff563534)オブジェクト。 AVStream では、pin、ミニドライバーは、そのフィルターを通じて公開の種類ごとに関連するフィルターをピン留めするファクトリを作成します。

フィルターにピン留めする指定された型への接続が確立、AVStream 暗証番号 (pin) のファクトリは、暗証番号 (pin) オブジェクトを作成します。 各フィルターが少なくとも 1 つの pin を公開する必要がありますに注意してください。 ミニドライバーを使用して、 **InstancesNecessary** KSPIN のメンバー\_記述子\_EX が正常に機能するフィルターのために必要なこのピンの型のインスタンスの数を識別するためにします。 同様に、ミニドライバーが最大値を使用してインスタンス化できる、暗証番号 (pin) ファクトリ ピンの数を適用できます、 **InstancesPossible**この構造体のメンバー。

AVStream が 2 つの種類の処理をサポートしています:[フィルターを中心とした処理](filter-centric-processing.md)、および[暗証番号 (pin) を中心とした処理](pin-centric-processing.md)します。 記述子をレイアウトするときに、各フィルターの種類の処理の種類は実行を決定します。

### <a name="installing-an-avstream-minidriver"></a>AVStream、ミニドライバーをインストールします。

AVStream ミニドライバーは、システムを使用してドライバーをインストールする INF ファイルが必要です。 AVStream INF ファイルが説明されている共通の INF 形式に基づいて[INF ファイルを作成する](https://msdn.microsoft.com/library/windows/hardware/ff549520)します。 AVStream サンプル ドライバーで、Windows Driver Kit (WDK) で提供される INF ファイルを参照することもできます。 AVStream 固有の次のガイドラインに留意してください。

親デバイスの場合、ミニドライバーを作成する場合、 **AddReg** INF ファイルのセクションを含める必要があります。

```INF
[ParentName.AddReg]
HKR,"ENUM\[DeviceName]",pnpid,,"[string]"
```

子デバイスの場合、ミニドライバーを作成する場合、 **AddReg**セクションを含める必要があります。

```INF
[Manufacturer]
...=ChildName
[ChildName]
...=ChildName.Device,AVStream\[string]
```

注"AVStream"ストリーム クラス ドライバーの"Stream"となります。

すべての AVStream ミニドライバーの INF ファイルでフィルターに固有の参照文字列が一致する必要があります、 **ReferenceGuid**のメンバー、 [ **KSFILTER\_記述子**](https://msdn.microsoft.com/library/windows/hardware/ff562553)構造体。

記述子の詳細については、[AVStream 記述子](avstream-descriptors.md)を参照してください。
