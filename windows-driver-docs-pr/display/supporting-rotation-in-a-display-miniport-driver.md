---
title: ディスプレイ ミニポート ドライバーでの回転のサポート
description: ディスプレイ ミニポート ドライバーでの回転のサポート
ms.assetid: 0c9bdd42-aeaf-4cc8-a979-9ed8eeda3811
keywords:
- ミニポートドライバー WDK ディスプレイ、ローテーション
- ローテーション WDK ディスプレイ
- 複製モード WDK ビデオの現在のネットワーク
- surface ローテーション WDK ディスプレイ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1952a1eccfc39e79dcce8a1dd0b0f7dbcf1e6d67
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72825604"
---
# <a name="supporting-rotation-in-a-display-miniport-driver"></a>ディスプレイ ミニポート ドライバーでの回転のサポート


ディスプレイミニポートドライバーの[**DxgkDdiEnumVidPnCofuncModality**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_enumvidpncofuncmodality)関数は、 [**Pfnupdatepathsupportinfo**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_vidpntopology_updatepathsupportinfo)関数を呼び出して、ビデオの存在するネットワーク (VidPN) トポロジの各パスのローテーションサポートを報告します。 ローテーションサポートのレポートの詳細については、「 [Cofunctional な VidPN ソースモードとターゲットモードの列挙](enumerating-cofunctional-vidpn-source-and-target-modes.md)」を参照してください。

Microsoft DirectX graphics カーネルサブシステムでは、回転されていない表面の寸法を使用して、共有プライマリサーフェスを作成します。 ディスプレイミニポートドライバーに画面を回転させるように通知するには、DirectX グラフィックスカーネルサブシステムで、 [**D3DKMDT\_vidpn\_存在する\_パス\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmdt/ne-d3dkmdt-_d3dkmdt_vidpn_present_path_rotation)、 [**D3DKMDT\_Vidpn**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmdt/ns-d3dkmdt-_d3dkmdt_vidpn_present_path)\_の**contenttransformation**メンバーに指定されている\_[**path\_TRANSFORMATION**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmdt/ns-d3dkmdt-_d3dkmdt_vidpn_present_path_transformation)構造体を指定**します。** を表示するには、ミニポートドライバーの[**DxgkDdiCommitVidPn**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_commitvidpn)関数と[**DxgkDdiUpdateActiveVidPnPresentPath**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_updateactivevidpnpresentpath)関数を表示します。\_\_\_

**   すべて**の回転角度は反時計回りの方向に定義されます。これは、GDI が回転を定義する方法と同じです。

 

DirectX サブシステムがディスプレイミニポートドライバーに画面を回転させるように通知する場合、ドライバーは、ドライバーの[**DxgkDdiPresent**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_present)関数の呼び出しで、 *ppresent*パラメーターが指す構造[ **\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgkarg_present)の**Flags**メンバーで、**回転**ビットフィールドフラグが設定されている場合にのみ、サーフェイスデータを回転させる必要があります。 ドライバーが、画面の現在の向きがプレゼンテーションデータから回転していると判断し、 **[回転]** が設定されていない場合でも、ドライバーはデータをローテーションしません。

### <a name="span-idclone-mode_behaviorspanspan-idclone-mode_behaviorspanspan-idclone-mode_behaviorspanclone-mode-behavior"></a><span id="Clone-mode_behavior"></span><span id="clone-mode_behavior"></span><span id="CLONE-MODE_BEHAVIOR"></span>複製モードの動作

*複製モード*は、ビデオの存在するソースがビデオの現在のネットワーク内の複数のパスを介して複数のビデオの存在に接続するためのモードです。 (ビデオの現在のネットワークの詳細については、「[マルチモニターとビデオの現在のネットワーク](multiple-monitors-and-video-present-networks.md)」を参照してください)。

各ターゲットで異なるローテーションが必要になる可能性があるため、表示ミニポートドライバーでは、複製モードで動作する場合、回転が異なる方法で処理されます。 オペレーティングシステム、さまざまなバージョンの Microsoft DirectX ランタイム、およびユーザーモードクライアントは、ビデオの現在のターゲットの向きのみを検出します。 したがって、ビデオの表示ソースのコンテンツは、常にプライマリビデオの現在のターゲットの向きと一致します。

次の表は、関連するすべての状況について、表示ミニポートドライバーが複製モードでどのように動作するかを示しています。 **回転**フラグの設定は、 [**Dxgkarg\_現在**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgkarg_present)の構造体の**Flags**メンバーの **[回転]** ビットフィールドの設定です。

