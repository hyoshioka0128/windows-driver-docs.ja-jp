---
title: Windows Display Driver Model (WDDM) の 64 ビット問題
description: Windows Display Driver Model (WDDM) の 64 ビット問題
ms.assetid: ab391fca-bc98-4e98-9531-7a1d24ee173d
keywords:
- 64-bit WDK display
- ディスプレイドライバーモデル WDK Windows Vista、64ビット
- Windows Vista display driver model WDK、64ビット
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 866a98eb54c80414cfd25ebb4025563541adfdb9
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840572"
---
# <a name="windows-display-driver-model-wddm-64-bit-issues"></a>Windows Display Driver Model (WDDM) の 64 ビット問題


32ビットアプリケーションを64ビットオペレーティングシステムで実行できるようにするには、64ビットアプリケーションで必要とされる、64ビットのユーザーモード表示ドライバーに加えて、32ビットのユーザーモード表示ドライバーを提供する必要があります。 ただし、64ビットのオペレーティングシステムでは、ディスプレイミニポートドライバーの64ビットバージョンのみが必要です。 Windows on Windows (WOW64) を使用すると、32ビットのアプリケーションを64ビットのオペレーティングシステムで実行できます。 詳細については、「 [64 ビットドライバーでの32ビット i/o のサポート](https://docs.microsoft.com/windows-hardware/drivers/kernel/supporting-32-bit-i-o-in-your-64-bit-driver)」を参照してください。

32ビットのユーザーモード表示ドライバーを64ビットオペレーティングシステムにインストールするには、グラフィックスデバイスのディスプレイミニポートドライバーの INF ファイルの [レジストリの追加] セクションで、次のエントリを設定する必要があります。 これは、ドライバーのインストール時に、32ビットのユーザーモード表示ドライバーの DLL 名がレジストリに追加されるようにするために必要です。

```inf
 [Xxx_SoftwareDeviceSettings]
...
 HKR,, UserModeDriverNameWow, %REG_MULTI_SZ%, Xxx.dll
...
```

INF ファイルには、32ビットのユーザーモード表示ドライバーをシステムの% systemroot%\\SysWOW64 ディレクトリにコピーするようにオペレーティングシステムに指示するための情報が含まれている必要があります。 詳細については、「 [**Inf CopyFiles ディレクティブ**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-copyfiles-directive)」と「 [**Inf Destinationdirs」セクション**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-destinationdirs-section)を参照してください。

WOW64 は、D3DDDICB などの非透過的または型指定されていないデータ構造を処理できないので、 [**Pfnallocatecb**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_allocatecb)関数を介して渡された構造体の[**割り当て\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/ns-d3dumddi-_d3dddicb_allocate)は、32ビットから64ビットへの自動変換を実行できません。 したがって、WOW64 が正常に機能するためには、64ビットのオペレーティングシステムで実行する32ビットのユーザーモードディスプレイドライバーを記述するときに、次の項目を考慮する必要があります。

-   複数のオペレーティングシステムに依存するポインターまたはデータ型を避けてください。たとえば、\_T や HANDLE などです。 これらの可変幅データ型は、構造体変数全体のサイズを作成することに加えて、個々のメンバーの配置と位置が異なるようにします。 可変幅のメンバーを使用できない場合は、別のメンバーを追加して、データ構造が32ビットのユーザーモード表示ドライバーからのものであることを示すことができます。 64ビット表示ミニポートドライバーは、変換を適切に実行できます。

-   可変幅のメンバーが存在しない場合でも、アーキテクチャ固有のアラインメント要件を考慮する必要がある場合があります。 たとえば、x64 では、UINT64 (または QWORD) が8バイトでアラインされている必要があります。 標準の32ビットコンパイラによってコンパイルされた32ビットのユーザーモード表示ドライバーでは、これらのネイティブ64ビット型が正しく配置されていない可能性があるため、64ビットディスプレイミニポートドライバーは、32ビットのユーザーモード表示ドライバーのデータに正確にアクセスできない可能性があります。 ただし、適切な**プラグマ**コンパイラディレクティブを使用して強制的にアラインメントできます。 **プラグマ**コンパイラディレクティブを使用すると、32ビットオペレーティングシステム上の領域がわずかに無駄になる可能性がありますが、これにより、32ビットおよび64ビットのオペレーティングシステムで、同じ32ビットユーザーモードディスプレイドライバーを使用できます。 適切な**プラグマ**コンパイラディレクティブを使用して配置を強制できない場合は、64ビットオペレーティングシステム上で WOW64 を使用して実行される32ビットユーザーモード表示ドライバーが、32ビットで実行されている32ビットユーザーモード表示ドライバーと異なる必要があります。オペレーティング システム。

 

 





