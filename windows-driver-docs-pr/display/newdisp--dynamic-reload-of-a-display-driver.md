---
title: ディスプレイ ドライバーの NewDisp 動的再読み込み
description: ディスプレイ ドライバーの NewDisp 動的再読み込み
ms.assetid: 0f8ac27c-8a42-4032-9974-89a7463dccbb
keywords:
- newdisp.exe
- 動的ドライバー WDK Windows 2000 の表示を再読み込み
- ドライバーを動的に再読み込み WDK Windows 2000 の表示
- 再起動による動的な再読み込み WDK Windows 2000 の表示防止
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 326c4a27c513995c2465fd58eb0717168826021f
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63345526"
---
# <a name="newdisp-dynamic-reload-of-a-display-driver"></a>NewDisp: ディスプレイ ドライバーの動的再読み込み


## <span id="ddk_newdisp_dynamic_reload_of_a_display_driver_gg"></span><span id="DDK_NEWDISP_DYNAMIC_RELOAD_OF_A_DISPLAY_DRIVER_GG"></span>


ドライバー開発キット (DDK) は、ディスプレイ ドライバーを再起動しなくても動的に再読み込みを可能にするツールを提供します。 このツールと呼ばれる*newdisp.exe*、ディスプレイ ドライバーがドライバー コードの表示を更新するときに再起動が必要な以下のことで開発中のテストを迅速化します。

**注**  このツールは、Windows Vista と Windows Driver Kit (WDK) の今後のリリースでは使用できません。

 

**実行する*newdisp.exe***

1.  すべての Direct3D や OpenGL アプリケーションを閉じます。

2.  更新されたディスプレイ ドライバーの DLL をコピー、  *\\system32*ディレクトリ。

3.  実行*newdisp* (引数) を使用せずします。

毎回*newdisp*は、ディスプレイ ドライバーを再読み込み、呼び出されます。 呼び出し時にドライバーの参照が存在しないと仮定*newdisp*によって動的な再読み込みを実現します。

-   呼び出す**ChangeDisplaySettings** 640 x 480 x 16、読み込みし、16 色 VGA を実行するシステムで色、ディスプレイ ドライバー DLL と同じ原因で、古いはドライバー DLL をメモリからアンロードできるを表示します。

-   すぐに実行する別**ChangeDisplaySettings**を元のモードは、新しいディスプレイ ドライバー DLL から読み込まれると、コールバック *\\system32*ディレクトリ、および 16 の色VGA ディスプレイ ドライバー DLL を読み込む。

ドライバーがアクティブの Direct3D を持っている場合、ドライバーのインスタンスへの参照が存在する[ **WNDOBJ**](https://msdn.microsoft.com/library/windows/hardware/ff570599)、または[ **DRIVEROBJ** ](https://msdn.microsoft.com/library/windows/hardware/ff556162)オブジェクト。 ときに*newdisp*を実行しているドライバーのインスタンスへの参照が存在する、古いディスプレイ ドライバー DLL をアンロードすることはありませんが、これに応じて拡大縮小、新しいディスプレイ ドライバー DLL は読み込むことはありません。

*Newdisp*動的ドライバーが Windows 2000 と; を再起動しなくてもドライバーを再読み込みするには、後で追加されている機能の読み込み依存その結果、これでは動作しません Windows NT 4.0 と以前のオペレーティング システムのバージョン。 ない場合でも機能グラフィックス デバイスでは、VGA ドライバーを読み込むことができませんまたは VGA ドライバーで処理するモードではなく 640 x 480 x 16 のモードの色、ネイティブ ドライバーでを表示する場合。

なお*newdisp*再読み込みするビデオのミニポート ドライバーは現在原因しません。 ミニポート ドライバーが変更された場合は、インストールし、テスト システムを再起動する必要があります。

 

 





