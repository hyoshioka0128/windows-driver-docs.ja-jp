---
title: ミラー ドライバー
description: ミラー ドライバー
ms.assetid: 7231375a-969b-4c55-83d4-96ba5caade20
keywords:
- ディスプレイ ドライバー WDK Windows 2000 では、ミラー ドライバー
- ミラー ドライバー WDK Windows 2000 の表示
- 仮想デスクトップ WDK の Windows 2000 を表示します。
- グローバル デスクトップのミラーリング WDK Windows 2000 の表示
- GDI 仮想デスクトップ WDK Windows 2000 の表示
- 仮想デバイスを Windows 2000 の WDK 表示のミラーリング
- ビデオのミニポート ドライバー WDK Windows 2000 では、ミラー ドライバー
- 支援技術とミラー ドライバー
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 432931f02678104afb7d657b26aeff5b5a40ca4f
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385591"
---
# <a name="mirror-drivers"></a>ミラー ドライバー


## <a name="span-idinthissectionspanin-this-section"></a><span id="in_this_section"></span>このセクションの内容


-   [リモートのディスプレイ ドライバー](remote-display-drivers.md)
-   [ビデオ ポート DDI サポート](video-port-ddi-support.md)
-   [ミラー ドライバーの INF ファイル](mirror-driver-inf-file.md)
-   [ミラー ドライバーのインストール](mirror-driver-installation.md)

## <a name="span-idmirrordriversinwindows8spanspan-idmirrordriversinwindows8spanspan-idmirrordriversinwindows8spanmirror-drivers-in-windows8"></a><span id="Mirror_drivers_in_Windows_8"></span><span id="mirror_drivers_in_windows_8"></span><span id="MIRROR_DRIVERS_IN_WINDOWS_8"></span>Windows 8 でミラー ドライバー


Windows 8 以降では、システム上のミラー ドライバーはインストールされません。 このセクションで説明されているミラー ドライバーはインストールし、Windows の以前のバージョンでのみ実行します。

