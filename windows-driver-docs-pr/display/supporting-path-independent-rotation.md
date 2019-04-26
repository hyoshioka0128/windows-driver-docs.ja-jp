---
title: パスに依存しない回転のサポート
description: Windows 8.1 Update 以降では、オペレーティング システムは、ランドス ケープ最初に表示する最も考えられる解決策を縦最初の複製の表示をサポートします。
ms.assetid: 136CEDA5-2839-4E6E-A032-1A9222C769C6
ms.date: 10/30/2018
ms.localizationpriority: medium
ms.openlocfilehash: 95eceac4bc6d2091b7e67c82d4db142d6bc6b728
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63350178"
---
# <a name="span-iddisplaysupportingpath-independentrotationspansupporting-path-independent-rotation"></a><span id="display.supporting_path-independent_rotation"></span>パスに依存しない回転をサポートしています。


Windows 8.1 Update 以降では、オペレーティング システムは、ランドス ケープ最初に表示する最も考えられる解決策を縦最初の複製の表示をサポートします。 ディスプレイのミニポート ドライバーで、適切なオフセット値を設定する必要があります、 [ **D3DKMDT\_VIDPN\_存在\_パス\_回転\_サポート**](https://msdn.microsoft.com/library/windows/hardware/ff546705)用の構造、*プライマリ複製パス*と*セカンダリの複製パス*」の説明に従って、[ディスプレイのミニポート ドライバーでのサポートのローテーション](supporting-rotation-in-a-display-miniport-driver.md)。

これらのデバイス ドライバー インターフェイス (Ddi) は、Windows 8.1 Update の新機能です。

-   D3DKMDT_VPPR_GET_CONTENT_ROTATION
-   D3DKMDT_VPPR_GET_CONTENT_ROTATION_PART
-   D3DKMDT_VPPR_GET_OFFSET_ROTATION

Ddi これらは、Windows 8.1 Update で更新されます。

-   [**D3DKMDT\_VIDPN\_PRESENT\_PATH\_ROTATION\_SUPPORT**](https://msdn.microsoft.com/library/windows/hardware/ff546705)

-   [**D3DKMDT\_VIDPN\_PRESENT\_PATH\_ROTATION**](https://msdn.microsoft.com/library/windows/hardware/ff546700)

## <a name="span-idcloningaportrait-firstdevicespanspan-idcloningaportrait-firstdevicespanspan-idcloningaportrait-firstdevicespancloning-a-portrait-first-device"></a><span id="Cloning_a_portrait-first_device"></span><span id="cloning_a_portrait-first_device"></span><span id="CLONING_A_PORTRAIT-FIRST_DEVICE"></span>縦最初のデバイスの複製


ランドス ケープ-1 つ目のモニターに複製する縦最初のデバイスのドライバーが要求されると、その前に、ソース モードを報告する必要があります (*x*、*y*) 複製のプライマリ パスで解像度に一致する解像度。 セカンダリの複製のパスは、90 および 270 度のオフセット値をサポートし、でした ([**D3DKMDT\_VIDPN\_存在\_パス\_回転\_サポート**](https://msdn.microsoft.com/library/windows/hardware/ff546705).**Offset90**または **。Offset270**は**TRUE**)。 VidPN がでコミットされるときに、 [ **D3DKMDT\_VIDPN\_存在\_パス\_回転**](https://msdn.microsoft.com/library/windows/hardware/ff546700) 90 - または 270-を示す列挙値角度オフセット、つまり、(*x*、*y*) 解決策が反転することでこの特定のパス。

既定では、オペレーティング システムは、内部の表示 パネルにセカンダリの複製のパスを選択します。 内部のパネルが縦最初、オペレーティング システムが必要ですがある場合に、 [ **D3DKMDT\_VIDPN\_存在\_パス\_回転\_サポート**](https://msdn.microsoft.com/library/windows/hardware/ff546705).**Offset270**横モードで表示の内部パネルに表示するためにこのパスに設定します。 セカンダリの複製のパスに外部モニターを横最初の場合、オペレーティング システムをサポートするドライバーが必要ですが**D3DKMDT\_VIDPN\_存在\_パス\_回転\_サポート**.**Offset90**、これはまれなシナリオを使用する可能性があります。

## <a name="span-idexampleclonescenariosspanspan-idexampleclonescenariosspanspan-idexampleclonescenariosspanexample-clone-scenarios"></a><span id="Example_clone_scenarios"></span><span id="example_clone_scenarios"></span><span id="EXAMPLE_CLONE_SCENARIOS"></span>複製シナリオの例


高さ 1080 ピクセルでランドス ケープ最初テレビに複製モードでネイティブの解像度 800 (幅) x 1280 ピクセル (高さ) を使用して縦最初のデバイスが接続されている一般的なシナリオを次に示します。 ドライバーはオペレーティング システムにこの情報を報告しました。

<span id="source_mode"></span><span id="SOURCE_MODE"></span>ソース モード  
1280 x 800

<span id="TV_target_mode"></span><span id="tv_target_mode"></span><span id="TV_TARGET_MODE"></span>テレビ ターゲット モード  
1920 x 1080 (縦横比は、スケーリングを保持)

<span id="device_target_mode"></span><span id="DEVICE_TARGET_MODE"></span>デバイス ターゲット モード  
800 x 1280 (identity スケーリング)

<span id="primary_clone_path__TV_"></span><span id="primary_clone_path__tv_"></span><span id="PRIMARY_CLONE_PATH__TV_"></span>プライマリの複製のパス (テレビ)  
ドライバーのみをサポート[ **D3DKMDT\_VIDPN\_存在\_パス\_回転\_サポート**](https://msdn.microsoft.com/library/windows/hardware/ff546705).**Offset0**も通常のローテーションのサポート

<span id="secondary_clone_path__device_"></span><span id="SECONDARY_CLONE_PATH__DEVICE_"></span>セカンダリの複製のパス (デバイス)  
ドライバーのみをサポート[ **D3DKMDT\_VIDPN\_存在\_パス\_回転\_サポート**](https://msdn.microsoft.com/library/windows/hardware/ff546705).**Offset270**も通常のローテーションのサポート

<span></span>  

呼び出し、 [ *DxgkDdiCommitVidPn* ](https://msdn.microsoft.com/library/windows/hardware/ff559597)関数がからこれらのパス設定で、返される、 [ **D3DKMDT\_VIDPN\_PRESENT\_パス\_回転**](https://msdn.microsoft.com/library/windows/hardware/ff546700)列挙体。

<span id="primary_clone_path__TV_"></span><span id="primary_clone_path__tv_"></span><span id="PRIMARY_CLONE_PATH__TV_"></span>プライマリの複製のパス (テレビ)  
**D3DKMDT\_VPPR\_IDENTITY**

<span id="secondary_clone_path__device_"></span><span id="SECONDARY_CLONE_PATH__DEVICE_"></span>セカンダリの複製のパス (デバイス)  
**D3DKMDT\_VPPR\_IDENTITY\_OFFSET270**

オペレーティング システムでは、指定されたコンテンツを 270 度回転するドライバーが必要です。

場合で、**表示**コントロール パネルの**向き**ドロップダウン ボックスで、ユーザーが、 **(反転) ランドス ケープ**オプションへの呼び出し、 [ *DxgkDdiCommitVidPn* ](https://msdn.microsoft.com/library/windows/hardware/ff559597)からこれらのパス設定で関数を返します、 [ **D3DKMDT\_VIDPN\_存在\_パス\_回転**](https://msdn.microsoft.com/library/windows/hardware/ff546700)列挙体。

<span id="primary_clone_path__TV_"></span><span id="primary_clone_path__tv_"></span><span id="PRIMARY_CLONE_PATH__TV_"></span>プライマリの複製のパス (テレビ)  
**D3DKMDT\_VPPR\_ROTATE180**

<span id="secondary_clone_path__device_"></span><span id="SECONDARY_CLONE_PATH__DEVICE_"></span>セカンダリの複製のパス (デバイス)  
**D3DKMDT\_VPPR\_ROTATE180\_OFFSET270**

デスクトップ ウィンドウ マネージャー (DWM) のコンテンツ 180 ° 回転既に場合、ドライバーする必要がありますも回転セカンダリの複製のパスで別の 270 度。 それ以外の場合、ドライバーはコンテンツ、テレビ番組用とデバイスの 90 °、180 度を回転する必要があります。 回転するには、コンテンツに、次の設定をする必要があることをドライバーに注意してください、**回転**のメンバー、 [ **DXGK\_PRESENTFLAGS** ](https://msdn.microsoft.com/library/windows/hardware/ff562005)構造体。

 

 





