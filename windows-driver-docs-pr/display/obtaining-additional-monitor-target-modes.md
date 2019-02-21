---
title: 追加のモニター ターゲット モードを取得します。
description: 追加のモニター ターゲット モードを取得します。
ms.assetid: fc0e2d43-8fc2-4757-ba77-f72a01e04343
keywords:
- WDK の表示モードをターゲットを監視します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b674b83ada8a0f5ddb9101f9016ab9ae34c1bd9f
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56535547"
---
# <a name="obtaining-additional-monitor-target-modes"></a>追加のモニター ターゲット モードを取得します。


Windows 7 以降、新しい監視インターフェイスが使用可能な[ **DXGK\_モニター\_インターフェイス\_V2**](https://msdn.microsoft.com/library/windows/hardware/ff561968)します。 元にない 2 つの追加機能を備えています[ **DXGK\_モニター\_インターフェイス**](https://msdn.microsoft.com/library/windows/hardware/ff561949)インターフェイス。

[**pfnGetAdditionalMonitorModeSet**](https://msdn.microsoft.com/library/windows/hardware/ff561970)

[**pfnReleaseAdditionalMonitorModeSet**](https://msdn.microsoft.com/library/windows/hardware/ff561977)

これらの関数は、動的かつスケーラブルなディスプレイ ミニポート ドライバー VidPN ターゲットにターゲット モードを追加する方法を提供します。 比較の場合、DXGK\_モニター\_インターフェイスのインターフェイスには、ターゲット モードの静的一覧のみが用意されています。 これらの関数を使用して、ドライバーは、それを列挙する必要があります追加モードの一覧については、オペレーティング システムに照会できます。 ドライバーは、要求されたモードを検証し、モニターがサポートされていないものを拒否できます。

ディスプレイのミニポート ドライバーがドライバー実装への呼び出しを受信すると[ **DxgkDdiEnumVidPnCofuncModality** ](https://msdn.microsoft.com/library/windows/hardware/ff559649) 、ターゲット モードを列挙するために関数

次の手順を使用して、ターゲット モードの設定に互換性のあるタイミング情報を追加するにする必要があります。

1.  呼び出すときに取得する追加のフィルター選択されたターゲット モードを返す[ **pfnGetAdditionalMonitorModeSet**](https://msdn.microsoft.com/library/windows/hardware/ff561970)します。 」の説明に従って、定期的なターゲット モードを返す必要がありますもこと[Cofunctional VidPN ソースを列挙し、ターゲット モード](enumerating-cofunctional-vidpn-source-and-target-modes.md)します。

2.  **PfnGetAdditionalMonitorModeSet**関数は、次を返します。
    -   *ppAdditionalModesSet*で追加のタイミングのモード一覧[ **DXGK\_TARGETMODE\_詳細\_タイミング**](https://msdn.microsoft.com/library/windows/hardware/ff562060)形式。
    -   *pNumberModes、* タイミング モードの数。

3.  これらのタイミングのモードのすべてを反復処理します。

4.  すべてのタイミングを互換性のないモードと、通常モードへの呼び出し中に既に指定されたフィルターで除外*DxgkDdiEnumVidPnCofuncModality*します。

5.  変換するために、残りのタイミング モード[ **D3DKMDT\_VIDPN\_ターゲット\_モード**](https://msdn.microsoft.com/library/windows/hardware/ff546729)型。

6.  VidPN 対象モードのセットには、残りのタイミング モードのすべてを追加します。

7.  呼び出す[ **pfnReleaseAdditionalMonitorModeSet** ](https://msdn.microsoft.com/library/windows/hardware/ff561977)から返されたタイミング モードの一覧を解放する**pfnGetAdditionalMonitorModeSet**します。

ディスプレイのミニポート ドライバーでは、VidPN ソース モードのセットと、ターゲット モードが設定するためのハードウェアでサポートされている他のすべてのタイミング モードを追加する必要があります。 表示モードのマネージャー (DMM) は、モードの一覧を生成してモニタによってサポートされていない別のタイミング モードを含む、すべての表示モード モニターによってサポートされていないと表示されていますの raw モードの一覧にのみ表示されます。 かどうかどうか、モニターが接続されてに関係なく、ミニポート ドライバーがすべて VidPN ソースとターゲット モードはサポートされているセット モニタによってを報告する必要があります。 のみモニターでサポートされているモードを報告するドライバーには、現在接続しているモニターがサポートされていないその他のモードも報告する必要があります。

## <a name="crt-monitors"></a>CRT モニター

CRT モニターでは、DMM を追加するタイミングを他のターゲット モード、640 x 480 x 60 Hz の標準的なモニターが、ビデオ Electronics Standards Association (VESA) 仕様で定義されている*VESA と業界標準とコンピューターのディスプレイのガイドラインモニター タイミング バージョン 1.0*します。

## <a name="dtv-and-hdtv-monitors"></a>デジタル テレビおよび HDTV モニター

デジタル テレビ (デジタル テレビ) と高精細テレビ (HDTV) のモニターは、DMM として追加モードの他のターゲットで必要なすべての標準のデジタル テレビ モード、 [WHCK](https://docs.microsoft.com/windows-hardware/test/hlk/windows-hardware-lab-kit)自動のテスト グラフィックス-0043、次に示すようにテーブル。 ディスプレイのミニポート ドライバーでは、ディスプレイ ハードウェアでサポートされていないすべてのモードを排除する必要があります。

**59.95 Hz デジタル テレビ システム:**

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">デジタル テレビの形式</th>
<th align="left">HDTV の形式</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>640 x 480 p x 59.94 Hz、縦横比 4:3</p></td>
<td align="left"><p>640 x 480 p x 59.94 Hz、縦横比 4:3</p></td>
</tr>
<tr class="even">
<td align="left"><p>720(1440) x 480i 59.94 Hz、縦横比 4:3 x</p></td>
<td align="left"><p>720(1440) x 480i 59.94 Hz、縦横比 4:3 x</p></td>
</tr>
<tr class="odd">
<td align="left"><p>720(1440) x 480i 59.94 Hz、縦横比 16:9 x</p></td>
<td align="left"><p>720(1440) x 480i 59.94 Hz、縦横比 16:9 x</p></td>
</tr>
<tr class="even">
<td align="left"><p>720 x 480 p x 59.94 Hz、縦横比 4:3</p></td>
<td align="left"><p>720 x 480 p x 59.94 Hz、縦横比 4:3</p></td>
</tr>
<tr class="odd">
<td align="left"><p>720 x 480 p x 59.94 Hz、縦横比 16:9</p></td>
<td align="left"><p>720 x 480 p x 59.94 Hz、縦横比 16:9</p></td>
</tr>
<tr class="even">
<td align="left"></td>
<td align="left"><p>1280 x 720 p x 59.94 Hz、縦横比 16:9</p></td>
</tr>
<tr class="odd">
<td align="left"></td>
<td align="left"><p>1920 x1080i 59.94 Hz、縦横比 16:9 x</p></td>
</tr>
<tr class="even">
<td align="left"></td>
<td align="left"><p>1920 x 1080 p x 59.94 Hz、縦横比 16:9</p></td>
</tr>
</tbody>
</table>

 

**50 Hz デジタル テレビ システム:**

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">デジタル テレビの形式</th>
<th align="left">HDTV の形式</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>640 x 480 p x 59.94 Hz、縦横比 4:3</p></td>
<td align="left"><p>640 x 480 p x 59.94 Hz、縦横比 4:3</p></td>
</tr>
<tr class="even">
<td align="left"><p>720(1440) x 576i 50 Hz、縦横比 4:3 x</p></td>
<td align="left"><p>720(1440) x 576i 50 Hz、縦横比 4:3 x</p></td>
</tr>
<tr class="odd">
<td align="left"><p>720(1440) x 576i 50 Hz、縦横比 16:9 x</p></td>
<td align="left"><p>720(1440) x 576i 50 Hz、縦横比 16:9 x</p></td>
</tr>
<tr class="even">
<td align="left"><p>720 x 576 p x 50 Hz、縦横比 4:3</p></td>
<td align="left"><p>720 x 576 p x 50 Hz、縦横比 4:3</p></td>
</tr>
<tr class="odd">
<td align="left"><p>720 x 576 p x 50 Hz、縦横比 16:9</p></td>
<td align="left"><p>720 x 576 p x 50 Hz、縦横比 16:9</p></td>
</tr>
<tr class="even">
<td align="left"></td>
<td align="left"><p>1280 x 720 p x 50 Hz、縦横比 16:9</p></td>
</tr>
<tr class="odd">
<td align="left"></td>
<td align="left"><p>1920 x 1080 i x 50 Hz、縦横比 16:9</p></td>
</tr>
<tr class="even">
<td align="left"></td>
<td align="left"><p>1920 x 1080 p x 50 Hz、縦横比 16:9</p></td>
</tr>
</tbody>
</table>

 

準拠している Windows Vista を継続する必要があります用に記述されたミニポート ドライバー、 [WHCK](https://docs.microsoft.com/windows-hardware/test/hlk/windows-hardware-lab-kit)テストのグラフィックス 0043 を自動化し、これらのテーブルで指定した追加のデジタル テレビ モードを追加します。 Windows 7 用のドライバーは、新しいをサポートする必要があるだけ**pfnGetAdditionalMonitorModeSet**と**pfnReleaseAdditionalMonitorModeSet**関数。


 
## <a name="see-also"></a>関連項目

[ディスプレイ アダプターではサポートされて、VidPN があるかどうかを決定します。](determining-whether-a-vidpn-is-supported-on-a-display-adapter.md)

[Cofunctional VidPN ソースとターゲット モードを列挙します。](enumerating-cofunctional-vidpn-source-and-target-modes.md)

[ビデオの存在するネットワーク用語](video-present-network-terminology.md)

[VidPN オブジェクトとインターフェイス](vidpn-objects-and-interfaces.md)