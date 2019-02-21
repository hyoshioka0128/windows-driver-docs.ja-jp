---
title: 複数の PDEVs をサポートしています。
description: 複数の PDEVs をサポートしています。
ms.assetid: e06fe2da-b677-4649-bf7a-09a8f2ddfc6b
keywords:
- ディスプレイ ドライバー WDK Windows 2000 では、デスクトップ管理
- デスクトップ管理 WDK Windows 2000 の表示
- PDEVs WDK Windows 2000 の複数の表示
- PDEV WDK Windows 2000 の表示
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 73767e0a78153195ca162eb8dc5a3805f09374fb
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56536673"
---
# <a name="supporting-multiple-pdevs"></a>複数の PDEVs をサポートしています。


## <span id="ddk_supporting_multiple_pdevs_gg"></span><span id="DDK_SUPPORTING_MULTIPLE_PDEVS_GG"></span>


このセクションでは、アプリケーション作成方法、新しい PDEV 現在 PDEV がまだ読み込まれて表示されます。 コントロール パネルの表示のプログラムでは、ディスプレイ ドライバーが新しい PDEV を新しいデスクトップを作成するアプリケーションの可能性があるため、追加の PDEVs の有効化、サポートする必要があります。 具体的には、エンド ユーザーは、表示のアイコンの変更、サイズ、色の数などの要素にテストを実行して、画面のリフレッシュ レート。 表示プログラムでは、新しいデスクトップ表示のモードの変更をテストするには、動的に作成します。

GDI は、ユーザーがモードの変更を要求する表示アイコンをクリックしたときに、次の手順を実行します。 次の手順では、Direct3D、WNDOBJ、または DRIVEROBJ のアクティブなオブジェクトが現在ドライバーのインスタンスによって所有されていないことを前提としています。