<table>
<colgroup>
<col width="25%" />
<col width="25%" />
<col width="25%" />
<col width="25%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">プライマリターゲット</th>
<th align="left">セカンダリターゲット</th>
<th align="left">回転フラグ</th>
<th align="left">ドライバーの動作</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>回転しない</p></td>
<td align="left"><p>回転しない</p></td>
<td align="left"><p>未設定</p></td>
<td align="left"><p>ドライバーは回転を実行しません。</p></td>
</tr>
<tr class="even">
<td align="left"><p>回転しない</p></td>
<td align="left"><p>あふれ</p></td>
<td align="left"><p>未設定</p></td>
<td align="left"><p><strong>回転</strong>フラグが設定されていない場合でも、ドライバーはセカンダリターゲットを回転します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>あふれ</p></td>
<td align="left"><p>回転しない</p></td>
<td align="left"><p>設定</p></td>
<td align="left"><p>ドライバーはプライマリターゲットをローテーションしますが、セカンダリターゲットは回転しません。</p></td>
</tr>
<tr class="even">
<td align="left"><p>あふれ</p></td>
<td align="left"><p>回転しない</p></td>
<td align="left"><p>未設定</p></td>
<td align="left"><p>[<strong>回転</strong>] が設定されていないため、ドライバーはプライマリターゲットを回転しません。 セカンダリターゲットがソース内のコンテンツの方向と一致しないため、ドライバーはセカンダリターゲットを回転させる必要があります。</p>
<p>この状況は、クライアントがローテーション対応であり、既にソースの内容を適切に配置している場合に発生します。 そのため、オペレーティングシステムは<strong>回転</strong>を設定しません。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>あふれ</p></td>
<td align="left"><p>あふれ</p></td>
<td align="left"><p>設定</p></td>
<td align="left"><p>ドライバーは、プライマリターゲットとセカンダリターゲットの両方をローテーションします。</p></td>
</tr>
<tr class="even">
<td align="left"><p>あふれ</p></td>
<td align="left"><p>あふれ</p></td>
<td align="left"><p>未設定</p></td>
<td align="left"><p>ローテーション対応のクライアントは、ソースのコンテンツを既に適切に配置しています。 そのため、追加のローテーションは必要ありません。</p></td>
</tr>
</tbody>
</table>

 

## <a name="span-idclone-mode_requirementsspanspan-idclone-mode_requirementsspanclone-mode-requirements-starting-with-windows81-update"></a><span id="clone-mode_requirements"></span><span id="CLONE-MODE_REQUIREMENTS"></span>Windows 8.1 の更新で始まる複製モードの要件


Windows 8.1 Update 以降では、ドライバーがこれらの要件を満たしている必要があります。 テスト署名が有効になっている場合、ドライバーがこれらの要件を満たしていないと、システムのバグチェックが発生します。

<span id="Primary_clone_path"></span><span id="primary_clone_path"></span><span id="PRIMARY_CLONE_PATH"></span>*プライマリ複製パス*  
**定義:** ソース表示を複製するターゲットモニターを含むパス。たとえば、ラップトップコンピューターのディスプレイを複製する外部モニターです。

**要件:** プライマリ複製パスでは、ドライバーは**Offset0**を**TRUE**に設定する必要があります。また、D3DKMDT\_\_VIDPN のその他の3つのオフセット値は[ **\_パス\_ローテーション\_サポート**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmdt/ns-d3dkmdt-_d3dkmdt_vidpn_present_path_rotation_support)を**FALSE**に設定する必要があります。

縦方向のソース表示の場合、プライマリ複製パスは rotationally offset ではありません。 これは、プライマリ複製パスのオフセットが常にゼロ (D3DKMDT\_VIDPN\_存在することを意味します。[ **\_パス\_ローテーション\_サポート**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmdt/ns-d3dkmdt-_d3dkmdt_vidpn_present_path_rotation_support)です。**Offset0**は**TRUE**)、デスクトップウィンドウマネージャー (DWM) は、適切な向きに合わせて事前にコンテンツを回転させます。

プライマリ複製パスによって、すべてのプライマリおよびセカンダリ複製ターゲットのモニターのリフレッシュレートが決まります。

<span id="Secondary_clone_path"></span><span id="secondary_clone_path"></span><span id="SECONDARY_CLONE_PATH"></span>*セカンダリ複製パス*  
**定義:** プライマリ複製パスの一部ではなく、ソース表示も複製する、追加のターゲットモニタを含むパス。

**要件:** セカンダリ複製パスでは、ドライバーは、D3DKMDT\_\_VIDPN の4つのオフセット値のうち少なくとも1つを設定する必要があります。 [ **\_パス\_ローテーション\_サポート**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmdt/ns-d3dkmdt-_d3dkmdt_vidpn_present_path_rotation_support)が**TRUE**になります。 ドライバーがパスに依存しないローテーションをサポートしていない場合は、すべてのセカンダリ複製パスで**Offset0**を**TRUE**に設定する必要があります。

パスに依存しないローテーションがサポートされている場合にドライバーが行う設定の例を2つ示します。

<span id="Landscape-first_example"></span><span id="landscape-first_example"></span><span id="LANDSCAPE-FIRST_EXAMPLE"></span>**横向き-最初の例**  
セカンダリ複製パスのソース表示とターゲットが両方とも横向きに設定されている場合、セカンダリ複製パスでは、ドライバーは[**D3DKMDT\_VIDPN\_\_パス\_ローテーション\_サポート**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmdt/ns-d3dkmdt-_d3dkmdt_vidpn_present_path_rotation_support)を設定します。**Offset0**に**TRUE**を指定すると、D3DKMDT\_VIDPN の他の3つのオフセット値は **\_パス\_\_ローテーション\_存在**し**ます。** また、この場合、セカンダリ複製パスでは、ドライバーは**Offset0**と**Offset180**の両方を**TRUE**に設定し、もう一方のオフセット値を**FALSE**に設定します。

<span id="Portrait-first_example"></span><span id="portrait-first_example"></span><span id="PORTRAIT-FIRST_EXAMPLE"></span>**縦-最初の例**  
ソースディスプレイが縦向きのデバイスで、横向きの外部モニターに接続している場合、ドライバーは**Offset270**または**Offset90**を**TRUE**に設定します。

詳細については、「[パスに依存しないローテーションのサポート](supporting-path-independent-rotation.md)」を参照してください。

 

 





