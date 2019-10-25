---
title: IViewHelper 複製ビュー COM オブジェクトの使用
description: IViewHelper 複製ビュー COM オブジェクトの使用
ms.assetid: 2f264c5d-0e12-4116-9561-16dce99ce1fe
keywords:
- TMM WDK display、IViewHelper について
- 監視構成 WDK display、IViewHelper について
- 構成の監視 WDK 表示、新しいモニターの検出
- 監視の構成 WDK の表示、永続化
- ビデオの現在のネットワーク WDK 表示、IViewHelper について
- VidPN WDK display、IViewHelper について
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f9491779601946a4df53684b2145e3757a0e82b3
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72829290"
---
# <a name="using-an-iviewhelper-clone-view-com-object"></a>IViewHelper 複製ビュー COM オブジェクトの使用


TMM は、ハードウェアベンダーの複製ビュー [IViewHelper](https://docs.microsoft.com/windows-hardware/drivers/ddi/index) COM インターフェイスオブジェクトのメソッドを、新しいモニターおよび永続化されたモニター構成で使用します。 保存されたモニター構成では、TMM によってモニターにデータ (表示モードとトポロジデータ) が表示されます。 TMM は、 [**IViewHelper:: SetConfiguration**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff568176(v=vs.85))メソッドを使用して、この表示データをユーザーモードの表示ドライバーに渡すことができます。これにより、ドライバーは他の表示データ (ガンマや TV の設定など) で変更またはフォールドすることができます。

[ビデオの現在のネットワーク (VidPN)](multiple-monitors-and-video-present-networks.md)からのエラーは、 [IViewHelper](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)のメソッドを通じて返されます。 そのため、TMM が不適切なトポロジを適用すると、VidPN は失敗し、呼び出し元の関数にエラーの結果が返されます。 ターゲットを2つのソースにマップするか、または VidPN が識別できないターゲットまたはソース識別子を使用して、不適切なトポロジの例を示します。

TMM は、 **UserModeDriverGUID** string レジストリ値を使用して[IViewHelper](https://docs.microsoft.com/windows-hardware/drivers/ddi/index) COM インターフェイスオブジェクトを決定します。 ハードウェアベンダーは、表示\_デバイス構造の**Devicekey**メンバーが指定するレジストリキーの下に、この値を追加する必要があります。 Win32 **Enumdisplaydevices**関数を呼び出すと、 *lpdisplaydevice*パラメーターが指す表示\_デバイスにこのレジストリキー情報が返されます。 複数の**devicekey**名が存在する場合は、これらの各キーの下にこの値が表示されます。 デバイスキーと**UserModeDriverGUID** string レジストリ値の例を次に示します。

```registry
[HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Video\{7661971C-A9BD-48B5-ACBC-298A8826535D}\0000]
"UserModeDriverGUID"="{YYYYYYYY-YYYY-YYYY-YYYY-YYYYYYYYYYYY}"
```

Com が[IViewHelper](https://docs.microsoft.com/windows-hardware/drivers/ddi/index) com インターフェイスオブジェクトを読み込むには、com オブジェクトをインプロセス (インプロセス) ハンドラーとして登録し、スレッドモデルを両方とも登録する必要があります。 登録されている GUID は、 **UserModeDriverGUID**の guid と一致している必要があります。 両方のスレッドモデル属性の詳細については、Microsoft Windows SDK のドキュメントを参照してください。

[IViewHelper](https://docs.microsoft.com/windows-hardware/drivers/ddi/index) COM インターフェイスオブジェクト dll の正しくコンパイルされたバージョンは、システムディレクトリにのみコピーして登録する必要があります。 つまり、64ビットオペレーティングシステムの場合は64ビット**IViewHelper** dll をコピーして登録し、32ビットオペレーティングシステムの場合は32ビット**IViewHelper** dll のみを登録する必要があります。 2つの DLL バイナリは、同じコンピューター上に同時に存在することはできません。 Windows on Windows (WOW) を使用していても、2つのバイナリが同時に同じコンピューターに存在する場合、TMM は正しく動作しません。

 

 





