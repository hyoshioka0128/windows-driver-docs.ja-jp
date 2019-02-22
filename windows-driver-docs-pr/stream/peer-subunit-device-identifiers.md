---
title: ピアのサブユニット デバイス識別子
description: ピアのサブユニット デバイス識別子
ms.assetid: f33c554b-77a7-4879-875e-12210b8a553f
keywords:
- AV/C WDK、識別子
- WDK AV/C 識別子
- デバイス Id の WDK AV/C
- Avc.sys 関数ドライバー WDK、識別子
- ピアのサブユニット デバイス識別子 WDK AV/C
- サブユニット サポート WDK AV/C
- ハードウェア Id WDK AV/C
- 互換性のある Id WDK AV/C
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3d2e8099058ab6524d79c43aaf285882cd6954c3
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56559167"
---
# <a name="peer-subunit-device-identifiers"></a>ピアのサブユニット デバイス識別子


次のハードウェア識別子と互換性のある識別子の例は、によって生成される*Avc.sys*で説明されている形式に基づいて、標準的なデバイス (つまり、1 つまたは複数のサブユニットを報告するデバイス) の[AV/Cデバイス Id](av-c-device-identifiers.md):

-   によって生成されたハードウェア識別子*Avc.sys*:

<a href="" id="avc-vendor-model-subunittype-subunitid"></a>**AVC\\*ベンダー*&*モデル*&*SubunitType*& * SubunitID***  
このハードウェア識別子は最も完全なはサブユニット識別子 (アンパサンド区切りの最後の部分デバイス識別子 (ID)) は通常、関係のないために、INF ファイルで指定めったにありません。

<a href="" id="avc-vendor-model-subunittype"></a>**AVC\\*ベンダー*&*モデル*& * SubunitType***  
このスタイルのデバイス識別子は、同一の複数のサブユニット可能性がある場合は特に、INF ファイルでの使用に適した***SubunitType***フィールドに、デバイス (およびそれらのサブユニット共有同じサブユニット ドライバー)。 この形式は、サブユニット ドライバーは、ユーザーによってハードウェア ベンダー、または、Microsoft によって使用できます。

-   によって生成された互換性のある識別子*Avc.sys*:

<a href="" id="avc-vendor-subunittype"></a>**AVC\\*ベンダー*& * SubunitType***  
ベンダー固有のサブユニット ドライバーを使用します。 通常のサブユニットの適切に定義されたクラス用の Microsoft 提供のサブユニット ドライバーの読み込みに Microsoft 提供の INF ファイルでのみ使用されます。

<a href="" id="avc-subunittype"></a>**AVC\\* SubunitType***  
AV/C サブユニット固有のドライバーを使用します。 通常のサブユニットの適切に定義されたクラス用の Microsoft 提供のサブユニット ドライバーの読み込みに Microsoft 提供の INF ファイルでのみ使用されます。

-   *Avc.sys*は次の互換性のある識別子を生成しません。

<a href="" id="avc-subunittype-subunitid"></a>**AVC\\*SubunitType*& * SubunitID***  
識別子固有では何もなしで実行できる、***ベンダー***フィールド。

<a href="" id="avc-vendor"></a>**AVC\\* 仕入先***  
ベンダー固有の「汎用」サブユニット ドライバーを含める必要がありますサポート**AVC\\*ベンダー*&&lt;SubunitType&gt;** の INF ファイル内のエントリ代わりに、この形式を使用します。

<a href="" id="avc-generic"></a>**AVC\\GENERIC**  
「汎用」サブユニット ドライバーを含める必要がありますサポート**AVC\\&lt;SubunitType&gt;** その INF 内のエントリがこの形式を使用するのではなくファイルします。

次のハードウェア識別子と互換性のある識別子の例は、によって生成される*Avc.sys* camcorder デバイス (1 つのカメラのサブユニット、1 つの VTR サブユニットおよびその他のサブユニットの任意の数のデバイス) の場合。

-   によって生成されたハードウェア識別子*Avc.sys*:

<a href="" id="avc-vendor-model-camcorder"></a>**AVC\\*ベンダー*&*モデル*& ビデオカメラ**  
場合に、ベンダー固有の INF ファイルで使用される*Msdv.sys*は読み込まれません。

-   によって生成された互換性のある識別子*Avc.sys*:

<a href="" id="avc-vendor-camcorder"></a>**AVC\\*ベンダー*& ビデオカメラ**  
使用される*Msdv.inf*を読み込む*Msdv.sys*します。

<a href="" id="avc-camcorder"></a>**AVC\\CAMCORDER**  
使用される*Msdv.inf*を読み込む*Msdv.sys*します。

-   *Avc.sys*は次の互換性のある識別子を生成しません。

<a href="" id="avc-vendor"></a>**AVC\\* 仕入先***  
ユニバーサル、ベンダー固有のサブユニット ドライバーを含める必要がありますサポート**AVC\\*ベンダー*& CAMCORDER**の INF ファイル内のエントリ。

<a href="" id="avc-generic"></a>**AVC\\GENERIC**  
ユニバーサルのサブユニット ドライバーを含める必要がありますサポート**AVC\\CAMCORDER**の INF ファイル内のエントリ。

