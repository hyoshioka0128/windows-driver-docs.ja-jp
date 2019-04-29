---
title: 現在の設定
description: 現在の設定
ms.assetid: 4de99ad0-fcd9-4f8d-8125-8f622443a0c6
keywords:
- 現在のレジストリ設定 WDK ジョイスティック
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: aae5edf8cdb3b551bb776063c6cf8cc5f98e4d03
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63390326"
---
# <a name="current-settings"></a>現在の設定





現在のレジストリ設定に 2 つの部分: の代わりに標準のポーリングと機能、調整された値、およびミニドライバーのデータが格納されるキーを格納する値。

標準のポーリングを置換する関連のミニドライバーがないデバイスのポーリングに使用されるミニドライバー REGSTR をという名前のキーで定義できる\_VAL\_JOYCALLOUT します。 この機能は、DirectX 3.0 の新機能でした。 値は、詳細設定 ページから、喜びがあるすべてのミニドライバーを含むリストから新しいグローバル ドライバーを選択するとで、コントロール パネルの設定は\_HWS\_ISGAMEPORTDRIVER フラグを設定します。

残りの設定が、REGSTR で格納されている\_キー\_JOYCURR キー。 コントロール パネルが REGSTR の下に関連した OEM キーから値をコピーする最初のデバイスが特定のジョイスティックの ID を構成するとき\_パス\_、REGSTR に JOYOEM\_キー\_JOYCURR キー。 このキーの下にあるキー値名の各ので、各ジョイスティックは、独自の設定、名前の一部としてジョイスティック ID は含まれています。 REGSTR\_VAL\_JOYOEMNAME 値を関連する REGSTR コピー\_VAL\_JOYNOEMNAME と存在する場合、REGSTR\_VAL\_JOYOEMCALLOUT 値 REGSTRをコピー\_VAL\_JOYNOEMCALLOUT します。 REGSTR\_VAL\_JOYOEMDATA 値、REGSTR の最初の 2 つのダブルワードとして使用されます\_VAL\_(展開時) を次のように定義されている値の全体で、JOYNCONFIG 値。

```cpp
struct {
    /* usage settings, copied from REGSTR_VAL_JOYOEMNAME */
    struct {
        DWORD   dwFlags;
        DWORD   dwNumButtons;
    } hws;
 
    /* usage flags, described below */
    DWORD    dwUsageSettings;
 
    struct {
        /* values returned by hardware during calibration */
        struct { 
            /* minimums for each axis */
            struct {
                DWORD    dwX;
                DWORD    dwY;
                DWORD    dwZ;
                DWORD    dwR;
                DWORD    dwU;
                DWORD    dwV;
            } jpMin;
            /* maximums for each axis */
            struct {
                DWORD    dwX;
                DWORD    dwY;
                DWORD    dwZ;
                DWORD    dwR;
                DWORD    dwU;
                DWORD    dwV;
            } jpMax;
            /* center positions for each axis */
            struct
            {
                DWORD    dwX;
                DWORD    dwY;
                DWORD    dwZ;
                DWORD    dwR;
                DWORD    dwU;
                DWORD    dwV;
            } jpCenter;
        } jrvHardware;
 
        /* POV values returned by hardware during calibration */
        DWORD   dwPOVValues[JOY_POV_NUMDIRS];
 
        /* calibration flags, described below */
        DWORD   dwCalFlags;
    } hwv; 
 
    /* type of joystick, described below */
    DWORD   dwType;
 
    /* reserved for OEM drivers */
    DWORD   dwReserved; 
};
```

使用状況の設定は、次の値の組み合わせです。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>JOY_US_HASRUDDER</p></td>
<td><p>0x00000001l</p></td>
<td><p>/* ラダーで構成されているジョイスティック <em>/</p></td>
</tr>
<tr class="even">
<td><p>JOY_US_PRESENT</p></td>
<td><p>0x00000002l</p></td>
<td><p>/</em> ジョイスティックが実際に存在するでしょうか。 <em>/</p></td>
</tr>
<tr class="odd">
<td><p>JOY_US_ISOEM</p></td>
<td><p>0x00000004l</p></td>
<td><p>/</em> ジョイスティックは、OEM が定義した型 <em>/</p></td>
</tr>
<tr class="even">
<td><p>JOY_US_RESERVED</p></td>
<td><p>0x80000000l</p></td>
<td><p>/</em> 予約済み */</p></td>
</tr>
</tbody>
</table>

 

調整フラグは、次の値の組み合わせ

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>JOY_ISCAL_XY</p></td>
<td><p>0x00000001l</p></td>
<td><p>/* お客様 xy のところを調整 <em>/</p></td>
</tr>
<tr class="even">
<td><p>JOY_ISCAL_Z</p></td>
<td><p>0x00000002l</p></td>
<td><p>/</em> 調整するには Z <em>/</p></td>
</tr>
<tr class="odd">
<td><p>JOY_ISCAL_R</p></td>
<td><p>0x00000004l</p></td>
<td><p>/</em> 調整するには R <em>/</p></td>
</tr>
<tr class="even">
<td><p>JOY_ISCAL_U</p></td>
<td><p>0x00000008l</p></td>
<td><p>/</em> U 調整するには <em>/</p></td>
</tr>
<tr class="odd">
<td><p>JOY_ISCAL_V</p></td>
<td><p>0x00000010l</p></td>
<td><p>/</em> V 調整するには <em>/</p></td>
</tr>
<tr class="even">
<td><p>JOY_ISCAL_POV</p></td>
<td><p>0x00000020l</p></td>
<td><p>/</em> 調整するにはハット スイッチ */</p></td>
</tr>
</tbody>
</table>

 

**DwType**メンバーが定義済みのジョイスティックの型を表す数値を保持します。 OEM の調整ユーティリティは、この値を設定、Mmddk.h で定義されている値の範囲外の値を設定があります。 正確な値は、標準のコントロール パネルによりリセットされるように重要ではありません。

 

 