ただし、特別な GDI アクセシビリティ ドライバー モデルはミラー ドライバー機能を提供する開発者向けに Windows 8 以降より使用可能[*支援技術*](https://go.microsoft.com/fwlink/p/?linkid=248209)お客様向けに障害または障碍があります。 この特別なドライバー モデルの詳細についてにお問い合わせください<acc_driver@microsoft.com>します。

A*リモート ディスプレイ ドライバー*ミラー ドライバーのアーキテクチャに基づいているモデルは、Windows 8 以降でも実行できます。 詳細については、次を参照してください。[リモート ディスプレイ ドライバー](remote-display-drivers.md)します。

## <a name="span-idddkmirrordriversggspanspan-idddkmirrordriversggspanmirror-driver-description"></a><span id="ddk_mirror_drivers_gg"></span><span id="DDK_MIRROR_DRIVERS_GG"></span>ミラー ドライバーの説明


A*ミラー ドライバー*は追加の物理ディスプレイ デバイスの 1 つまたは複数の描画操作をミラー化された仮想デバイスのディスプレイ ドライバー。 これは実装されており、ディスプレイ ドライバー; と同様の動作ただし、ペアになっているビデオのミニポート ドライバーは、一般的なミニポート ドライバーと比べて最小限です。 参照してください[ビデオのミニポート ドライバー (Windows 2000 モデル) でミラー ドライバー サポート](mirror-driver-support-in-video-miniport-drivers--windows-2000-model-.md)ミラーリング システム内のミニポート ドライバーの詳細についてはします。 Windows 7 のエディション (バージョン 7600) から、Windows Driver Kit (WDK) には、3 つのディレクトリに格納されているコンポーネントのソース ファイルを含むミラー ドライバー サンプルにはが含まれています。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">Directory</th>
<th align="left">ソース ファイルが含まれています</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>\src\video\displays\mirror\disp</p></td>
<td align="left"><p>ミラー ドライバー。</p></td>
</tr>
<tr class="even">
<td align="left"><p>\src\video\miniport\mirror\mini</p></td>
<td align="left"><p>ミニポート ドライバー。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>\src\video\displays\mirror\app</p></td>
<td align="left"><p>ユーザー モード サービスです。 含まれています<em>mirror.inf します。</em></p></td>
</tr>
</tbody>
</table>

 

GDI のサポート、*仮想デスクトップ*し、ミラーのデバイス上の仮想デスクトップの一部を複製する機能を提供します。 GDI は、物理ディスプレイ ドライバー レイヤー上のグラフィックス レイヤーとして仮想デスクトップを実装します。 この仮想のデスクトップ領域ですべての描画操作を開始します。GDI はクリップし、仮想デスクトップ内に存在する物理的な画面が適切なデバイスでレンダリングします。

ミラー デバイスを任意に指定できる*クリップ領域*仮想デスクトップでは、複数の物理ディスプレイ デバイスにまたがる 1 つを含むです。 GDI は、そのドライバーのクリップ領域と交差するすべての描画操作をミラー デバイスに送信されます。 ミラー デバイスは、特定の物理デバイスを正確に一致するクリップ領域を設定できます。そのため、そのデバイスを効果的にミラー化ができます。

**注**  ミラー ドライバーのクリップ領域では、Windows 2000 以降、プライマリ ディスプレイ デバイスを含める必要があります。

 

**注**  ミラー ドライバーが読み込まれるときに、Windows デスクトップ マネージャー (DWM) は無効にする Windows Vista 以降では、します。

 

*ミラー*ドライバーのコード サンプルは、ミラー ドライバーを実装する方法を示します。 詳細についてには、サンプルを理解するのに役立ちます。

-   サンプルの INF ファイルを使用して、 *mirror.inf*、テンプレートとして。 参照してください[ミラー ドライバーの INF ファイル](mirror-driver-inf-file.md)詳細についてはします。

-   参照してください、 *mirror.exe*アプリケーションで、仮想デスクトップにミラー ドライバーを添付する方法を示します。 参照してください[ミラー ドライバーのインストール](mirror-driver-installation.md)詳細についてはします。

-   については、Win32 を使用して Windows SDK のマニュアルを参照してください**EnumDisplayDevices**関数。 この関数を使用して決定、  **\\ \\.\\表示\#** ミラー ディスプレイ デバイスに関連付けられた名前。 ミラー化されたデバイスの設定を変更するには、この数値が必要です。 複数のインスタンスに対して **\#** ; インスタンスごとに異なる数は、そのため、使用可能な表示デバイスを反復処理するこの数を決定する必要があります。

**グローバル デスクトップをミラー化されたデバイスを接続するには**

1.  登録の追加\_DWORD レジストリ エントリ**Attach.ToDesktop**ドライバーのサービスのキーにします。

2.  このキーのエントリを 1 に設定します。

ミラー ドライバーを無効にするには、このエントリを 0 (ゼロ) に設定します。

前述のように、ドライバーがインストールされているし、デバイスのレイヤーの上に存在するための描画層で動作します。 ミラー ドライバーの座標空間は、デスクトップの座標空間であるために、1 つ以上のデバイスにまたがることもできます。 ミラー ドライバーをプライマリ ディスプレイをミラー化する場合は、画面座標は、プライマリ ディスプレイのデスクトップ座標と一致する必要があります。

-   ミラー ドライバーをインストールした後は、ドライバーの表示領域と交差するすべてのレンダリング操作に対して呼び出されます。 [マルチ モニター システム](multiple-monitor-support-in-the-display-driver.md)、描画操作がすべて含まれませんこれでもミラー ドライバーには、プライマリ ディスプレイ デバイスのみが重なっている場合。

-   ユーザー モード サービスがミラー ドライバーの設定を維持するために使用することをお勧めします。 このアプリケーションはいることを確認、ドライバーがブート時に正しく読み込まれて、WM 経由での表示の変更の通知を取得することによって、デスクトップへの変更に適切に応答できます\_DISPLAYCHANGE メッセージ。

-   GDI は、ドライバーの外接する四角形と交差する DDI 描画操作、2 D グラフィックスのミラー ドライバーを呼び出します。 いる GDI チェックを実行しない、外接する四角形、サーフェスがデバイスの形式のビットマップ; である場合に注意してください。つまり場合、 [ **SURFOBJ** ](https://docs.microsoft.com/windows/desktop/api/winddi/ns-winddi-_surfobj)が、 **i 種類**%s 型の\_DEVBITMAP します。

-   常に、グローバル変数を使用せず、ミラー ドライバーを実装する必要があります。 すべての状態が存在する必要があります、 *PDEV*ドライバー。 GDI は呼び出す[ **DrvEnablePDEV** ](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvenablepdev)ビデオのミニポート ドライバーによって作成された各ハードウェア デバイスの拡張機能用です。

-   ミラー ドライバーが、DirectDraw をサポートしていません。

-   ミラー ドライバーが、GCAPS を設定する必要があります\_階層フラグを**TRUE**で、 **flGraphicsCaps**のメンバー、 [ **DEVINFO** ](https://docs.microsoft.com/windows/desktop/api/winddi/ns-winddi-tagdevinfo)構造体。

-   ユーザー補助のミラー ドライバーが、GCAPS2 を設定する必要があります\_EXCLUDELAYERED と GCAPS2\_INCLUDEAPIBITMAPS フラグを**TRUE**で、 **flGraphicsCaps2** のメンバー[ **DEVINFO** ](https://docs.microsoft.com/windows/desktop/api/winddi/ns-winddi-tagdevinfo)構造体。

-   ミラー ドライバーを実装してブラシの実現をサポートできます必要に応じて[ **DrvRealizeBrush**](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvrealizebrush)します。

GDI では、単一およびマルチ モニターの両方のシステムで実行する同じドライバーをできます。 マルチ モニター システムでのドライバーは、グローバル デスクトップ内での位置を追跡のみ必要があります。 GDI 提供されるたびに、Win32 のドライバーには、この位置**ChangeDisplaySettings**ときに、ユーザーに動的に変化するかなど、デスクトップで、モニターの配置コントロール パネルの 表示プログラムを使用して、呼び出しが発生します。 GDI の更新プログラム、 **dmPosition**のメンバー、 [ **DEVMODEW** ](https://docs.microsoft.com/windows/desktop/api/wingdi/ns-wingdi-_devicemodew)このような変更が発生した場合は、それに応じて構造体します。 ドライバーが実装することでこのような変更の通知を受信できる[ **DrvNotify**](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvnotify)します。 参照してください[ミラー ドライバーのインストール](mirror-driver-installation.md)詳細についてはします。

**注**  ミラー ドライバーは、このような精度で、クライアント側でレンダリングが困難な可能性がある場合に正確にピクセル単位で正確にレンダリングする必要はありません。 たとえば、ミラー化されたイメージを受信アダプターまたはモニターは、レンダリングする必要はありません[グリッド交差量子化](cosmetic-lines.md)ミラー化されているアダプター/モニターと同じ精度で (GIQ) 線画と多角形を塗りつぶします。

 

 

 





