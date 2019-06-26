---
title: IViewHelper 複製ビュー COM オブジェクトの使用
description: IViewHelper 複製ビュー COM オブジェクトの使用
ms.assetid: 2f264c5d-0e12-4116-9561-16dce99ce1fe
keywords:
- IViewHelper について、TMM WDK の表示
- モニターの構成の WDK 表示、IViewHelper について
- 新しいモニターを検出するモニターの構成の WDK 画面
- モニターの構成の WDK の表示、永続化
- IViewHelper について、ビデオの存在するネットワーク WDK を表示します。
- IViewHelper について、VidPN WDK の表示
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 68a9a030264a6edbdb0bfafd854b8793512aa1ba
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67373582"
---
# <a name="using-an-iviewhelper-clone-view-com-object"></a>IViewHelper 複製ビュー COM オブジェクトの使用


TMM がハードウェア ベンダーの複製-ビューのメソッドを使用して[IViewHelper](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)および永続化されたモニターの構成で新しいモニターの COM インターフェイスのオブジェクト。 永続化されたモニターの構成では、TMM は、モニターに (つまり、表示モードとトポロジのデータ) データを表示を復元します。 TMM がこのデータの表示をユーザー モードのディスプレイ ドライバーを通じてに渡すことができます、 [ **IViewHelper::SetConfiguration** ](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff568176(v=vs.85))のため、ドライバーを変更したりその他の表示データ (たとえば、ガンマまたはテレビのフォールド メソッド設定)。

エラー、[ビデオ存在するネットワーク (VidPN)](multiple-monitors-and-video-present-networks.md)のメソッドによって返される[IViewHelper](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)します。 そのため、TMM、不適切なトポロジを適用する場合は、VidPN は失敗し、エラー結果が呼び出し元の関数に渡されます。 2 つのソースへのターゲット マッピングまたは識別できない、VidPN ターゲットまたはソースの識別子を使用して、不適切なトポロジの例を示します。

TMM 決定、 [IViewHelper](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)を介して COM インターフェイス オブジェクト、 **UserModeDriverGUID**レジストリ値の文字列します。 ハードウェア ベンダーは、この値をレジストリ キーを追加する必要があります、 **DeviceKey**表示のメンバー\_デバイス構造体を指定します。 Win32 への呼び出し**EnumDisplayDevices**表示で、このレジストリ キーの情報を返します\_デバイスを*lpDisplayDevice*パラメーターを指します。 複数**DeviceKey**名前存在、それらのキーの下にこの値が表示されます。 デバイス キーの例を次に、 **UserModeDriverGUID**レジストリ値の文字列します。

```registry
[HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Video\{7661971C-A9BD-48B5-ACBC-298A8826535D}\0000]
"UserModeDriverGUID"="{YYYYYYYY-YYYY-YYYY-YYYY-YYYYYYYYYYYY}"
```

Com を読み込む、 [IViewHelper](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index) COM インターフェイス オブジェクト、COM オブジェクトは、プロセス (インプロセス) ハンドラーとして登録する必要があり、スレッド処理モデル両方を指定する必要があります。 登録されている GUID が内の GUID と一致する必要があります**UserModeDriverGUID**します。 両方にスレッド モデル属性については、Microsoft Windows SDK のドキュメントを参照してください。

だけする必要がありますコピーし、正しくコンパイルされたバージョンの登録[IViewHelper](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)システム ディレクトリ内の COM インターフェイス オブジェクトの Dll。 つまり、する必要がありますのみをコピーし、64 ビットの登録**IViewHelper** 64 ビット オペレーティング システムと 32 ビットの DLL **IViewHelper** 32 ビットのオペレーティング システム用の DLL。 2 つの DLL バイナリを同じコンピューターに同時に存在することはできません。 TMM は、2 つのバイナリは Windows on Windows (WOW) を使用しても、同じコンピューターに同時に存在する場合に動作しません。

 

 





