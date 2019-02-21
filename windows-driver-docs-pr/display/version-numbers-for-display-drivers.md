---
title: ディスプレイ ドライバーのバージョン番号
description: ディスプレイ ドライバーのバージョン番号
ms.assetid: 73d26532-61c1-45d1-a388-7c0befc53487
keywords:
- Windows 2000 の WDK のバージョン番号を表示します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4dabe47e0f30e73e63831039886eebbcffd33a32
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56528990"
---
# <a name="version-numbers-for-display-drivers"></a>ディスプレイ ドライバーのバージョン番号


## <span id="ddk_ensuring_correct_version_numbers_gg"></span><span id="DDK_ENSURING_CORRECT_VERSION_NUMBERS_GG"></span>


エンドユーザーが特定のオペレーティング システムで DirectX の特定のバージョンを使用して、ディスプレイ ドライバーを使用することであることを確認するには、ドライバーを適切なバージョン番号を適用する必要があります。 DirectX でバージョン番号はデバイス ドライバーを非常に重要になります。 すべての DirectX アプリケーションのインストール時にデバイス ドライバーが正しくない形式を使用するバージョン番号または不適切なバージョン番号に出荷された場合に、エンド ユーザーで問題が発生します。

**注**、 **DriverVer**ディレクティブは、ドライバー パッケージをドライバー ファイル、INF ファイル自体には、INF ファイルなどのバージョン情報を追加する方法を提供します。 使用して、更新、 **DriverVer**ディレクティブ、ドライバー パッケージを安全かつ明確置き換えることができます、同じパッケージの将来のバージョンでします。 このディレクティブの詳細については、Windows Driver Kit (WDK) ドキュメントの「デバイスのインストール」セクションで、INF DriverVer ディレクティブを参照してください。

次の表では、DirectX のさまざまなバージョンと互換性のためのドライバーの IHV または OEM によって提供される適切なバージョン番号の範囲を示します。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">ターゲット システム</th>
<th align="left">［バージョン番号］
<div>
 
</div>
差出人:</th>
<th align="left">［バージョン番号］
<div>
 
</div>
至るまで。</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>Windows 98 専用ドライバー (DirectX5)</p></td>
<td align="left"><p>4.05.00.0000</p></td>
<td align="left"><p>4.05.00.9999</p></td>
</tr>
<tr class="even">
<td align="left"><p>DirectX 1.0 と互換性のあるドライバー</p></td>
<td align="left"><p>4.02.00.0095</p></td>
<td align="left"><p>4.03.00.1096</p></td>
</tr>
<tr class="odd">
<td align="left"><p>DirectX の 2.0 と互換性のあるドライバー</p></td>
<td align="left"><p>4.03.00.1096</p></td>
<td align="left"><p>4.03.00.2030</p></td>
</tr>
<tr class="even">
<td align="left"><p>DirectX 3.0 と互換性のあるドライバー</p></td>
<td align="left"><p>4.03.00.2030</p></td>
<td align="left"><p>4.04.00.0000</p></td>
</tr>
<tr class="odd">
<td align="left"><p>DirectX 5.0 と互換性のあるドライバー</p></td>
<td align="left"><p>4.10.10.0000</p></td>
<td align="left"><p>4.10.10.9999</p></td>
</tr>
<tr class="even">
<td align="left"><p>DirectX 6.0 と互換性のあるドライバー</p></td>
<td align="left"><p>4.11.10.0000</p></td>
<td align="left"><p>4.11.10.9999</p></td>
</tr>
<tr class="odd">
<td align="left"><p>Windows 98/Me DirectX 7.0 と互換性のあるドライバー</p></td>
<td align="left"><p>4.12.10.0000</p></td>
<td align="left"><p>4.12.10.9999</p></td>
</tr>
<tr class="even">
<td align="left"><p>Windows 2000 の DirectX 7.0 と互換性のあるドライバー</p></td>
<td align="left"><p>5.12.10.0000</p></td>
<td align="left"><p>5.12.10.9999</p></td>
</tr>
<tr class="odd">
<td align="left"><p>Windows XP およびそれ以降の DirectX 7.0 と互換性のあるドライバー</p></td>
<td align="left"><p>6.12.10.0000</p></td>
<td align="left"><p>6.12.10.9999</p></td>
</tr>
<tr class="even">
<td align="left"><p>Windows 98/Me DirectX 8.0 と互換性のあるドライバー</p></td>
<td align="left"><p>4.13.10.0000</p></td>
<td align="left"><p>4.13.10.9999</p></td>
</tr>
<tr class="odd">
<td align="left"><p>Windows 2000 の DirectX 8.0 と互換性のあるドライバー</p></td>
<td align="left"><p>5.13.10.0000</p></td>
<td align="left"><p>5.13.10.9999</p></td>
</tr>
<tr class="even">
<td align="left"><p>Windows XP およびそれ以降の DirectX 8.0 と互換性のあるドライバー</p></td>
<td align="left"><p>6.13.10.0000</p></td>
<td align="left"><p>6.13.10.9999</p></td>
</tr>
<tr class="odd">
<td align="left"><p>Windows 98/Me DirectX 9.0 と互換性のあるドライバー</p></td>
<td align="left"><p>4.14.10.0000</p></td>
<td align="left"><p>4.14.10.9999</p></td>
</tr>
<tr class="even">
<td align="left"><p>Windows 2000 の DirectX 9.0 と互換性のあるドライバー</p></td>
<td align="left"><p>5.14.10.0000</p></td>
<td align="left"><p>5.14.10.9999</p></td>
</tr>
<tr class="odd">
<td align="left"><p>Windows XP およびそれ以降の DirectX 9.0 と互換性のあるドライバー</p></td>
<td align="left"><p>6.14.10.0000</p></td>
<td align="left"><p>6.14.10.9999</p></td>
</tr>
</tbody>
</table>

 

