---
title: ドライバーの初期化とクリーンアップ
description: ドライバーの初期化とクリーンアップ
ms.assetid: 57f22818-a298-4f9a-87a6-5ca4d97bf32b
keywords:
- 描画の WDK GDI、初期化の説明
- グラフィックス ドライバー WDK Windows 2000 を表示する説明を初期化しています
- GDI WDK Windows 2000 の表示、初期化の説明
- グラフィック ドライバー WDK Windows 2000 を表示、初期化、説明
- DrvEnableDriver
- WDK の GDI 描画のクリーンアップ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: fb0f1436dcc7a6ff015eec75e900388e8b7f2097
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67381098"
---
# <a name="driver-initialization-and-cleanup"></a>ドライバーの初期化とクリーンアップ


## <span id="ddk_driver_initialization_and_cleanup_gg"></span><span id="DDK_DRIVER_INITIALIZATION_AND_CLEANUP_GG"></span>


のみエクスポート中に、デバイス ドライバーは、いくつかまたは複数の関数を実装することが、 [ **DrvEnableDriver** ](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvenabledriver) GDI にします。 ドライバーは、関数テーブルを介してサポートされているその他の関数を公開します。 GDI は、デバイス ドライバーへの最初の呼び出しは、 **DrvEnableDriver**関数。 この関数内で、ドライバーは、渡されたが[ **DRVENABLEDATA** ](https://docs.microsoft.com/windows/desktop/api/winddi/ns-winddi-tagdrvenabledata) GDI は他に確認できるように構造体*DrvXxx*関数がサポートされていると場所配置されています。 ドライバーは、DRVENABLEDATA で次の情報を指定します。

-   **IDriverVersion**メンバーには、グラフィックス、特定の Windows オペレーティング システムのバージョンの DDI バージョン番号が含まれています。 *Winddi.h*ヘッダーは、次の定数を定義します。

    <table>
    <colgroup>
    <col width="50%" />
    <col width="50%" />
    </colgroup>
    <thead>
    <tr class="header">
    <th align="left">定数</th>
    <th align="left">オペレーティング システムのバージョン</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td align="left"><p>DDI_DRIVER_VERSION_NT4</p></td>
    <td align="left"><p>Windows NT 4.0</p></td>
    </tr>
    <tr class="even">
    <td align="left"><p>DDI_DRIVER_VERSION_NT5</p></td>
    <td align="left"><p>Windows 2000</p></td>
    </tr>
    <tr class="odd">
    <td align="left"><p>DDI_DRIVER_VERSION_NT5_01</p></td>
    <td align="left"><p>Windows XP</p></td>
    </tr>
    </tbody>
    </table>

     

これらの定数の使用方法の詳細については、次を参照してください。 [ **DRVENABLEDATA**](https://docs.microsoft.com/windows/desktop/api/winddi/ns-winddi-tagdrvenabledata)します。

-   **C**メンバーには、配列内の DRVFN 構造体の数が含まれています。

-   **Pdrvfn**の配列を指すメンバー [ **DRVFN** ](https://docs.microsoft.com/windows/desktop/api/winddi/ns-winddi-_drvfn)構造体をサポートされている関数とそのインデックスを一覧表示します。

ドライバーの有効化以外の関数を呼び出すし、関数を無効にする、GDI のドライバーする必要があります、関数の名前と場所を利用 GDI。

中に[ **DrvEnableDriver** ](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvenabledriver) 1 回限りの初期化を実行することも、セマフォの割り当てなどのドライバー実際に有効にしないでください中にハードウェア**DrvEnableDriver**. ドライバーのハードウェアの初期化が発生する[ **DrvEnablePDEV** ](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvenablepdev)関数。 同様に、ドライバーを有効にする、画面で、 [ **DrvEnableSurface** ](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvenablesurface)関数。

GDI の呼び出し、 [ **DrvDisableDriver** ](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvdisabledriver)アンロードしようとしていますが、ドライバーに通知します。 この呼び出しに応答してでは、ドライバーはすべてのリソースともこの時点で、ドライバーによって割り当てられたメモリを解放する必要があります。

GDI がドライバーを呼び出す場合は、ハードウェアをリセットする必要があります、 [ **DrvAssertMode** ](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvassertmode)関数。

 

 