**注**  :追加された DV に固有の検出メカニズムでは、Windows Vista、Windows Server 2003、および Windows XP オペレーティング システム、 *Avc.sys* (camcorders を含む) 任意の DV テープ デバイスが必要がありますように"& DV"ハードウェアに追加されます識別子とによって生成された互換性のある識別子*Avc.sys*します。 このメカニズムは、すべて VTR サブユニットの既定で有効です (場所***SubunitType*** 4 = =)。 ハードウェア id など、 **AVC\\*ベンダー*&*モデル*& CAMCORDER**なります**AVC\\*ベンダー*&*モデル*& CAMCORDER & DV**サブユニットが DV デバイスの場合。 メカニズムを指定することで、デバイスをインストールする INF ファイルで無効にできます**AvcFlags**ビット 3 が設定されていない (**AvcFlags & 0x8** 0 を = =)。

 

ハードウェア識別子とによって生成された互換性のある識別子*Avc.sys*のデバイスの非標準と準拠していない場合にのみ表示は、 **AvcFlags**レジストリ値に 1 セットのビット (**AvcFlags &** 0x2 0x2 = =)。 このフラグは、デバイスの INF ファイルを設定する必要があります。 デバイスの INF ファイルに次の行 (以下の太字で) 使用して、ハードウェアをインストールするときに、非標準および非準拠デバイスを公開することができます。

```INF
[CompanyName] ;INF Models section
%Subunit.DeviceDesc%=Subunit,AVC\GENERIC

[Subunit.NT] ;INF DDInstall section
;Other installation directives
AddReg=Subunit.NT.AddReg

[Subunit.NT.AddReg]
;Other registry settings
HKR,,"AvcFlags",0x00000001,0x2 ;0x00000001 = Binary value, 0x2 = Registry key value

[Strings]
;Other strings
Subunit.DeviceDesc="Fabrikam, Inc. Subunit"
```

デバイス識別子の次の例は、によって生成される*Avc.sys*標準および非準拠デバイスの 1 ビット**AvcFlags**設定。

-   ハードウェア id

<a href="" id="avc-vendor-model"></a>**AVC\\*ベンダー*& * モデル***  
ベンダー固有の INF ファイルで使用すると、標準および非準拠デバイス ドライバーをロードします。

-   互換性のある識別子

<a href="" id="avc-vendor"></a>**AVC\\* 仕入先***  
ベンダー固有の汎用単位ドライバーには、INF ファイルでのこのエントリが含まれています。

<a href="" id="avc-generic"></a>**AVC\\GENERIC**  
ユニバーサルの単体ドライバーには、INF ファイルでのこのエントリが含まれています。

ハードウェア識別子と互換性のある識別子の例を次に示します。 なお、会社「Fabrikam, inc.」 0x50F2 ベンダー コードを使用して、***ベンダー***フィールド。

A Fabrikam, Inc.DV カメラ (前述のよう上記の注 camcorders が特殊なケースである):

-   Camcorder ハードウェア識別子:

<a href="" id="avc-ven-50f2-mod-0-camcorder-dv--can-be-used-by-fabrikam--inc--in-an-inf-file-to-override-msdv-sys-as-the-driver-for-their-av-c-device--"></a>**AVC\\VEN\_50F2 MOD &\_0 & CAMCORDER DV** (INF ファイルでは、Fabrikam, Inc. によって上書きに使用できる*Msdv.sys* AV C/デバイスのドライバーとして)。  

-   ビデオ_カメラの互換性のある識別子:

<a href="" id="avc-ven-50f2-camcorder-dv--this-is-the-style-of-device-identifier-used-in-msdv-inf-to-load-msdv-sys-"></a>**AVC\\VEN\_50F2 & CAMCORDER & DV** (これは、スタイルで使用するデバイス識別子の*Msdv.inf*を読み込む*Msdv.sys*)  

<a href="" id="avc-camcorder-dv"></a>**AVC\\CAMCORDER&DV**  

A Fabrikam, Inc.1 つのチューナーのサブユニットと 1 つのテープのレコーダー/プレーヤーのサブユニット DVHS テープ デッキ:

-   テープ レコーダー/プレーヤーのサブユニットの (場所***SubunitType*** = 4) デバイス id は、INF ファイルに表示されます。

<a href="" id="avc-ven-50f2-mod-0-typ-4-id-0"></a>**AVC\\VEN\_50F2&MOD\_0&TYP\_4&ID\_0**  

-   テープのレコーダー/プレーヤーのサブユニットの互換性のある識別子は次のようになります。

<a href="" id="avc-ven-50f2-mod-0-typ-4"></a>**AVC\\VEN\_50F2&MOD\_0&TYP\_4**  

<a href="" id="avc-ven-50f2-typ-4--used-in-mstape-inf-to-load-mstape-sys-"></a>**AVC\\VEN\_50F2 & TYP\_4** (で使用される*Mstape.inf*を読み込む*Mstape.sys*)  

<a href="" id="avc-typ-4"></a>**AVC\\TYP\_4**  

-   チューナーのサブユニットの (場所***SubunitType*** = 5) デバイス id は、INF ファイルに表示されます。

<a href="" id="avc-ven-50f2-mod-0-typ-5-id-0"></a>**AVC\\VEN\_50F2&MOD\_0&TYP\_5&ID\_0**  

-   チューナーのサブユニットの互換性のある識別子は次のようになります。

<a href="" id="avc-ven-50f2-mod-0-typ-5"></a>**AVC\\VEN\_50F2&MOD\_0&TYP\_5**  

<a href="" id="avc-ven-50f2-typ-5"></a>**AVC\\VEN\_50F2 &AMP; TYP\_5**  

<a href="" id="avc-typ-5"></a>**AVC\\TYP\_5**  

**注**  :ベンダーは、上記で説明したような状況でのみハードウェア識別子を指定する必要があり、互換性のある識別子を指定していません。 また、ベンダーは INF ファイルに Microsoft によって提供されていたものと一致するデバイスの id を提供する必要がありますされません。

 

 

 