**注**   6 から Windows XP と以降のバージョンの DirectX と互換性のあるドライバーのバージョン番号があります、DirectX 9.0 DDK ドキュメントが示されます *。nn*6.01.0000 *。nn*.01.9999 します。 ただし、従来の WHQL 手動テストの仕様をサポートするために、ドキュメントも示されます 6 からバージョン番号があります。*nn*6.10.0000 *。nn*.10.9999 します。
DirectX アプリケーションによってこの従来の WHQL 要件のためのディスプレイ ドライバーのバージョン番号が必要な*n*.*nn*.10 *。nnnn*します。 ディスプレイ ドライバーのバージョン番号の切り替え元場合*n*.*nn*.10 *。nnnn*に*n*.*nn*.01 *。nnnn*できるように、また、DirectX 9.0 DDK ドキュメント要件をより正確に最適化、このようなアプリケーション実行されないようにドライバーを以前のバージョンとして解釈するためです。

したがって、ディスプレイ ドライバーのバージョン番号に設定する必要があります*n*.*nn*.10 *。nnnn*します。

 

DirectX をサポートしていないデバイス ドライバーのバージョン番号は 4.00.00.0095 とより小さい 4.02.00.0095 より大きくなければなりません。 たとえば、デバイスのディスプレイ ドライバーが Windows 3.1 のディスプレイ ドライバーまたは Windows 95 専用ディスプレイ ドライバーの場合は、4.01.00.0000 のバージョン番号は正しいのようになります。

逆に、このドライバーの 4.03.00.0000 のバージョン番号が正しくないがあります。 Windows 95 で DirectX をサポートするデバイス ドライバーは、等しくまたは 4.02.00.0095 とより小さい 4.04.00.0000 よりも大きいバージョン番号のみが必要です。

### <a name="span-idstoringinternalversionnumbersspanspan-idstoringinternalversionnumbersspanstoring-internal-version-numbers"></a><span id="storing_internal_version_numbers"></span><span id="STORING_INTERNAL_VERSION_NUMBERS"></span>内部バージョン番号を格納します。

多くのベンダーだけでなく、バージョン番号を Microsoft が必要とする形式、製品サポートの内部バージョン番号を格納する希望を表現がテストを目的とします。 すべての DirectX ドライバーが重複してに格納されている 1 つのバージョン番号: 2 つの Dword として格納されている 1 つのバイナリ バージョンと 1 つの文字列バージョン。 バイナリのバージョンは変更できません。

ただし、文字列のバージョンは、次のように追加できます。

1.  仕入先は、この記事で前述したように、バージョン番号を作成します。 このバージョン番号は、「現状有姿をバイナリのバージョン番号に使用されます。

2.  仕入先は、基盤として、バージョン番号の文字列のこのバージョン番号を使用します。 必要な場合、ベンダー固有のバージョン文字列は、バージョン番号の完全な文字列を形成する既存のバージョン番号を追加できます。 ベンダー固有の文字列とバージョン番号の間、"-"(ハイフン文字)。

たとえば、「4.03.00.2100」DirectX 互換のディスプレイ ドライバーのバージョン番号は、仕入先"xx.xx.xx"形式を内部的に使用する場合は、"4.03.00.2100-xx.xx.xx"は、ドライバーのバージョン番号の結合された文字列にします。

お客様が、ドライバーのバージョン番号を確認します (で Windows エクスプ ローラーでファイルを右クリックし、選択**プロパティ**、 をクリックし、**バージョン** タブ)、Windows は、文字列を表示します。バージョン。 ベンダーの製品のサポートは、存在する場合は、バージョン番号のベンダー固有の部分を識別し、適切なアクションを実行できる必要があります。

 

 





