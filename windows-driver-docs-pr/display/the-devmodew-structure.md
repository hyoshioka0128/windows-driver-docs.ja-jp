---
title: DEVMODEW 構造体
description: DEVMODEW 構造体
ms.assetid: 26212e3b-a591-4ed6-b441-b130d8d4d948
keywords:
- GDI WDK Windows 2000 display、DEVMODEW 構造体
- グラフィックスドライバー WDK Windows 2000 display、DEVMODEW 構造体
- DEVMODEW structure WDK Windows 2000 display
- Unicode WDK グラフィック
- WDK GDI、DEVMODEW 構造の描画
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 41c5d761890c02a33fb0891b83950406adeb4e37
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72825512"
---
# <a name="the-devmodew-structure"></a>DEVMODEW 構造体


## <span id="ddk_the_devmodew_structure_gg"></span><span id="DDK_THE_DEVMODEW_STRUCTURE_GG"></span>


[**Devmodew**](https://docs.microsoft.com/windows/desktop/api/wingdi/ns-wingdi-_devicemodew)構造体は、Microsoft Windows SDK のドキュメントで説明されている DEVMODE 構造体の Unicode バージョンです。 (DEVMODEW の ' W ' サフィックスは、"wide" または Unicode 文字を表します)。アプリケーションではいずれかの構造体を使用できますが、DEVMODE 構造体ではなく DEVMODEW 構造体を使用するにはドライバーが必要です。

### <a name="span-idpublic_and_private_membersspanspan-idpublic_and_private_membersspanpublic-and-private-members"></a><span id="public_and_private_members"></span><span id="PUBLIC_AND_PRIVATE_MEMBERS"></span>パブリックメンバーとプライベートメンバー

DEVMODEW 構造体の定義済みメンバー (多くの場合、パブリック DEVMODEW メンバーと呼ばれます) の直後には、ドライバー定義メンバー (プライベート DEVMODEW メンバー) のセットが存在する場合があります。 次の図は、パブリックセクション (実際の DEVMODEW 構造体自体) とプライベートセクションを示しています。

![devmodew 構造体のパブリックセクションとプライベートセクションを示す図](images/devmode.png)

通常、プライベートメンバーはプリンタードライバーによってのみ使用されます。 ドライバーは、 **dmDriverExtra**メンバー内のこのプライベート領域のサイズ (バイト単位) を提供します。 ドライバーによって定義されるプライベートメンバーは、ドライバーによって排他的に使用されます。

プリンタードライバーの場合、DEVMODEW 構造体を使用して、印刷ドキュメントのユーザー選択を指定します。 また、印刷部数、用紙サイズ、その他の属性など、プリンターに対して選択した既定値を指定するためにも使用されます。 ディスプレイデバイスの場合、DEVMODEW 構造体は、ピクセルあたりのビット数、ピクセルディメンション、表示頻度などの表示属性を指定します。

### <a name="span-idinitializing_a_devmodew_structurespanspan-idinitializing_a_devmodew_structurespaninitializing-a-devmodew-structure"></a><span id="initializing_a_devmodew_structure"></span><span id="INITIALIZING_A_DEVMODEW_STRUCTURE"></span>DEVMODEW 構造体の初期化

ディスプレイドライバーまたはプリンタードライバーによって使用されるかどうかに応じて、DEVMODEW 構造体は2つの異なる方法で初期化されます。

-   ディスプレイドライバー DEVMODEW 初期化

    ディスプレイドライバーの[**DrvGetModes**](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvgetmodes)エントリポイントは、DEVMODEW 構造体のすべてのメンバーをゼロに初期化します。 次に、 *DrvGetModes*は、表示ドライバー DLL の名前を**dmdevicename**メンバーにコピーし、 **dmspecversion**と**dmDriverVersion**のメンバーに devmodew 構造体のバージョンを入力して、表示属性をコピーします。適切なメンバーに対する情報。

-   プリンタドライバ DEVMODEW 初期化

    アプリケーションが**DocumentProperties** (Microsoft Windows SDK のドキュメントで説明されているプリンターインターフェイス DLL 関数) または[**DrvDocumentPropertySheets**](https://docs.microsoft.com/windows-hardware/drivers/ddi/winddiui/nf-winddiui-drvdocumentpropertysheets) (NT ベースのオペレーティングシステムグラフィックス DDI) のいずれかを呼び出すと、DEVMODEW 構造体が既定値で作成されます。 その後、アプリケーションは、任意のパブリック DEVMODEW メンバーを自由に変更できます。 変更後、アプリケーションは、変更されたメンバーをドライバーの内部 DEVMODEW 構造体とマージするために、前に呼び出したのと同じ関数に対して2回目の呼び出しを行う必要があります。 いくつかの変更が正しく機能しない可能性があるため、2回目の呼び出しが必要です。DEVMODEW 構造を修正するには、プリンタードライバーを呼び出す必要があります。 ドキュメントが印刷されるときに、アプリケーションは、マージされた DEVMODEW 構造を**Createdc** (Microsoft Windows SDK ドキュメントで説明) に渡します。これにより、 [**Drvenablepdev**](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvenablepdev) DDI に渡されます。 その時点で、ドライバーの表示 DLL は DEVMODEW 構造を検証し、必要に応じて、印刷ジョブを実行する前に修復を行います。

### <a name="span-idusing_a_devmodew_structurespanspan-idusing_a_devmodew_structurespanusing-a-devmodew-structure"></a><span id="using_a_devmodew_structure"></span><span id="USING_A_DEVMODEW_STRUCTURE"></span>DEVMODEW 構造体の使用

いくつかの Api とグラフィックス DDIs は、印刷、デバイスの機能のクエリ、ユーザーインターフェイスの表示などの目的で、DEVMODEW 構造の情報を使用します。 たとえば、 [**DrvConvertDevMode**](https://docs.microsoft.com/windows-hardware/drivers/ddi/winddiui/nf-winddiui-drvconvertdevmode)は、DEVMODEW 構造をオペレーティングシステムのバージョン間で変換する印刷スプーラグラフィック DDI です。 これは、プリンタードライバーが別のオペレーティングシステムのバージョンで実行されている別のコンピューターから DEVMODEW 構造体を取得する場合に必要になることがあります。

### <a name="span-idmodifying_a_devmodew_structurespanspan-idmodifying_a_devmodew_structurespanmodifying-a-devmodew-structure"></a><span id="modifying_a_devmodew_structure"></span><span id="MODIFYING_A_DEVMODEW_STRUCTURE"></span>DEVMODEW 構造体の変更

アプリケーションとドライバーは、DEVMODEW 構造を自由に要求し、パブリックパートを直接変更することができます。 ただし、ドライバーだけがプライベート DEVMODEW 構造体のメンバーを変更できます。

プライベート DEVMODEW 構造体のメンバーを変更するには、まず、ドライバーがプライベートデータの先頭のオフセットを確認する必要があります。 この構造体の先頭へのポインターと、構造体のパブリックな部分のサイズを保持する**Dmsize**メンバーが見つかった場合、プライベート部分の先頭が見つかります。 次の例は、プライベートセクションの先頭へのポインターを初期化する方法を示しています。 この例では、 *pdm*は DEVMODEW 構造体の先頭を指しています。

```cpp
PVOID pvDriverData = (PVOID)  (((BYTE *) pdm) + (pdm -> dmSize));
```

### <a name="span-idprinter_driver_display_driver_devmodew_differencesspanspan-idprinter_driver_display_driver_devmodew_differencesspanprinter-driverdisplay-driver-devmodew-differences"></a><span id="printer_driver_display_driver_devmodew_differences"></span><span id="PRINTER_DRIVER_DISPLAY_DRIVER_DEVMODEW_DIFFERENCES"></span>プリンタドライバ/ディスプレイドライバ DEVMODEW の相違点

DEVMODEW 構造体のメンバーは、次の3つのカテゴリに分類されます。

-   プリンタードライバーによってのみ使用されるメンバー

-   ディスプレイドライバーによってのみ使用されるメンバー

-   プリンターとディスプレイの両方のドライバーで使用されるメンバー

次の表は、プリンタードライバーで*のみ*使用される、いくつかのパブリック DEVMODEW メンバーを示しています。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">プリンタードライバーによってのみ使用される DEVMODEW メンバー</th>
<th align="left">目的</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>dmScale</strong></p></td>
<td align="left"><p>画像を印刷用にスケーリングする割合を指定します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>dmCopies</strong></p></td>
<td align="left"><p>印刷する部数を指定します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>dmColor</strong></p></td>
<td align="left"><p>カラープリンターでカラーまたはモノクロを印刷するかどうかを指定します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>dmOrientation</strong></p></td>
<td align="left"><p>用紙の向きを縦または横に指定します。</p></td>
</tr>
</tbody>
</table>

 

次の表に、表示ドライバーで*のみ*使用される、いくつかのパブリック DEVMODEW メンバーを示します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">ディスプレイドライバーによってのみ使用される DEVMODEW メンバー</th>
<th align="left">目的</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>dmBitsPerPel</strong></p></td>
<td align="left"><p>ディスプレイデバイスの色解像度をピクセルあたりのビット数で指定します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>dmPelsWidth</strong></p></td>
<td align="left"><p>表示されるデバイスの画面の幅 (ピクセル単位) を指定します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>調べ</strong></p></td>
<td align="left"><p>表示されるデバイスの画面の高さ (ピクセル単位) を指定します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>dmDisplayFlags</strong></p></td>
<td align="left"><p>表示モード (色はモノクロ、インターレース、ノンインターレース) を指定します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>dmDisplayFrequency</strong></p></td>
<td align="left"><p>ディスプレイのリフレッシュレートをヘルツ単位で指定します。</p></td>
</tr>
</tbody>
</table>

 

3番目のテーブルには、プリンターとディスプレイの両方のドライバーで使用される、いくつかのパブリック DEVMODEW メンバーが一覧表示されます。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">プリンターおよびディスプレイドライバーで使用される DEVMODEW メンバー</th>
<th align="left">目的</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>dmDeviceName</strong></p></td>
<td align="left"><p>ディスプレイの場合は、表示ドライバーの DLL を指定します。</p>
<div>
 
</div>
プリンターの場合は、プリンターの "フレンドリ名" を指定します。</td>
</tr>
<tr class="even">
<td align="left"><p><strong>dmFields</strong></p></td>
<td align="left"><p>後に続く DEVMODEW メンバーのうち、どのメンバーが使用されているかを識別するビットフラグを指定します。 たとえば、DM_BITSPERPEL フラグは、 <strong>dmBitsPerPel</strong>メンバーに有効なデータが含まれている場合に設定されます。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>dmSize</strong></p></td>
<td align="left"><p>DEVMODEW 構造体のパブリックな部分のサイズをバイト単位で指定します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>dmDriverExtra</strong></p></td>
<td align="left"><p>パブリック構造のメンバーに続くプライベートドライバーデータのバイト数を指定します。 ディスプレイドライバーの場合、通常はゼロになります。</p></td>
</tr>
</tbody>
</table>

 

 

 





