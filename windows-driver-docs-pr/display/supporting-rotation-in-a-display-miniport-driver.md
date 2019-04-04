---
title: ディスプレイ ミニポート ドライバーでの回転のサポート
description: ディスプレイ ミニポート ドライバーでの回転のサポート
ms.assetid: 0c9bdd42-aeaf-4cc8-a979-9ed8eeda3811
keywords:
- ミニポート ドライバー WDK 表示の回転
- WDK の表示の回転
- 複製モード WDK ビデオ存在するネットワーク
- 画面の回転 WDK の表示
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 171bc23d8d25dadb2d4106d65edb61676d17c422
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56581344"
---
# <a name="supporting-rotation-in-a-display-miniport-driver"></a>ディスプレイ ミニポート ドライバーでの回転のサポート


ディスプレイ ミニポート ドライバーの[ **DxgkDdiEnumVidPnCofuncModality** ](https://msdn.microsoft.com/library/windows/hardware/ff559649)関数呼び出し、 [ **pfnUpdatePathSupportInfo** ](https://msdn.microsoft.com/library/windows/hardware/ff562106)関数ビデオの表示 (VidPN) のネットワーク トポロジ内の各パスのレポートの回転のサポート。 レポートのローテーションのサポートの詳細については、[Cofunctional VidPN ソースを列挙し、ターゲット モード](enumerating-cofunctional-vidpn-source-and-target-modes.md)を参照してください。

Microsoft DirectX グラフィックスのカーネル サブシステムは、共有のプライマリ画面を作成するのに画面ディメンションの非回転を使用します。 DirectX グラフィックスのカーネル サブシステムの指定、画面の回転をディスプレイ ミニポート ドライバーを通知する[ **D3DKMDT\_VIDPN\_存在\_パス\_回転** ](https://msdn.microsoft.com/library/windows/hardware/ff546700)-型指定された値で、**回転**のメンバー、 [ **D3DKMDT\_VIDPN\_存在\_パス\_変換**](https://msdn.microsoft.com/library/windows/hardware/ff546719)構造体で指定されている、 **ContentTransformation**のメンバー、 [ **D3DKMDT\_VIDPN\_存在する\_パス**](https://msdn.microsoft.com/library/windows/hardware/ff546647)ディスプレイ ミニポート ドライバーの呼び出しで構造[ **DxgkDdiCommitVidPn** ](https://msdn.microsoft.com/library/windows/hardware/ff559597)と[ **DxgkDdiUpdateActiveVidPnPresentPath** ](https://msdn.microsoft.com/library/windows/hardware/ff560803)関数。

**注**  すべて回転の角度は、反時計回りの方向は、GDI が回転をどのように定義する方法と整合性がで定義されます。

 

Surface データのみの場合、画面の回転をディスプレイ ミニポート ドライバーに通知する DirectX サブシステム、ドライバーのローテーションが必要、**回転**でビット フィールドのフラグが設定された、**フラグ**のメンバー[**DXGKARG\_存在**](https://msdn.microsoft.com/library/windows/hardware/ff557618)構造体、 *pPresent*ドライバーの呼び出しでパラメーターが指す[ **DxgkDdiPresent** ](https://msdn.microsoft.com/library/windows/hardware/ff559743)関数。 ドライバーでは、プレゼンテーション データから、画面の向きを回転するかを決定します。 場合でも、**回転**がセットされていなかった、ドライバーは、データを回転する必要があります。

### <a name="span-idclone-modebehaviorspanspan-idclone-modebehaviorspanspan-idclone-modebehaviorspanclone-mode-behavior"></a><span id="Clone-mode_behavior"></span><span id="clone-mode_behavior"></span><span id="CLONE-MODE_BEHAVIOR"></span>複製モードの動作

*複製モード*ビデオ存在するネットワークに複数のパスを複数のビデオの存在ターゲットに接続するビデオの存在するソース モードです。 (ビデオの存在するネットワークの詳細については、次を参照してください[複数のモニターとビデオの存在するネットワーク](multiple-monitors-and-video-present-networks.md)。)。

ディスプレイのミニポート ドライバーは各ターゲットは、さまざまな回転を必要がありますので、複製モードで動作する場合、回転を異なる方法で処理します。 オペレーティング システムでは、さまざまなバージョンの Microsoft DirectX のランタイム、およびユーザー モードのクライアントは、プライマリのビデオの存在ターゲットの向きのみを検出します。 したがって、存在するソース ビデオ内コンテンツは常にプライマリのビデオの存在ターゲットの向きを一致します。

次の表では、すべての関連する状況の複製モードでのディスプレイのミニポート ドライバーの動作方法を示します。 設定、**回転**フラグの設定は、**回転**ビット フィールドで、**フラグ**のメンバー、 [ **DXGKARG\_存在する**](https://msdn.microsoft.com/library/windows/hardware/ff557618)構造体。

<table>
<colgroup>
<col width="25%" />
<col width="25%" />
<col width="25%" />
<col width="25%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">プライマリ ターゲット</th>
<th align="left">セカンダリ ターゲット</th>
<th align="left">フラグを回転します。</th>
<th align="left">ドライバーの動作</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>回転していません</p></td>
<td align="left"><p>回転していません</p></td>
<td align="left"><p>設定されていません</p></td>
<td align="left"><p>ドライバーには、ローテーションは実行されません。</p></td>
</tr>
<tr class="even">
<td align="left"><p>回転していません</p></td>
<td align="left"><p>回転</p></td>
<td align="left"><p>設定されていません</p></td>
<td align="left"><p>ドライバーが場合でも、セカンダリのターゲットを回転、<strong>回転</strong>フラグは設定されません。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>回転</p></td>
<td align="left"><p>回転していません</p></td>
<td align="left"><p>Set</p></td>
<td align="left"><p>プライマリ ターゲットですがセカンダリのターゲットではなく、ドライバーが回転します。</p></td>
</tr>
<tr class="even">
<td align="left"><p>回転</p></td>
<td align="left"><p>回転していません</p></td>
<td align="left"><p>設定されていません</p></td>
<td align="left"><p><strong>回転</strong>が設定された場合、ドライバーでは、プライマリのターゲットは回転しません。 セカンダリのターゲットがソースのコンテンツの方向が一致しないため、ドライバーはセカンダリのターゲットを回転する必要があります。</p>
<p>このような状況は、クライアントは回転に対応してとは、コンテンツ ソースの既に指向正しく発生します。 そのため、オペレーティング システムは設定しません<strong>回転</strong>します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>回転</p></td>
<td align="left"><p>回転</p></td>
<td align="left"><p>Set</p></td>
<td align="left"><p>ドライバーは、プライマリとセカンダリの両方のターゲットを回転します。</p></td>
</tr>
<tr class="even">
<td align="left"><p>回転</p></td>
<td align="left"><p>回転</p></td>
<td align="left"><p>設定されていません</p></td>
<td align="left"><p>回転対応のクライアントは、ソースのコンテンツを既に正しく指向が。 そのため、追加の回転を必要はありません。</p></td>
</tr>
</tbody>
</table>

 

## <a name="span-idclone-moderequirementsspanspan-idclone-moderequirementsspanclone-mode-requirements-starting-with-windows81-update"></a><span id="clone-mode_requirements"></span><span id="CLONE-MODE_REQUIREMENTS"></span>Windows 8.1 Update 以降複製モードの要件


Windows 8.1 Update 以降では、ドライバーは、これらの要件を満たす必要があります。 テスト署名が有効になっている場合、ドライバーがこれらの要件を満たすために失敗した場合、システムでバグチェックが発生します。

<span id="Primary_clone_path"></span><span id="primary_clone_path"></span><span id="PRIMARY_CLONE_PATH"></span>*プライマリの複製のパス*  
**定義:** ソースの表示に重複するターゲットのモニターを含むパス-外部モニターに表示するには、ラップトップ コンピューターに重複するなど。

**要件:** プライマリの複製のパスにドライバーを設定する必要があります**Offset0**に**TRUE**および、その他の 3 つのオフセット値で[ **D3DKMDT\_VIDPN\_PRESENT\_パス\_回転\_サポート**](https://msdn.microsoft.com/library/windows/hardware/ff546705)に**FALSE**します。

場合は縦最初のソースの表示では、プライマリの複製のパスしない回転軸相殺されます。 つまり、プライマリの複製のパスがゼロのオフセットを常が ([**D3DKMDT\_VIDPN\_存在\_パス\_回転\_サポート**](https://msdn.microsoft.com/library/windows/hardware/ff546705).**Offset0**は**TRUE**)、し、デスクトップ ウィンドウ マネージャー (DWM) は、適切な方向が一致するように事前にそのコンテンツを回転します。

プライマリの複製のパスは、すべてのプライマリとセカンダリの複製のターゲットのモニターのリフレッシュ レートを決定します。

<span id="Secondary_clone_path"></span><span id="secondary_clone_path"></span><span id="SECONDARY_CLONE_PATH"></span>*セカンダリの複製のパス*  
**定義:** 含む、他のターゲットのモニター、ソースの表示にも重複する主な複製のパスに含まれていないパス。

**要件:** セカンダリの複製のパスにドライバーを設定する必要がありますで 4 つのオフセット値の少なくとも 1 つ[ **D3DKMDT\_VIDPN\_存在\_パス\_回転\_サポート**](https://msdn.microsoft.com/library/windows/hardware/ff546705)に**TRUE**します。 設定する必要がありますが、ドライバーがパスに依存しない回転をサポートしていない場合**Offset0**に**TRUE**ですべてのセカンダリの複製のパス。

パスに依存しない回転をサポートしている場合、ドライバーを作成する必要があります設定の 2 つの例を次に示します。

<span id="Landscape-first_example"></span><span id="landscape-first_example"></span><span id="LANDSCAPE-FIRST_EXAMPLE"></span>**ランドス ケープ最初の例**  
ソースの表示とセカンダリの複製のパスのターゲットは、両方のランドス ケープ-1 つ目のモニターには、場合、セカンダリの複製のパス、ドライバーは設定[ **D3DKMDT\_VIDPN\_存在\_のパス\_回転\_サポート**](https://msdn.microsoft.com/library/windows/hardware/ff546705).**Offset0**に**TRUE**および、その他の 3 つのオフセット値で**D3DKMDT\_VIDPN\_存在\_パス\_回転\_サポート**に**FALSE**します。 またはここでは、セカンダリの複製のパスで、ドライバーが両方設定**Offset0**と**Offset180**に**TRUE**とその他のオフセット値を**FALSE**.

<span id="Portrait-first_example"></span><span id="portrait-first_example"></span><span id="PORTRAIT-FIRST_EXAMPLE"></span>**縦最初の例**  
ソースの表示が縦最初のデバイスで、ランドス ケープ最初外部モニターに接続する場合、セカンダリの複製のパスにドライバーは設定**Offset270**または**Offset90**に**TRUE**します。

詳細については、[をサポートしているパスに依存しない回転](supporting-path-independent-rotation.md)を参照してください。

 

 