1.  現在 PDEV を一時的に無効にします。
    -   呼び出す[ **DrvAssertMode** ](https://msdn.microsoft.com/library/windows/hardware/ff556178) (古い PDEV インスタンス)。 使用して呼び出しが行われた**FALSE**ミニポート ドライバーが、コントロールを想定することがある場合と**TRUE** PDEV を使用する場合。

2.  (新しい PDEV インスタンスで必要な) 場合は、新しいドライバーを読み込む
    -   呼び出す[ **DrvEnableDriver** ](https://msdn.microsoft.com/library/windows/hardware/ff556210) (新しいドライバーのインスタンス)。

3.  新しい PDEV を作成します。
    -   呼び出す[ **DrvEnablePDEV** ](https://msdn.microsoft.com/library/windows/hardware/ff556211) (新しい PDEV インスタンス)。
    -   呼び出す[ **DrvCompletePDEV** ](https://msdn.microsoft.com/library/windows/hardware/ff556181) (新しい PDEV インスタンス)。
    -   呼び出す[ **DrvEnableSurface** ](https://msdn.microsoft.com/library/windows/hardware/ff556214) (新しい PDEV インスタンス)。

4.  (DirectDraw はドライバーによって接続されている) 場合は、DirectDraw 情報を取得します。 2 つ目の呼び出しを[ **DrvGetDirectDrawInfo** ](https://msdn.microsoft.com/library/windows/hardware/ff556229)最初の呼び出しが成功した場合にのみが行われます。
    -   呼び出す*DrvGetDirectDrawInfo* (新しい PDEV インスタンス)。
    -   呼び出す*DrvGetDirectDrawInfo* (新しい PDEV インスタンス)。

5.  DirectDraw を有効にする (ドライバーと以前の呼び出しによって接続されている場合*DrvGetDirectDrawInfo*に成功しました)。
    -   呼び出す[ **DrvEnableDirectDraw** ](https://msdn.microsoft.com/library/windows/hardware/ff556208) (新しい PDEV インスタンス)。

6.  (両方のインスタンスが同じドライバーを使用して、ドライバーによって DirectDraw がフックされている) 場合は、古い PDEV 状態を新しい PDEV インスタンスにコピーします。
    -   呼び出す[ **DrvResetPDEV**](https://msdn.microsoft.com/library/windows/hardware/ff556276)します。

7.  その新しい HDEV アソシエーションの各ドライバーのインスタンスに通知します。 最初の呼び出し[ **DrvCompletePDEV** ](https://msdn.microsoft.com/library/windows/hardware/ff556181)新しいドライバーのインスタンスを通知します。 2 番目の呼び出しが古いドライバーのインスタンスに通知します。

    -   呼び出す*DrvCompletePDEV* (新しい PDEV インスタンス)。
    -   呼び出す*DrvCompletePDEV* (古い PDEV インスタンス)。

    ドライバーでは、gdi、HDEV を必要とする任意のコールバックで新しい HDEV 値を使用する必要があります。

8.  DirectDraw を無効にする (ドライバーと DirectDraw によって接続されている場合は、有効)。
    -   呼び出す[ **DrvDisableDirectDraw** ](https://msdn.microsoft.com/library/windows/hardware/ff556195) (古い PDEV インスタンス)。

9.  画面を無効にします。
    -   呼び出す[ **DrvDisableSurface** ](https://msdn.microsoft.com/library/windows/hardware/ff556200) (古い PDEV インスタンス)。

10. PDEV を無効にします。
    -   呼び出す[ **DrvDisablePDEV** ](https://msdn.microsoft.com/library/windows/hardware/ff556198) (古い PDEV インスタンス)。

この例では、GDI 一時的に無効に現在 PDEV ユーザーの適用 をクリックするし、表示モードの選択 ダイアログ ボックスに一致する 2 つ目の PDEV が作成されます。 テスト モードの場合、ディスプレイの画面で、ビットマップを表示する、2 つ目の PDEV が破棄され、表示プログラム、デスクトップの元の PDEV を復元します。 その設定を元に戻すことはできません、システムは使用できなくなる、設定は、ハードウェアとドライバーの互換性がない場合に注意してください。

ドライバーの現在のインスタンスに、Direct3D、WNDOBJ、または DRIVEROBJ オブジェクトが所有している場合の以前のモードの変更のシーケンス、ドライバーの表示 (Windows 2000 以降では、DirectDraw は常に有効になっているすぐドライバーが初期化されるように注意してください) を次のように変更します。

-   所有しているドライバーのインスタンスの破棄は延期されます。 2 番目の呼び出しを具体的には、 [ **DrvCompletePDEV** ](https://msdn.microsoft.com/library/windows/hardware/ff556181)手順 7. で、手順 8、し、手順 9. のモードの変更時に行われません。 呼び出しにより、古いドライバーのインスタンスが無効になっている結果として、 [ **DrvAssertMode**](https://msdn.microsoft.com/library/windows/hardware/ff556178)(**FALSE**) では、手順 1 とは、システムは、モードまで保持されますに戻す元のモードでは、インスタンスを参照するすべてのオブジェクトが破棄されるまで、または。

-   場合は、システムは、参照元のオブジェクトが破棄される前に、元のモードに戻ります、ドライバーの元のインスタンスが復元します。 手順 2 ~ 5 が発生しないし、元のドライバーのインスタンスへの呼び出しで再び有効に*DrvAssertMode*(**TRUE**) (手順 1 を参照してください)。

-   システムは、すべての参照する前に元のモードに戻すに戻すことできない場合オブジェクトが破棄され、最終的に参照元オブジェクトが破棄されるときに、ドライバーのインスタンスは破棄されます。 2 番目の呼び出しには、 *DrvCompletePDEV*手順 7. で、手順 8、および手順 9 が (たとえば、所有しているすべてのプロセスが終了した) 場合、最終的に参照元オブジェクトが破棄される時点で発生します。

つまりは、いつでもドライバーを非アクティブなインスタンスを破棄する Direct3D や OpenGL ドライバーを呼び出すことができます。 ドライバーの別のインスタンスが現在アクティブな場合でも場合、ドライバーが全画面表示 MS-DOS モード、または別のドライバーが完全 (VGA driver) などのハードウェアを所有している場合、これらのドライバーを呼び出すことができます。 その結果、 [ **DrvDisableDirectDraw**](https://msdn.microsoft.com/library/windows/hardware/ff556195)、 [ **DrvDisableSurface**](https://msdn.microsoft.com/library/windows/hardware/ff556200)、および[ **DrvDisablePDEV** ](https://msdn.microsoft.com/library/windows/hardware/ff556198)デバイスがグラフィック モードであると、排他アクセスを所有しているドライバーの (手順 8 ~ 10 を参照してください) ルーチンとは限りません。 一般的な規則としてドライバーする必要がありますいない操作で、ビデオ ハードウェアの*DrvDisableXxx*ルーチンのインスタンスが現在アクティブであることを知らない限り (過去の状態を記憶して[ **DrvAssertMode** ](https://msdn.microsoft.com/library/windows/hardware/ff556178)呼び出します)。

**注**   A PDEV はドライバーにプライベートであり、すべての情報と関連付けられている物理デバイスを表すデータが含まれています。 複数 PDEVs を作成するには、グラフィック ドライバーは、次の要件の両方で満たす必要があります。
1.  ドライバーは、PDEV 構造体のメンバーを逆参照ではなくグローバル変数を使用する必要があります。 グローバル変数を使用している場合はこれらを含むや新しい PDEV を作成すると、またはいずれかの復元、古いときに、ランダムなデータを指す可能性があります。 すべての状態情報は、PDEV で保存する必要があります。 PDEV は常にすべてのグラフィックス操作に渡され、取得またはグローバル データを設定するためです。

2.  [ **DrvDisableSurface**](https://msdn.microsoft.com/library/windows/hardware/ff556200)、 [ **DrvDisablePDEV**](https://msdn.microsoft.com/library/windows/hardware/ff556198)、および[ **DrvDisableDriver**](https://msdn.microsoft.com/library/windows/hardware/ff556196)ようにアプリケーションを作成および追加の PDEVs を破棄して場合によっては 1 つ以上のドライバーの読み込み、グラフィックス ドライバーでルーチンを実装する必要があります。

 

**注**  ドライバーのバージョン番号が 1.0 の場合は、GDI が 2 つ目の PDEV を作成するドライバーを呼び出しません。 ドライバーのバージョン番号が返される[ **DRVENABLEDATA**](https://msdn.microsoft.com/library/windows/hardware/ff556206)します。

 

**注**  現在読み込まれているドライバーよりもさまざまなドライバーを使用して表示プログラムのテストのビットマップが表示される場合があります。 たとえば、16 色のモードでシステムが実行されている場合、VGA ドライバーとテスト、VGA64K を 64 K color モードのディスプレイ ドライバー、VGA64K ドライバーを動的に読み込まれ、テストの完了時にアンロードされます。

 

 

 





